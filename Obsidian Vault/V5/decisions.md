---
title: "V5 — Decisions"
tags: [v5, decisions]
created: 2026-09-11
type: decisions
---

- **2026-09-11** — Any tool script calling one paid vendor for a generic creative capability (TTS, SFX, music, image, video-clip, avatar, transcription) gets isolated behind a `PROVIDERS` dict + `<CAPABILITY>_PROVIDER` env var, so vendors can be swapped without lock-in. Destination-specific integrations (YouTube upload, Notion sync) and intentionally single-vendor tools are left un-abstracted.
- **2026-09-11** — The `remotion/` backfill's brand triad (brand.md + brand.ts from `video_editor`, fonts.ts from `short_creator`) is a deliberate, working-but-generic placeholder, not a real brand identity — expected to be superseded the first time `/brand-setup` runs.
- **2026-09-11** — "Honest-by-construction" is a house content policy for physics/geography/probability niche shorts: the video must derive its payoff from real computation at render time (real projections, real numerical integration, seeded Monte-Carlo, real synthesis), never fake it with an authored animation that merely looks right.
- **2026-09-11** — Environment prerequisites for the ported `remotion/`/`tools/` skills (npm install, ffmpeg/ffprobe on PATH, per-script Python deps, `.env` API keys, `media/library` assets) are documented directly in `CLAUDE.md` (auto-loaded every session) rather than a separate doc, with a standing rule: check before running, confirm with the user before installing anything missing.
- **2026-09-12** — `.venv/` and `.node_env/` are never portable across project copies (they embed absolute paths at creation time) — a new project made from this template must run `scripts/setup-venv.ps1` fresh rather than copying either folder over. `tools/bin/`'s ffmpeg/ffprobe `.exe` binaries have no embedded paths and can be copied directly instead of re-downloaded.
