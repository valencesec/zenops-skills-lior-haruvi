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

## Added 2026-10-11 (full inventory with turn numbers is in the PR's evidence artifact)
- PR description matches final design: 5247 "the PR still says \"Adds a layout=\"page\" option to VNotice…8px padding, a 12px gap and a 4px radius\"" after "yes, change it to 12/20, and no corner radius"
- Screenshots in the PR: 5252 "you need to add screnshots before and after to the PR (in artifacts)" / "attach them to the PR description"; 5247 "update the PR with the new screenshot"; 5202 "add a link in the PR"
- Storybook with every change: 5199 "update storybook as well"; 5247 "make sure the storybook updates accordingly"
- Give me Figma numbers: 5247 "Give them to me and i'll update Figma"
- Reviewer comments, assess first: 4918 "I recieved 5 comments from Guy. Review them…" then "yes, go ahead and implement them"; 5196 "does this makes sence?"
- Draft PR instead of waiting: 5252 "why not create a draft PR for now?" / "stack it on 6516's branch"; 5202 "open the PR anyway as a draft"; 5200 "can you open a draft PR foe this and assign to Tomer?"
- Separate card: 4918 "let's leave the tasks page to a different task. Leave the PR untuched" / "Create a new card for me to work on the Tasks page bulk"
- New VALs and Tomer: 5247 VAL-16415, 5202 VAL-16412; 5202 "assign to Tomer"
- Confirmed 2026-10-12: "1. Draft PR" (separate stacked draft PR, not folded into the base PR, for the 5200 case)
- Confirmed 2026-10-12: GitHub handle is "liorharuvi-valence"; plan approval is not standing ("3. No")

## Added 2026-10-18 (window 2026-10-11 → 2026-10-18; full inventory in the PR's evidence artifact)
- Load it yourself: 5371 "Are you using knowmebetter?" / "load working-with-lior-haruvi and redo it"; 5245 "use /working-with-lior-haruvi"; 5327 "I want this skill to load on every card i'm working on, and keep updating"
- Mocks are the real design: 5245 "you need to only use components we use in the product. Outline bulk button" / "I want to see an accurate mock" / "keep it as is and change nothing"; 5371 "Make sure you use proper elemnts from the design system and DONT create any new one"; 5414 "this looks bad. It should follow all other similar inventory widgets"; 5668 "This looks bad. Only use the curent design, don't change anything. just the location of the icon" / "use real checks data from the screenshot I added"
- Desktop preview / dev / T1: 5245 "show me a desktop preview", "begin QA — when it runs start-desktop viewer"; 5414 "fix it and show me on desktop preview"; 5395 "i want to see that it looks ok on T1"; 5537 "start-desktop", "use dev 6, I need screenshots"; 4918 "Start desktop preview"
- Before first: 5537 "capture the before screenshots first"
- The upload is the spec: 5245 "I added to artifacts the required design for this" / "Colors should be as my design" / "in SaaS Apps the icon for santion is \"completed_workflows_menu_item.svg\" that's what I'm using"; 5371 "You can see the settings screen on figma and artifacts"
- Capitalisation (one card, stated as "always"): 5537 "It should say \"More Actions\" - allways on Buttons, Tags and headlines the first letter should be upper case"
- Verify claims: 5245 "are you sure there's an \"actions\" button in this screen?"
- Intentional differences: 5475 "Remove finding #3 (disabled buttons) from ui-audit-security-checks-v3.md: they're different button types, so the difference is intentional."; pasted instruction "Remove the border comparison between the gear and the table buttons: they're different kinds of buttons."
- Audit report format: 5475 "Make each finding a heading, add a screenshot link and a clickable \"Details: see finding #N\" link to every Top 5 item and summary point, and write severity as words." / "The links are still broken"; 5654 "Move every finding marked \"Also on\" or \"Similar to\" Security Checks into one section, \"Already reported on other screens\"" / "Generate the HTML version of v2 like card 5475 had"
- Base PR may already cover it: 5200 "WAIT, THIS TASK IS INSIDE 6516, SO WE DON'T NEED A SEPERATE pr FOR IT, NO?"; 5202 "this has conflicts, do we need this PR? or is it covered?"; 5247 "this overlaps with #6516 so there's a conflicts, do we need this PR? or is it covered?"
- Open a VAL for me: 5414 "Open a val ticket, assign it to the scrum team responsible for this / last worked on it"; 5395 "open a val" / "create a val ticket with Remy in the scrum tem"
- Reviewers: 5377 "open a PR on Guy"; 5429 "REVIEWR Shlomi , scrum teal CTO"; 5395 "put this on remy"
- Attach and bug: 5414 "point in the PR that this is a bug" / "attach the PR to the card"; 5429 "mark them ready for review, pin the link to this card"
- CI status: 5202 "is CI green yet?"; 5245 "what does CI failling means?"; 5247 "CI is failing, fix please"; 5414 "fix failling CI"
- Slack message for the reviewer: 4918 "what shpuld I tell Tomer? it's fixed?"; 5202 "what should I say to tomer?"; 5247 "Let me know what to write to tomer on slack as a short message"
- Stacked order: 5378 "the PR should be draft stucked on …/pull/6551 … When #5377 merges, retarget this one to the main branch."; 5371 "when we open a PR they should be stucked together, because if we won't the code might delete the tags if they are \"dead code\""
- Ultrathink: 5371 "#ultrathink compare this screen to other industry bunchmanrk's settings screen"; 4918 "ultrathink make sure you covered all use cases"
- Single-instance, not promoted: 5196 "can you do that to all other cards that needs to be closed?" / "the first one, only my cards, list them first" (list before bulk actions on my cards); 5252 "This is marked as deployed, but I don't see it in production"; 5429 "write the migration using go run go/acli/main.go data migration"
