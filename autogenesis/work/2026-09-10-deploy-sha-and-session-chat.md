---
type: work
title: Stamp deployed SHA and route canvas chat through the host session
created: 2026-09-10
work_id: 2026-09-10-deploy-sha-and-session-chat
status: done
description: Released in v0.4.0 with stamped source identity and acknowledged session-backed chat, including real-host page reads and citation navigation.
origin: internal
sensitivity: internal
relates_to:
  - path: autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md
    kind: related
  - path: work/cartograph-v030-2026-09-10.md
    kind: follows
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: related
  - path: autogenesis/discussions/2026-09-10-atlas-chat/index.md
    kind: related
  - path: decisions/cartograph-ux-principles-protostar.md
    kind: related
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/pull/10
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/releases/tag/v0.4.0
  - https://github.com/sergio-sisternes-epam/apm-marketplace/pull/12
---

# Deploy SHA and session chat

## Scope

Fix two user-visible gaps after v0.3.0: deployed canvases reporting
`SHA unavailable`, and canvas chat answering with local keyword search
instead of the underlying Copilot session.

## Status

`done`. Runtime, tests and docs were merged in PR #10 and released as v0.4.0
at `0e391ffb530252874b5ed163a17228a471789a12`.

The initial completion claim was corrected after native testing on 2026-09-10:
the question reached the session, but the canvas displayed a UUID instead of
the answer. That failure is preserved in the linked discussion. It was
subsequently resolved by the activation and acknowledged reply contract below;
it is no longer an open delivery defect.

## Outcomes

- Source checkouts still read Git first so `+ local` stays honest.
- APM packaging stamps `cartograph-build.json` and `cartographBuild`.
- Unsubstituted `$Format:%H$` stamps are ignored; missing identity stays
  `SHA unavailable` rather than a consumer Git SHA.
- Native `onChat` calls `session.send` on the joined session with Atlas ids,
  selection and query. Page bodies are not inlined. Failures do not fall back
  to `answerQuery`. HTTP/dev without a host session still uses local search.
- `session.send` returns dispatch acceptance, not answer text. The bundled
  `cartograph-chat` activation directs actual mounted-page reads and sends
  request-correlated progress/final replies through `update_chat`.
- Chat revisions advance on mutations rather than unrelated snapshots, keeping
  large histories from being serialized again merely to detect UI changes.
- Full-screen citations restore the drawer and reveal the referenced Markdown
  page without clearing the draft or conversation.

## Final acceptance and publication

The exact main-CI runtime was installed in an isolated APM 0.30.0 consumer with
an initially empty allow-map and an exact-content, canvas-only grant. All 57
deployed runtime files matched. The real native host displayed v0.4.0 and the
released source SHA without borrowing the consumer repository identity.

The successful interactive probe yielded immediately after dispatch. The
actual activation arrived in a new session turn, the agent read the mounted
mini Atlas decision page, and `update_chat` acknowledged the cited answer as
`answered`. Full-screen citation navigation, draft/history retention and
unchanged-snapshot DOM retention were also observed. The earlier queued-only
probe and synthetic SDK tests alone were not treated as native acceptance.

The tag workflow published the archive, checksum and `release.json`. Its runtime
and plugin files were byte-identical to the native-accepted main artifact; only
the generated lockfile packing timestamp differed.

[sergio-sisternes-epam/apm-marketplace#12](https://github.com/sergio-sisternes-epam/apm-marketplace/pull/12)
merged at `3fc66231cf61f93611a4fc51696c1208365ceb90`,
pinning v0.4.0 to the released source commit. Isolated marketplace resolution
confirmed that version and SHA. Existing installations require an explicit
refresh/update; the owner's separately requested global update subsequently
completed without changing unrelated toolkit references.

## Related

- Plan: `autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md`
- Prior contract: `decisions/cartograph-v030-interaction-contract.md`
