---
title: "Codex_V1 — Library design-brief blocks and fluid-effect fix"
tags: [codex_v1, session-log]
created: 2026-09-17
type: session-log
status: imported
---

# Library design-brief blocks and fluid-effect fix

## Summary
Continued work on "Internal ideas and improvement hub/library.html". Implemented three new Library asset blocks (Quiet Console dashboard, Proof Stack marketing page, Signal Loader intro) from an earlier 11-section web-design research brief, each ambient/auto-cycling rather than requiring real clicks, with a `setInterval`-under-reduced-motion guard pattern added to CODE_MAP.md. Then added two more asset blocks approximating the WebGL Fluid Simulation concept (light-colored and dark-colored ambient blob/lava-lamp backgrounds via Canvas 2D, split specifically for photosensitivity/flashing safety, no mouse input required). The user then reported the fluid effect was broken (dark variant froze into static "bulbs", light variant washed out to solid white); root cause was `ctx.globalCompositeOperation = 'lighten'` creating a one-way brightness ratchet that could only brighten pixels, never dim them. Fixed by switching to `'source-over'` normal blending (matching the existing `createMatrixRain` pattern), verified visually across a 20-second window and via a re-run Playwright suite. Both tasks went through the full Completion Loop (`goal-evaluator` dispatched, verdict `ok` each time) before being reported done.

## Decisions
- Ambient auto-cycling demos stay the house style for all Library asset blocks (console tabs, stack accordion) rather than becoming genuinely operable controls — confirmed with the user via `AskUserQuestion`, consistent with prior blocks (matrix rain, wall effect) and avoids an accessibility contradiction of hiding a real control behind `aria-hidden`.
- Fluid-motion background is a Canvas 2D blob/lava-lamp approximation, not a real WebGL fluid solver — confirmed with the user via `AskUserQuestion` as a deliberate fidelity trade-off appropriate for a decorative sandbox demo.
- Split into two color-scheme blocks (light and dark) specifically as a photosensitivity/flashing-safety measure, not just aesthetic variety — each block stays low-contrast internally by construction (light hues on light background, dark hues on dark background). A toggle between them is a possible future direction, out of scope now.
- Canvas-based effects that call `getBoundingClientRect()` for real pixel sizing (matrix rain, fluid backgrounds) must defer modal-canvas initialization until that modal's first open, guarded by a started-flag — a modal `display:none` canvas reports zero size at page load. Pure CSS/DOM-transform effects (wall, console, stack, signal) don't have this problem and can init eagerly.
- `ctx.globalCompositeOperation = 'lighten'` must never be used for the fluid backgrounds' foreground draws — it only ever brightens a pixel toward the lighter of its current and new value, never dims it, which combined with a background-fade produces a one-way brightness ratchet (light variant washes to solid white, dark variant's periodic paths lock into static bright spots). Normal `'source-over'` blending is required so the trail-fade can actually pull brightness back down each frame.

## Open items
- None explicitly pending from the user as of this session's end. The fluid-effect fix was reported complete with `goal-evaluator`'s verdict quoted; the user has not yet confirmed they're satisfied with the corrected visual result.

## Files touched
- `Internal ideas and improvement hub/library.html`
- `Internal ideas and improvement hub/css/styles.css`
- `Internal ideas and improvement hub/js/site.js`
- `AGENT_LOG.md` (Task 6, Task 7 entries)
- `CODE_MAP.md` (`createConsoleDemo`/`createStackDemo` entry; `createFluidBackground` entry, added then rewritten to lead with the compositing-mode ratchet explanation)
