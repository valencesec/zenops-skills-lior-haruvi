# Evidence

Quotes are verbatim, typed by me (human-classified turns only). Card numbers refer to ZenOps cards.

## Show me, don't tell me
- 5196: "Show me what you mean by the drawer tab component. I need to see it before I approve." / "show me a creenshot of them (preior to the change)"
- 4641 (repeatedly): "show me screenshot and explain", "show me the toolbar for the tickets page too", "show me the Full-page crash screen", "I don't see a severity badge in screenshots Data Shares (023, 024) and Security Checks (025)"
- 4720: "show me screenshot of the change"
- 4909: "where can I see the change?"
- 4918: "show me this on storybook", "build the preview now"
- 5201: "add a screenshot to Artifacts with the current design and one with the design change."
- 5200: "add a mock screenshot to the artifacts."
- 5199: "I can't see it in the artifacts" / "add a link from the artifacts to the PR" / "create a mock of the new component replacing what is currntly used"
- 4562: "show me the screen using the Success 2 and the the auth error screen"

## Match Figma / platform
- 4918: "it should be aligned to what we have in the platform, you can see it in SC bulk change severity"; "You used Icons we don't have in the design system"; "The icons should always keep their color and not be as the text"; "on hover the icon color changes. it shouldn't"
- 4909: "To match the design we are using in security checks for bulk change severity"
- 5199: "we also need to make sure the Vnotice text weghit and color are aligned with the design on Figma"

## Audits
- 4641: "I think it's fine for toolbars to differ between pages as long as they follow a consistent structure, spacing, and UI patterns." and again: "we already discussed 3. Page Layout Patterns - it's fine for toolbars to differ"
- 4641: "Go over the report and make it more focused on UI and user experience rather than on technical or code-level details"
- 4641: "I don't think 'youve reached the end of results' count as an error."
- 4641: "Do you still think we have a misalignment there? If so, show me screenshots"

## Keep work separate
- 4909: "I want the storybook task to be seperated and that it won't interfear or block current PR that is work in progress."
- 5201: "new plan, unstuck this and wait for #6516 before creating a PR"
- 5200: "go with the stacked PR"; "can we add this task to the #6516 PR, so this be handled together and avoid a dead code situation?"
- 4562: "Don't create another card, and don't create additional steps. Just create a pull request"

## PR handoff
- Scrum team: 5203 "what scrum team has the responsability on this?"; 5196 "which team last worked on these components?"; 5200 "Which scrum team last worked on this SC screen?"; 5201 "What scrum team last worked on this?"
- VAL ticket pasted after that: 5203 VAL-16404, 5196 VAL-16389, 5199 VAL-16394, 5200 VAL-16407, 5201 VAL-16411, 4918 VAL-16299 / VAL-16378
- Code review: `/code-review low --fix …` on 5203, 5196, 5199, 5200; `medium` on 4918
- Assign/request: 5196 "ASSIGN to Tomer"; 5199 "request review from Tomer"; 5203 "card owner tomer"; 4918 "assign the PR to Tomer from Shukron"
- 5199: "mark the PR ready for review" (he asked for this explicitly; also "leave it" when told to stop)

## Think hard
- "ultrathink" appears on 4562 (3×), 4641 (2×), 4918. 4562: "make sure the order I created is the most efficiant and follows industry standards such as material deaign, apple, attlasian and more"

## Single-instance, not promoted to rules
- 5196 (PR #6514): reviewer comment I relayed — "Isn't it better to create 2 dedicated components on top of this component, that will have this message and won't get a message as a parameter?" (only once; maybe a component-design preference)
- 4562/4937: "I think we need to save this as a skill" and push it to my skills repo (done twice, produced the two existing skills)
