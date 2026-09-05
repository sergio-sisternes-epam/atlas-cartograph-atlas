---
type: work
title: Recover Cartograph activity startup in a consuming project
created: 2026-09-05
work_id: cartograph-activity-startup-2026-09-05
status: done
description: Restore the activity endpoint and confirm session-scoped Atlas accesses.
origin: internal
sensitivity: internal
relates_to:
  - path: experiences/2026-09-05-stale-runtime-activity-404.md
    kind: related
  - path: experiences/2026-09-05-eslogger-waiting-startup.md
    kind: related
---

# Activity startup recovery

## Scope

Investigate Cartograph in the consuming project's "Initialize sdlc atlas"
Copilot session. Recover the activity connection and confirm real reads without
changing monitor provider, broadening process scope, or patching installed code.

## Status

Done on 2026-09-05. Both incidents were resolved operationally.
No runtime code fix or application merge was required.

## Outcomes

- [Runtime mismatch](../experiences/2026-09-05-stale-runtime-activity-404.md):
  reloading the extension restored the missing endpoint and preserved the Atlas.
- [Collector startup](../experiences/2026-09-05-eslogger-waiting-startup.md):
  matching tool reads reached Live after separate authorization and restart.

Potential follow-ups remain proposals, not completed features: explain
preauthorization before a shell pipeline; distinguish collector connectivity
from the first accepted access; and make UI/backend mismatch easier to diagnose.

## Evidence provenance

Sanitized account of the "Activity connection fix" session
`387a71e8-d2e6-40ff-96b2-3e8c5ef25ffe` and read-only observations plus controlled
reads from "Initialize sdlc atlas" session
`3adf71b2-c667-4194-abf5-9bd89384b381`. Raw transcripts are not copied because
they included private connection information.
