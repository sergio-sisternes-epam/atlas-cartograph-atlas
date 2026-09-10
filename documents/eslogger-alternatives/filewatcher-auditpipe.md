---
type: document
title: Alternative report — santoru/filewatcher
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: filewatcher can filter opens by path or process, but it reads /dev/auditpipe, which requires root.
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
  - https://github.com/santoru/filewatcher
---

# santoru/filewatcher

## Claim

This macOS utility filters auditpipe events by file or process and can show
open/read/write. Informal summaries sometimes call it unprivileged. The
producer is `/dev/auditpipe`, which is a privileged interface.

## Coverage versus eslogger

Closer to access monitoring than FSEvents: opens can be filtered to a path.
It is still a host audit stream, not a folder grant, and it needs root.

## Why it is not a replacement

The ask was no sudo. auditpipe does not satisfy that. The project is also
not a Cartograph provider and is not a canvas component.

## Canvas embed

Cannot be iframed. A spawned command would still require administrator
approval, like eslogger.

## Verdict

Reject as an unprivileged alternative. Folder filtering does not drop root.
