---
type: document
title: Cartograph Atlas authoring guide
created: 2026-09-05
description: Scope, safe authoring, and publication of Cartograph experience.
origin: internal
sensitivity: internal
relates_to:
  - path: index.md
    kind: related
---

# atlas-cartograph-atlas

Private Atlas knowledge store for [Cartograph](https://github.com/sergio-sisternes-epam/atlas-cartograph).
It records observed experiences and their evidence, not executable extension code.

Start at [the Atlas index](index.md). The initial collection covers the
2026-09-05 activity-connection and collector-startup investigation.

## Building experience

Mount `github.com/sergio-sisternes-epam/atlas-cartograph-atlas` from the active
project using the Atlas skill's mount path. Write through its remember path.
Create a dated experience under `experiences/`, link its `work_id` to a
`work/<work_id>.md` hub with `kind: implements`, and keep the indexes current.

Separate observed facts, interpretations, recovery steps, and unresolved causes.
Include evidence provenance without copying private connection tokens, complete
collector commands, local absolute paths, or raw system-wide activity logs.
An operational recovery does not prove every suspected cause.

Finish each store mutation with `atlas compile --root <mounted-root>` using the
installed Atlas CLI. Commit and push the store first, then update the consuming
project's submodule pointer. Change schemas only through Atlas's schema path.
There is no unattended experience collection or background capture.

## Contents

- [Experiences](experiences/index.md): dated observations and outcomes.
- [Work](work/index.md): scope and outcomes for related experiences.
- [Structural log](log.md): initialization and work lifecycle changes.
- [Templates](templates/index.md): the initialized Atlas authoring templates.
