---
type: protostar
title: Keep Cartograph UX compact, truthful and accessible
created: 2026-09-10
status: open
kva: forming
growth: true
star_kind: refine
origin: derived
sensitivity: internal
description: Forming UX principles from user-led refinements, with a proposal for a focused project-local review skill.
relates_to:
  - path: decisions/readable-external-source-links.md
    kind: derived_from
  - path: decisions/cartograph-v030-interaction-contract.md
    kind: derived_from
sources:
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/blob/f0e713136774e8d56a8993acbc5017e100124872/.apm/extensions/cartograph/public/styles.css
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/commit/aa6b2ed50e1d4879f920ed7dda57abec0efbd926
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/commit/ac9608710e9f23a3e8b30518168270dbc0143f90
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/commit/ecffaae63607de0c84e722805cce0016fa0695b1
  - https://github.com/sergio-sisternes-epam/atlas-cartograph/commit/88cb4f39bf64ac5e6b7bf1ab7227912ccda36d7a
---

# Compact, truthful and accessible UX

## Pending

Use these patterns to guide the next UX change and evaluate a small
project-local review skill before promoting the synthesis to an accepted
standard. The individual implemented interactions are evidence; the broader
principles and skill proposal remain forming.

## Origin

The user-led chat, navigation and activation-menu refinements culminated in a
request to make information buttons smaller and preserve the design approach.
This extends the existing [source-link decision](readable-external-source-links.md)
and [interaction contract](cartograph-v030-interaction-contract.md), rather than
replacing their behavioral boundaries.

Evidence is from this development branch, not a claim of published release
content. The linked commits were inspected locally; remote availability was
not established.

## Observed project patterns

| Principle | Apply it in Cartograph |
| --- | --- |
| Content first | Keep the graph central, search always visible and full-width between its two controls. Group activation, View and zoom in the floating status bar instead of scattering controls and hints. |
| Brief copy, reachable explanation | Use short action labels and one useful status line. Put longer explanations behind a labelled, keyboard-accessible information button, not a hover-only tooltip. |
| Do not hide consequences | Keep operational errors, permissions, private-token warnings and meaningful counters visible. Brevity must not conceal risk or what the user must do next. |
| One action, one recognizable control | Retain the single persistent chat toggle in both states. Use consistent SVG close, expand and collapse symbols, shared disclosure chevrons and aligned two-line summaries. |
| Panels have stable roles | Options opens from the left with Atlas branding; chat lives on the right and can fill the canvas. Chat and Markdown preview can coexist. Bound and scroll overlays instead of overflowing the viewport. |
| Motion explains state | Opening and closing use symmetric slide transitions. Honor reduced motion without losing access to controls or changing a saved preference. |
| Readability beats compression | Preserve full Atlas/schema identities and descriptive source labels. Shorten explanations, not identifiers needed to distinguish destinations. Small text still needs readable contrast. |
| Preserve user intent | Keep drafts, caret, focus, selection and filters through background updates. Use explicit Save/Cancel for unsaved settings; failed saves must not erase the draft. |
| Status must be truthful | Separate collector health from highlighting, display pace from collection latency, and decorative motion from file reads. Async progress belongs to its own request; do not simulate completion. |
| Reuse safe interaction paths | Prefer shared controllers and native controls. Render help as literal text, preserve focus on dismissal, and clean up observers. No remote assets, automatic collectors or implicit privilege escalation. |

## Current visual reference

These values describe the current interface, not universal design tokens.
Read the canonical runtime styles before changing them.

- Information buttons: 24px target and 12px glyph, reduced from 28px and 14px.
  Keep visible focus and a usable target when reducing visual weight; primary
  actions and touch-heavy layouts may need larger targets.
- Top-section SVGs: 80% opacity. Use local assets and a consistent visual weight.
- Options header: Atlas in large white type, Cartograph in smaller silver type,
  on the same line.
- Options and chat: symmetric 180ms sliding transitions; no transition under
  reduced motion.
- Source rows: descriptive 12px labels/context, 11px full URLs and generous
  whole-row targets. Do not trade away meaning to make labels shorter.

## Review practice

Start from the user's task, not a generic aesthetic checklist. Inspect existing
components and states before proposing another control or interaction pattern.
For review-only requests, report the findings before changing behavior.

Exercise the changed surface in a real browser at wide and narrow widths, with
chat open and closed as relevant. Include keyboard access, focus restoration,
outside dismissal, reduced motion and scrolling. Settings work also needs
pending drafts, delayed snapshots and failed saves. CSS assertions and synthetic
DOM tests cannot establish those visible outcomes alone.

Report reproducible problems by user impact, with the smallest coherent remedy.
Avoid sweeping visual redesigns, duplicate controllers and speculative polish.

At capture, the smaller button measured 24 by 24 CSS pixels with a 12px glyph
at desktop and 600px viewport widths. Its popup opened and Escape restored
focus; the narrow page had no horizontal overflow. The targeted information
popup and frontend interaction run passed 60 tests. This is evidence for this
change, not a claim of a complete accessibility audit.

## UX skill assessment

A focused **project-local UX review skill is justified** by the repeated
menu, panel, copy and state-preservation reviews. It is not needed to execute
every spacing or label adjustment, and a generic UX skill would be too broad.
No skill is created by this capture.

Proposed scope: `cartograph-ux-review`, invoked for UI reviews and substantial
interaction changes. It should discover the current contracts, map the affected
states, inspect the real browser behavior and return prioritized findings with
evidence and a bounded acceptance checklist. It must preserve the distinction
between reviewing and implementing.

Keep the review procedure in the skill; reference this Atlas guidance and
repository contracts rather than copying design values or runtime code into it.
Pilot it on two independent future UX changes. Promote it only if it catches
actionable consistency or usability defects without irrelevant checklist noise.
A shared cross-project skill would require evidence from another product, not
just repetition within Cartograph.

## Related

- [Readable external sources](readable-external-source-links.md) establishes
  meaningful labels, safe destinations and accessible source rows.
- [Interaction contract](cartograph-v030-interaction-contract.md) establishes
  visible search, bounded motion and honest activity semantics.
