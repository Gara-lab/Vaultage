---
title: "Loan_application_requirement — Duplicate-detection hook, task-declaration fields, and closed architecture threads"
tags: [loan_application_requirement, session-log]
created: 2026-08-27
type: session-log
status: imported
---

# Duplicate-detection hook, task-declaration fields, and closed architecture threads

## Summary
Ran `/fewer-permission-prompts` to add two read-only Bash patterns (`node --check *`, `curl -sf http://127.0.0.1:*`) to `.claude/settings.json`. Produced a token/quality efficiency report grounded in real session/transcript data. Investigated the `learn-claude-code` reference repo's task-claiming system (s07/s11) and hooks system (s04) to address two remaining duplication failure modes not covered by the earlier cross-task `Produces`/`Depends on` fix. Built and tested a deterministic `PostToolUse` hook (`.claude/hooks/check_duplication.py`) that rescans `site/js/*.js` after every Edit/Write and flags near-duplicate 6+-line blocks — catching the copy-paste class of bug that `enforcer` (a model-judgment reviewer) had missed three times. Extended `planner.md` to require `Depends on` / `Produces` / `Directly related tasks` fields on every task plan entry, and updated `CLAUDE.md` so the lead agent pastes sibling tasks' declared `Produces` verbatim into Implementer dispatch prompts. Both changes passed the Completion Loop (`goal-evaluator: ok`). Closed out a follow-up architectural discussion about vault-hosted skills and a teammate/task-board capability — both declined for this project, confirmed by the user as cross-project future-use ideas, not needed here.

## Decisions
- Read-only Bash allowlist extended with `node --check *` and `curl -sf http://127.0.0.1:*` in `.claude/settings.json`.
- New `PostToolUse` hook (`check_duplication.py`) wired into `.claude/settings.json`, scoped to `site/js/*.js` only, tuned to `WINDOW_LINES=6` / `MIN_SIGNIFICANT_CHARS=40` after an over-sensitive first calibration produced too many false positives.
- `planner.md` PLAN mode now requires `Depends on` / `Produces` / `Directly related tasks` on every task-plan entry; `CLAUDE.md` requires the lead agent to paste sibling tasks' `Produces` verbatim into Implementer dispatch prompts.
- Standing rule adopted: a capability needing constant/semi-constant verification should be a Subagent (dispatch enforceable by process), not a Skill (depends on discretionary recall). Neither mechanism burns context just by existing in the project — both are lazy-loaded.
- Declined for this project: moving skills/subagents into the Obsidian vault (no token-saving benefit — premise was false), and building a persistent teammate/task-board capability (existing `Agent` + `Workflow` tools already cover this project's actual parallelism needs). Both confirmed by the user as cross-project future-use ideas to revisit separately, not required here.

## Open items
None. Both architectural threads (vault-skill migration, teammate/task-board capability) were explicitly closed by the user as not needed for this project. Module 1 (docs) and Module 2 (site) remain complete and verified from the prior session.

## Files touched
- `.claude/settings.json` (permission allowlist + new `hooks.PostToolUse` entry)
- `.claude/hooks/check_duplication.py` (new)
- `.claude/agents/planner.md` (task-plan field requirements)
- `CLAUDE.md` (Implementer dispatch-prompt rule)
- `AGENT_LOG.md` (decision entries for the hook/planner change and the declined vault-skill/teammate-board threads)
