---
type: experience
title: Reload restored installed v0.4.0 chat but exposed a missing source-install SHA stamp
created: 2026-09-10
work_id: 2026-09-10-deploy-sha-and-session-chat
status: observed
description: Installed files and running code differed; reloading recovered chat, while global source-based installation still lacked usable provenance metadata.
origin: internal
sensitivity: internal
relates_to:
  - path: autogenesis/work/2026-09-10-deploy-sha-and-session-chat.md
    kind: implements
  - path: experiences/2026-09-05-stale-runtime-activity-404.md
    kind: related
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/issues/12
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/releases/tag/v0.4.0
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/0e391ffb530252874b5ed163a17228a471789a12/.apm/extensions/cartograph/build-info.mjs
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/0e391ffb530252874b5ed163a17228a471789a12/.gitattributes
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/0e391ffb530252874b5ed163a17228a471789a12/scripts/package-apm.mjs
---

# Installed v0.4.0: two different problems

## Context

After the v0.4.0 release, marketplace publication and global installation, the
user reported that installed chat did not work. The environment was macOS on
Apple Silicon, Copilot CLI 1.0.83 and APM 0.30.0. Inspection distinguished an
already-running extension from the newly installed files and then exposed a
separate provenance gap.

## Stale runtime evidence and recovery

The user extension process in the affected session had started at 13:22 local
time, before the update. Its registered canvas actions lacked `update_chat`.
An older project canvas also reported v0.3.0. In contrast, the installed
`package.json` reported v0.4.0, and the entrypoint, chat modules, bundled
activation, browser application and styles matched the released source.
The missing capability and file comparison, not process age alone, established
that the affected session had not loaded the installed chat implementation.

The old project canvas's server-side snapshot was saved for recovery. Reloading
extensions in the affected session exposed `update_chat`; opening fresh
`user:cartograph` canvases then exercised the installed implementation.
This was an extension reload, not the graph's filesystem rescan action.
The server-side snapshot did not establish preservation of browser-only drafts.

Two separate real-host requests completed: the user's "What is atlas?" question
and a diagnostic question about the v0.4.0 work hub. After the sending turn
yielded, the actual session activations arrived. The agent searched the mounted
project Atlas, read the authoring guide/index or work hub as appropriate, and
sent cited answers to each originating canvas/request. Both replies received
matching `ok: true`, `status: answered` acknowledgements; the diagnostic answer
was also visible in the browser conversation.

No installed source file was patched to recover chat. No collector was started,
and no new executable trust or global package change was needed.

## Separate source-install provenance gap

The fresh installed canvas reported `v0.4.0 / SHA unavailable` after the reload.
The installed package had no `cartographBuild` field, and its
`cartograph-build.json` still contained the literal `$Format:%H$` placeholder
with `dirty: false`. The recorded installation had resolved to released source
commit `0e391ffb530252874b5ed163a17228a471789a12`; the visible badge nevertheless
had no usable stamp.

The inspected source declares `export-subst` for the build JSON. That substitution
applies to Git archive export, not an ordinary checkout. The repository packer
separately stamps its isolated runtime output. The observed global source-based
installation had neither usable form of stamp. The exact correction at the
installation/packaging boundary was not implemented or assigned to an upstream
component during this investigation.

Rejecting the placeholder is intentional: the deployed viewer must not borrow
the consumer repository's SHA or invent a source identity. Reloading loaded the
new chat code but could not manufacture missing deployment metadata.

## Acceptance boundary and remaining work

The earlier real-host acceptance remains valid for the exact stamped CI/release
package. It did not prove that the separate marketplace Git/source installation
path preserved provenance. Resolving the expected version/ref in the catalog and
successfully installing it were insufficient evidence for that claim.

[Cartograph issue #12](https://github.com/sergio-sisternes-epam/atlas-cartograph/issues/12)
records the reproduction, observed metadata, environment and acceptance criteria.
The source-install SHA defect remained open and unfixed at this capture.
Reproduction should exercise the actual source installation in an isolated
consumer/profile and inspect both deployed metadata and the fresh native badge.
It must preserve source-checkout dirty-state behavior, stamped-archive support
and the refusal to use consumer Git as a fallback. Existing v0.4.0 tags and
release assets were not replaced.

Chat recovery does not close the SHA issue, and this follow-up does not negate
the earlier packaged-runtime chat acceptance. The release work hub is qualified
accordingly rather than treating all deployment paths as proven.
