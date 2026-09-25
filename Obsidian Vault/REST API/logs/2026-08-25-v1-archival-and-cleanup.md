---
title: "REST API — V1 archival, repo review, and cleanup"
tags: [rest-api, session-log]
created: 2026-08-25
type: session-log
status: imported
---

# V1 archival, repo review, and cleanup

## Summary
User created a `V1/` folder and asked for the whole project to be reorganized around a versioned-folder layout: the project root now holds only governance/source-of-truth files (`CLAUDE.md`, `.claude/`, `ARCHITECTURE.md`, `CONTRACTS.md`, `AGENT_LOG.md`), while the runnable program (Modules 1-4: `app/`, `tests/`, `ui/`, `pyproject.toml`, `HOW_TO_USE.md`) was moved into `V1/`, a frozen, rewindable snapshot. Old root-level `.venv`, `app.egg-info`, and `.pytest_cache` were deleted (regenerable) and recreated inside `V1/`; full suite re-verified passing (164 tests) from the new location. `goal-evaluator: ok`. Then, since `.claude/settings.json` and `CLAUDE.md` had both been edited, did a full review of everything outside `V1/` (8 files), surfacing one real typo in CLAUDE.md and one real chronological-ordering issue in `AGENT_LOG.md`'s Progress section (a "Task 13" entry had ended up placed after "Task 14" entries); confirmed `goal-evaluator: ok` with no security/secrets issues. User then asked for both to be fixed, which was done and re-verified `goal-evaluator: ok`.

## Decisions
- Adopted a versioned-folder repository layout: `V1/` holds the current runnable program as a frozen snapshot; `CLAUDE.md`, `.claude/`, `ARCHITECTURE.md`, `CONTRACTS.md`, and `AGENT_LOG.md` stay at the project root as the shared, version-spanning source of truth. Future work happens in a new version folder (e.g. `V2/`) alongside `V1/`, not by editing `V1/` in place. Reason: user is starting a second version of the program and wants V1 preserved as a rewindable, reusable foundation.
- `AGENT_LOG.md` stays at the root (not per-version) as one continuous cross-version log, per user's explicit choice.
- Regenerable build artifacts (`.venv`, `app.egg-info`, `.pytest_cache`) are deleted and recreated rather than moved when restructuring, since `pyproject.toml` fully specifies dependencies.

## Open items
- No V2 planning has begun yet — the user hasn't specified what the second version should contain or how it should differ from V1.
- Same two backlog items carried over from the Module 3/4 log (error-code string literals not yet converted to `ErrorCode` enum members; missing `lastUpdated`-unchanged assertion in one Module 4 test) — both live inside `V1/` now, untouched this session.

## Files touched
- Moved into `V1/`: `app/`, `tests/`, `ui/`, `pyproject.toml`, `HOW_TO_USE.md` (plus a regenerated `.venv` inside `V1/`)
- Deleted from root: old `.venv`, `app.egg-info`, `.pytest_cache`, a stray 0-byte `.py` file
- `ARCHITECTURE.md` — added "Repository layout (versioned)" section
- `AGENT_LOG.md` — added Task 15 (archival) progress entry and a versioned-layout decision entry; fixed a Task 13/Task 14 ordering bug
- `CLAUDE.md` — fixed a typo in the bash-approval-explanation rule
- `.claude/settings.json` — reviewed only, unchanged this session (previously had 3 MCP read-only patterns added)
