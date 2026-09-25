---
title: "Customer support ticketing system — desktop outro reversal + clone template lessons"
tags: [customer-support-ticketing-system, session-log]
created: 2026-09-14
type: session-log
status: imported
---

# Desktop outro reversal + clone template lessons

## Summary
After a debate, the user reversed Task 15's "no outro" decision and asked for
`Short1HelpdeskDesktop.tsx` to get the same `DeviceMockup` outro as its mobile sibling
`Short1Helpdesk.tsx`. Wired it identically (a `<Sequence from={1005}>` wrapping `DeviceMockup`,
`BrowserFrame` gaining an `opacity` prop to mirror `PhoneFrame`'s fade-out), bumped
`compositionConfig.durationInSeconds` from 33.5 to 39, regenerated the registry/manifest,
re-rendered the mp4, pulled 5 QA stills confirming a clean crossfade into the outro, and updated
`script.md`. `goal-evaluator` returned `VERDICT: ok` against 8 explicit completion conditions.
Also updated the `screencast-demo-video-craft` memory file with a third lesson (ambiguous
"another X" asset naming). The user then asked what durable lessons from this project should feed
the two sibling clone templates, now living at
`...\Bureau\AI\system_workflow_template\Codex_V1` (coder clone) and `...\Luminara_V1` (video
clone) — the same two clones from the 2026-09-13 split, since relocated/renamed. Propagated only
what each was missing: both `CLAUDE.md` files got a new "ambiguous asset naming" rule and a new
"don't poll a harness-tracked background task with a self-scheduled wakeup tool" rule (generic
wording in Codex_V1, concrete incident wording in Luminara_V1); `Luminara_V1`'s
`.claude/skills/fake-screencast/SKILL.md` also got 5 new reusable Gotchas (click-keyframe
alignment, beat-label-matches-footage, `objectFit:cover` aspect-ratio cropping, mobile→desktop
porting-as-respatializing, `capture_web.py`'s missing bounding-box capability) plus a Step-1 note
on verifying demo sample content against the current spec.

## Decisions
- `Short1HelpdeskDesktop.tsx` keeps the `DeviceMockup` outro after all — final call, not
  expected to flip again.
- Lessons fed into the clone templates were scoped per-domain: `Codex_V1` (no video tooling) got
  only the two generic process rules; `Luminara_V1` got those two rules with concrete video
  incident wording plus the video-craft-specific `fake-screencast` Gotchas, since those are the
  reusable technique lessons a brand-new future video project would actually need.
- Only user-taught/corrected lessons go into auto-memory; self-observed process notes (like the
  wakeup-polling anti-pattern) are propagated into clone `CLAUDE.md`s when the user asks for that
  explicitly, but are not saved as auto-memory on their own.

## Open items
- None — both clone `CLAUDE.md` edits and the `Luminara_V1` `SKILL.md` edits were verified via
  grep for correct placement before this log was written.

## Files touched
- `remotion/src/shots/short-1/Short1HelpdeskDesktop.tsx`, `remotion/registry.gen.tsx`,
  `remotion/shots.manifest.json`, `remotion/out/Short1HelpdeskDesktop.mp4`,
  `shorts/short-1-helpdesk-demo/script.md`, `AGENT_LOG.md`, `CODE_MAP.md`
- `...\system_workflow_template\Codex_V1\CLAUDE.md`
- `...\system_workflow_template\Luminara_V1\CLAUDE.md`,
  `...\Luminara_V1\.claude\skills\fake-screencast\SKILL.md`
- memory: `screencast-demo-video-craft.md` (third lesson appended)
