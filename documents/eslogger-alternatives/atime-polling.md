---
type: document
title: Alternative report — atime polling
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Access-time polling is not a reliable substitute for open observation on modern macOS.
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
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/file-access.md
---

# atime polling

## Claim

Repeatedly reading file access timestamps needs no sudo on files the user
owns. That still does not reconstruct eslogger events.

## Coverage versus eslogger

Updates may be delayed, coalesced, or disabled. Cached application reads
may never hit the filesystem. There is no PID, no open flags, and no
session ancestry.

## Why it is not a replacement

Product docs already reject this as a read-monitor. False idleness and false
activations would both be worse than Waiting.

## Canvas embed

Polling from Node would still live in a collector process. It would not
become more accurate inside the canvas.

## Verdict

Do not implement.
