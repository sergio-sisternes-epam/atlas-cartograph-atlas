---
type: document
title: "Atlas onboarding and Cartograph: connected knowledge"
created: 2026-09-10
reviewed_at: 2026-09-10
status: published
origin: derived
sensitivity: internal
description: "Link Cartograph's product knowledge to Atlas-owned visualiser help and onboarding."
relates_to:
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: derived_from
  - path: work/cartograph-v030-2026-09-10.md
    kind: related
  - path: atlas://atlas-skill-memory/help/cartograph.md
    kind: related
  - path: atlas://atlas-skill-memory/help/open-cartograph.md
    kind: related
  - path: atlas://atlas-skill-memory/help/install-and-open-cartograph.md
    kind: related
  - path: atlas://atlas-skill-memory/autogenesis/work/2026-09-10-skill-help-pilot-cartograph.md
    kind: related
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/41ca3e2a0c2918acaa57ce5ec898033d7a17b786/atlas-mesh.json
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/41ca3e2a0c2918acaa57ce5ec898033d7a17b786/README.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph-atlas/blob/fd17c25c7bf4151e4e86960a987a605324a64901/decisions/cartograph-v030-interaction-contract.md
---

# Keep help connected to product knowledge

Cartograph visualises Atlas pages and relationships; Atlas owns the knowledge
protocol and its onboarding. Keep detailed Cartograph behavior and operational
experience here, and follow these links to the Atlas-owned help:

- [What is Cartograph?](atlas://atlas-skill-memory/help/cartograph.md)
- [Open from the Copilot Canvas menu](atlas://atlas-skill-memory/help/open-cartograph.md)
- [Install and open with APM](atlas://atlas-skill-memory/help/install-and-open-cartograph.md)
- [Pilot memory and consent boundary](atlas://atlas-skill-memory/autogenesis/work/2026-09-10-skill-help-pilot-cartograph.md)

These are navigation links, not a dependency on the Atlas executable package
and not authorization to install extensions. The native help is specific to
GitHub Copilot App with canvas support. Read monitoring remains separate from
ordinary opening and graph updates, as the
[interaction contract](../decisions/cartograph-v030-interaction-contract.md)
requires.

## Identities and availability

The Atlas CLI identities are
`github.com/sergio-sisternes-epam/atlas-atlas` and
`github.com/sergio-sisternes-epam/atlas-cartograph-atlas`. Mount and resolve
using those full identities in the active project.

The graph-qualified links use the stores' existing schema IDs:
`atlas-skill-memory` and `atlas-cartograph-atlas`. They are Cartograph graph
identities, not shorthand arguments to Atlas mount/resolve. Open both stores
in the same Cartograph view to follow the links; opening one explicit root
does not fetch the other. Do not rename schema IDs or construct filesystem
paths that escape a store to make the connection.

The current Atlas CLI may emit non-blocking `atlas_uri_unmounted` warnings
for these short graph IDs even with both canonical repositories registered:
its URI normalizer expects host/org/repo. Graph navigation was checked
separately. This is a naming compatibility limit, not permission to invent
mesh entries or claim that every Atlas consumer resolves the links.

The connection was authored locally on 2026-09-10 at the user's request.
Publication is separate: until the linked Atlas changes are committed and
pushed, another consumer's older pin may not contain the articles. A missing
target must be reported, not treated as evidence that the article was read.
If help references lack the answer, query the owning Atlas; if retrieval
fails, disclose limited help and the unavailable knowledge store.
