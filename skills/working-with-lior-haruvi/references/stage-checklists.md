# Stage checklists

Re-read the block for the step you are entering. Tick each item in the hand-back (rule numbers refer to `SKILL.md`).

## Intake
- [ ] Load `working-with-lior-haruvi` yourself (don't wait to be told).
- [ ] If the card names a WIP branch or PR, check what is on it and what is left before changing anything (19).
- [ ] If I asked a question about card state ("needs input", "is this done"), answer it and don't start work (22, 26).

## Triage
- [ ] Say which scrum team last worked on the area (24a).
- [ ] Use the VAL I give; if none, open it with that team (24b).
- [ ] A separate task or missing component becomes its own card (9, 17).

## Planning
- [ ] I approve each plan myself; wait every time (25).
- [ ] Scope is limited to the card; shared styles and other screens are listed as separate (15).
- [ ] Name the existing component, layout and tokens you will reuse (9, 10).

## Engineering
- [ ] Reuse existing components and tokens; build nothing new (9, 10).
- [ ] Only the card's scope changes; confirm no content changed on any screen using the changed component (15, 16).
- [ ] Storybook story updated in the same PR (7).
- [ ] Stacked PR: base PR checked for overlap (18).

## Code review
- [ ] `/code-review low --fix` on the card's diff (24c).
- [ ] No dead code left behind (18).

## QA
- [ ] Before screenshot first, then after, on desktop preview, Storybook or dev/T1 (2).
- [ ] Artifacts hold only this task's before/after, refreshed after each revision (3, 4).
- [ ] Every claim about the screen checked against the screen (14).

## Review / PR hand-off
- [ ] Before and after screenshots in the PR description, matching the final design (5).
- [ ] PR assigned, review requested from the reviewer I name (24d).
- [ ] PR link given to me and attached to the card (24e).
- [ ] CI status and a short Slack message for the reviewer (24g).
- [ ] Not marked ready for review, done or merged until I say so (22, 24f).

## Audit cards
- [ ] Findings in UI/UX terms, one heading each, working links, severity in words (27).
- [ ] Measured values in findings; intentional variation not flagged (28, 29).
- [ ] My answers applied, report regenerated (.md and HTML), end with what is done and what is open (30).
