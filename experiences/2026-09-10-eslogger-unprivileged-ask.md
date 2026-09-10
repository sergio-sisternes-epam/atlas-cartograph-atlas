---
type: experience
title: User asked for a sudo-less folder monitor matching eslogger
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Two linked questions: replace macos-eslogger for a specific folder without sudo, then embed an open-source project in the canvas.
origin: user
sensitivity: internal
relates_to:
  - path: work/eslogger-unprivileged-alternatives-2026-09-10.md
    kind: implements
  - path: documents/eslogger-unprivileged-investigation.md
    kind: related
  - path: lessons/macos-eslogger-requires-privileged-open-observation.md
    kind: related
  - path: experiences/2026-09-05-eslogger-waiting-startup.md
    kind: related
---

## Context

A Copilot session on Cartograph asked whether the Knowledge Activation
collector could drop `macos-eslogger` for something that watches one folder
and does not need administrator approval. After the first answer, the user
asked whether any open-source project could be embedded into the canvas.

The store for this memory is `atlas-cartograph-atlas`, not the Atlas skill
store. The investigation did not start a collector or change runtime code.

## What happened

The first question required same monitoring capability as eslogger, scoped to
a folder, without sudo. Product docs already separate the unprivileged graph
watcher from the privileged access provider. macOS has no user-space API that
reports other processes' reads of a folder.

The second question asked about embedding open-source monitors in the canvas.
The canvas is a web UI. Collectors stay out of process and post the normalized
activity protocol. The runtime may import only Node built-ins and the host
Copilot SDK, so npm watchers cannot be vendored into the extension.

The user then asked to persist why eslogger is required, why it needs sudo,
limitations, the lack of equivalents, a summary, and a detailed report for
each alternative, all linked to this ask.

## Outcome

Investigation memory is recorded under
[work/eslogger-unprivileged-alternatives-2026-09-10](../work/eslogger-unprivileged-alternatives-2026-09-10.md).
No provider was enabled. No silent fallback was added.

## Related

- [Investigation summary](../documents/eslogger-unprivileged-investigation.md)
- [Privileged-open lesson](../lessons/macos-eslogger-requires-privileged-open-observation.md)
- [Alternative reports](../documents/eslogger-alternatives/index.md)

## Follow-ups

A cooperating Copilot or editor reporter remains a possible future provider
with weaker coverage. It is not implemented.
