---
type: document
title: Unprivileged eslogger alternative investigation
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Summary of the 2026-09-10 search for a folder-scoped, sudo-less replacement that still observes other-process Atlas opens.
origin: derived
sensitivity: internal
relates_to:
  - path: work/eslogger-unprivileged-alternatives-2026-09-10.md
    kind: implements
  - path: experiences/2026-09-10-eslogger-unprivileged-ask.md
    kind: derived_from
  - path: lessons/macos-eslogger-requires-privileged-open-observation.md
    kind: related
  - path: documents/eslogger-alternatives/index.md
    kind: related
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/file-access.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/monitor-providers.md
---

# Investigation summary

Root ask:
[User asked for a sudo-less folder monitor matching eslogger](../experiences/2026-09-10-eslogger-unprivileged-ask.md).

Question 1 asked for the **same capability** as `macos-eslogger` over a
specific folder without sudo. Question 2 asked whether an open-source project
could be **embedded in the canvas**.

## Result

There is no shipped Cartograph provider, and no embeddable open-source
project, that matches eslogger's other-process open/read/write observation
without privileges.

macOS does not offer an unprivileged "who read this folder" API. eslogger
subscribes system-wide through Endpoint Security; Cartograph then matches
exact Atlas paths. Restricting interest to a folder does not remove root or
Full Disk Access.

The canvas cannot host a native monitor. It is web UI. Collectors are
separate processes using the loopback activity protocol. The runtime bundle
cannot vendor npm watchers.

## What already exists without sudo

[Cartograph's directory watcher](eslogger-alternatives/directory-watcher.md)
already tracks creates, edits, deletes, and renames for live graph
synchronization. It must not be described as a read monitor.

## Candidate classes

| Class | Unprivileged | Sees foreign reads | Canvas embed |
| --- | --- | --- | --- |
| Directory / FSEvents watchers | yes | no | no (and redundant) |
| osquery ES / auditpipe tools | no | yes, with OS privileges | no |
| FUSE overlay | mostly | only via the mount | no |
| Cooperating Copilot/editor/wrapper | yes | only cooperating tools | reporter, not iframe |
| atime polling | yes | unreliable | no |

Detailed reports live under
[eslogger-alternatives](eslogger-alternatives/index.md).

## Product consequence

Keep `macos-eslogger` as the default access provider. Register alternatives
explicitly; never silent-fallback. The useful unprivileged future is a
provider that posts the existing protocol from Copilot or editor hooks, with
honest weaker coverage.

## Provenance

Read-only review of Cartograph docs and the eslogger provider, plus public
project pages for chokidar, fswatch, Watchman, osquery, filewatcher, and
FUSE-T. No collector was started.
