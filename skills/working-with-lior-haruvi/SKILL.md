---
name: working-with-lior-haruvi
description: How I want agents to work on my cards. Load at session start, at every stage (intake, triage, planning, engineering, QA, code review, review), and before showing or describing a UI change, opening a PR, or reporting a finding.
---

# Working with me (Lior Haruvi)

I'm a product designer. My GitHub handle is `liorharuvi-valence`. My cards are UI and design-system work in frontglance. I judge by looking, not by reading a diff.

Every rule below is cited in [references/evidence.md](references/evidence.md) with card/PR and my own words. Mined 2026-10-01 → 2026-10-18.

| Load | When |
|---|---|
| [references/evidence.md](references/evidence.md) | To check where a rule came from, or before arguing with one |
| `design-system-storybook` skill | Adding or moving anything in Storybook |
| `ui-consistency` skill | Auditing a page or flow for inconsistencies |

## Load this skill yourself
I should never have to ask. Load it at the start of every card I own, not only when I type its name.

## Show me, don't tell me
- Before I approve a design change, show a screenshot of the current state and of the change. Never ask me to approve a description.
- Put screenshots and mocks in Artifacts, and link them from the PR. If I say I can't see it, it isn't saved where I look.
- For Storybook work, build the preview and tell me where to open it. When a component changes, update its Storybook story in the same PR.
- Put before and after screenshots in the PR description, not only in Artifacts. If the design changes after QA, retake the "after" screenshot and rewrite the PR description so it describes the final design.
- When I ask "where can I see the change?", the answer is a screenshot or a link, not an explanation.
- A mock is the real component rendered (Storybook story or the desktop preview), never hand-drawn HTML/CSS. Use the real data from the screenshot I attach. Change only what I asked for; every other pixel stays the current design.
- Capture the "before" screenshot first, then the "after". I look at it on the desktop preview (`start-desktop`), Storybook, or dev/T1 — offer the one that fits.
- After every revision, re-save the mock to Artifacts and check it actually updated before telling me it did.
- When I ask how something used to look (e.g. the nav with the beta tag), show every state: expanded, collapsed, narrow.

## Match Figma and what the product already does
- Copy the existing platform pattern (e.g. the Security Checks bulk change-severity dropdown) rather than inventing one.
- Use only icons and components that exist in the design system. If you need one that doesn't, say so first; it becomes its own card, stacked under the work that uses it.
- Text weight, color, spacing and icon behaviour must match Figma. Check hover and states, not just the default.
- When the code and Figma disagree, give me the exact values (padding, radius) so I can update Figma.
- What I upload to Artifacts or link from Figma is the spec. Read it before designing, and use the same icon or component the existing screen already uses.
- Button, tag and headline text starts every word with a capital: "More Actions".
- Check a claim about the screen (e.g. that a button exists) against the screen before stating it.

## When I ask why a card is "needs input"
Look at the card's open items and answer in two sentences: which gate or item is open, who it is assigned to, and what clears it. Don't start work.

## Audits: report what a user sees
- Write findings in UI/UX terms, not code terms.
- I accept differences that follow a consistent structure, spacing and pattern. Don't flag intentional variation (e.g. toolbars that differ per page) as an inconsistency. If unsure, ask me and show screenshots.
- Check a claim against the real screen before putting it in the report. I will ask for the screenshot.
- Different kinds of controls (e.g. disabled vs. enabled buttons, a gear vs. table buttons) differ on purpose; don't compare them.
- Each finding is its own heading, with a screenshot link and a working "Details: see finding #N" link from every summary line. Severity is written as words. I check the links.
- Findings already reported on another screen go in one "Already reported on other screens" section. Offer an HTML version of the final report.

## Keep work separate
- A separate task (e.g. a new Storybook component) goes on its own card and must not block a PR that is in progress.
- Avoid dead code: if a change is only used by another open PR, stack on it or add it to that PR.
- Do not create extra cards or steps when I ask only for a PR.
- Before pushing a stacked PR, check whether the base PR already covers it or conflicts with it, and tell me.
- If a PR depends on another open PR, open it as its own draft PR stacked on that branch rather than waiting or folding it into the base PR.
- Before a batch action across cards (closing, withdrawing items), list the cards first, only mine, and wait for my pick before changing anything.
- When I relay a reviewer's comment, tell me whether you agree and why before changing anything. Implement once I say so.

## PR handoff (every card, in roughly this order)
1. Tell me which scrum team last worked on the area.
2. I give the VAL ticket; use it. Open the VAL yourself, with the scrum team you found in step 1; I said "you can always open".
3. Run `/code-review low --fix` on the card's diff.
4. Push, open the PR, assign it and request review from the reviewer I name (recently Tomer, Guy, Shlomi).
5. Attach the PR to the card. If the card is a bug, say so in the PR description.
6. Mark ready for review only when I say so.
7. Tell me whether CI is green, and give me a short Slack message for the reviewer.

## Plans
I approve each plan myself. Do not treat an earlier approval as standing; wait for it every time.

## Think hard on design judgment
When I write "ultrathink", or ask whether an organization, naming or CTA-placement choice follows industry standards (Material, Apple, Atlassian), compare against those systems and the product, and say what you are unsure about.

## Open questions
See the PR that last updated this skill; unresolved contradictions are listed there.
