---
name: ui-consistency
description: Use to audit a frontglance page, flow, or component for UI inconsistencies and Design System gaps, or to design new UI from existing patterns.
---

# UI consistency and Design System alignment

Find where the product's UI patterns differ, decide which differences are intentional and which are accidental, and
recommend how to align the product and the Design System.

The goal is not to make everything identical. The goal is a consistent, predictable, reusable product language and a
Design System that accurately describes the patterns we intend to repeat.

**Core principle:** reuse before you create, and understand before you standardize. Keep differences that have a
reason, remove the ones that don't, and make the Design System describe the patterns we mean to repeat.

Applies to the `frontglance` repo (`/workspace/frontglance`). Paths below are relative to it.

## When to use

- Reviewing a page, area, flow, or component for consistency.
- Finding components or patterns across the product that are similar to a given one.
- Deciding whether multiple variations of a component are necessary.
- Deciding whether a pattern should be standardized or added to the Design System.
- Designing a new experience from existing product patterns (see "Designing something new").

This skill analyses and recommends. Adding or moving a Storybook story is **design-system-storybook**'s job; changing
code goes through the card's engineering step.

## Where patterns live

Search all of these. Each source answers a different question.

| Source | What it tells you |
| --- | --- |
| `src/frontend/vaila/` (`@vaila`, V-prefixed) | The canonical Design System components. `agents/vaila.md` lists the ones to prefer. |
| `src/frontend/components/shared/` | Generic components. Some belong in the Design System, and some are near-duplicates of Vaila. |
| Feature folders (`components/<Area>/...`, `dataexploration/`, `tasksmanagement/`, ...) | What the product actually ships, including local one-offs. |
| `agents/deprecated.md` | Deprecated components. Any usage of one is an inconsistency by definition. |
| Storybook (`src/stories/`, `npm run storybook` on port 6006) | How the Design System is documented. Gaps and drift show up here. |
| Figma library "Valence Platform" | The design source of truth that Storybook mirrors, when the user provides a link or export. |
| Theme tokens (`src/frontend/_themeColors.scss`, `_variables.scss`, `styles.ts`) | Colors, spacing, and typography. Hard-coded values that bypass them are inconsistencies. |

Do not stop at visually identical matches. Look for components with the same function, hierarchy, interaction, or UX
purpose. Grep for direct `antd` imports (`Modal`, `Drawer`, `Tooltip`, `Button`, `Table`, ...) next to their Vaila
equivalents, and for locally styled wrappers that re-implement a Vaila component.

## Analysis process

### 1. Find similar patterns

List every implementation that serves the same or a similar purpose, across the product and the Design System. Record
the file path and the screen or flow where each one appears.

### 2. Compare them

Compare the examples on:

- structure and layout
- spacing
- typography
- colors (tokens or hard-coded values)
- component variants and states (hover, focus, disabled, loading, empty, error)
- interaction patterns and behavior
- placement on the page
- content hierarchy
- responsive behavior, when relevant

Read the implementation, not only the rendered result. Two components can look the same and behave differently.

### 3. Identify inconsistencies

Look specifically for:

- several button styles that serve the same purpose
- components that are almost identical but differ slightly
- different spacing or typography for the same information hierarchy
- similar pages that use different layouts
- different modal, drawer, tooltip, filter, table, card, or navigation patterns for similar use cases
- components that exist in the product but not in the Design System
- Design System components that no longer match how the product actually uses them
- usage of anything listed in `agents/deprecated.md`, or a direct `antd` component where a Vaila one exists

### 4. Understand why they differ

Do not assume every difference is a problem. For each meaningful variation, look for a UX, product, technical, or
contextual reason. Check the surrounding feature, its data density, and the user's task, and use `git log` on the file
when the history explains the choice. Then classify the variation:

| Classification | Meaning |
| --- | --- |
| **Intentional variation** | There is a clear reason for the difference. It should remain. |
| **Potential inconsistency** | The difference serves no meaningful purpose and should be reviewed. |
| **Design System gap** | A useful pattern exists in the product but is missing or under-represented in the Design System. |
| **Duplicate pattern** | Several patterns solve essentially the same problem and could be consolidated. |

State the evidence behind each classification. When you cannot find a reason, say so instead of inventing one.

### 5. Recommend alignment

For each inconsistency, name the existing pattern that should become the standard. Prefer an established pattern,
usually the Vaila component or the most widely used implementation, over a new component or variant. Explain the
choice from actual product usage and UX behavior, with usage counts when they help.

If no existing pattern fits, recommend how the Design System should evolve.

## Screenshots

Include screenshots whenever possible. Capture Design System components from Storybook and product usage from a running
environment (a dev stage via **dev-stage**, driven with **agent-browser-core**). Put examples you compare side by side
at the same viewport size. Save them under the rules in **artifacts**. When no environment is available, say so and
cite file paths and line numbers instead.

## Expected output

Every analysis returns these sections:

1. **Summary**: what you analyzed and the main consistency issues.
2. **Existing patterns**: each example with a screenshot when possible, where it appears, what it is used for, and how
   it differs from the others.
3. **Inconsistencies**: the differences that look unnecessary or problematic.
4. **Intentional variations**: the differences that have a valid reason and should stay.
5. **Recommendation**: what to standardize, consolidate, update, or add to the Design System.
6. **Design System impact**: for each recommendation, one of the following:
   - reuse an existing component
   - update an existing component
   - add a variant
   - add a new component or pattern
   - deprecate or consolidate existing variations (and add them to `agents/deprecated.md`)

## Designing something new

When asked to create or suggest a new page, flow, or component, search the product and the Design System first.

1. Find the closest existing patterns. For example, if a new feature needs a modal, start from the existing modal
   patterns (`VModal`, `useErrorModal()`) and pick the one that fits the use case. Do not invent a new modal.
2. Reuse them wherever they fit, and say which pattern each part of the design is built from.
3. Introduce a new pattern only when the existing Design System cannot meet the UX requirement. Say what is missing, and
   treat the addition as a Design System change: frontglance requires a Design System task before any new design.
