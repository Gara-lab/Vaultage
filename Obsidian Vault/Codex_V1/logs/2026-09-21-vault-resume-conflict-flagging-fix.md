---
title: "Codex_V1 — vault-resume conflict-flagging fix"
tags: [codex_v1, session-log]
created: 2026-09-21
type: session-log
status: imported
---

# vault-resume conflict-flagging fix

## Summary
Session started with a full folder review and `/vault-resume`. The project root currently only contains an empty `Anti-pomodoro/` subfolder and blank template governance docs (AGENT_LOG.md/ARCHITECTURE.md/CONTRACTS.md/CODE_MAP.md) — none of the three subprojects described in the vault's prior logs ("Service website refinement/", "Internal ideas and improvement hub/", "Customer support ticketing system/") exist on disk. This was initially flagged to the user as a disk/vault conflict. The user corrected that: in this factory-root workspace, a new empty named subfolder appearing, or a previously-logged subfolder no longer being present, is normal factory turnover (projects finish/move elsewhere or haven't started yet) — not an error or sync discrepancy — and the same applies if an older project folder is brought back into the root. This is now a standing rule for all future `/vault-resume` (or similar) checks in Codex_V1.

## Decisions
- Confirmed here for permanence (already captured in local memory too): a new empty named subfolder, a previously-described subfolder missing from disk, or an older project folder being reintroduced into Codex_V1's root are all normal factory-workspace turnover, not errors or vault/disk conflicts. Never flag these as discrepancies during `/vault-resume` or similar — just treat current disk state as the current project scope and proceed.

## Open items
- None from this session beyond the rule confirmation above.

## Files touched
- None (docs-only correction, saved to memory + vault).
