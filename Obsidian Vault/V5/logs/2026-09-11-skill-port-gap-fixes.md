---
title: "V5 — Skill-bundle comparison, gap fixes, and prerequisites doc"
tags: [v5, session-log]
created: 2026-09-11
type: session-log
status: imported
---

# Skill-bundle comparison, gap fixes, and prerequisites doc

## Summary
Compared the two source skill-bundle zips (`claude_short_creator`, `claude_video_editor`) against each other and against this project's already-merged `.claude/skills/`+`tools/` port, on efficiency/accuracy/workflow and on real-use quality for editing a video vs. creating a short. That review surfaced three gaps: `remotion/`/`brand.md`/media libraries were never backfilled, `suggest-sfx`'s SKILL.md only covered the video-domain path convention, and `tools/gen_vo.mjs`'s locked-voice `ARCHITECTURE.md` entry could be confused with `tools/gen_voice.py`'s separate one. All three were fixed same-day (remotion backfill via Implementer + Enforcer subagents, suggest-sfx and ARCHITECTURE.md rescoping done directly), and a follow-up question ("what's needed to actually run this in Claude Code") led to adding a permanent "Prerequisites" checklist to `CLAUDE.md` so future sessions auto-check the toolchain (npm install, ffmpeg/ffprobe, Python deps, `.env` keys, media assets) before running anything, without installing anything now.

## Decisions
- See `decisions.md` for the durable ones (provider-abstraction pattern, brand-triad placeholder, honest-by-construction content policy, prerequisites-in-CLAUDE.md approach).

## Open items
- `npm install` for `remotion/`, ffmpeg/ffprobe binaries, `.env` population, and any actual render/execution are all still not done — deliberately deferred, not yet requested.
- `brand.md` §4 has a known pre-existing inconsistency (says Spectral/`FONT_SERIF` is retired for wordmarks, but `kit.tsx`'s Claude Code wordmark clone still uses it) — left as-is, to be resolved whenever `/brand-setup` runs.

## Files touched
- `CLAUDE.md` (added Prerequisites section)
- `AGENT_LOG.md` (multiple progress/error entries, one marked RESOLVED)
- `ARCHITECTURE.md` (gen_vo.mjs rescoping + two new decision-log entries)
- `CODE_MAP.md` (~25 new entries for backfilled remotion content, one corrected post-Enforcer)
- `.claude/skills/suggest-sfx/SKILL.md` (dual path-convention fix)
- `remotion/` (backfilled: root scaffold, src/lib/ union, brand triad, src/shots/brand/)
- `brand.md` (new, hand-merged §8)
