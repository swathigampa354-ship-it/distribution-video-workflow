# Video workflow workspace

Repositories checked out here:
- `hypit/` — Hypit source and `/hypit` skill.
- `hyperframes/` — HyperFrames source and skills.
- `reelmimic/` — ReelMimic source, a reference-led **2D animation** application (not a live-action clipper).
- `video-use/` — video-use source, best-fit agent workflow for live-action raw footage.
- `awesome-opus5-5-videos/` — prompt/example collection.
- `previous-video-editing/` — sparse, read-only checkout of the user's existing 9:16 editing skill and references.

Useful skill bundles are copied into the persistent, non-hidden `skills/` folder. `skills/video-use/` keeps the scripts next to its SKILL.md. Read `AGENTS.md`, `DISTRIBUTION_CAMPAIGN_RULES.md`, and `CAMPAIGN_SOURCE_ARCHIVE.txt` before editing. Repo review notes are in `GITHUB_REPO_REVIEW.md`.

Incoming footage: `clips/incoming/` (or use an uploaded attachment path directly). Working edits: `clips/working/`. Review-ready exports: `clips/final/`.

## GitHub review and workspace status

The supplied GitHub credential was used for account inventory and authorized repo creation/push; it was not written into the workspace. 100 repositories were visible. No existing repository was modified or deleted. No Codespaces existed initially; after the user approved it, a new Codespace was created for this workspace.

The public repository excludes generated account-wide inventory and private repository-name snapshots. The user's selected reference repositories are linked as submodules. `podcli` is excluded and must not be used.

## Environment status

**GitHub Codespace** (`distribution-video-workflow`, basicLinux32gb): Node.js v24.22.2, Python 3.14.2, FFmpeg/ffprobe 6.1.1 installed; four approved reference submodules initialized. It is ready for code/video tasks. The Codespace does not have video-use's Python dependencies or a transcription provider key installed. No paid API calls have been made.

**Arena local workspace:** Node.js v20.20.2; FFmpeg/ffprobe were not found. Hypit requires Node.js 22.15+ and ReelMimic 22.18+. ReelMimic additionally needs Chrome and Claude Code or Codex; it makes original 2D animation, not live-action podcast edits. Avoid paid or publishing operations without explicit user approval.
