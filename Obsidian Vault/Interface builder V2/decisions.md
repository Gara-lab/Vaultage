---
title: "Interface builder V2 — decisions"
tags: [interface-builder-v2, decisions]
created: 2026-09-08
type: decision-log
status: imported
---

# Decisions

- **2026-09-08** — Unified productivity app (Kanban + Notes + Calendar) under one shared nav and one design-token set, built as plain static HTML/CSS/JS with no framework and no build step, reason: Static_projects convention, no dependency justifies itself for this scope. Built with ponytail lazy-mode applied throughout (native platform features preferred over custom code/libraries).
- **2026-09-08** — Palette is beige/tan (`--bg #f1e7d6`, `--surface #f9f4ea`) as the main theme with two green accents (`--heading #3e6b54`, `--accent #3c6b52`) and a tan/brown accent (`--accent-2 #6b4e30`), reason: user-directed during design-canvas Phase B direction check (liked the "Docs" beige/light-brown theme plus the "Design"/"Bug" greens); all color pairs re-tuned to pass WCAG AA contrast (>=4.5:1) via `check_contrast.py`.
- **2026-09-08** — Drag-and-drop implemented with native HTML5 DnD + a small hand-rolled FLIP animation helper instead of a library, reason: no dependency installed and none needed for this scope.
- **2026-09-08** — Single `index.html` shell with in-page tab nav (`shell.js`) instead of separate HTML pages per view, reason: user explicitly wants only one page load ("don't make me load a completely different html file each time"); per-view JS/CSS still stays in its own file (`app.js`, `notes.js`) for organization, only the markup lives together in `index.html` as toggled `.view` sections.
- **2026-09-08** — `contentEditable` on Kanban card titles must be flipped to `true` on `mousedown`, never on `click` or via a later `focus()` + manual selection call — toggling on `click` is too late for native caret placement and any compensating `selectAllChildren()` reintroduces the "whole title selected on single click" bug. Documented in `CODE_MAP.md` so it isn't reintroduced.
- **2026-09-09** — Each Kanban tag-picker state (None/Design/Bug/Docs) must have its own distinct color pair, no sharing. Bug uses a new rust/terracotta (`--accent-3` #a6402b / `--accent-3-soft` #f4ddd3) instead of Design's green; None uses a new neutral grey (`--neutral-soft` #e4e1d8) instead of Docs' tan family. All pairs WCAG AA verified.
- **2026-09-09** — Calendar ships month view only as its own checkpoint; week/day views and drag-to-create time-range events (from the original Calendar concept) are deferred, not part of this task's scope.
- **2026-09-09** — Calendar reuses Kanban's existing 4-category tag-picker (None/Design/Bug/Docs) and its color tokens for event categories, instead of introducing a separate calendar-specific taxonomy or palette.

## Logs
- [[Interface builder V2/logs/2026-09-08-kanban-notes-unified-shell-tag-picker|Kanban notes unified shell tag picker]]
- [[Interface builder V2/logs/2026-09-09-calendar-month-view-and-workflow-review|Calendar month view and workflow review]]
- [[Interface builder V2/logs/2026-09-09-tag-picker-completion-and-distinct-colors|Tag picker completion and distinct colors]]
