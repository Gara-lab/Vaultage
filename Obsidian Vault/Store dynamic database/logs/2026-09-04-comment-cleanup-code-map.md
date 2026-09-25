---
title: "Store dynamic database — Comment cleanup + CODE_MAP.md"
tags: [store-dynamic-database, session-log]
created: 2026-09-04
type: session-log
status: imported
---

# Comment cleanup + CODE_MAP.md

## Summary
User flagged that roughly a third of the codebase was inline comments, and questioned
the point of maintaining extensive spec `.md` files if the same explanations were also
duplicated as code comments. An audit confirmed ~34% comment density project-wide (up
to 40-41% in the two most recently touched files). Recommended against AST-parsing
tooling as disproportionate for this project's scale (10 files, ~3065 lines) and
proposed a hand-authored `CODE_MAP.md` instead — the user approved and escalated to an
absolute requirement: zero comment lines anywhere in `js/*.js`, with `CODE_MAP.md`
capturing everything genuinely non-obvious that the comments used to carry, plus a
durable enforcement mechanism so the regression can't recur silently. Ran the full
CM1-CM5 pipeline (planner PLAN mode → 4 parallel Agent dispatches doing per-file
extraction+stripping → two content promotions to proper spec docs → enforcement wiring
→ enforcer review → goal-evaluator judgment), fully verified and reported to the user
as complete. Also answered a follow-up factual question ("is the app mobile-first?")
by checking actual evidence (viewport meta tag, CSS media-query direction, nav
breakpoint behavior) rather than trusting ux.md's claims alone — confirmed yes.

## Decisions
- Zero comments in `js/*.js`, no exceptions (not even JSDoc) — durable rule added to
  CLAUDE.md itself, 2026-09-04. Any non-obvious why/invariant/gotcha goes into
  `CODE_MAP.md` instead; a genuine product/business decision hiding in what would have
  been a comment gets promoted into the applicable spec doc instead (ux.md, architecture.md
  decision log, etc.), not into `CODE_MAP.md`.
- Enforcement mechanism chosen: CLAUDE.md rule + a new "Zero stray comments" checklist
  item in `.claude/agents/enforcer.md`, checked on every future task — not a git hook
  (project has no git repo) and not a lint/CI step (disproportionate for this scale).
- `CODE_MAP.md` format: hand-authored and hand-maintained (no AST parsing, no
  doc-generation script), one entry per non-obvious code region, anchored by
  `file.js → functionName()` (never a line number, since nothing keeps line numbers in
  sync), three fields — Location / Why-invariant-gotcha / Spec cross-reference.
- Two genuine spec-doc promotions found while extracting comments: `format.js`'s
  zero-amount unsigned-money-rendering rule → new ux.md FMT-2; `validate.js`'s
  `validateItemInput` 3-argument signature → corrected a stale architecture.md T4
  Produces line that had only documented the 1-argument shape.
- Confirmed: the app is mobile-first (viewport meta tag, base CSS unqualified for
  mobile with `min-width: 768px` breakpoints scaling up, bottom tab nav by default
  becoming a top nav only at the wider breakpoint) — matches ux.md's MOB-1/NAV-2 claims.

## Open items
None — the comment-cleanup task (CM1-CM5) is complete, verified by both `enforcer` and
`goal-evaluator` with `ok` verdicts. View Items work remains cancelled per the user's
own explicit instruction earlier in the session (no longer necessary, nothing was
started).

## Files touched
- CODE_MAP.md — new file, all extracted comment content
- All 10 `js/*.js` files — every comment line removed (app.js, calc.js, calc.test.js,
  db.js, format.js, image.js, validate.js, view-accounting.js, view-add-item.js,
  view-items.js)
- architecture.md — new D10 decision, full "Comment cleanup & CODE_MAP.md" section,
  corrected T4 Produces line for `validateItemInput`
- ux.md — new FMT-2 bullet
- risks.md — new R8 (mechanical risk of stripping ~1000 comment lines with no git
  safety net)
- data-model.md — cross-reference bullet to D10
- CLAUDE.md — new zero-comments-in-js rule
- .claude/agents/enforcer.md — new "Zero stray comments" checklist item
- AGENT_LOG.md — full task-status and decision log for CM1-CM5
