---
type: document
title: Alternative report — Copilot tool instrumentation
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Cooperating Copilot tools can POST the activity protocol without sudo, but they miss unwrapped shells and other apps.
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
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/monitor-providers.md
---

# Copilot tool instrumentation

## Claim

A provider with empty permissions can report reads and writes that
cooperating Copilot tools already perform, using the normalized loopback
API.

## Coverage versus eslogger

Sees explicit tool file access in the current session. Does not see
arbitrary `cat`/`head`, other terminals, or unrelated editors unless those
also report.

## Why it is not a replacement

The ask wanted the same capability. This is the honest unprivileged subset:
useful, narrower, and already described as a future provider. It is not
enabled.

## Canvas embed

Fits the architecture: a reporter beside the canvas, not an iframe. Session
scope can be implicit because the tools are the session.

## Verdict

Best unprivileged *future* provider if coverage is labeled as cooperating
tools only. Not an eslogger equivalent.
