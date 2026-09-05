---
type: work
title: Bring activated nodes and connections closer
created: 2026-09-05
work_id: cartograph-closer-activation-framing-2026-09-05
status: implementing
description: Local camera framing improvement with delivery and user validation still pending.
origin: internal
sensitivity: internal
relates_to:
  - path: experiences/2026-09-05-closer-activation-framing.md
    kind: related
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: follows
---

## Scope

Respond to the user's confirmed-working activation cues being too far away.
Frame the whole displayed active group and its connecting paths more closely,
without changing capture semantics, installed collectors, or Atlas content.

## Status

Local implementation and targeted validation completed on 2026-09-05.
The code is uncommitted in the Cartograph worktree based on
`75c0d234994924225067e4185e427924cdb0639f` at the time of this memory.
It has not been pushed, merged, or installed in the reporting project's user
extension. Keep this work open until delivery and user acceptance are confirmed.

## Outcomes

- [Request and implementation experience](../experiences/2026-09-05-closer-activation-framing.md):
  identified the 3x automatic cap, raised it to the existing 20x manual ceiling,
  and enlarged the padded fit area.
- The reported four-node group's stable target bounds increased from about
  70 x 52 to 467 x 349 pixels in an 800 x 600 viewport.
- Added geometry and shared-renderer regression coverage; updated usage
  documentation and the Unreleased changelog.

## Remaining work

Review and publish the camera changes, update the consuming installation through
its approved distribution path, and confirm the closer framing with the user.
Record the eventual code commit and deployment evidence here. Do not treat
publishing this memory as publishing the runtime change.

Capture overload and the misleading Live freshness indicator remain a separate
reliability concern from the preceding work hub.
