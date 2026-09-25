---
title: "Tutoring interface — Decisions"
tags: [tutoring interface, decisions]
created: 2026-09-11
type: decisions
status: imported
---

# Decisions

- **2026-09-11** — `plan.md` ("CallSim Town," a call-center agent simulation platform) confirmed by the user as the authoritative spec over the stale "Tutoring interface" folder name.
- **2026-09-11** — Project split into two top-level folders: `seed/` (self-hosted HTML/CSS/JS visual-only MVP mockup, no real backend/data) and `logic/` (business rules, data model, simulation/KPI/scoring logic as spec docs, not necessarily code). Reason: lets UX get validated fast without the simulation engine blocking it, while `logic/` becomes the real spec the eventual implementation is built from. Risk: `seed/` must only use rules already written in `logic/`, never invent behavior backfilled later, or the two will drift.
- **2026-09-11** — Build order is `logic/` docs before the `seed/` mockup, so mock data/behavior is shaped by already-written rules rather than the reverse.
- **2026-09-11** — `seed/`'s visual direction is "technical & precise," Grafana/Datadog-style dense monitoring-dashboard convention, with the isometric town as one panel within that dashboard rather than the primary visual language (chosen via design-canvas intake over a Linear-style minimal-chrome direction and a SimCity-style town-first layout).
- **2026-09-11** — Executive View in the Town View is an overlay on the live 3D scene (Option B: KPI strip overlaid on the scene), not a scene replacement (Option A), per the user's choice after viewing both as live screenshots.
- **2026-09-11** — Long/complex projects on this account should have implementation delegated to subagents/teammates/background workflows rather than the lead agent authoring every step directly, to avoid burning the lead's context window; the lead's role is coordination, review, and enforcement.
