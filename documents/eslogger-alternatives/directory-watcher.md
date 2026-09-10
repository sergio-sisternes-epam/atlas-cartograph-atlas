---
type: document
title: Alternative report — Cartograph directory watcher
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: The existing unprivileged folder watcher synchronizes the graph; it does not observe reads.
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
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/architecture.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/file-access.md
---

# Cartograph directory watcher

## Claim

`atlas/watch.mjs` plus `atlas/live.mjs` already watch mounted Atlas roots
without sudo. They publish create/delete/edit deltas for lifecycle effects.
They do not emit the access protocol and must not inherit process scope.

## Coverage versus eslogger

Sees filesystem changes from any application that mutates files Cartograph
can read. Does not see opens, reads, unmodified closes, or which PID did
the work. Coalesced events are possible.

## Why it is not a replacement

The original ask wanted the same monitoring capability as eslogger on a
folder. Change notifications are a different job, already shipped. Using
this watcher as a silent access fallback would claim reads that never
occurred.

## Canvas embed

Not applicable. This source is already in the runtime as graph
synchronization, not as a canvas iframe.

## Verdict

Keep it for live graph updates. Do not register it as a monitor provider.
