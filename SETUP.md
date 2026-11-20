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

## GitHub review status

The supplied GitHub credential was used for read-only account inventory/API review only and was not written into the workspace. 100 repositories were visible; no Codespaces were listed. No remote repository was modified or deleted. No Codespace was created or started.

## Environment status

No render dependencies or credentials have been installed. This workspace has Node.js v20.20.2; Hypit needs Node.js 22.15+ and ReelMimic 22.18+. FFmpeg/ffprobe were not found. ReelMimic additionally needs Python 3.10+, Chrome and Claude Code or Codex; it makes original 2D animation, not live-action podcast edits. Video-use needs Python dependencies, FFmpeg/ffprobe and (by default) an ElevenLabs Scribe API key for word-level transcription. No key has been added and no paid call has been made. **Do not use podcli** (explicit user instruction). Avoid paid or publishing operations without explicit user approval.
