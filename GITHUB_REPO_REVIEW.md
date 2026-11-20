# GitHub repository review — short-video workflow

**Review date:** 20 Nov 2026 (local workspace)
**Scope:** Read-only account inventory plus deeper README/tree review of video, speech, editing and social-publishing repositories. No repository was deleted or modified. No Codespace was created or started.

## Access and inventory

- GitHub API authenticated successfully for the supplied account.
- **100 repositories** were visible in the account inventory. A local metadata inventory and text index were created for the review; those account-wide files are excluded from the public repository because they list private repository names.
- **0 Codespaces** were listed for the account, so there was no existing Codespace to connect to. This review used GitHub's read-only repository APIs and the current local workspace instead.
- Private video output repositories were inspected at metadata/tree level only; their MP4 files were not downloaded.

## Best things in your repos for this work

### `podcli` — reviewed, excluded from this workflow

Repo: https://github.com/swathigampa354-ship-it/podcli

The user explicitly instructed: **“Don't use podcli.”** I will not install, execute, include it as a submodule, or use it for clip discovery/rendering. Its README was read during the repo review only; no installer or code was run.

### 2. `vertical-video-edits-2026-10-16` — your proven visual/editing reference

Repo: https://github.com/swathigampa354-ship-it/vertical-video-edits-2026-10-16

This contains three prior 9:16 edit approaches, an actual editable video-editing skill, scripts, QC guidance, and a lookbook. The skill emphasizes inspecting the real source, faithful speech/timing, readable typography, safe subject framing, still-frame review, and checking the encoded export. The Morph v3 README describes a polished continuous-object motion-graphics style. These are useful references—not automatic presets. The Distribution campaign's restrictions override any old profile, logo, color, audio, or style defaults.

The selected skill and references are available in `previous-video-editing/video-editing-skill/` (sparse checkout; existing repo is untouched).

### 3. `my-video` / `trypost-brag-video` — prior HyperFrames production example

Repos: https://github.com/swathigampa354-ship-it/my-video and https://github.com/swathigampa354-ship-it/trypost-brag-video

Both contain a TryPost product-animation brief, scene plan, HyperFrames setup and render logs. Useful for studying an existing code-authored motion workflow. They are TryPost-specific product work and are **not** a source for Distribution footage, claims, or branding.

### 4. `awesome-opus5-5-videos` and `deepseek-openai-title-variants`

The prompt collection is useful for inspiration about pacing and motion, not for copying other clippers or guaranteeing viral performance. The title-variants repo can inspire title testing, but any campaign hook/title must be faithful to the actual audio and not introduce unsourced claims or competitor comparisons.

## Other related repositories — why I would not start there

- **`supoclip`** — featureful clipper, but its quickstart calls for Docker, AssemblyAI transcription and an AI provider (or local Ollama). More setup/provider surface than the current transcript-led workflow.
- **`clipforge`** — its own README marks it development/not production-ready and says worker/render/auth areas are incomplete/stubbed. Not a dependable first choice for delivering campaign exports.
- **`Handy`** — a useful offline speech-to-text desktop app, but its README describes push-to-talk dictation rather than a full long-video clip pipeline.
- **`trypost`, `agentp`, `AutoSocial` / `social-mcp`, and `tiktok-posting-memoir`** — scheduling/publishing or TikTok-focused. TikTok is excluded from this Distribution campaign; don't use these to publish campaign clips. We can prepare post copy separately, but the user should approve any actual post/schedule action.
- **`media-grabber`** — may help save media from a browser, but it does not override the campaign's source rules. Use only official A-roll/B-roll resources the campaign permits.
- **`YouTube-Viewer`** — a view-bot project. Do not use it or any artificial engagement for campaign views.
- One private media-only repository was present in the inventory. I inspected filenames/metadata only; I did not download or reuse its media. Its private repository name is intentionally omitted from this public-facing report.

## Recommended workflow from your existing assets

1. Wait for your official Distribution A-roll and (if needed) approved B-roll files.
2. Use your `video-editing-skill` and `video-use` for source inspection, concise spoken hooks, faithful transcript-based cuts, clean captions and export QC.
3. Use HyperFrames only for optional, understated, original overlays/graphics where they don't conflict with campaign rules.
4. Produce a reviewable draft; confirm speech, spelling, safe zones, content compliance, and duration before delivery. Never claim a clip is “viral” or guarantee views.

## Campaign rule archive

The newly attached full text archive is copied to `CAMPAIGN_SOURCE_ARCHIVE.txt`. The concise working checklist is `DISTRIBUTION_CAMPAIGN_RULES.md`; its campaign-specific A-roll/B-roll, no-synthetic-speaker, no-logo-overlay and no-posting rules take precedence over generic skills and stale templates.
