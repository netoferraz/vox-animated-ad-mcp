```
   _____                   _____            .__
  /     \ _____  ___  ____/ ____\_ __  _____|__| ____   ____
 /  \ /  \\__  \ \  \/  /\   __\  |  \/  ___/  |/  _ \ /    \
/    Y    \/ __ \_>    <  |  | |  |  /\___ \|  (  <_> )   |  \
\____|__  (____  /__/\_ \ |__| |____//____  >__|\____/|___|  /
        \/     \/      \/                 \/               \/
```

# Vox Explainer Method

A [Claude](https://claude.com) skill that turns a single sentence into a complete Vox-style paper-collage animated video — researched script, per-clip prompts, every image and clip generated, chained into one continuous animation — without you ever leaving the chat.

It does two things:

- **Make ad videos** — Vox Style Ad Animation for your product or offer, ready to run paid or drop organic.
- **Make explainers for faceless YouTube channels** — editorial storytelling that sells nothing.

You give it a topic or a product. The skill walks a fixed gate flow — content mode, a quick research pass, script and prompt approval — then generates every clip through the [Higgsfield CLI](https://github.com/higgsfield-ai/cli) (Gemini Omni Flash, 10-second clips) and returns the finished clips in chat. The consistency trick: it extracts the last frame of each finished clip and passes it as the reference into the next clip's generation, which is why the result plays as one continuous animation instead of disconnected AI shots.

## Examples

| | |
| --- | --- |
| ![coffee](examples/coffee-preview.gif) | ![eels](examples/eel-preview.gif) |
| *coffee explainer* | *eel explainer* |
| ![eggs](examples/final-preview.gif) | ![painkillers](examples/painkillers-preview.gif) |
| *egg explainer* | *painkillers explainer* |

## What the skill does

- **Two content modes, chosen at intake** — a product/offer **AD** written in 9-figure direct-response style, or a **PURE EXPLAINER** that sells nothing (editorial storytelling, faceless-channel ready, no CTA by default).
- **A quick research pass before writing** — a hard-budgeted web pass (snippets only, under 5 tool calls) so the script carries specific, current substance instead of generic filler.
- **Writes the full voice-over script** — emotion-first, benefit-driven in AD mode; editorial in EXPLAINER mode — then splits it into 10-second clips with internal timeframes.
- **Builds every clip prompt in the locked Vox visual system** — torn-paper collage, cutout elements, one locked font per video, style wording identical across clips so the video reads as one piece.
- **Generates everything itself through the Higgsfield CLI** — live capability check first, then image references, then every clip via Gemini Omni Flash. No canvas, no UI, no timeline — the whole run happens in chat.
- **Chains clips into one continuous animation** — downloads each finished clip, extracts its last frame with ffmpeg, and passes it as a reference into the next clip's generation command before submitting.
- **Handles real products and mascots** — your product image is uploaded and attached as a true generation reference in every clip where it appears; photorealistic mascots are composited so the person stays a real photograph inside the collage.
- **Delivers finished clips in chat** — each one returned with its playable result URL as it completes.

## Requirements

- **[Claude Code](https://claude.com/claude-code)** (or any agent that can follow the skill file).
- **[Higgsfield CLI](https://github.com/higgsfield-ai/cli)** — required (`npm i -g @higgsfield/cli`, then `higgsfield auth login`). All image and video generation runs through it; the skill does not work without it.
- **ffmpeg** — required for last-frame chaining.

## Install

1. Drop `SKILL.md` into your skills directory:

```
mkdir -p ~/.claude/skills/vox-animated-ad-mcp
curl -o ~/.claude/skills/vox-animated-ad-mcp/SKILL.md \
  https://raw.githubusercontent.com/netoferraz/vox-animated-ad-mcp/main/SKILL.md
```

2. Install and authenticate the Higgsfield CLI:

```
npm i -g @higgsfield/cli
higgsfield auth login
```

   Complete the sign-in in the browser it opens. Generation costs credits — `higgsfield account` shows your balance.

3. In Claude Code, say something like:

> *make a vox explainer about how coffee conquered the world*

The skill takes it from there: content mode, research, script, prompt approval, then generation.

## License

[GNU AGPL v3.0](LICENSE) — Copyright (C) 2026 Maxfusion AI.

Free to use, study, modify and share. If you modify it and let others use it —
including over a network — the modified version must be released under the
same license.
