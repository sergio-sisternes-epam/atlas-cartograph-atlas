---
type: document
title: Cartograph experiences
created: 2026-09-05
description: Observed incidents, evidence, recovery, and remaining uncertainty.
origin: internal
sensitivity: internal
relates_to:
  - path: experiences/2026-09-05-stale-runtime-activity-404.md
    kind: related
  - path: experiences/2026-09-05-eslogger-waiting-startup.md
    kind: related
  - path: experiences/2026-09-05-live-without-activation-capture-pressure.md
    kind: related
  - path: experiences/2026-09-05-closer-activation-framing.md
    kind: related
---

# Experiences

Experiences describe what happened in a specific context. They are not blanket
prescriptions or claims that a suspected cause has been proven.

- [Stale runtime caused activity connection 404](2026-09-05-stale-runtime-activity-404.md):
  updated UI assets were served by a process without the activity backend.
- [Collector remained Waiting until startup was separated](2026-09-05-eslogger-waiting-startup.md):
  explicit authorization and restart restored capture; the initial authorization
  state was not conclusively observed.
- [Live without activation under capture pressure](2026-09-05-live-without-activation-capture-pressure.md):
  matching reads and visual cues recovered after restart, while high producer
  resource usage recurred and the freshness problem remained unresolved.
- [Closer activation framing](2026-09-05-closer-activation-framing.md):
  a user request exposed a restrictive 3x automatic zoom cap; a locally
  implemented 20x cap substantially enlarges the reported active group.
