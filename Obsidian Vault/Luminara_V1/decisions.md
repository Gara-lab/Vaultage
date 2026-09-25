---
title: "Luminara_V1 — Decisions"
tags: [luminara_v1, decisions]
created: 2026-09-15
type: decisions
---

- **2026-09-15** — When re-assembling a `@remotion/transitions` `TransitionSeries` composition from rendered chunks, chunk boundaries must be non-overlapping absolute frames across the whole composition, not per-phase `frameRange` spans — a phase's own local span already includes the transition-blend window shared with each neighbor, so per-phase chunks duplicate every transition on concat.
- **2026-09-15** — Use the ffmpeg binary already bundled inside `@remotion/compositor-win32-x64-msvc` for local video concat/frame-extraction needs instead of installing a system-wide ffmpeg, since none is on PATH in this environment; note it has a restricted filter set (no `select`/`trim` video filters), so frame-exact extraction needs `-ss`-based seeking instead.
