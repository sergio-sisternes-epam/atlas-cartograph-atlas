---
type: document
title: Alternative report — osquery
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: recorded
description: osquery file_events uses FSEvents; Endpoint Security tables that see opens need root and Apple entitlements.
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
  - https://github.com/osquery/osquery
  - https://blog.trailofbits.com/2021/11/10/announcing-osquery-5-now-with-endpointsecurity-on-macos/
---

# osquery

## Claim

osquery can query file events on macOS. That does not make it an unprivileged
eslogger replacement.

## Coverage versus eslogger

`file_events` is FSEvents-based: writes and metadata changes, not every
foreign open. `es_process_file_events` and related tables use Endpoint
Security, which needs root and `com.apple.developer.endpoint-security.client`.

## Why it is not a replacement

The tables that approach eslogger coverage reimpose the same OS privilege
bar, plus an Apple entitlement Cartograph does not ship. The unprivileged
table is another change watcher.

## Canvas embed

osquery is a daemon/CLI, not a canvas widget. Embedding it would still
require the user to grant ES privileges for open observation.

## Verdict

Do not embed. It does not remove sudo for the capability we need.
