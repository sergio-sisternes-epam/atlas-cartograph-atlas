---
type: protostar
title: Design an atlas-chat activation with acknowledged canvas replies
created: 2026-09-10
work_id: 2026-09-10-deploy-sha-and-session-chat
status: fulfilled
kva: forming
growth: true
star_kind: action
stage: implementation-review
artifact: autogenesis/plans/2026-09-10-deploy-sha-and-session-chat.md
description: Historical forming proposal fulfilled by v0.4.0's deployed activation and request-correlated reply contract.
origin: derived
sensitivity: internal
relates_to:
  - path: autogenesis/discussions/2026-09-10-atlas-chat/index.md
    kind: derived_from
  - path: autogenesis/work/2026-09-10-deploy-sha-and-session-chat.md
    kind: implements
---

# Candidate activation and delivery contract

This preserves the forming proposal as written before implementation. It was
subsequently fulfilled; the final outcome is recorded below rather than
retroactively treating the proposal as implementation authority.

The user proposes a dedicated `atlas-chat` activation path containing the
session instructions for answering graph questions. The agent recommends a
Cartograph-owned adapter over Atlas query, paired with runtime delivery.

Before implementation, formal design should establish:

- A discoverable, deployed activation and explicit invocation contract.
  Do not merely name an uninstalled path in a prompt.
- An envelope containing session, canvas instance and request correlation,
  mounted roots/Atlas identities, selection, and the user's question.
- Atlas search and actual page reads through existing session tools.
  Citations preserve the originating Atlas; insufficient evidence is a gap.
  Answering does not automatically mutate Atlas memory.
- A proposed reply action that accepts only the matching pending request in
  the owning instance/session, acknowledges delivery and tolerates retries
  without duplicating messages. No bearer credentials in prompt text.
- Pending, answered, failed, cancelled and expired request behaviour. Sending
  a prompt is not answer completion. Late replies cannot resurrect closed
  instances or overwrite another request.
- A real-host acceptance check: question arrives, pages are read, answer
  appears in the originating drawer. Add out-of-order, duplicate, foreign
  instance, empty reply and host-error cases to synthetic tests.

Verify the actual host SDK event/completion semantics before choosing whether
an explicit agent reply action or a correlated completion subscription is the
best return channel. Never capture the latest unrelated session response.
Keep the adapter independent of Autogenesis for ordinary question answering.

This forming proposal has no implementation authority.

## Fulfilled in v0.4.0

The deployed activation is `cartograph-chat`; the acknowledged reply action is
`update_chat`. Both ship in the runtime bundle, preserve the owning session and
request, and keep mounted Atlas content as evidence rather than authority.
Real-host acceptance demonstrated actual page reads, a cited answer delivered
to its own pending request, and usable citation previews. See the
[work hub](../../work/2026-09-10-deploy-sha-and-session-chat.md)
for the released source and acceptance record. This candidate is no longer
awaiting implementation; its forming classification preserves its origin.
