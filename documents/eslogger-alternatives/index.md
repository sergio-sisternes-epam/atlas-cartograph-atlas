---
type: document
title: eslogger alternative reports
created: 2026-09-10
work_id: eslogger-unprivileged-alternatives-2026-09-10
description: Spine for each unprivileged or embeddable candidate compared with macos-eslogger.
origin: derived
sensitivity: internal
relates_to:
  - path: work/eslogger-unprivileged-alternatives-2026-09-10.md
    kind: implements
  - path: documents/eslogger-unprivileged-investigation.md
    kind: related
  - path: documents/eslogger-alternatives/directory-watcher.md
    kind: related
  - path: documents/eslogger-alternatives/chokidar.md
    kind: related
  - path: documents/eslogger-alternatives/fswatch.md
    kind: related
  - path: documents/eslogger-alternatives/watchman.md
    kind: related
  - path: documents/eslogger-alternatives/osquery.md
    kind: related
  - path: documents/eslogger-alternatives/filewatcher-auditpipe.md
    kind: related
  - path: documents/eslogger-alternatives/fuse-t.md
    kind: related
  - path: documents/eslogger-alternatives/copilot-tool-hooks.md
    kind: related
  - path: documents/eslogger-alternatives/editor-integration.md
    kind: related
  - path: documents/eslogger-alternatives/opt-in-wrapper.md
    kind: related
  - path: documents/eslogger-alternatives/atime-polling.md
    kind: related
  - path: documents/eslogger-alternatives/canvas-embed.md
    kind: related
---

# Alternative reports

Each page is a candidate from the 2026-09-10 ask. None replaces eslogger's
other-process open coverage without privileges.

- [Directory watcher](directory-watcher.md): already shipped; changes only.
- [chokidar](chokidar.md): Node FSEvents wrapper; cannot vendor into runtime.
- [fswatch](fswatch.md): cross-platform change CLI; not reads.
- [Watchman](watchman.md): recursive change service; not reads.
- [osquery](osquery.md): FSEvents table is writes; ES tables need root.
- [filewatcher](filewatcher-auditpipe.md): auditpipe requires root.
- [FUSE-T](fuse-t.md): reads only through a mount; not a canvas embed.
- [Copilot tool hooks](copilot-tool-hooks.md): unprivileged, cooperating tools only.
- [Editor integration](editor-integration.md): unprivileged, that editor only.
- [Opt-in wrapper](opt-in-wrapper.md): unprivileged, wrapped commands only.
- [atime polling](atime-polling.md): not a reliable read signal.
- [Canvas embed](canvas-embed.md): canvas cannot host a native OS monitor.
