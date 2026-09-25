---
title: "Interface builder — decisions"
tags: [interface-builder, decisions]
created: 2026-09-07
type: decision-log
status: imported
---

# Decisions

- **2026-09-07** — Removed `@corbe30/fortune-excel`; added `chart.js` and `@office-kit/xlsx@0.11.0` as the real dependencies for the v2 template-builder editor. ExcelJS-based export (which `@corbe30/fortune-excel` wrapped) cannot write native Excel chart objects; `@office-kit/xlsx` can, at the cost of being pre-1.0. The `export` module isolates this dependency and must never throw — it falls back to a data-only workbook if chart-writing fails.
- **2026-09-07** — Page component contract (`CONTRACTS.md` §4) carries `{ model, theme, layoutConfig, onModelChange, onThemeChange, onLayoutChange }`. `layoutConfig` (widget order/visibility) is kept separate from `model` — it's presentation config, not row data, and keeping it separate means the grid module's `fromGridData` (which only ever produces a model) can't accidentally clobber the user's layout choices.
- **2026-09-07** — Added a `preview` module to the architecture: a per-template-kind live preview renderer (`BudgetPreview`/`TaskPreview`) that is the only place that knows how to turn a model + theme + layoutConfig into actual dashboard widgets. Kept outside the page modules since it's template-kind-specific rendering, not config editing.
- **2026-09-07** — Style page's v1 scope is deliberately limited to picking between the two built-in theme presets (Calm/Warm) — no custom color/font/radius editing UI. Avoids unrequested scope; can be extended later if needed.
- **2026-09-07** — `grid` module's `fromGridData(gridData, kind)` intentionally returns a fresh model with only `categories`/`tasks` populated (it cannot and does not preserve other settings like period/currency/income for budget, or structure/statusOptions for task). Any caller (the Advanced Grid page) must merge its output into the existing model, never replace the model outright with it.

## Logs
- [[Interface builder/logs/2026-09-07-v2-implementation-phases-1-3|V2 implementation phases 1 3]]
