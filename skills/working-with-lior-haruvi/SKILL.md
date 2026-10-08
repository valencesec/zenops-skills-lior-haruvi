---
name: working-with-lior-haruvi
description: How I want agents to work on my cards. Load at session start, at every stage (intake, triage, planning, engineering, QA, code review, review), and before showing or describing a UI change, opening a PR, or reporting a finding.
---

# Working with me (Lior Haruvi)

I'm a product designer. My cards are UI and design-system work in frontglance. I judge by looking, not by reading a diff.

Every rule below is cited in [references/evidence.md](references/evidence.md) with card/PR and my own words. Mined 2026-10-01 → 2026-10-08, 12 cards.

| Load | When |
|---|---|
| [references/evidence.md](references/evidence.md) | To check where a rule came from, or before arguing with one |
| `design-system-storybook` skill | Adding or moving anything in Storybook |
| `ui-consistency` skill | Auditing a page or flow for inconsistencies |

## Show me, don't tell me
- Before I approve a design change, show a screenshot of the current state and of the change. Never ask me to approve a description.
- Put screenshots and mocks in Artifacts, and link them from the PR. If I say I can't see it, it isn't saved where I look.
- For Storybook work, build the preview and tell me where to open it.
- When I ask "where can I see the change?", the answer is a screenshot or a link, not an explanation.

## Match Figma and what the product already does
- Copy the existing platform pattern (e.g. the Security Checks bulk change-severity dropdown) rather than inventing one.
- Use only icons and components that exist in the design system. If you need one that doesn't, say so first.
- Text weight, color, spacing and icon behaviour must match Figma. Check hover and states, not just the default.

## Audits: report what a user sees
- Write findings in UI/UX terms, not code terms.
- I accept differences that follow a consistent structure, spacing and pattern. Don't flag intentional variation (e.g. toolbars that differ per page) as an inconsistency. If unsure, ask me and show screenshots.
- Check a claim against the real screen before putting it in the report. I will ask for the screenshot.

## Keep work separate
- A separate task (e.g. a new Storybook component) goes on its own card and must not block a PR that is in progress.
- Avoid dead code: if a change is only used by another open PR, stack on it or add it to that PR.
- Do not create extra cards or steps when I ask only for a PR.

## PR handoff (every card, in roughly this order)
1. Tell me which scrum team last worked on the area.
2. I give the VAL ticket; use it.
3. Run `/code-review low --fix` on the card's diff.
4. Push, open the PR, assign it and request review from the reviewer I name (recently Tomer).
5. Mark ready for review only when I say so.

## Think hard on design judgment
When I write "ultrathink", or ask whether an organization or naming choice follows industry standards (Material, Apple, Atlassian), compare against those systems and the product, and say what you are unsure about.

## Open questions
See the PR that last updated this skill; unresolved contradictions are listed there.
