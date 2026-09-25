---
title: "Interface builder V2 — Kanban+Notes unified shell, tag-picker in progress"
tags: [interface-builder-v2, session-log]
created: 2026-09-08
type: session-log
status: imported
---

# Kanban+Notes unified shell, tag-picker in progress

## Summary

Used the design-canvas skill to design and build a unified static productivity app
(Kanban board → Notes → Calendar, in that order) as one shared design system, plain
HTML/CSS/JS, ponytail lazy-mode applied throughout per user request. Built Kanban
(native HTML5 drag-and-drop + hand-rolled FLIP animation, click-to-edit card titles,
add-card per column) and Notes (native `details`/`summary` collapsible sections,
selection-driven `execCommand` formatting toolbar, tag filtering) as separate
checkpoints, each verified via the goal-evaluator Completion Loop. Palette iterated
through several rounds of user feedback to a beige/tan theme with two green/brown
accents, all pairs WCAG AA verified. Per user correction, merged the two views into a
single `index.html` shell with an in-page tab nav (`shell.js`) instead of separate page
loads, deleting the standalone `notes.html`. Fixed a user-reported bug where clicking a
card title to edit it selected the entire text instead of placing the caret — root
cause was flipping `contentEditable` on `click` instead of `mousedown`; fixed and the
gotcha recorded in `CODE_MAP.md` per the user's explicit "make sure it won't come back"
request. Currently mid-implementation on a Kanban card tag-type picker (None/Design/
Bug/Docs, changeable per-card): first attempt used an unstyled native `<select>` which
the user rejected as "really ugly"; now restyled with `appearance: none` + a custom SVG
chevron so it still looks like the original pill-shaped tag chip, color-coded by a
`data-type` attribute, contrast-checked. 5 of 8 existing cards converted; remaining
work is 3 more cards, wiring `app.js` to sync `data-type` on selection change, and
defaulting new cards to a grey "None" tag.

## Decisions

See `decisions.md` for the durable ones (palette, native-DnD-over-library, single-page
shell, mousedown-vs-click contentEditable gotcha) — not repeated here.

## Open items

- Finish the Kanban tag-picker feature: convert the remaining 3 cards ("Collapsible
  section animation for notes", "Set up shared design tokens", "Wire month/week/day
  view transitions") from static `.tag` spans to `.tag-picker` selects; add a `change`
  listener in `app.js` to sync `dataset.type`; default new cards (from the
  `.column-add` button) to a grey "None" tag-picker.
- Re-grep changed files for stray comments (zero-comments rule) and re-verify new
  color pairs with `check_contrast.py` before declaring the feature done.
- Run the Completion Loop (`goal-evaluator`) for the tag-picker feature and log the
  verdict in `AGENT_LOG.md`.
- Build the Calendar view (3rd tab): click-and-draw event creation, color-coded
  categories, month/week/day view transitions — same design-canvas checkpoint process
  as Kanban/Notes.

## Files touched

- `index.html` (Kanban + Notes markup, tab shell, tag-picker CSS)
- `tokens.css` (shared palette/design tokens)
- `app.js` (Kanban DnD, FLIP, card editing, tag-picker wiring in progress)
- `notes.js` (selection toolbar, tag filtering)
- `shell.js` (tab switching)
- `CODE_MAP.md`, `AGENT_LOG.md` (gotcha + decision + progress entries)
- `notes.html` deleted (merged into `index.html`)
