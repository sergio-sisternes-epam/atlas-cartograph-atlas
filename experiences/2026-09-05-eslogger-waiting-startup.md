---
type: experience
title: Collector startup output did not establish working file capture
created: 2026-09-05
work_id: cartograph-activity-startup-2026-09-05
status: raw
description: Separate sudo authorization and collector restart restored matching Atlas reads; the original startup cause remained partly uncertain.
tags: [cartograph, eslogger, sudo, waiting, process-scope, diagnostics]
origin: internal
sensitivity: internal
relates_to:
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: implements
  - path: experiences/2026-09-05-stale-runtime-activity-404.md
    kind: follows
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/2372272dc5c282f1b1a472483a412ef394971764/.apm/extensions/cartograph/activity/collector.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/2372272dc5c282f1b1a472483a412ef394971764/.apm/extensions/cartograph/activity/providers/eslogger.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/2372272dc5c282f1b1a472483a412ef394971764/.apm/extensions/cartograph/activity/service.mjs
---

## Context

After the activity endpoint was repaired, the user manually ran the generated
macOS eslogger-to-Node pipeline. Terminal printed the collector's coverage
disclaimer, while Knowledge Activation remained Waiting.

Waiting alone was inconclusive: the receiver requires its first accepted access
to an open Atlas file before reporting Live. Process lifecycle events, unrelated
files, other sessions, and the viewer's own reads cannot establish Live.

## What happened

Controlled reads of `discussion-home.md` from the monitored Copilot session
initially produced no highlights. The readers' parent was the configured session
root, the file belonged to the open Atlas, and its lexical and physical paths
matched. Installed collector sources matched the investigated worktree.
Those observations ruled out the checked path and root-PID mismatches, but not
every possible capture or attribution failure.

With the user's approval, a temporary 45-second diagnostic counted input and
reported only bounded session/Atlas metadata. It used no collector credential,
did not publish fake activity, and retained no system-wide event log.
An initial diagnostic reported zero input lines. Its Node-side READY message
could appear independently of whether sudo had authorized eslogger.

The user then authorized sudo separately with `sudo -v` and reran the pipeline.
The producer was observed running. A later diagnostic sample reported 5,944
input lines, two in-scope target events, and zero parser errors. Cartograph's own
reads were correctly rejected as out-of-scope; they were not evidence of a
broken process filter.

## Outcome

After restarting the normal collector, controlled reads from the monitored
session reached the real receiver. At 22:24 UTC on 2026-09-05, bootstrap reported
Live with two observations on `atlas-sdlc-atlas::discussion-home`; a later sample
remained Live without an error.

The diagnostic did not itself make the graph Live because it deliberately sent
no activity events. Only the normal collector established the final result.
No monitor fallback, expanded process scope, permission bypass, or runtime code
change was needed. The temporary diagnostic was removed afterward.

## Uncertainty

The exact initial authorization state was not captured. A hidden or interleaved
sudo prompt is plausible, but not proven. The initial receiver message also
suggested some valid input may have existed during an earlier attempt, so the
later zero-line diagnostic must not be generalized to the entire incident.
The demonstrated recovery is separate preauthorization followed by restart,
not proof that all Waiting states have the same cause.

## Evidence provenance

Sanitized observations from the work hub's two Copilot sessions on 2026-09-05,
including user-supplied diagnostic counts and controlled reads in the affected
session. The local `eslogger(1)` manual confirmed that the producer requires
superuser authorization and responsible-application Full Disk Access.
Tokens, complete connection commands, absolute user paths, and raw events are
intentionally omitted.

## Follow-ups

Startup guidance could separate sudo authorization from pipeline startup.
Diagnostics could distinguish producer input, receiver connectivity, and the
first accepted Atlas access. These were proposed improvements, not delivered
features. Node's startup banner alone should not be treated as evidence of
successful capture.
