---
type: document
title: Alternative report — chokidar
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: chokidar is an MIT Node filesystem watcher; it cannot observe foreign reads and cannot be vendored into Cartograph.
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
  - https://github.com/paulmillr/chokidar
---

# chokidar

## Claim

chokidar wraps FSEvents, inotify, and similar change APIs for Node. It does
not require sudo for directories the user can already read.

## Coverage versus eslogger

add/change/unlink only. No other-process open, no PID, no read versus write
open flags, no session ancestry.

## Why it is not a replacement

Same class as Cartograph's existing watcher, with a third-party dependency.
The runtime may import only Node built-ins and the Copilot SDK, so chokidar
cannot be bundled into the canvas extension.

## Canvas embed

A spawned user-installed CLI could theoretically POST changes. That would
duplicate `watch.mjs` and still miss reads.

## Verdict

Do not add. No new coverage over the shipped directory watcher.
