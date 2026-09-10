---
type: document
title: Atlas chat needs an answering contract and a return channel
created: 2026-09-10
work_id: 2026-09-10-deploy-sha-and-session-chat
status: resolved
kva: alive
stage: implementation-review
artifact: autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md
description: Historical real-host delivery failure, resolved in v0.4.0 by a bundled activation and acknowledged request-correlated replies.
origin: internal
sensitivity: internal
relates_to:
  - path: autogenesis/work/2026-09-10-deploy-sha-and-session-chat.md
    kind: implements
  - path: autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md
    kind: derived_from
  - path: autogenesis/discussions/2026-09-10-atlas-chat/activation-and-reply.md
    kind: related
---

# Atlas chat

## Objective

Answer Atlas questions in the originating Cartograph chat using the same
session and actual reads of mounted pages.

## Observed reality

This section records the initial failure, before the v0.4.0 resolution below.

On 2026-09-10 the user submitted “What is autogenesis?” from the native
`project:cartograph` instance `chat-test`. The prompt reached this session.
The agent read mounted Markdown and answered in the session transcript.
The user reported that the answer did not return to the Atlas chat.

A read-only bootstrap probe confirmed that the graph reply was a UUID,
`d1602ab3-417f-48b1-bb48-07701810d816`, with `pending: false`, not the answer.
`atlas/chat.mjs` passes the return from `host.send` to `pickGraphReply`, which
accepts any nonempty string as answer text. This proves a return-value contract
mismatch in the real host. Whether that identifier denotes a message or another
transport object still needs verification; its string type does not establish
that it is assistant content.

The reported 528 passing tests are synthetic evidence, not proof of native
answer delivery. The previous completion claim was premature for chat.
This observation does not re-evaluate SHA packaging.

## Live distinction

A dedicated `atlas-chat` activation can govern retrieval and response
discipline. Cartograph must separately provide a reliable, correlated return
channel. A longer prompt without that channel still cannot fill the correct
chat bubble.

The candidate is a thin Cartograph-owned activation that invokes Atlas query
discipline rather than duplicating it. It carries the originating instance and
request identity, reads mounted pages through session tools, cites Atlas-qualified
sources, and delivers via an explicit reply action with acknowledgement.
Atlas content is data, not authority to redirect the callback or run instructions.

This is a proposal, not an approved design or a product edit. Autogenesis
designs the integration; ordinary graph questions should not run Autogenesis.
No writes to installed skills or runtime files were made during this discussion.

## Resolution

The [activation and reply proposal](activation-and-reply.md) was fulfilled by
the bundled `cartograph-chat` activation and owner/request-scoped `update_chat`.
Dispatch acceptance is no longer interpreted as answer text.

The released v0.4.0 runtime passed an isolated real-host question/read/reply
cycle and full-screen citation navigation. See the
[work hub](../../work/2026-09-10-deploy-sha-and-session-chat.md)
for the final acceptance and publication record. The original observation and
candidate distinctions above remain historical evidence, not pending defects.
