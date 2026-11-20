# Distribution Video Workflow

Workspace for reviewing and editing authorized short-form clips for the Distribution podcast campaign.

## Start here

1. Read `AGENTS.md`.
2. Read `DISTRIBUTION_CAMPAIGN_RULES.md` and the supplied `CAMPAIGN_SOURCE_ARCHIVE.txt` before selecting or editing a campaign clip.
3. Put approved source footage in `clips/incoming/`.
4. Keep edit plans and intermediates in `clips/working/`; reviewed exports go in `clips/final/`.
5. Do not post or schedule without explicit approval.

## Workflow/tool references

- `skills/video-use/` — transcript-led live-action editing guide and helper scripts.
- `skills/hypit/` — editable, reference-led video-workflow skill.
- `skills/hyperframes/` and `skills/hyperframes-cli/` — authored graphics, validation and render workflows.
- `skills/reverse-any-video/` — reference analysis/reconstruction.
- `previous-video-editing/` — submodule with the author's prior 9:16 editing skill, lookbooks and examples.
- `reelmimic/` — source of a reference-style **2D animation** workflow; not a live-action clipper.
- `awesome-opus5-5-videos/` — source/prompt inspiration, not a guaranteed viral recipe.

See `GITHUB_REPO_REVIEW.md` and `RESEARCHED_VIDEO_TOOLS.md` for why tools were selected. This repository contains mixed upstream projects and preserves their own license/notice files; see `THIRD_PARTY_NOTICES.md`.

## Campaign non-negotiables

Use only campaign-supplied official A-roll and approved B-roll. No synthetic speakers or voices, fabricated claims, phonk, Distribution logo overlays, or unapproved music/assets. Keep names, captions, claims, safe zones, and platform tags accurate. Campaign platforms are YouTube, Instagram and X only. The exact detailed rules and source conflicts are documented in the two campaign files above.

## Environment status at setup

This is a prepared source/skills workspace, not a verified render installation. Node 20.20.2 is below the Hypit/ReelMimic requirements; FFmpeg/ffprobe and provider credentials were not installed. Check `SETUP.md` before attempting a render. The tools' third-party installers have not been run.

## Git submodules

Initialize reference repos after cloning if desired:

```bash
git submodule update --init --recursive
```

The project does not automatically install dependencies, transcribe footage, call paid services, or publish anything.
