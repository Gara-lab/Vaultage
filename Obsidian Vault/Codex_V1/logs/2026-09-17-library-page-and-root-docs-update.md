---
title: "Codex_V1 — Library page (asset sandbox) + root docs lessons update"
tags: [codex_v1, session-log]
created: 2026-09-17
type: session-log
status: imported
---

# Library page (asset sandbox) + root docs lessons update

## Summary
Added a new "Library" page to the "Internal ideas and improvement hub" sub-project: a sandbox for testing/storing individual visual assets (background/motion effects) before they'd be promoted into the main site, using the same card+modal interaction pattern already proven on the idea board. Built two asset blocks — a CSS drifting-gradient background and a canvas-based "hacker effect" (matrix-rain) background — including two rounds of user-requested tweaks to the matrix effect (slower fall speed, English-alphabet-only character set). Each build step was verified live via Playwright (not just static review) and passed through the mandatory `goal-evaluator` completion check. Closed the session by updating Codex_V1's root governance docs (CODE_MAP.md, ARCHITECTURE.md, AGENT_LOG.md) so this session's technical gotchas and process-level lessons are captured for reuse in future, unrelated Codex_V1 projects.

## Decisions
- "Internal ideas and improvement hub" gained a second page, `library.html`: a sandbox for testing/storing visual assets before they're considered for the live site. Each asset is a self-contained "asset block" (card + demo + pop-up modal with a larger version of the same demo), mirroring the idea-board card pattern.
- Each asset block gets its own dedicated modal (one-modal-per-block), not a single shared modal — a shared modal only worked while there was exactly one block; a second, structurally different block (canvas vs. CSS div) needed either a content-cloning fill function or a separate modal per block, and the latter was chosen to match the codebase's existing explicit-named-controller style.
- Process/workflow lessons from this session, meant to generalize to future unrelated Codex_V1 projects (also recorded in the project's own AGENT_LOG.md "Lessons" section):
  - Never trust a subagent's self-report of what it did — independently re-verify live (this session used ad-hoc Playwright scripts exercising real clicks/keyboard nav/canvas frame-diffing, not just re-reading files).
  - Only the lead agent should dispatch `goal-evaluator` before declaring work done — a subagent's own nested self-invocation isn't authoritative.
  - Watch for CSS shorthand-property cascade collisions: two different class selectors applying to the same element that both declare the same shorthand property (e.g. `display`, `transition`) don't merge — only one rule's full declaration wins the cascade. This caused one real bug (`.submit-form`/`[hidden]` vs. `display`) and was deliberately designed around a second time by keeping `transition` off a new shared `.reveal-on-scroll` class.
  - Apply design-token discipline (no hardcoded hex/rgba in new CSS) proactively while writing new rules, rather than reactively after a `goal-evaluator` block catches it.
  - A "reusable template" component verified against only one instance can still hide bugs that only show up at N=2 — sanity-check a template pattern against at least two real instances before trusting it as proven.

## Open items
- No further Library asset blocks, site features, or vault-save actions were requested beyond this save.
- None else — the user has not indicated further work for this session.

## Files touched
- `Internal ideas and improvement hub/index.html` — Library nav link, `.reveal-on-scroll` class on idea cards.
- `Internal ideas and improvement hub/library.html` — new page; two asset blocks (gradient, matrix) + two dedicated modals.
- `Internal ideas and improvement hub/css/styles.css` — `.asset-library`/`.asset-block` rules, shared `.reveal-on-scroll` class, matrix color tokens.
- `Internal ideas and improvement hub/js/site.js` — `createMatrixRain`, per-block modal wiring, `.reveal-on-scroll` query update.
- `Codex_V1/CODE_MAP.md` — 6 new gotcha entries.
- `Codex_V1/ARCHITECTURE.md` — refreshed module breakdown (two-page site, Library module).
- `Codex_V1/AGENT_LOG.md` — Task 3/4 entries, new Decision, new "Lessons" section.
