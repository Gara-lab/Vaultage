---
title: "UX Contract"
tags: [ux, ai-coding, contract]
created: 2026-08-25
updated: 2026-08-25
status: draft
type: permanent
---


# UX Contract


## Context

This document defines the non-negotiable UX/UI rules that all AI-generated and human-written frontend code must follow. It serves as the **Spec + Environment** layer in our AI workflow: before implementing any UI feature, the AI must ensure the feature's behavioral spec respects these rules, and the **Verifier** layer (tests/CI) must confirm compliance.

These rules exist because AI coding agents cannot "see" or "feel" the interface. They optimize for what they can verify: passing tests, lint, and build. This contract encodes UX expectations in a testable, rule-based format so the AI can reliably produce interfaces that work well for humans.


## Details

### 1. Performance Rules

All pages must meet Core Web Vitals thresholds on a mid-tier mobile connection (simulated in CI):

- **Largest Contentful Paint (LCP)**: ≤ 2.5 seconds
- **Interaction to Next Paint (INP)**: ≤ 200 milliseconds
- **Cumulative Layout Shift (CLS)**: ≤ 0.1

Additional heuristics:

- No full-page loading spinner should block interactivity for > 2 seconds. Prefer skeleton screens or progressive content.
- Any async action that may take > 200ms must show a visible loading state (e.g., disabled button + spinner/text).

**Verifiers:**

- Lighthouse CI (or equivalent) in CI pipeline:
  - Fail build if LCP > 2.5s, INP > 200ms, or CLS > 0.1 on critical pages.
- Manual or automated checks that loading states appear for async actions > 200ms.


### 2. Typography Rules

These rules ensure readable, accessible text across devices.

**Font size:**

- Base body font size: **16px (1rem)** minimum.
- Meaningful text must never be < 12px.
- Headings must be at least **20% larger** than body text to establish clear hierarchy.

**Line height:**

- Body text line height: **≥ 1.5× font size** (e.g., `line-height: 1.5` or higher).
- Must support WCAG 1.4.12: users must be able to increase line height to 1.5× without breaking layout.

**Line length:**

- Optimal line length for body text: **45–75 characters per line**.
- In CSS, constrain text blocks to **max-width: 70ch** (or equivalent).

**Paragraph and text spacing:**

- Paragraph spacing (vertical margin between paragraphs): **≥ 2× font size**.
- Must support WCAG 1.4.12 overrides:
  - Line spacing: ≥ 1.5× font size
  - Paragraph spacing: ≥ 2× font size
  - Letter spacing: ≥ 0.12× font size
  - Word spacing: ≥ 0.16× font size

**Implementation rules:**

- Use design tokens (CSS variables or theme values) for:
  - `--font-size-base` (≥ 1rem)
  - `--line-height-base` (≥ 1.5)
  - `--max-text-width` (≈ 70ch)
  - `--paragraph-spacing` (≥ 2× font size)
- Do not hard-code font sizes or line heights that violate these minima.

**Verifiers:**

- Stylelint (or equivalent) rules:
  - `line-height` ≥ 1.5 on body text selectors (`p`, `li`, `.prose`, etc.).
  - Body `font-size` ≥ 1rem (or token equivalent).
  - Text containers use `max-width` ≤ 70ch (or token).
- Manual review of key pages to ensure comfortable reading.


### 3. Color and Contrast Rules

Ensure text and UI elements are perceivable by users with low vision or color deficiencies.

**Contrast ratios (WCAG AA):**

- Normal text: **≥ 4.5:1** contrast ratio against background.
- Large text (≥ 18px or 14px bold): **≥ 3:1**.
- UI components and graphics (icons, input borders, etc.): **≥ 3:1** against adjacent colors.

**Implementation rules:**

- Use design tokens for colors; do not introduce new colors without adding them to the token file and verifying contrast.
- Avoid conveying information by color alone (e.g., "red means error" must also have an icon or text label).

**Verifiers:**

- Automated accessibility tools in CI (axe-core, pa11y, Lighthouse accessibility):
  - Fail build on critical contrast violations.
- Manual spot checks on key components (buttons, links, form fields, error states).


### 4. Accessibility Rules (WCAG 2.2 AA)

All interactive UI must be perceivable, operable, understandable, and robust.

**Keyboard and focus:**

- All interactive elements (buttons, links, inputs, menus, modals) must be:
  - Reachable via keyboard (Tab/Shift+Tab).
  - Activatable via Enter/Space where appropriate.
- Visible focus indicators must be present for all focusable elements (do not remove default outlines without providing a custom, visible focus style).

**Forms:**

- Every input must have an associated label (visible or programmatically associated).
- Error states must:
  - Show inline error messages near the relevant field.
  - Use `aria-invalid="true"` on invalid fields.
  - Use `aria-live` regions or equivalent to announce errors to screen readers.
- On validation error:
  - Focus must move to the first invalid field.
  - Field values must be preserved (do not clear the form on error).

**Semantic structure:**

- Use proper heading hierarchy (`h1` → `h2` → `h3`...), one `h1` per page.
- Use semantic HTML elements (`<nav>`, `<main>`, `<button>`, etc.) instead of generic `<div>`s where possible.
- Images must have meaningful `alt` text, or `alt=""` if decorative.

**Verifiers:**

- Automated accessibility checks in CI:
  - No critical WCAG 2.2 AA violations on critical pages.
- Manual keyboard-only navigation test on key flows (login, forms, navigation, modals).


### 5. Interaction and Feedback Rules

Ensure the interface clearly communicates what is happening and responds predictably to user actions.

**System status visibility:**

- For any action that may take > 200ms:
  - Show a visible loading state (spinner, progress bar, or disabled button with loading text).
  - Do not leave the user guessing whether their action was registered.
- For multi-step processes (e.g., checkout, onboarding):
  - Show progress indicators (e.g., "Step 2 of 4").

**Error handling:**

- Errors must be:
  - Specific (explain what went wrong and where).
  - Actionable (tell the user how to fix it).
  - Shown inline near the relevant context (e.g., under form fields, near the relevant section).
- Do not rely solely on top-level toasts for critical errors; use inline messages for form and field-level issues.

**Confirmation and safety:**

- Destructive actions (delete, cancel subscription, irreversible changes) must:
  - Require explicit confirmation (modal or dedicated confirmation step).
  - Clearly describe the consequences.
- Provide undo or recovery options where feasible (e.g., "Undo" toast for recent deletions).

**Consistency:**

- Similar actions must behave similarly across the app (e.g., all forms use inline errors, all modals have consistent close behavior).
- Reuse existing components and patterns instead of inventing new ones for common tasks.

**Verifiers:**

- E2E tests (Playwright/Cypress) for critical flows:
  - Loading states appear for async actions.
  - Inline errors appear on invalid form submission.
  - Focus moves to first invalid field on error.
  - Destructive actions require confirmation.
- Manual review of key flows to ensure feedback feels appropriate.


### 6. Layout and Spacing Rules

Ensure visual consistency and comfortable scanning.

**Spacing system:**

- Use a consistent spacing scale (e.g., 4px/0.25rem base unit: 4, 8, 12, 16, 24, 32, 48, 64px).
- Use design tokens for spacing (e.g., `--space-4`, `--space-8`, etc.).
- Do not introduce arbitrary pixel values; use the defined scale.

**Component spacing:**

- Consistent padding within components (e.g., buttons, cards, inputs).
- Adequate whitespace between sections to avoid visual clutter.

**Responsive behavior:**

- Layouts must work on mobile (≥ 320px width) up to desktop.
- No horizontal scrolling on body content (except for intentional wide elements like code blocks or tables with overflow handling).

**Verifiers:**

- Visual regression tests on key pages (Playwright screenshots or similar).
- Manual checks on mobile, tablet, and desktop breakpoints.


### 7. AI Workflow Rules (How to Use This Contract)

These rules define how the AI must use this contract in practice.

**Spec First:**

- For every new UI feature or change:
  - Co-create a behavioral spec with the human before coding.
  - The spec must explicitly state how the feature satisfies relevant sections of this contract (performance, typography, accessibility, interaction, etc.).
- Do not start implementation until the spec is agreed upon.

**Verifiers Before Implementation:**

- For each spec:
  - Propose 3–10 E2E tests (Playwright/Cypress) or other verifiers that check the UX behaviors and constraints.
  - Include at least one test for:
    - Loading state for async actions > 200ms.
    - Error state and focus management (for forms).
    - Success state and feedback.
- Do not start implementation until tests are approved.

**Environment & Reuse:**

- Use existing design tokens, components, and patterns defined in the project.
- Do not introduce new colors, spacings, or font sizes without:
  - Adding them to the design token file.
  - Ensuring they comply with this contract (contrast, sizing, spacing).
- Do not change `data-testid` or role selectors without updating related tests.

**Incremental, Skeleton-Based Work:**

- Implement features component-by-component or flow-by-flow.
- For each component:
  - Define its spec using the standard template.
  - Implement.
  - Ensure all related tests pass.
  - Manually verify the flow in the browser before moving on.

**No Silent UX Regressions:**

- If a change affects:
  - Performance (LCP, INP, CLS),
  - Accessibility (contrast, labels, keyboard),
  - Core interaction patterns (forms, navigation, modals),
  then:
  - Add or update tests.
  - Run CI checks.
  - Do not merge if checks fail.


## Related links

- WCAG 2.2 Guidelines: https://w3c.github.io/wcag/guidelines/22/
- WCAG 1.4.12 Text Spacing: https://accessibility.build/wcag/1-4-12
- Core Web Vitals (Google): https://web.dev/articles/vitals
- Web Almanac – Performance chapter: https://almanac.httparchive.org/en/2025/performance
- Nielsen Norman Group – UX heuristics: https://www.nngroup.com/articles/ten-usability-heuristics/