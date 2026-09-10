---
type: work
title: Stamp deployed SHA and route canvas chat through the host session
created: 2026-09-10
work_id: 2026-09-10-deploy-sha-and-session-chat
status: done
description: Deployed Cartograph keeps its source SHA via file/package stamps, and native canvas chat sends a compact envelope to the joined Copilot session.
origin: internal
sensitivity: internal
relates_to:
  - path: autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md
    kind: related
  - path: work/cartograph-v030-2026-09-10.md
    kind: follows
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: related
---

# Deploy SHA and session chat

## Scope

Fix two user-visible gaps after v0.3.0: deployed canvases reporting
`SHA unavailable`, and canvas chat answering with local keyword search
instead of the underlying Copilot session.

## Status

`done`. Runtime, tests and docs landed on the worktree branch.

## Outcomes

- Source checkouts still read Git first so `+ local` stays honest.
- APM packaging stamps `cartograph-build.json` and `cartographBuild`.
- Unsubstituted `$Format:%H$` stamps are ignored; missing identity stays
  `SHA unavailable` rather than a consumer Git SHA.
- Native `onChat` calls `session.send` on the joined session with Atlas ids,
  selection and query. Page bodies are not inlined. Failures do not fall back
  to `answerQuery`. HTTP/dev without a host session still uses local search.

## Related

- Plan: `autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md`
- Prior contract: `decisions/cartograph-v030-interaction-contract.md`
