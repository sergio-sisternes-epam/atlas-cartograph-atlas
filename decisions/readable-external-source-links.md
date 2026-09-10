---
type: decision
title: Make external sources readable without turning them into graph relationships
created: 2026-09-10
status: accepted
description: Use accessible external-source rows with explicit or locally derived labels, preserving exact web destinations.
origin: user
sensitivity: internal
relates_to:
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: related
  - path: work/cartograph-v030-2026-09-10.md
    kind: derived_from
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/27a5090/.apm/extensions/cartograph/public/app.js
---

# Readable external sources

## Evidence and approval

On 2026-09-10 the user opened the v0.3.0 delivery page to try external
frontmatter sources. Its preview reduced three URLs to `8`, `v0.3.0` and `10`.
The implementation used the last path segment for every source chip.
Those labels concealed whether the destination was a pull request, a release,
or a different repository.

The user approved recording and implementing the proposed design with
"Build a memory of this change and proceed." This page records that accepted
design, not a claim that browser behavior has already been verified.

## Decision

Separate HTTP/HTTPS provenance into an **External sources** section in the
page preview. Keep internal Atlas sources and relationships as compact chips.
Each external row has a descriptive label, visible repository/domain context,
an external-link icon and a generous whole-row click target. Use readable,
higher-contrast text, visible keyboard focus and the full destination on hover
and focus. Long destinations must wrap without widening the preview or
covering the chat drawer.

Prefer an optional explicit frontmatter title. Otherwise derive a useful
label locally: distinguish GitHub pull requests, issues, releases, commits and
files; show a readable path and domain for other sites. Do not fetch remote
titles, favicons or other metadata simply by opening a page.

Accept source strings and source objects with `path`, `url` or `uri` and an
optional `title`. Preserve web URLs, including `.md` suffixes, query strings
and fragments; never run them through internal-page slug normalization.
Retain the existing internal source and graph relationship contracts.

Metadata is untrusted display data, not executable content. Only HTTP/HTTPS
destinations become external-source links. Reuse the delegated navigation
path, open a destination once, retain native link semantics and do not infer
graph edges from external source rows.

## Acceptance

The original delivery page should distinguish both pull requests by
repository and clearly identify the release. Mouse and keyboard activation
should open the intended destination, with focus revealing its full URL.
Internal navigation, graph edges and chat/preview coexistence must remain
unchanged. No automatic remote requests are needed for labels.

## Implementation outcome

Implemented in the same worktree on 2026-09-10. Preview payloads retain
`sources: string[]` and add ordered `sourceDetails: [{ path, title? }]`.
The source-specific parser supports strings and titled `path`/`url`/`uri`
records without becoming a general YAML parser. Unsupported schemes do not
become external-source rows.

The targeted parser, page, HTTP, frontend and canonical/deployed native suite
passed 115 tests. On the reopened native canvas server, browser checks showed
the three readable destinations, visible focus/hover URLs, and no horizontal
overflow with chat open at viewport widths from 600 to 1600 pixels. Pointer
click and Enter each opened one tab at the expected URL; those destination
requests were intercepted locally, so this proves navigation rather than
remote website availability or authentication. A modified-click exercise
opened the marketplace destination in a separate tab, but its popup-event
wait timed out; it was not counted as a completed automated assertion.

The v0.3.0 delivery preview was left selected for the user's native-host
exercise. No collectors or remote metadata fetches were started by the new
source-label rendering.
