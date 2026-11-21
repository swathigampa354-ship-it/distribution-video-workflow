# Social MCP

AI-controlled social media automation platform. An agent talks to **high-level MCP tools**; a campaign engine, PostgreSQL, Redis/BullMQ, and an `agent-browser` worker decide *how* to post.

TikTok is the first platform. The data model already has Instagram, YouTube, X, and Facebook.

This is a new TypeScript system. It reuses *concepts* from [AutoSocial Studio](https://github.com/Katzca/AutoSocial) (MIT) — isolated per-account sessions, queues, a posting daemon — and does **not** copy that repository. See [docs/ATTRIBUTION.md](docs/ATTRIBUTION.md).

---

## Project overview

The AI agent says what it wants:

> Create campaign Alpha. Add these campaign videos and these normal videos. Assign Alpha to 20 TikTok accounts. Use a 3 campaign / 1 normal pattern. Post twice a day. Generate a 7-day schedule.

The MCP server performs the calculations. The agent never clicks through TikTok for normal operations.

```
AI Agent
  │
  ├── Social MCP   (high-level tools: campaigns, schedules, posts)
  └── agent-browser MCP   (debug / manual login only)

Social MCP
  → PostgreSQL (source of truth)
  → Campaign engine (pattern cursor per account)
  → Scheduler (per-account posting times)
  → Redis + BullMQ
  → Posting worker
  → agent-browser (isolated session per account)
  → TikTok
```

---

## Architecture

```
apps/
  api/            REST management API (Vercel-compatible)
  mcp-server/     High-level MCP tools over stdio
  worker/         BullMQ workers + agent-browser + TikTok adapter
packages/
  shared/         types, config, errors, auth
  database/       Prisma client
  campaign-engine/  3 campaign / 1 normal (configurable)
  scheduler/      staggered posting times
  queue/          BullMQ + lock helpers
  storage/        local + S3 video/session storage
  core/           domain services used by API and MCP
prisma/           schema + SQL migrations
```

### Campaign pattern

Default:

```json
{ "pattern": ["campaign", "campaign", "campaign", "normal"] }
```

Each TikTok account stores `campaign_pattern_position` in PostgreSQL.

| Post status   | Pattern cursor                         |
|---------------|----------------------------------------|
| pending/queued/processing | reserved on the post, cursor unchanged |
| posted        | cursor confirmed (`position + 1`)      |
| failed        | retry **the same post** first          |
| unknown       | **do not** auto-retry (duplicate risk) |
| cancelled     | reservation released, cursor unchanged |

The cursor survives process restart, worker crash, and paused schedules because it lives in the database, not in memory.

### Posting frequency

Default: **2 posts/day** per account.

Times are per account, not global:

- Account 1 → `10:00`, `18:00`
- Account 2 → `11:30`, `20:00`

If two accounts share a time, the scheduler adds a 1-minute stagger so workers do not collide.

---

## Installation

Requires Node.js 20+.

```bash
git clone https://github.com/swathigampa354-ship-it/AutoSocial.git
cd AutoSocial
cp .env.example .env
npm install
```

---

## Environment variables

See `.env.example`. Required for local use:

| Variable | Purpose |
|----------|---------|
| `DATABASE_URL` | PostgreSQL |
| `REDIS_URL` | Redis / BullMQ |
| `API_SECRET` | API + MCP access key |
| `OBJECT_STORAGE_PROVIDER` | `local` or `s3` |
| `LOCAL_STORAGE_DIR` | Dev video storage |
| `SESSION_STORAGE_DIR` | Encrypted session blobs (references only in DB) |
| `SESSION_ENCRYPTION_KEY` | AES-256-GCM key (64-char hex in production) |
| `AGENT_BROWSER_PATH` | `agent-browser` binary |
| `S3_*` | Used when provider is `s3` |

Do not put browser cookies, session JSON, or API secrets in git.

---

## Database setup

```bash
docker compose up -d postgres redis
npx prisma migrate deploy --schema prisma/schema.prisma
npx prisma generate --schema prisma/schema.prisma
```

---

## Redis setup

```bash
docker compose up -d redis
# REDIS_URL=redis://localhost:6379
```

The database is the source of truth. Redis only holds jobs. A restart re-enqueues due `pending` posts.

---

## Running locally

```bash
cp .env.example .env
docker compose up -d postgres redis
npx prisma migrate deploy
npm run dev:api        # http://localhost:3000
npm run dev:worker     # posting + scheduler poll
npm run dev:mcp        # stdio MCP server (spawned by the agent)
```

Or all containers:

```bash
docker compose up --build
```

The default worker image does **not** include Chrome. Live TikTok publishing needs `Dockerfile.worker.browser` or a host with `agent-browser install`.

---

## Running the worker

```bash
npm run dev:worker
```

Flow when a post is due:

1. Scheduler poll finds `pending` posts with `scheduled_at <= now`
2. Account must be active and not paused
3. Post is locked `pending → queued → processing` (compare-and-set)
4. Worker loads **that account’s** encrypted session
5. `agent-browser --session social-<accountId>`
6. TikTok upload workflow
7. Verify result
   - success → `posted`, cursor advances
   - clear failure → `failed`, retry same post
   - uncertain → `unknown`, **no automatic republish**

If the worker dies mid-publish, recovery marks the row `unknown` after 15 minutes so a second worker cannot double-post.

---

## Running the MCP server

```bash
npm run dev:mcp
```

Stdio JSON-RPC. The process inherits `DATABASE_URL` / `REDIS_URL` from the environment.

---

## Connecting an AI agent

### Claude Desktop / Cursor

Copy [scripts/mcp-claude-desktop.json](scripts/mcp-claude-desktop.json) into the client config (update paths and secrets):

```json
{
  "mcpServers": {
    "social-mcp": {
      "command": "npx",
      "args": ["tsx", "/absolute/path/to/apps/mcp-server/src/server.ts"],
      "env": {
        "DATABASE_URL": "postgresql://social:social@localhost:5432/social_mcp?schema=public",
        "REDIS_URL": "redis://localhost:6379"
      }
    },
    "agent-browser": {
      "command": "agent-browser",
      "args": ["mcp"]
    }
  }
}
```

Keep **Social MCP** and **agent-browser MCP** as separate servers.

- Social MCP = production scheduling
- agent-browser MCP = headed login, debugging, selector inspection

### High-level tools

Account: `social_create_account`, `social_list_accounts`, `social_get_account`, `social_update_account`, `social_enable_account`, `social_disable_account`, `social_get_account_status`

Video: `social_add_video`, `social_list_videos`, `social_get_video`, `social_delete_video`

Campaign: `social_create_campaign`, `social_list_campaigns`, `social_get_campaign`, `social_update_campaign`, `social_add_campaign_video`, `social_assign_campaign_to_accounts`, `social_set_campaign_pattern`, `social_get_campaign_status`

Schedule: `social_generate_schedule`, `social_schedule_post`, `social_get_schedule`, `social_pause_schedule`, `social_resume_schedule`, `social_cancel_post`

Post: `social_create_post`, `social_get_post`, `social_get_post_status`, `social_retry_post`

Status: `social_get_system_status`, `social_get_account_statistics`, `social_get_campaign_statistics`, `social_get_failed_posts`

Agent ops: `social_setup_campaign`, `social_get_next_actions`, `social_get_recommendations`

---

## Adding accounts

```bash
curl -X POST http://localhost:3000/accounts \
  -H "x-api-key: $API_SECRET" \
  -H "content-type: application/json" \
  -d '{"username":"brand_one","timezone":"Asia/Calcutta","postingTimes":["10:00","18:00"]}'
```

Or via MCP: `social_create_account`.

Then capture a TikTok login **once** (headed, not production scheduling):

```bash
npm i -g agent-browser
agent-browser install
ACCOUNT_ID=<cuid from API>
agent-browser --session social-$ACCOUNT_ID --restore open https://www.tiktok.com
# log in manually, then:
agent-browser --session social-$ACCOUNT_ID state save /tmp/tiktok-state.json
```

Place the saved state in session storage (the worker encrypts it when `SESSION_ENCRYPTION_KEY` is set). Database rows only store `storage_reference`, never cookies.

---

## Adding videos

Videos are **not** stored in git.

- Development: `OBJECT_STORAGE_PROVIDER=local`
- Production: S3-compatible (`S3_ENDPOINT`, `S3_BUCKET`, keys)

`social_add_video` accepts `bytesBase64` or an existing `storageUrl`. Mark each file `campaign` or `normal`.

---

## Creating campaigns

```
social_create_campaign { name: "Campaign Alpha" }
social_add_campaign_video { campaignId, videoId }   # repeat
social_assign_campaign_to_accounts { campaignId, accountIds: [...] }
social_set_campaign_pattern { campaignId, pattern: ["campaign","campaign","campaign","normal"] }
social_generate_schedule { days: 7 }
```

---

## Scheduling posts

`social_generate_schedule` walks each account’s posting times, asks the campaign engine for the next content type + video, and inserts idempotent `posts` rows (`acct:<id>:slot:<iso>`). Re-running the tool will not duplicate slots.

Pause / resume is per account and does not reset `campaign_pattern_position`.

---

## Campaign pattern explanation

Example, Account A starting at position 0:

1. Campaign
2. Campaign
3. Campaign
4. Normal
5. Campaign
…

Account B can sit at a different cursor. Failed post 3 is retried as post 3 — the engine does not skip ahead to Normal.

---

## API

Authenticated with `x-api-key` or `Authorization: Bearer`. `/health` is open.

- `/accounts`
- `/campaigns`
- `/videos`
- `/posts`
- `/schedules`
- `/status`

Validation is Zod. Errors return `{ error, message }`.

---

## Deployment

Do **not** run the browser worker as a Vercel serverless function.

```
Vercel
  ├── API
  ├── MCP HTTP endpoint (future)
  ├── Dashboard
  └── Webhooks

Persistent infrastructure
  ├── PostgreSQL
  ├── Redis
  └── Object storage (S3)

Worker environment (pick one)
  ├── VPS / Docker
  ├── Render / Railway worker
  ├── container job
  └── Vercel Sandbox (future)
```

API entrypoint: `apps/api/src/vercel.ts`.

---

## Security notes

- Management API is not public without `API_SECRET`.
- Browser session files are encrypted at rest when `SESSION_ENCRYPTION_KEY` is set.
- Session JSON is never logged. Cookie-like keys are redacted.
- Sessions are isolated: `social-<accountId>`. Using account A’s session for account B throws.
- Do not commit `.env`, `storage/sessions`, or agent-browser state.

---

## Content shortage (STRICT)

If a pattern slot needs `normal` and no ready normal video exists, schedule generation **refuses to create posts**. Campaign videos are never substituted. Policy is `STRICT` (no silent FALLBACK).

## Account locking

Workers take Redis lock `lock:account:{accountId}` so two browser sessions cannot post as the same TikTok account at once.

## Known limitations

- **Live TikTok publishing has not been verified** in this environment. The adapter implements the workflow and stops cleanly when no session exists.
- TikTok Studio UI changes. Selectors live in `apps/worker/src/tiktok/selectors.ts` only.
- Instagram / YouTube / X / Facebook are schema-ready, not implemented.
- MCP is stdio. There is no hosted MCP HTTP gateway yet.
- Default Docker worker image has no Chrome; use `Dockerfile.worker.browser`.
- Caption/language localization of TikTok UI may require extending `publishNames`.

---

## Troubleshooting

| Symptom | What to do |
|---------|------------|
| `prisma migrate` fails | Postgres not up; check `DATABASE_URL` |
| Worker idle | Redis down, or accounts `schedulePaused` / `DISABLED` |
| Posts stuck `processing` | Wait 15m for unknown recovery, inspect logs, **do not** force retry if status is `unknown` |
| `unknown` status | Verify on TikTok manually. Never auto-repost. |
| Session expired | Headed re-login with agent-browser for that account id only |
| `agent-browser binary not found` | `npm i -g agent-browser && agent-browser install` |
| Duplicate key on generate | Harmless — idempotency reused the existing slot |

---

## Tests

```bash
npm test
```

Coverage:

- Campaign engine: 3+1 loop, persistence, failed retry, unknown block
- Scheduler: 7-day / 2-per-day, stagger, past-slot skip, idempotency keys
- Locks: two workers cannot publish the same post
- Account isolation: session A never binds to account B
- API: auth, validation, error mapping

---

## Tech stack

TypeScript, Node.js 20, PostgreSQL, Prisma, Redis, BullMQ, MCP SDK, agent-browser, Zod, Express, local/S3 storage.

No deviations from the recommended architecture. `node-cron` is not used.
