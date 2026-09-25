---
title: "Saas metrics dashboard — Decisions"
tags: [saas-metrics-dashboard, decisions]
created: 2026-08-28
type: decisions
status: active
---

# Decisions

- **2026-08-27** — Scope: revenue & churn metrics only, no CAC/LTV (user confirmed planner's recommendation).
- **2026-08-27** — Include working filter controls (segment + time range) rather than a static-only dashboard (user confirmed planner's recommendation).
- **2026-08-27** — This device has no system-installed Node.js or Chromium/Playwright. Always install these into an isolated/virtual environment (Python venv + `nodeenv` for Node, Playwright's own install for Chromium) rather than searching the filesystem or system PATH for them.
- **2026-08-27** — KPI info-link highlight feature (T10) is click-triggered only, never scroll-triggered — passive scrolling into the Metrics & Definitions section must never add a highlight, only a click (or a matching `#definition-*` hash present on page load) may.
## Logs
- [[Saas metrics dashboard/logs/2026-08-28-highlight-feature-and-full-build|Highlight feature and full build]]
