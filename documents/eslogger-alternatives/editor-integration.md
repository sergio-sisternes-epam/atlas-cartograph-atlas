---
type: document
title: Alternative report — editor integration
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: An editor plugin can report opens and saves without sudo, limited to that editor.
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

# Editor integration

## Claim

An editor that already opened the Atlas files can notify Cartograph of
opens, reads, and saves using ordinary file permission.

## Coverage versus eslogger

Only the instrumented editor. Shell tools, other IDEs, and preview helpers
stay invisible.

## Why it is not a replacement

Knowledge Activation is meant to show session tools and, in standalone
mode, other applications. One editor cannot stand in for Endpoint Security.

## Canvas embed

A plugin talks HTTP to the receiver. It is not embedded inside the canvas
document.

## Verdict

Possible symbiont reporter with declared editor-only operations. Not
enabled, and not same-capability.
