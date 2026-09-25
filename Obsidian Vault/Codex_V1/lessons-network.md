---
title: "Codex_V1 — Lessons network"
tags: [codex_v1, lessons, synthesis]
created: 2026-09-25
type: synthesis
status: active
---

# Lessons network

A weighted, three-layer synthesis of every `decisions.md` in this vault (19 other
projects + Codex_V1's own history). Modeled as a small neural net: **input nodes** are
raw, single-project observations; **hidden nodes** are patterns two or more projects
independently converged on (weight = number of source projects feeding it — the
"replication" signal); **output nodes** are the handful of top-level doctrines a new
Codex_V1 sub-project should inherit by default. A `✅` marks a lesson that has already
been codified into live governance (Codex_V1's own `CLAUDE.md`) rather than just
observed here.

This is a living map — re-run this synthesis after enough new projects accumulate
that the weights would meaningfully shift.

## Input layer — one signal per project

| Project | Strongest exportable signal |
|---|---|
| [[Checkout flow optimization/decisions\|Checkout flow optimization]] | No-build-step CSS framework chosen for zero JS runtime, not brand fit; demo data sourced from real research (Baymard), not invented. |
| [[Customer support ticketing system/decisions\|Customer support ticketing system]] | Static-only forces localStorage + a client-side "gate" documented as non-auth; a mixed/unrelated project root was split into independent sibling clones. |
| [[Customer support ticketing system_V1/decisions\|Customer support ticketing system_V1]] | Reused an existing pill-pattern for a new toggle instead of a parallel one; a body-bottom auth guard was a real bug, not a nitpick — must block in `<head>`. |
| [[Employee recognition wall/decisions\|Employee recognition wall]] | Started static, added a minimal server only once shared persistence was actually needed; never guess a missing real person's data field. |
| [[Graphify/decisions\|Graphify]] | Rejected an automated pipeline that would send project code to a third-party LLM, in favor of a manual, local-only, stdlib-only alternative. |
| [[Interface builder/decisions\|Interface builder]] | Config (`layoutConfig`) kept structurally separate from data (`model`) so one write path can never clobber the other. |
| [[Interface builder V2/decisions\|Interface builder V2]] | Native HTML5 DnD + hand-rolled FLIP over a library; an existing tag-picker was reused for Calendar instead of a new taxonomy. |
| [[Library templates/decisions\|Library templates]] | A throwaway maquette became a mandatory direction-check before any full build; real published token data used over invented values. |
| [[Loan_application_requirement/decisions\|Loan_application_requirement]] | A deterministic hook was added only after model-judgment review missed the same bug class three times; versioned folders must never reference each other. |
| [[Luminara_V1/decisions\|Luminara_V1]] | Used the ffmpeg already bundled inside an installed package instead of assuming a system install existed. |
| [[Markdown-powered blog_portfolio/decisions\|Markdown-powered blog_portfolio]] | This OneDrive-synced tree denies delete operations at the OS ACL level — an environment constraint, not a design choice, and one that recurs in any project stored here. |
| [[REST API/decisions\|REST API]] | stdlib `sqlite3` chosen over an ORM specifically so the injection-prevention goal stayed real; versioned folders (`V1/`, `V2/`) as frozen, independent siblings. |
| [[Saas metrics dashboard/decisions\|Saas metrics dashboard]] | This device has no system Node/Chromium — always install into an isolated env, never assume PATH. |
| [[Storage interface/decisions\|Storage interface]] | A UI action was placed on the flow that matched its real-world frequency (price update on Purchase, not the far-busier Sale action). |
| [[Storage_interface_templates/decisions\|Storage_interface_templates]] | A visual bug (status-dot drift) traced to conflating box alignment with text alignment — fixed with a dedicated class, not a text-align hack. |
| [[Store dynamic database/decisions\|Store dynamic database]] | WCAG AA contrast passing did not mean the fill color read as "selected" — needed a real in-browser look, not just the ratio math; spec content had been silently re-duplicated into code comments (~34% density) before being banned outright. |
| [[Tutoring interface/decisions\|Tutoring interface]] | Spec docs (`logic/`) were written before the visual mockup (`seed/`) specifically so the mockup couldn't invent behavior that would later drift from the real rules. |
| [[V2/decisions\|V2]] | The frozen mockup and the eventual real MVP were kept explicitly separate projects, not conflated into one evolving codebase. |
| [[V5/decisions\|V5]] | Every paid-vendor capability isolated behind a `PROVIDERS` dict + env var so a vendor swap never touches call sites; `.venv`/`.node_env` never portable across copies. |
| Codex_V1 (own history) | Never assume shared audience/branding across sub-projects sharing this root; a subagent's self-report was ruled non-authoritative — only independent live re-verification (and the lead agent's own `goal-evaluator` dispatch) counts as proof. |

## Hidden layer — patterns (weight = source-project count)

| # | Pattern | Weight | Fed by |
|---|---|---|---|
| H1 | Default to static/dependency-free; add a library, framework, or backend only once a concrete, already-hit need forces it | **8** | Checkout flow optimization, Customer support ticketing system, Customer support ticketing system_V1, Interface builder V2, Library templates, Markdown-powered blog_portfolio, REST API, Employee recognition wall |
| H2 | Environments and their quirks are per-project and non-portable — isolate tooling, never assume a system install, a copied `.venv`, or an OS operation (like delete) will just work | **5** | Saas metrics dashboard, V5, Luminara_V1, Markdown-powered blog_portfolio |
| H3 | Cheap direction-check (throwaway maquette / intake step) before committing to a full build | **5** | Library templates, Tutoring interface, Interface builder V2, Customer support ticketing system, Codex_V1 |
| H4 | Reuse an existing UI/interaction pattern for a new-but-similar need instead of inventing a parallel one | **3** | Customer support ticketing system_V1, Store dynamic database, Interface builder V2 |
| H5 | Keep unrelated or version-separated work fully independent — no shared root/config/audience across sibling sub-projects, no version folder depending on another | **3** | Customer support ticketing system (clone split), Codex_V1 (factory-root rule), REST API / Loan_application_requirement (versioned siblings) |
| H6 | Ground illustrative/demo content in real, sourced data — never fabricate what can be looked up | **2** | Checkout flow optimization, Library templates |
| H7 | Automated or numeric checks (contrast ratio, a subagent's self-report) are not proof by themselves — verify visually/live and independently before trusting them | **2** | Store dynamic database, Codex_V1 |
| H8 | A gate that isn't real auth must say so, in the UI, where the person relying on it will see it | **2** | Customer support ticketing system, Employee recognition wall |
| H9 | On long/complex work, delegate implementation to subagents or background workflows — the lead's job is coordination, review, and enforcement, not authoring every line | **4** | Tutoring interface, V2, Loan_application_requirement, REST API |
| H10 | Never guess or backfill a missing field on real, user-submitted data — only fabricate for clearly-fictional sample data, and degrade gracefully otherwise | **1** (single-source, high-stakes) | Employee recognition wall |
| H11 | A deterministic, automatically-run check catches defect classes that repeated model-judgment review keeps missing — codify it once found, don't rely on remembering | **1** (single-source, high-lineage — seeded Codex_V1's own Completion Loop) | Loan_application_requirement |
| H12 | Spec/rationale content belongs in a dedicated map doc, never duplicated into inline code comments | **1** (single-source, high-lineage — this exact rule is now ✅ live in Codex_V1's `CLAUDE.md`) | Store dynamic database |

## Output layer — top-level doctrine

| Doctrine | Weight (Σ hidden) | Rolls up | Status |
|---|---|---|---|
| **Lazy-by-default architecture** — build the smallest thing the actual request needs: static before backend, native features before libraries, an existing pattern before a new one, a cheap direction-check before a full build. | **16** | H1, H3, H4 | ✅ partially codified — matches this session's own Ponytail mode |
| **Isolation as a first principle** — environments, unrelated sub-projects, and version folders never share state, config, or assumptions with each other. | **10** | H2, H5 | ✅ codified — Codex_V1 `CLAUDE.md`'s Environment section and factory-root rule |
| **Honesty over convenience** — sourced data over invented data, labeled fake-auth over silent fake-auth, verified-live over self-reported, spec docs over comments-as-a-shortcut. | **8** | H6, H7, H8, H10, H12 | ✅ partially codified — the no-comments rule is verbatim in `CLAUDE.md` |
| **Process discipline at scale** — delegate long/complex work instead of authoring it directly, and back that delegation with a deterministic check rather than a step someone has to remember. | **7** | H9, H11 | ✅ codified — Codex_V1's Completion Loop / `goal-evaluator` gate |

## Reading this graph

Highest-weight doctrine first: when a new Codex_V1 sub-project starts, **lazy-by-default
architecture** is the default lens (16 independent projects converged on it) — reach for
static/native/reused-pattern before anything else, and cheapen the direction-check before
committing scope. **Isolation** is the next-heaviest and the one most likely to cause real
damage if skipped (H2's OneDrive-delete-ACL node applies to this very vault). The two
lowest-weight-but-highest-lineage nodes (H11, H12) are single-project in origin but are
exactly the two that already made it into `CLAUDE.md` verbatim — a reminder that weight
here means *replication*, not *importance*; a single sharp incident can still outrank
weight if the failure mode is bad enough.
