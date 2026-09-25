---
title: "Tutoring interface — CallSim Town seed + logic tracks complete"
tags: [tutoring interface, session-log]
created: 2026-09-11
type: session-log
status: imported
---

# CallSim Town seed + logic tracks complete

## Summary
Resolved a spec mismatch (folder named "Tutoring interface" but `plan.md` describes "CallSim Town," a call-center simulation platform) in the user's favor of `plan.md`. Split the project into `logic/` (six spec docs: data model, scenario config schema, state machine, simulation rules, KPI formulas, scoring rubric) and `seed/` (a self-hosted HTML/CSS/JS visual mockup with no real backend). Built `seed/` checkpoint by checkpoint via the design-canvas skill: app shell/nav, dashboard (3x2 KPI grid), Town View (5x5 isometric Three.js grid with sentiment/wait-time color coding, click-to-inspect, filter/pause/rewind toolbar, toggleable executive KPI overlay), and Training View (scenario library, session flow, scoring report using the exact `logic/scoring-rubric.md` formula). A live-reload dev server was run on port 8123 throughout for real-time review. Both tracks were verified complete via the mandatory `goal-evaluator` Completion Loop, including a whole-task check that caught and fixed one real bug (a dashboard pulse-glow animation hardcoded to the dark theme's literal color instead of using `color-mix` against the current theme token).

## Decisions
See `decisions.md` in this project folder for the full list; the durable choices from this session are logged there (spec authority, seed/logic split, build order, visual direction, executive-view overlay choice, and the delegation-to-subagents working style).

## Open items
- None outstanding — both `logic/` and `seed/` tracks are complete per the two-folder plan approved at project start.
- This is a clean session boundary; a future session can pick up with a new feature/checkpoint if one is requested.

## Files touched
- `logic/data-model.md`, `logic/scenario-config-schema.md`, `logic/state-machine.md`, `logic/simulation-rules.md`, `logic/kpi-formulas.md`, `logic/scoring-rubric.md`
- `seed/index.html`, `seed/css/tokens.css`, `seed/css/base.css`, `seed/js/theme.js`, `seed/js/nav.js`
- `seed/css/dashboard.css`, `seed/js/dashboard.js`
- `seed/css/town.css`, `seed/js/town.js`, `seed/vendor/three/three.module.js`
- `seed/css/training.css`, `seed/js/training.js`
- `seed/direction-check.html` (kept as a design reference artifact)
- `AGENT_LOG.md`, `CODE_MAP.md` (updated throughout as the project's source of truth)
