---
type: document
title: Alternative report — Watchman
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: Facebook Watchman is a recursive change subscription service, not an open/read observer.
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
  - https://facebook.github.io/watchman/
---

# Watchman

## Claim

Watchman watches directory trees and notifies subscribers of filesystem
changes. It does not need Endpoint Security.

## Coverage versus eslogger

Recursive change events with its own query language. No foreign opens, no
session PID ancestry.

## Why it is not a replacement

Heavy external daemon for a job Cartograph already does with Node built-ins.
Still cannot satisfy the same-capability requirement.

## Canvas embed

A native service, not a canvas component. Wiring it would add an out-of-process
change producer, not a read producer.

## Verdict

Out of scope. Do not embed or register.
