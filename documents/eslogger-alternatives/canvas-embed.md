---
type: document
title: Alternative report — embedding OSS in the canvas
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: The Cartograph canvas cannot host a native file monitor; collectors stay out of process and the runtime forbids third-party imports.
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
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/monitor-providers.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/.apm/extensions/cartograph/activity/providers/index.mjs
---

# Embedding open-source monitors in the canvas

## Claim

The follow-up ask was whether an open-source project could be embedded into
the canvas to watch a folder without sudo.

## Coverage versus eslogger

A browser canvas cannot observe host file opens. The File System Access API
sees only user-granted browser files, not Copilot tools. Native collectors
must remain separate processes that POST the activity protocol.

## Why it is not a replacement

The runtime bundle may import only Node built-ins and the host Copilot SDK.
chokidar and similar libraries cannot be vendored. Provider modules may
spawn a user-installed command, as eslogger does, but that is not an embed.

Synthetic second providers in tests are not registered for production.

## Canvas embed

The canvas can show setup text and connection status. It cannot become the
monitor.

## Verdict

No OSS project is embeddable as a same-capability collector. Future
unprivileged producers should implement the HTTP reporter contract instead.
