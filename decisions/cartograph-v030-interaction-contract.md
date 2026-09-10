---
type: decision
title: Keep graph interaction visible, bounded and independent of capture
created: 2026-09-10
work_id: cartograph-v030-2026-09-10
status: accepted
description: The final v0.3.0 design supersedes the session's popup-search, static-galaxy and arrival-limited-glow experiments.
origin: derived
sensitivity: internal
relates_to:
  - path: work/cartograph-v030-2026-09-10.md
    kind: implements
  - path: experiences/2026-09-10-cartograph-v030-delivery.md
    kind: derived_from
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/fe6de71e56422bda09dd0a92cf59d683d883e396/AGENTS.md
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/fe6de71e56422bda09dd0a92cf59d683d883e396/docs/usage.md
---

# Final interaction contract

## Search and selection

Keep one always-visible toolbar search field, not a launch-button popup.
Typing shows accessible bounded result pages; Down can browse all nodes from
an empty field; Escape returns focus without hiding the query. Search results,
renderers and activation framing share title, ID, Atlas, path, type and kind
matching. Hidden-layer results remain discoverable. Pending text and caret
must survive older snapshots.

First interactive activation focuses the node, direct relationships and
visible first-degree neighbors. Repeating activation opens Markdown. Resolve
both stages together on the server, not through racing select/preview calls.
Page links and native explicit selection retain their direct-preview contract.

## Geometry and camera

Use bounded deterministic volumetric galaxies for Layers and Atlases, with
high-mass bulges, three arms and real bulk depth. Keep Proximity placement.
Do not infer relationships from spatial proximity. Start obliquely but retain
the original idle rotation; selection, manual control and reduced motion take
priority. Grouping navigation uses shortest speed-limited turns and yields
stale activation following for five seconds.

Accelerate only single-node close-in framing, coordinating pan with zoom.
Couple restoration pan to zoom progress so the graph remains in view throughout
the return; matching only final coordinates is insufficient.

## Clocks, effects and package boundary

Use one shared renderer clock and equivalent WebGL/2D behavior. Anchor the
decorative pulse to projected galaxy cores or the selected node; it does not
mean a file was accessed. Freeze motion for reduced-motion preferences.
New-node glow fades over ten seconds from creation, independently of arrival;
node opacity, relationship and deletion effects retain 3.5-second deadlines.
Keep ghosts outside selection and read traversal.

Display version/SHA/FPS with footer clearance. FPS uses real frame timestamps
and bounded samples, not the capped simulation delta. Only a source checkout
may inspect its Git identity; deployed artifacts use stamped metadata or an
explicitly unavailable SHA, never the consumer repository's commit.

Cartograph remains self-contained, with no pinned Atlas package dependency.
Atlas stores are input data, not executable code. Do not conflate opening a
store with authorizing a collector or a workload.
