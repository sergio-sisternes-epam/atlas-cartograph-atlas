---
type: experience
title: Visual feedback and staged delivery shaped Cartograph v0.3.0
created: 2026-09-10
work_id: cartograph-v030-2026-09-10
status: recorded
description: A dated account of design reversals, measured behavior and the completed source-to-consumer release chain.
origin: internal
sensitivity: internal
relates_to:
  - path: work/cartograph-v030-2026-09-10.md
    kind: implements
  - path: experiences/2026-09-05-closer-activation-framing.md
    kind: follows
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: records
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/commit/fe6de71e56422bda09dd0a92cf59d683d883e396
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/pull/8
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/actions/runs/34416224828
  - https://github.com/sergio-sisternes-epam/apm-marketplace/pull/10
---

# From minor animation requests to a released interaction contract

## Discussion and iteration

The initial requests were a small version/SHA display, longer lifecycle effects
and faster zoom toward one activated node on the stress Atlas. Follow-up
feedback exposed loss of focus during zoom-out, clipped footer text, a thin
side profile, disappearing decoration, confusing duplicate searches and
unbounded turns after grouping changes.

The first galaxy implementation added a core and some depth but still put
most arm nodes near a disk. A side-view screenshot disproved the adequacy of
that change. Increasing only halo extremes or choosing a flattering camera
angle was insufficient; the final implementation fills the bounded arm volume.

Two intermediate choices were explicitly reversed. Disabling galaxy idle
rotation to avoid an edge-on view removed behavior the user wanted; the
original 0.16-radian/second rate was restored. Combining search behind a
launch-button popup also lost the preferred interaction; the final release
keeps one always-visible toolbar field and removes only the duplicate search.

The new-node glow requirement evolved from ending at arrival or timeout to a
confirmed ten seconds total from creation. Final behavior fades independently
of arrival, rather than holding then starting a second ten-second timer.

## Implementation and evidence

The shared runtime handles the same camera, clock, matching and lifecycle
model for WebGL and Canvas 2D. First activation highlights the selected node
and its immediate neighbors; a repeated activation opens Markdown atomically
on the server. Explicit page navigation retains its direct-preview behavior.

Deterministic tests cover singleton framing at multiple frame rates, the
complete restoration trajectory, shortest turns after many manual revolutions,
bounded galaxy groups and the central 80% side profile. A browser observation
of the stress graph measured a side-profile bulk width/height ratio near 0.635
and idle movement near 0.161 radians over one second. These are observations
of that fixture and view, not universal layout or performance guarantees.

The final source suite passed 520 tests. A native filesystem-watcher timing
failure passed on isolated and full-suite reruns; no unproven root cause was
claimed. A review found that a declared type could hide its independent
rendering kind from search. The index now includes both, with a dedicated test.

## Release and consumer delivery

Source CI covered Node 22/24 on Linux/macOS and isolated APM 0.30.0 packaging.
The exact clean candidate opened in the real native host. Native state,
layers, explicit selection and reload were exercised; toolbar search was
checked against the real 477-node Atlas without copying its contents.

The stable release archive SHA-256 is
`967ea0e6d564c1af6c351f839d7a20fa491382b105c0897fb4957463709f9983`.
All 52 published runtime files matched the native-tested candidate. The
marketplace update waited for its review/publication boundary; global state
was left untouched until the PR merged and both catalog representations
published the same version and source SHA.

The ordinary scoped global updater failed on an unrelated missing
`apm-toolkit#v1.0.23` ref. An exact-ref Cartograph install preview succeeded,
but did not preview stale-file cleanup. A private isolated rehearsal then
established the intended change before the live install. Cartograph advanced
from 0.2.0 to 0.3.0; the marketplace and direct-source declarations remained,
and unrelated pins, ownership, settings and trust were preserved.

## Limits

Synthetic activity is not OS capture evidence; no collector or privileged
workload was started. Local FPS observations are not a performance promise.
The global deployment was compared with the released source commit; only the
release archive carries stamped build metadata. An unstamped source deployment
may correctly show an unavailable SHA instead of borrowing the consumer SHA.

This record derives from session `98b03fc7-7d67-4041-a211-c128477b7875`,
2026-09-09 through 2026-09-10, and the linked immutable delivery evidence.
