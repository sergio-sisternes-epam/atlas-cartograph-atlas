---
type: work
title: Bring activated nodes and connections closer
created: 2026-09-05
work_id: cartograph-closer-activation-framing-2026-09-05
status: done
description: Closer framing delivered; completion evidence recorded with the v0.3.0 release and global upgrade.
origin: internal
sensitivity: internal
relates_to:
  - path: experiences/2026-09-05-closer-activation-framing.md
    kind: related
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: follows
  - path: work/cartograph-v030-2026-09-10.md
    kind: related
---

## Scope

Respond to the user's confirmed-working activation cues being too far away.
Frame the whole displayed active group and its connecting paths more closely,
without changing capture semantics, installed collectors, or Atlas content.

## Status

At the original capture, local implementation and targeted validation completed on 2026-09-05.
The code is uncommitted in the Cartograph worktree based on
`75c0d234994924225067e4185e427924cdb0639f` at the time of this memory.
It had not then been pushed, merged, or installed in the reporting project's
user extension. That historical local-only status is superseded by the closure
evidence below, not silently rewritten as an earlier successful deployment.

## Outcomes

- [Request and implementation experience](../experiences/2026-09-05-closer-activation-framing.md):
  identified the 3x automatic cap, raised it to the existing 20x manual ceiling,
  and enlarged the padded fit area.
- The reported four-node group's stable target bounds increased from about
  70 x 52 to 467 x 349 pixels in an 800 x 600 viewport.
- Added geometry and shared-renderer regression coverage; updated usage
  documentation and the Unreleased changelog.

## Closure on 2026-09-10

The v0.3.0 release at `fe6de71e56422bda09dd0a92cf59d683d883e396`
retains the 20x fit and adds faster singleton framing and stable restoration.
The user accepted the real-Atlas view and requested release. Source release,
marketplace publication and scoped global deployment are complete; see the
[delivery hub](cartograph-v030-2026-09-10.md) for linked evidence.
The global native canvas opened successfully. This does not claim a separate
post-upgrade acceptance run in the original reporting session.

Capture overload and the misleading Live freshness indicator remain a separate
reliability concern from the preceding work hub.
