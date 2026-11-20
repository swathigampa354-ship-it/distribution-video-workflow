# Video editing tools researched (20 Nov 2026)

## Best fit for incoming raw clips: video-use

**Repo:** https://github.com/browser-use/video-use
Agent skill plus FFmpeg/Python helpers for transcript-led live-action editing. Its workflow inventories footage, proposes a cut strategy for approval, renders, then checks output around cuts. It is the most directly relevant of the researched tools for podcast/interview footage. It expects FFmpeg/ffprobe and, by default, an ElevenLabs Scribe key for word-level transcripts. No key has been added and no paid transcription call has been made. Consider local transcription if the user prefers not to use a paid/cloud transcript provider.

## ReelMimic: useful, but not a live-action clip editor

**Repo:** https://github.com/edenfunf/reelmimic
Cloned here. It analyzes a reference and makes a new original **2D animation** in a similar style; its README explicitly says it does not edit real people/live-action footage. Useful for studying pacing/framing or producing original animated supporting material, not for cutting Arthur/Subah footage. Its desktop app expects Node 22.18+, Python 3.10+, FFmpeg, Chrome and Claude Code or Codex. This workspace is not yet at those prerequisites; the install script has not been run.

## Existing tools that complement one another

- **Hypit:** reference-led, editable video workflows; keep for learning a reference's production grammar and constructing a new clip/video workflow.
- **HyperFrames:** code-authored motion graphics/overlays with validation; use only when a clip benefits from a tasteful, campaign-compliant graphic.
- **awesome-opus5-5-videos:** inspiration/prompts, not an editor or a guaranteed viral recipe.

## X discovery / public repo recommendations

An X post on 19 Oct 2026 collected ten agent video repos and singled out **video-use** for dropping raw footage into a folder and asking an agent to cut, grade and caption it: https://x.com/thisguyknowsai/status/2112110489560027144

A separate April 2026 X post demonstrated the same raw-footage → `final.mp4` workflow and linked the repo: https://x.com/socialwithaayan/status/2047568884304367722

A September 2026 X post describes ReelMimic's niche—rebuilding an original 2D video from reference style rather than reusing the footage: https://x.com/madzadev/status/2100268479463186580

Other candidates discovered (not installed; tradeoffs differ):
- **AutoClip** — https://github.com/zhouxiaoka/autoclip — local desktop/CLI/MCP project for long video → shorts; potentially useful for candidate discovery, but adds a separate application and setup. Reassess if you want a one-click ranked-clip batch.
- **OpenShorts** — https://github.com/mutonby/openshorts — clip-generation project with self-host/cloud modes. Its current repo includes a paid hosted mode; not needed for an agent-led manual-review workflow.
- **opensource-clipping** — https://github.com/NaufalRizqullah/opensource-clipping — feature-heavy auto-clip pipeline with several AI/provider integrations and optional uploaders. Not installed: more dependencies and publishing risk than needed.

## Editorial guardrails for “viral”

Use hooks, strong moments and tight pacing, but do not equate “viral score” or social-post hype with a guaranteed outcome. Choose moments based on actual dialogue, preserve context, do not invent claims, and have a human review every export. The Distribution-specific hard rules are in `DISTRIBUTION_CAMPAIGN_RULES.md`.
