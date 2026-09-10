---
type: document
title: Alternative report — FUSE-T
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: A FUSE overlay can log reads that pass through its mount, but only those paths, and it cannot live inside the canvas.
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
  - https://www.fuse-t.org/
  - https://github.com/macos-fuse-t/fuse-t
---

# FUSE-T

## Claim

FUSE-T is kext-less FUSE for macOS. A user-space filesystem can intercept
open/read/write for processes that use the mount. Everyday mounts often
avoid sudo after install.

## Coverage versus eslogger

Sees reads only when the application uses the FUSE path. Direct access to
the real Atlas directory bypasses it. Installing the cask and mounting still
changes how the store is reached.

## Why it is not a replacement

It rewrites workspace paths instead of observing the live store. Copilot
tools that open the real `.atlas` files would be invisible. Complexity and
path identity risk are high relative to Knowledge Activation.

## Canvas embed

A filesystem driver is not a canvas surface. Cartograph would still need an
out-of-process reporter posting the activity protocol.

## Verdict

Not a drop-in provider. Do not overlay Atlas roots for monitoring.
