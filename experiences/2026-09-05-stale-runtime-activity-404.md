---
type: experience
title: Updated Cartograph UI encountered an older in-memory server
created: 2026-09-05
work_id: cartograph-activity-startup-2026-09-05
status: raw
description: A missing activity endpoint was recovered by reloading the extension, not changing collector permissions.
tags: [cartograph, activity, initialization, stale-runtime, http-404]
origin: internal
sensitivity: internal
relates_to:
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: implements
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/2372272dc5c282f1b1a472483a412ef394971764/.apm/extensions/cartograph/server.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/2372272dc5c282f1b1a472483a412ef394971764/.apm/extensions/cartograph/activity/service.mjs
---

## Context

The installed user Cartograph canvas was open in another project's Copilot
session. Knowledge Activation displayed "Could not load the activity connection.
Activity request failed (404)." The UI also lacked provider and process-scope
information.

## What happened

Read-only inspection identified the existing user-scoped extension instance and
confirmed that its process owned the canvas's loopback listener. The installed
entrypoint file was newer than the running process.

The existing server returned HTML fallback content with HTTP 404 for
`GET /api/activity/connection` even with the required canvas header. Both
`get_state` and the successful `/api/bootstrap` response lacked activity fields.
The worktree implementation and copied-consumer exercise did support that route.

Together, these observations identified a stale in-memory backend serving newer
UI assets. File modification time alone would not have established that
diagnosis; the missing route and state fields were the stronger evidence.

## Outcome

The affected session reloaded its extensions and reopened the same Cartograph
instance and explicit Atlas root. The activity connection then returned HTTP 200,
and bootstrap supplied `macos-eslogger` provider metadata and session process
scope. The same initial graph, three nodes and one edge, and its UI state were
preserved. No collector was started or elevated as part of this recovery.

The fix required neither an application code change nor an installed-file edit.
Collector permissions were not the cause of this HTTP 404.

## Evidence provenance

Observed on 2026-09-05 during the work hub's two linked Copilot sessions.
Endpoint comparisons and process/file timing were obtained from the affected
session before restarting it. The source links identify the inspected code
revision; they do not prove the exact old revision loaded into memory.

## Follow-ups

A future compatibility diagnostic could identify missing activity capabilities
and suggest an extension reload instead of displaying only a generic HTTP error.
This improvement was proposed, not implemented.
