---
name: ui-screen-audit
description: Audit one screen of the Valence platform for UI consistency, classify every finding with Lior's triage rules, and (when the card asks) route findings to fix cards, UX/UI cards and a decisions card. Use when a card asks for a UI screen audit.
---

# UI Screen Audit

You audit ONE screen of the Valence Security platform for design-system consistency. You never fix anything yourself. You produce evidence, a tagged component inventory, and a classified list of findings that Lior (product designer, owner of the design system) uses to decide what to align. Her calls are final.

**First, add the label "screen audit" to this card.** If you have no way to add labels, say so once in the progress headline and continue.

## Read these first (every run)

- `references/design-decisions.md`: rules Lior has already approved. Never flag what they allow; anything that breaks them is a Bug.
- `references/triage-rules.md`: how to give every finding a category and tag.
- `references/issue-kinds.md`: the catalog of known issue kinds. Match each finding to a kind and reuse its ID and category.
- `references/routing.md`: what happens to each category after the report. Only used when the card's mode is `propose` or `create`.

## Inputs (from the card description)

- **Screen**: name + URL. If the URL is missing, stop and ask; don't guess.
- **Previous audits**: card numbers of earlier screen audits. Read their latest report and inventory.
- **Mode**: `report` (default), `propose` or `create`. See `references/routing.md`.
- **Environment / login**: use what the card says, otherwise the shared T1 admin test user. If login fails, stop and open a pick-up action item; don't audit from code alone.

## Rules

- Read-only. Never push code, open PRs to the product repo, or change Storybook.
- Every finding needs evidence a person can open: a screenshot that clearly shows the problem, a measured value, or a file path + line. If a screenshot doesn't clearly show it, drop the finding.
- Only flag differences in HOW something looks or behaves, never in WHAT a screen contains (different columns, menu items, widgets or copy per screen are not findings).
- Different variants are not inconsistencies (primary vs secondary vs tertiary, filled vs outlined, compact vs full, danger vs normal). Group by role: compare page links with page links and content actions with content actions. If you can't tell the variant, ask instead of flagging.
- Never invent a new component when an existing one could take a variant or prop.

## Run the whole audit

Complete every step below before writing the report. Never end with a partial run. If something blocks a step (login, a state you can't reach, an action that would change data), finish everything else and list exactly what was blocked and why under "what wasn't checked".

## Process

1. **Map the screen.** Find the route/page component and walk its render tree to leaf UI elements. Record each component: name, import path, screen region. Include ad-hoc UI (styled divs, inline styles, overrides that recreate a library component). Open the screen with Playwright; screenshot the full page and each region at 1280px and 1440px; capture default, loading, empty, filtered-to-zero, long content, and open modals/drawers/menus.
2. **Storybook coverage.** For each component: `in-storybook`, `variant-missing`, `missing-story`, or `local-one-off`.
3. **Duplicates.** Two or more components doing the same job with different implementations. Name the one to keep (in Storybook, most used, or most complete) and count usages.
4. **UI bugs.** Tokens (hard-coded values), alignment and spacing, typography, states, overflow and truncation, contrast, console errors. Skip anything `design-decisions.md` says not to flag.
5. **Classify.** For each finding: match it to a kind in `issue-kinds.md`. If it matches, use that kind's ID and category, and treat breaks of approved rules as Bug. If nothing matches, classify it with `triage-rules.md` and mark it **"Proposed new kind"**; never add it to the catalog yourself.
6. **Group** (from `triage-rules.md`): one issue per shared component with the affected screens listed; merge symptoms into their cause; split "align now" from "redesign later".
   One finding = one kind. If an observation touches two kinds (e.g. a T02 gray and a T03 per-component color), split it into two findings.
7. **Previous audits.** A finding that repeats an earlier audit's issue (same kind, same shared component or same screen) goes in "Already reported on other screens", one line each with a screenshot from this screen and "Also on: <screen> (card N, finding #N)". A repeat stays a repeat even if its category has changed since (e.g. an approved Trivial decision that is now a Bug). Keep the earlier severity; breaking a rule doesn't raise severity. Add a "Worse here" line only when this screen differs.
8. **Route** only if mode is `propose` or `create`: follow `references/routing.md`.

## Writing for a product designer

- Lead with what a person sees on screen, named the way a designer would. Component names, paths and counts go only in a short "Developer notes" line.
- No unexplained codes or jargon. Give each finding a short descriptive title; #1, #2 are fine for cross-references.
- Every finding has four labelled lines: **What you see** (with screenshot links), **Why it matters**, **Recommendation**, **Developer notes**.
- Each finding is a heading (`#### #1 Title`) and every cross-reference is a clickable link with words, never a bare "(#1)".
- Each finding states: **Category**, **Kind** (ID or "Proposed new kind"), **Severity** (Must fix / Should fix / Consider), **Confidence**, and the **Accessibility** tag when it applies.

## Outputs (save to `artifacts/`)

1. `ui-audit-<screen-slug>.md`, in this order:
   1. How to read this report (categories, severity, confidence; 5 lines max)
   2. Summary (5 lines max): elements checked, Storybook coverage, things built more than once, count per category, the single most useful change
   3. Top 5 changes (fixes only), then **Decisions needed** (Trivial decisions not yet approved and proposed new kinds, one line each with a link)
   4. Already reported on other screens
   5. Findings grouped by category: Bug, Engineering only, Trivial decision, UX/UI process
   6. Missing from Storybook
   7. Questions for the designer, and what wasn't checked
   8. Code health (for developers): code-only issues nobody can see
2. `component-inventory-<screen-slug>.csv` and `.json`: `name, ui_description, import_path, type, storybook, consistency, duplicate_group, keep, usages_in_repo, screen, issues, notes`. Keep these exact columns for the roll-up.
3. `screens/`: every screenshot referenced.
4. `ui-audit-<screen-slug>.html`: self-contained HTML of the report with screenshots embedded and links working. Regenerate it whenever the .md changes.
5. In `propose` or `create` mode: `routing-plan.md` (see `references/routing.md`).

Update the progress headline with the summary line, then complete the session as the card's track expects.

## Quality bar

- Every component on the screen appears exactly once in the inventory.
- Every finding has a category and a kind, and every Must fix has evidence someone can open.
- Counts in the summary match the sections.
- A designer understands every finding without reading code.
