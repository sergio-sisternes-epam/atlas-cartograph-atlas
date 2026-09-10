---
type: lesson
title: Knowledge Activation needs privileged open observation on macOS
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
status: active
description: macos-eslogger exists because other-process file opens are Endpoint Security events; sudo and Full Disk Access are OS requirements, not Cartograph ceremony.
origin: derived
sensitivity: internal
relates_to:
  - path: work/eslogger-unprivileged-alternatives-2026-09-10.md
    kind: implements
  - path: experiences/2026-09-10-eslogger-unprivileged-ask.md
    kind: derived_from
  - path: documents/eslogger-unprivileged-investigation.md
    kind: related
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/file-access.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/docs/monitor-providers.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/main/.apm/extensions/cartograph/activity/providers/eslogger.mjs
---

# Why Cartograph uses eslogger

Knowledge Activation highlights Atlas pages when tools in scope open them.
That is not the same as watching the directory for creates, edits, and
deletes. The graph already has an unprivileged watcher for those filesystem
changes. The access provider must see **opens by other processes**, classify
read versus write from open flags and modified closes, and attribute session
descendants via fork, exec, and exit.

A normal macOS process cannot subscribe to another process's file opens.
Apple exposes that through Endpoint Security. `/usr/bin/eslogger` is the
shipped producer. Cartograph filters those events to exact open-graph paths
after the privileged stream exists. Folder interest is a filter, not a
weaker permission grant.

# Why it requires sudo

`eslogger` needs root and Full Disk Access because the kernel will not give
an unprivileged process a system-wide open/close stream. Cartograph cannot
bypass TCC. The adapter never auto-elevates. Live status requires a valid
file-access observation, not merely starting the process.

# Limitations to keep visible

Do not describe eslogger as an audit log or as every `read`/`write` syscall.
It misses already-open descriptors, memory-mapped I/O, and cache hits. An
open does not prove bytes were consumed. The schema is diagnostic, not
stable. Events can be lost. Session mode drops unknown ancestry rather than
broadening to the host app. There is no Linux or Windows collector.

# Do not substitute folder watchers

FSEvents, kqueue, Node `fs.watch`, chokidar, fswatch, and Watchman report
changes, not foreign reads. Polling `atime` is delayed, coalesced, or
disabled, and cached reads may never touch the filesystem. Cooperating tools
and editors can report without sudo, but they do not see arbitrary shells.
Do not silently fall back to a weaker producer while claiming eslogger
coverage.
