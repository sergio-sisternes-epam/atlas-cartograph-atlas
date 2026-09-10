---
type: document
title: Alternative report — opt-in command wrapper
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Wrappers and intercepting libraries see only commands that opt in; unwrapped access is invisible.
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

# Opt-in command wrapper

## Claim

A wrapper, preload, or library around `open`/`read` can report accesses
without sudo when programs are launched through it.

## Coverage versus eslogger

Only wrapped invocations. Direct binaries, already-running editors, and
cached content bypass the wrapper.

## Why it is not a replacement

Cartograph cannot force every Copilot tool and host helper through a
wrapper. Missed unwrapped access would look like an idle Atlas.

## Canvas embed

A wrapper is a process launcher, not a canvas component.

## Verdict

Reject as a default. Acceptable only as an explicit, labeled producer.
