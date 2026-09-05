---
type: experience
title: User feedback exposed a restrictive automatic activation zoom cap
created: 2026-09-05
work_id: cartograph-closer-activation-framing-2026-09-05
status: raw
description: Measured compact-group framing, implemented a closer bounded camera target, and preserved the distinction between local work and deployed behavior.
tags: [cartograph, user-feedback, camera, activation, zoom, framing]
origin: internal
sensitivity: internal
relates_to:
  - path: work/cartograph-closer-activation-framing-2026-09-05.md
    kind: implements
  - path: experiences/2026-09-05-live-without-activation-capture-pressure.md
    kind: follows
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/public/activity-camera.js
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/public/graph-canvas.js
---

## User request

After confirming that activation cues worked, the user said:

> The zoom should be closer to the nodes that are been activated. Right now is too far away.

The request was relayed from the "Initialize sdlc atlas" session. Its canvas used
Atlas grouping with 14 graph nodes. A recent multi-file read activated four
related nodes and four connecting edges. This was camera readability feedback,
not another report of failed file capture.

## Investigation

The shared activity camera capped automatic zoom at 3x, while manual zoom already
allowed 20x. Its fitted active bounds occupied at most 65% of viewport width
and 60% of height.

A read-only geometry comparison used the four reported nodes:
`sdlc-model/episode-discussion`, `sdlc-model/episode-boundary`,
`sdlc-model/capture-choice-experience`, and `sdlc-model/event-level-capture`.
The computation used Atlas layout, settled node shells, and the calculated
active-surface orientation in an 800 x 600 viewport.

| Geometry measure | Before | Local implementation |
| --- | ---: | ---: |
| Automatic zoom ceiling | 3x | 20x |
| Maximum fitted width | 65% | 80% |
| Maximum fitted height | 60% | 70% |
| Reported active group's target width | 70.10 px | 467.35 px |
| Reported active group's target height | 52.40 px | 349.33 px |

The automatic cap, rather than the full-set fit, limited this compact group.
The new stable target expands each axis by about 6.7 times. These are calculated
target bounds, not an observation of the updated behavior in the user's
installed canvas or a claim about every transient animation frame.

## Work performed

Changed `.apm/extensions/cartograph/public/activity-camera.js` to use the
existing 20x manual ceiling for automatic framing and a larger padded fit area.
Wider sets can still zoom out to retain all active endpoints. The change does
not impose a minimum close zoom that would crop dispersed activity.

The shared camera continues to fit displayed activations and lifecycle
endpoints, not raw queued reads. It preserves the default-on client-side option,
200 ms fit pacing, speed-limited damping, zoom-in hysteresis, manual orbit and
navigation rules, selection priority, idle restoration, and reduced motion.
WebGL and Canvas 2D still use the same camera.

Added regression coverage in `test/activity-camera.test.mjs` for a compact
four-node patch, a wider set, and an already-close manual view. Updated expected
bounds and the existing camera-control cases. Added WebGL and 2D integration
coverage in `test/graph-renderer.test.mjs` showing that a single displayed
activation can reach above 19x during its five-second lifetime, with the
WebGL activation remaining inside the padded view.

The targeted command `node --test test/activity-camera.test.mjs
test/graph-renderer.test.mjs` passed all 37 tests. Usage guidance and the
Unreleased changelog were updated to describe closer framing.

## Outcome and limits

The user request and local implementation were completed far enough to measure
the improvement and cover the changed behavior, but runtime delivery was not
performed. At capture time the five changed application files remained
uncommitted; the source links above identify their base revision, not the
unpublished camera change.

No installed user extension was edited or reloaded, no collector was restarted,
and no target-project Atlas content was changed. The reporting canvas still
used the previous camera implementation. User confirmation of the new framing
remains pending and must not be confused with the earlier confirmation that
activation cues worked.

## Evidence provenance

Request relayed on 2026-09-05 from Copilot session
`3adf71b2-c667-4194-abf5-9bd89384b381`; source investigation, geometry comparison,
implementation, and targeted validation performed in session
`387a71e8-d2e6-40ff-96b2-3e8c5ef25ffe`.
This memory records a local work-in-progress snapshot, without credentials,
absolute user paths, or raw activity logs.
