---
type: experience
title: Live status concealed missing activations during heavy capture traffic
created: 2026-09-05
work_id: cartograph-activity-startup-2026-09-05
status: raw
description: Restart restored actual activation cues, but producer resource pressure recurred and capture freshness remained unmeasured.
tags: [cartograph, eslogger, capture-lag, reliability, activity, diagnostics]
origin: internal
sensitivity: internal
relates_to:
  - path: work/cartograph-activity-startup-2026-09-05.md
    kind: implements
  - path: experiences/2026-09-05-eslogger-waiting-startup.md
    kind: follows
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/activity/collector.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/activity/service.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/activity/model.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/75c0d234994924225067e4185e427924cdb0639f/.apm/extensions/cartograph/public/activity-playback.js
---

## Context

Later on 2026-09-05, the user reported no Knowledge Activation cues while the
collector still said Live. The open Atlas had grown to 14 nodes. Grouping was
`atlases`, highlighting was enabled, all layers were visible, and the highlight
lifetime was initially 10 seconds.

## What happened

Both a native view read and controlled shell reads were absent from immediate
receiver snapshots. The original `discussion-home.md` and a newly created page
were both exact lexical and physical members of the collector target allowlist.
The reader processes belonged to the configured Copilot session, and eslogger's
process group differed from the monitored session's group.

Earlier qualified graph IDs and current unqualified IDs were investigated, but
no ID-mapping or grouping fault was established. The empty receiver arrays
located the missing observations before browser rendering.

The existing eslogger process was running at approximately 99% CPU with about
1.8 GB resident memory after 20 minutes. With user approval, the normal collector
was stopped and a bounded, token-free producer/parser diagnostic was run.
It printed aggregate counters and limited session/target metadata, not raw
system-wide event history.

Its 60-second summary contained:

| Counter | Observed value |
| --- | ---: |
| Input bytes | 1,108,228,515 |
| Input lines | 538,965 |
| Access events | 534,454 |
| Process lifecycle events | 4,511 |
| Target-file events | 50 |
| In-scope target events | 9 |
| Viewer target events | 28 |
| Parser errors | 0 |

Target results comprised 28 excluded viewer events, nine accepted parser events,
and 13 unmodified closes. Accepted here means the diagnostic parser accepted
them; this diagnostic did not post to the real receiver.

The first four periodic reports contained no accepted target events. Matching
reader metadata appeared between the fourth and fifth reports, several seconds
after the controlled reads. This supports delayed capture under heavy traffic.
The detail limit prevented attributing every accepted count to a specific tool.
Process birth timestamps are not access timestamps, so the diagnostic did not
measure an exact producer lag for every event.

## Timestamp and health findings

The normal collector forwards path, PID, operation kind, and ancestry, but no
original OS event timestamp. The receiver stamps an accepted read with its own
current time and starts the highlight lifetime then. Browser playback starts
the displayed lifetime at presentation.

Consequently, more than 10 seconds of upstream delay does not by itself make a
read expire before receipt. It delays when the highlight can begin. Short
post-read snapshots can be empty because capture has not reached the receiver.
Delayed browser delivery can miss an expired receiver snapshot, but cannot
explain an empty receiver array.

Live is also not a freshness guarantee. After one accepted access, later empty
heartbeats can maintain Live. The 1,024-item collector queue only bounds filtered
target events, not eslogger's upstream system-wide JSON backlog. The browser's
adaptive queue/lag display measures visual playback, not producer capture lag.

## Outcome

After the user restored the normal collector, a controlled read of `log.md`
reached the receiver about 189 ms after the read. Native view reads also appeared.
In a separate visible browser client, the actual playback frames activated
`sdlc-model/experience-capture` and `log` 12 and 13 ms after receipt respectively.
The native-view activation persisted for about 10 seconds. A concurrent change
to a five-second lifetime explained the shorter later log activation.

The user then explicitly confirmed activation cues in the original embedded
canvas. This established end-to-end recovery, not just a successful HTTP
response or a separate-browser result. No renderer fix, installed-file update,
scope expansion, or provider switch was made.

## Remaining uncertainty and follow-up

Capture pressure is a strong explanation for the delayed observations, but
eventual delivery from the old long-running collector was not observed.
Its exact contribution to every missing cue is therefore not proven.

Resource pressure recurred quickly: a fresh normal producer was observed at
roughly 96% CPU and 830 MB resident memory after about 78 seconds. Restart was
an operational recovery, not evidence of a permanent fix or proof of a memory
leak. Capture loss remains unknown.

A proposed reliability improvement is provider-neutral transient telemetry for
input volume, forwarded and accepted counts, heartbeat age, and source-event
freshness where the provider's actual timestamp schema has been verified.
Connection health, legitimate idle, capture lag, and visual playback lag should
be distinguishable. These are proposals, not implemented features.
Dropping lifecycle records would undermine ancestry, and slowing input draining
could worsen upstream backlog; neither was used as a shortcut.

## Evidence provenance

Sanitized observations from the two Copilot sessions identified in the work hub,
between approximately 22:41 and 22:50 UTC on 2026-09-05. Evidence included
controlled reads, target membership, process resource snapshots, user-supplied
diagnostic counters, receiver timing, temporary browser playback observation,
and the user's embedded-canvas confirmation.

Connection credentials, complete collector commands, raw events, local absolute
paths, and unrelated process metadata are omitted. The diagnostic script and
temporary screenshot were removed, and browser instrumentation was restored.
