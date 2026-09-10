---
type: document
title: Alternative report — fswatch
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: fswatch is a cross-platform FSEvents/inotify CLI; it reports folder changes, not foreign reads.
origin: derived
sensitivity: internal
relates_to:
  - path: work/eslogger-unprivileged-alternatives-2026-09-10.md
    kind: implements
  - path: documents/eslogger-alternatives/index.md
    kind: related
  - path: documents/eslogger-unprivileged-investigation.md
    kind: derived_from
sources:
  - https://github.com/emcrisostomo/fswatch
---

# fswatch

## Claim

fswatch can watch a folder without sudo using platform change APIs.

## Coverage versus eslogger

Create, modify, delete, and rename notifications. No open/read stream, no
process attribution.

## Why it is not a replacement

Folder-scoped and unprivileged, but not the same capability. Cartograph
already consumes equivalent change events internally.

## Canvas embed

Could be a user-run command like eslogger, posting to the activity API, but
the events would be writes. Declaring operations honestly would forbid
advertising reads.

## Verdict

Not a read-monitor provider. Redundant with the graph watcher.
