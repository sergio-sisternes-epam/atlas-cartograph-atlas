---
type: work
title: Investigate unprivileged replacements for macos-eslogger
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: done
description: Record why Knowledge Activation uses privileged eslogger, and why folder-scoped or embeddable open-source monitors cannot match that coverage without sudo.
origin: user
sensitivity: internal
relates_to:
  - path: experiences/2026-09-10-eslogger-unprivileged-ask.md
    kind: related
  - path: documents/eslogger-unprivileged-investigation.md
    kind: related
  - path: lessons/macos-eslogger-requires-privileged-open-observation.md
    kind: related
  - path: documents/eslogger-alternatives/index.md
    kind: related
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: related
---

# Unprivileged eslogger alternatives

## Scope

Answer whether Cartograph can replace `macos-eslogger` with a monitor that
watches a specific folder, does not need sudo, and still sees other processes
open Atlas pages. A follow-up asked whether an open-source project could be
embedded into the canvas for that job.

This work does not change the default provider, add a registry implementation,
or weaken process scope.

## Status

Done on 2026-09-10 as an investigation. No runtime change. `macos-eslogger`
remains the only shipped access provider.

## Outcomes

- [Root ask](../experiences/2026-09-10-eslogger-unprivileged-ask.md):
  the user asked for same-capability folder monitoring without sudo, then for
  an embeddable open-source collector.
- [Why eslogger needs sudo](../lessons/macos-eslogger-requires-privileged-open-observation.md):
  other-process opens require Endpoint Security; folder APIs do not emit reads.
- [Investigation summary](../documents/eslogger-unprivileged-investigation.md):
  no shipped or embeddable equivalent; unprivileged options lose read coverage
  or need cooperating tools.
- [Alternative reports](../documents/eslogger-alternatives/index.md):
  one page per candidate, including the existing directory watcher.

## Related
