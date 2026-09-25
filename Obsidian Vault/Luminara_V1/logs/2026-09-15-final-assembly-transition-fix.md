---
title: "Luminara_V1 — Final assembly and transition-duplication fix for Video1RecognitionWall"
tags: [luminara_v1, session-log]
created: 2026-09-15
type: session-log
status: imported
---

# Final assembly and transition-duplication fix for Video1RecognitionWall

## Summary
All 7 phase clips of `Video1RecognitionWall` (the Employee Recognition Wall promo video) had already been rendered and QA-confirmed individually. The user asked to assemble them into the final video and reported that some phase clips appeared to start with content from the previous scene. Root-caused this to `render-phases.mjs` rendering each phase's `frameRange` as its own `TransitionSeries.Sequence` local span, which already includes the 18-frame transition-blend window shared with each neighbor — so every transition was rendered twice and replayed on concat. Fixed by re-rendering the full 1152-frame composition as six non-overlapping 192-frame chunks and stream-copy concatenating them with the ffmpeg binary already bundled inside Remotion's compositor package. Final deliverable: `remotion/out/final/Video1RecognitionWall.mp4` (1152 frames, ~38.5s, 1280x720, h264/aac).

## Decisions
- Chunk boundaries for re-assembly can fall anywhere in the composition (including mid-transition) as long as consecutive chunks are exactly back-to-back with no overlap/gap — no special-casing of transition frames needed, since Remotion frames are a pure function of frame number.
- Used the ffmpeg binary already bundled in `@remotion/compositor-win32-x64-msvc` instead of installing a system-wide ffmpeg (none is on PATH in this environment) — honors the project's "do not install tools system-wide" rule.
- That bundled ffmpeg has a restricted filter set (no `select`/`trim` video filters) — QA frame extraction had to use accurate `-ss`-based seeking instead of filter-based frame selection.
- Kept re-render chunk size near the previously-proven-safe ~200-frame length as a hedge against the `angle` GL backend's known long-render memory leak.

## Open items
- None — Task 11 is complete, goal-evaluator returned `ok`, and visual QA (all 6 internal seams pixel-identical, transition blend confirmed intact) passed. Awaiting user review of the final assembled video before any further work.

## Files touched
- `remotion/out/assembly/seg1.mp4` … `seg6.mp4` (new, six 192-frame chunks)
- `remotion/out/assembly/concat_list.txt` (new)
- `remotion/out/final/Video1RecognitionWall.mp4` (new — final deliverable)
- `remotion/out/qa/seams/*.png` (new — QA stills)
- `CODE_MAP.md` (new entry: `render-phases.mjs` frameRange vs. TransitionSeries overlap lesson)
- `AGENT_LOG.md` (Decision entry + Task 11 complete entry)
