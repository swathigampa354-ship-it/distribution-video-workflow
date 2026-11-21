# Video workspace instructions

Use the local skills in `skills/` as the workflow references for video tasks. For your existing custom editing approach, read `previous-video-editing/video-editing-skill/SKILL.md` and its `references/` when useful; campaign-specific rules below override its general style choices:
- `skills/hypit/SKILL.md` for reference-led, word/time-anchored video editing and production.
- `skills/hyperframes/SKILL.md` and `skills/hyperframes-cli/SKILL.md` for project creation, validation and render workflows.
- `skills/reverse-any-video/SKILL.md` when matching/rebuilding an existing reference video.
- `skills/media-use/SKILL.md` for media/transcription/audio workflow; do not call paid or external services without user approval.
- `skills/video-use/SKILL.md` is the primary live-action editing guide; its helpers are alongside it. Do not use `podcli` (per the user's explicit instruction). Use the relevant ReelMimic skill copies only when their 2D animation scope fits. The remaining HyperFrames skills and Opus 5.5 example prompt library are available when relevant.

## This campaign's non-negotiable rules

Read `DISTRIBUTION_CAMPAIGN_RULES.md` and `CAMPAIGN_SOURCE_ARCHIVE.txt` before making campaign clips. Key checks:
- Clips must focus on Arthur and Subah; keep a host visible for 5–7 seconds minimum per clip.
- Campaign platforms: YouTube, Instagram, X only (not TikTok).
- Clean, accurate captions; names exactly Arthur and Subah; no profanity, sexual/explicit, political, controversial, defamatory/negative, misleading, competitor, or harassment-bait material.
- A-roll must come only from official interview footage supplied for this campaign. Never source speakers/guests from public YouTube, LinkedIn, other podcasts, or conference recordings.
- B-roll should come from the campaign's linked folder. If third-party B-roll is explicitly approved, it must be generic and show no competitor branding or identifiable customers/partners.
- No AI voiceovers, AI avatars, synthetic speaker recreations, fabricated quotes/stats/claims, or meaning-changing transcript edits. Light filler cleanup only.
- Do not place the Distribution logo in an intro, outro, overlay, thumbnail, or end card; don't use Distribution brand fonts/colors for text. Use the supplied safe-zone template for platform UI clearance.
- No phonk; no copied work; no duplicate same-platform post; avoid excessive jump cuts, meme spam, distracting effects, flashy/neon text.
- Do not infer claims; use only what the footage actually says. Flag doubtful context for the user rather than inventing it.
- Never use view bots or fake engagement. Do not post, schedule, automate comments, or invoke publishing tools without explicit approval; automated comments need a prior ticket with campaign moderation.
- A clip needs 1,500 views to qualify. Post at least one weekly. Spread accepted posts across the three supported platforms.
- Each 3 campaign clips requires 1 non-campaign post; a non-campaign post must contain no Distribution footage/logo/name/host/guest/show reference.
- Add the platform-specific official account tag, 2–3 caption lines and relevant hashtags; use the required Atomik attribution in the account profile/description.

## Media workflow

1. Put user-provided source footage in `clips/incoming/` (or use the uploaded attachment path directly).
2. Confirm A-roll is the official campaign-supplied footage and B-roll is campaign-approved. Inspect footage/audio; identify candidate moments from actual dialogue, preserving context and speaker identity. Propose a concise edit strategy and wait for approval before executing substantive edits. Never use paid/external generation without approval.
3. Keep editable project/source files in `clips/working/`; final reviewed exports go in `clips/final/`.
4. Check every proposed clip against the campaign rules and the supplied footage. Do not claim a render or install succeeded unless verified.
5. Ask the user for any missing campaign input (e.g., source episode, preferred length, or platform) only when it blocks the edit.

## GitHub preservation

The user authorized GitHub repo review but explicitly forbids deleting repos. Do not delete, archive, transfer, force-push, or rewrite repositories. Use existing Codespaces only; if none are listed, ask before creating one because it can incur compute charges. Do not publish, schedule, or write to any remote repo without a clear request for that particular action.
