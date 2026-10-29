---
name: ui-audit-rollup
description: Combine several UI screen audit cards into one master component inventory and one cross-screen list of issue kinds, classified with Lior's triage rules, and plan or create the fix, UX/UI and decision cards for them. Use when a card asks for a roll-up of UI screen audits.
---

# UI Audit Roll-up

You combine the results of several screen-audit cards into one master component inventory and one cross-screen list of issues, then turn that list into cards. This is the only place where cards are planned or created: screen audits only write reports. You never fix anything and you don't re-audit screens: you only read the audit cards' saved files.

## Read these first

The `ui-screen-audit` skill's reference files are the source of truth:
- `skills/ui-screen-audit/references/design-decisions.md`
- `skills/ui-screen-audit/references/triage-rules.md`
- `skills/ui-screen-audit/references/issue-kinds.md`
- `skills/ui-screen-audit/references/routing.md` (how issues become cards)

Write for a product designer, following the "Writing for a product designer" section of `skills/ui-screen-audit/SKILL.md`.

## Inputs

- The card lists the audit card numbers to combine. Only read artifacts of those cards. Use each card's newest report version.
- **Mode:** `report` (default: roll-up only), `propose` (roll-up plus a card plan for Lior to approve; creates nothing) or `create` (roll-up plus creating the cards). If the roll-up card ran in `propose` mode and Lior then approves the plan in its session, create exactly the approved cards.

## Steps

1. For each card: `list_artifacts(cardId)`, then read `component-inventory-*.json` and the newest `ui-audit-*.md` with `get_artifact_content`. If a card has no report, list it under Gaps and continue.
2. **Merge inventories:** one row per component, deduped by `import_path`. Union `screens` and `issues`, and keep the most specific tags and the clearest `ui_description`.
3. **Merge findings into issue kinds:** every finding goes under its kind ID from `issue-kinds.md`. A finding counts once per report, whether it was a full finding or an "Already reported" line. Re-check across screens: something unique on one screen may duplicate something on another.
4. **Classify:** use the kind's category. Findings marked "Proposed new kind" stay proposed; group similar ones and suggest one kind for them.
5. **Route** (only in `propose` or `create` mode): follow `routing.md` for every issue in the merged list. One card per issue, with every affected screen listed, never one card per screen. Before creating anything, check for open cards from earlier roll-ups on the same issue and update them instead.

## Outputs (save to `artifacts/`)

1. `component-inventory-master.csv` and `.json`: the screen-audit columns plus `screens` as a list and `screen_count`.
2. `ui-audit-rollup.md`:
   1. How to read this report (categories, severity, confidence, the Accessibility tag)
   2. Summary: screens covered, unique UI elements, Storybook coverage, count per category
   3. All issue kinds in one table: ID, kind, screens affected, highest severity, category, tag, decision status
   4. One section per category (Bug, Engineering only, Trivial decision, UX/UI process), each kind with its screens, a screenshot, and the fix or the question
   5. **Decisions needed:** pending Trivial decisions and proposed new kinds
   6. **Alignment backlog by element type:** for each type (status chips, buttons, filters, empty states…), the versions that exist, where they appear, how they differ, and the one to keep. Order by number of versions × screens affected
   7. Missing from Storybook, ordered by how many screens use the element
   8. Gaps: listed cards with missing or incomplete audits
   9. Code health (for developers)
3. `ui-audit-rollup.html`: self-contained HTML version with screenshots embedded. Regenerate it whenever the .md changes.
4. In `propose` or `create` mode: `routing-plan.md` (format in `routing.md`). In `propose` mode, stop after writing it and ask Lior to approve it in this card's session.

Update the progress headline with the summary, then complete the session as the track expects.
