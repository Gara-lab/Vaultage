---
title: "Customer support ticketing system — coding/video clone split"
tags: [customer-support-ticketing-system, session-log]
created: 2026-09-13
type: session-log
status: imported
---

# Coding/video clone split

## Summary
Continued from the mobile-first Short1Helpdesk.mp4 revisions (phone mockup, cursor easing, beat
content accuracy, and a final +2s-per-beat lengthening — all completed and goal-evaluator-verified
earlier in the session). The user then asked how much the video-creation skill set had actually
improved through repeated use; the answer was that the skills' own "promote improvements back into
the shared library" compounding mechanism never fired here — two real fixes (cursor easing, phone
mockup rendering) were forked into shot-local code in `Short1Helpdesk.tsx` instead of being promoted
into the shared `remotion/src/lib/screencast.tsx`, so that library is unimproved from before this
project touched it. This led the user to request a structural split: the root previously mixed a
static ticketing-site harness (`.claude/`, `CLAUDE.md`, `ARCHITECTURE.md`, `CONTRACTS.md`,
`AGENT_LOG.md`, `CODE_MAP.md`) with an unrelated video-production pipeline (`remotion/`, `tools/`,
12 video skills) merged in by accident from another project, governed by an awkward "Scope guard"
section telling the agent to ignore the video content. After an initial misunderstanding (building
this as a nested `remotion/CLAUDE.md` subtree) was corrected by the user, two full standalone sibling
clones were built under the project root: `coding-clone/` (site code only, trimmed docs, no Scope
guard needed, design-canvas + planning skills, fresh empty `.venv`) and `video-clone/` (remotion +
tools + media + shorts + brand.md, all 12 video skills, new docs including a visual-QA-aware
Completion Loop and a new "Library-first" rule, fresh empty `.venv`). The original root was left
completely untouched. A `goal-evaluator` dispatch verified the full split: `VERDICT: ok` — both
clones have exactly the expected scoped contents, no cross-contamination, correct venv paths, and
the root shows no post-clone modification.

## Decisions
- Split the mixed root into two independent clones rather than nesting a second harness inside
  `remotion/` — each clone is meant to be relocated to its own project location later.
- AGENT_LOG.md/CODE_MAP.md video-only entries were copied in full into `video-clone/`, not
  relocated-with-pointer, so each clone's history reads as a complete, self-contained record.
- Shared infra (`goal-evaluator.md`, `settings.json`, `workflows/`) was duplicated fully into each
  clone's own `.claude/`, rather than kept shared from one canonical location.
- Neither clone's `.venv` was copied from the original — each got a freshly bootstrapped, empty
  `.venv` via `scripts/setup-venv.ps1`, since a copied venv's activation scripts embed the absolute
  path it was created at and would break once the clones are relocated.
- `video-clone/CLAUDE.md` gained a new "Library-first" rule: before writing shot-local code, check
  whether `remotion/src/lib/` already solves it; a shot that forks something local instead of
  improving the shared lib must be flagged in CODE_MAP.md as a promotion candidate.

## Open items
- `sampleCursor`/`EASE_CURSOR` (phone-mockup rendering, snappier cursor easing) remain shot-local in
  `video-clone/remotion/src/shots/short-1/Short1Helpdesk.tsx`, flagged in `video-clone/CODE_MAP.md`
  as an un-promoted promotion candidate — the next video that would benefit from either should
  promote them into `lib/screencast.tsx` first, or explicitly note why it forked again.
- The user plans to relocate `coding-clone/` and `video-clone/` to their own separate project
  locations later; no further action needed from this session.

## Files touched
- `coding-clone/` — new clone: CLAUDE.md, ARCHITECTURE.md, CONTRACTS.md, AGENT_LOG.md, CODE_MAP.md,
  HOW_TO_USE.md, .gitignore, .claude/ (design-canvas + planning skills), fresh .venv, and all
  site code/assets copied unmodified.
- `video-clone/` — new clone: CLAUDE.md, ARCHITECTURE.md, CONTRACTS.md, AGENT_LOG.md, CODE_MAP.md,
  HOW_TO_USE.md, .claude/skills/README.md, fresh .venv, and remotion/ + tools/ + media/ + shorts/ +
  brand.md + .env.example + .gitignore copied unmodified.
- Original root — untouched (verified by mtime scan in the goal-evaluator dispatch).
