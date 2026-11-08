---
name: working-with-lior-haruvi
description: How I want agents to work on my cards. Load at session start, at every stage (intake, triage, planning, engineering, QA, code review, review), and before showing or describing a UI change, opening a PR, or reporting a finding.
---

# Working with me (Lior Haruvi)

I'm a product designer (GitHub `liorharuvi-valence`). My cards are UI and design-system work in frontglance, plus UI audits. I judge by looking, not by reading a diff.

These rules are injected into every session. If you cannot see them in your context, load this skill again (compaction and `/clear` drop it). Quotes and card/PR citations for every rule are in [references/evidence-log.md](references/evidence-log.md); do not load it to work. Mined through 2026-11-08.

## Rules

### Show me
1. Before I approve a design change, show a screenshot of the current state and of the change. Never ask me to approve a description.
2. Capture "before" first, then "after". I look on the desktop preview (`start-desktop`), Storybook, or dev/T1; offer the one that fits.
3. Screenshots and mocks live in Artifacts and are linked from the PR. If I say I can't see it, it isn't where I look.
4. Keep Artifacts to this task: after every revision re-save, check it updated, and delete screenshots that no longer apply. Keep before and after only.
5. Put before and after screenshots in the PR description. If the design changes after QA, retake "after" and rewrite the PR description to the final design.
6. A mock is the real component rendered (Storybook story or desktop preview), never hand-drawn HTML/CSS, with the real data from my screenshot. Change only what I asked.
7. Storybook: build the preview and tell me where to open it; update the story in the same PR. "Where can I see it?" is answered with a screenshot or a link.
8. When I ask how something used to look, show every state: expanded, collapsed, narrow.

### Match Figma and the product
9. Copy the existing platform pattern, or reuse the existing component or layout I name. Never build a new component, style or spacing value; if none fits, say so first and it becomes its own stacked card.
10. Use existing tokens, never hard-coded colors or eyeballed spacing; if no token matches, flag it instead of adding one.
11. Text weight, color, spacing and icon behaviour match Figma, including hover and states. When code and Figma disagree, give me the exact values (padding, radius).
12. What I upload to Artifacts or link from Figma is the spec. Read it first.
13. Button, tag and headline text starts every word with a capital: "More Actions".
14. Check a claim about the screen (e.g. a button exists) against the screen before stating it.

### Scope
15. Do only what the card says. Don't touch other screens, shared styles or design-system components; list what would need a shared change in the PR description as "Shared drawer styles, handled separately".
16. When I change styling or layout, confirm no content changed: list every screen that uses the changed component and compare before and after (fields, labels, values, tabs, counts).
17. A separate task goes on its own card and must not block a PR in progress. Don't create extra cards or steps when I ask only for a PR.
18. Avoid dead code: stack on the open PR it depends on, as its own draft PR. Before pushing a stacked PR, check whether the base PR already covers or conflicts with it, and tell me.
19. If I ask you to investigate, summarize or compare, change nothing until I decide. Push only when I say.
20. When I relay a reviewer's comment, say whether you agree and why before changing anything.
21. Before a batch action across cards, list the cards first (only mine) and wait for my pick.

### Status and hand-off
22. I decide when a card is done, ready for review, or merged. Never mark it yourself; when I ask "is this done / ready?", answer yes or no first, then what is left.
23. When I say stop or cancel, stop; no further work.
24. PR hand-off, in order: (a) tell me which scrum team last worked on the area; (b) use the VAL I give, or open it with that team ("you can always open"); (c) run `/code-review low --fix` on the diff; (d) push, open the PR, assign it and request review from the reviewer I name; (e) give me the PR link and attach it to the card (say so if it is a bug); (f) mark ready for review only when I say so; (g) tell me whether CI is green and give me a short Slack message for the reviewer.
25. I approve each plan myself; an earlier approval is never standing.
26. A card showing "needs input": read its open items and answer in two sentences (which item, who it is assigned to, what clears it). Don't start work.

### Audits
27. Write findings in UI/UX terms, not code terms. Each finding is its own heading with a screenshot link and a working "Details: see finding #N" link; severity in words. Offer an HTML version.
28. Measure, don't describe: write the measured values (size, colors) in the finding.
29. Don't flag intentional variation (toolbars per page, different control types, behaviour I call by design). If unsure, ask me with screenshots.
30. Apply my answers exactly (reclassify, remove, "No longer reproduces"), regenerate the report, and end with whether it is done and which decisions are still open. Findings already on other screens go in one "Already reported on other screens" section.

### Judgment
31. On "ultrathink", or when I ask whether an organization, naming or CTA-placement choice follows industry standards (Material, Apple, Atlassian), compare against those systems and the product and say what you are unsure about.

## Precedence
These rules override default habits and the style of pipeline skills (e.g. what step-engineering or step-qa say about screenshots, scope or hand-offs). They never override approval gates, `human-gate`, `state-management` transitions, the `git` skill, or journaling. A waiver counts only when I say it on the card or in a message. If two rules collide, ask me one short question instead of picking silently. Known collision: the design-doc process on card 6550 ("I approve and merge this myself, don't request Tomer") beats rule 24(d) only for that card.

## Situational
| Load | When |
|---|---|
| [references/stage-checklists.md](references/stage-checklists.md) | At every pipeline step change; re-read the matching block and tick it in the hand-back |
| [references/evidence-log.md](references/evidence-log.md) | To check where a rule came from, or before arguing with one |
| `design-system-storybook` skill | Adding or moving anything in Storybook |
| `ui-consistency` skill | Auditing a page or flow for inconsistencies |
| `ui-screen-audit`, `ui-audit-rollup`, `ui-audit-status` skills | Audit cards |

## Open questions
Unresolved contradictions are listed in the PR that last updated this skill.

## Maintaining this file
Keep this file under ~120 lines and ~16 KB: numbered one-line rules only. Put quotes and citations in `references/evidence-log.md`, depth in `references/`, and link every reference file from the table above. A new or strengthened rule gets one line here; evidence goes in the log.
