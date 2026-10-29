# Routing findings to cards

Used only by the `ui-audit-rollup` skill, after it has merged all screen reports into one list of issues. Screen audits never use this file. The roll-up card's mode decides what happens:

- **`propose`**: don't create anything. Write `routing-plan.md` listing every card you would create or update, then stop and ask Lior to approve it.
- **`create`**: create and update the cards, then write `routing-plan.md` as a record of what you did.

## What happens per category

| Category | Action |
|---|---|
| Bug | Fix card (bundling allowed, see below) |
| Engineering only | Fix card (bundling allowed, see below) |
| Trivial decision, **Approved** kind | It breaks a rule, so treat it as a Bug |
| Trivial decision, **Pending** or **Per component** kind, or proposed new kind | Add to the decisions card. No fix card until Lior says yes |
| UX/UI process | One UX/UI card per issue |
| Won't fix, Not an issue | Nothing |

## Before creating any card

Search for an open card about the same issue kind (`list_cards` with a keyword from the kind, owner Lior). If one exists, add this screen and its evidence to it as a comment or in its card journal, instead of creating a new card. One card per issue, never one per screen.

## Fix cards (Bug, Engineering only)

- **Title:** `[UI fix] <what's wrong, in user terms>`
- **Track:** engineering. **Team** and **owner**: same as the roll-up card unless the roll-up card says otherwise.
- **Description:** each issue with its kind ID, every screen affected (with its audit card number), screenshot links (from the audit cards' artifacts), the expected result in design terms, and the developer notes. End with: "Before merging, attach before-and-after screenshots of every screen listed, for Lior's design review."

### Bundling small fixes

Combine up to **3** issues in one fix card only when ALL of these hold:
- They're clearly related: the same shared component (e.g. the table toolbar) or the same area of one screen (e.g. the side panel header).
- Each is a small, contained change: a tooltip, a color token, a label, a spacing value, a cursor.
- None of them changes layout or behavior, or touches a whole component (e.g. the widgets row). Those always get their own card.

Inside a bundle, list each issue separately with its own screenshot, so Lior can approve or reject each one on its own.

## UX/UI cards

- **Title:** `[UX/UI audit] <the design question>`
- **Track:** product. **Owner:** Lior.
- **Description:** the problem in user terms, every screen affected with screenshots, the options already known, and any rules from `design-decisions.md` that constrain the answer. Don't propose a final design.

## Decisions card

One card per roll-up run, collecting everything that needs Lior's yes/no:
- **Title:** `[UI decisions] roll-up <date>`
- **Track:** raw. **Owner:** Lior.
- **Description:** one item per decision: the question, the options, a screenshot, and which kind it belongs to (or "Proposed new kind" with its suggested category). Also list any proposed new kinds.
- **When Lior answers in that card's session:** for each approved decision, open a draft pull request in `valencesec/zenops-skills-lior-haruvi` that adds the rule to `skills/ui-screen-audit/references/design-decisions.md` and updates the kind's status in `skills/ui-screen-audit/references/issue-kinds.md`. Then create the fix card for it. For approved new kinds, add them to `issue-kinds.md` in the same pull request.

## routing-plan.md

A table with one row per card: action (create / update existing #N), card title, category, kind IDs, screens, and why bundled (if it is a bundle). Follow it with the list of findings that got no card and why (Won't fix, Not an issue, waiting for a decision).
