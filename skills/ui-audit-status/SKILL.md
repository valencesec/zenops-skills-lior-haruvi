---
name: ui-audit-status
description: Build the UI audit progress dashboard (screens audited, issues found per screen, issues fixed, screens left to audit) as an HTML report on this card. Use when a card asks for the UI audit status or progress dashboard.
---

# UI audit status dashboard

You build a one-page progress report on Lior's UI audit work, for Lior and the people she shares it with (product and engineering managers). It answers four questions: which screens were audited, how many issues each has, how many are fixed, and which screens are left. Read-only: never change other cards, reports or code.

## Sources (read every run, never from memory)

1. **Screen list:** `references/screens.md`. Every screen in the product's side menu, with its URL and section. This is the full scope: "left to audit" = screens here with no audit card.
2. **Audit cards:** `list_cards` with keyword "UI Screen Audit" and owner lior.haruvi@valencesecurity.com, plus any card with the label "screen audit". Ignore rejected cards. If two audit cards cover the same screen, use the newer one that has a report. Match a card to a screen by the URL in its description.
3. **Each audit's latest report:** `list_artifacts` and `get_artifact_content` on the card. Use the highest version (`-v3` over `-v2` over none). From it take, for **new findings only** (not "Already reported on other screens", not dropped ones): the count per category (Bug, Engineering only, Trivial decision, UX/UI process) and the number marked Accessibility. Also take the number of repeats. If a report has no counts you can trust, count the `#### #N` findings under each category heading.
4. **Roll-up cards:** cards titled "UI audit roll-up" owned by Lior. From the latest one, read `routing-plan.md` to map findings to the cards created for them.
5. **Fix and UX/UI cards:** cards titled `[UI fix]` or `[UX/UI audit]` owned by Lior, plus the cards the roll-up updated instead of creating (listed in its routing-plan.md). Their status decides progress:
   - **Fixed:** status `merged`, `deployed` or `done` (a PR was merged). For `[UX/UI audit]` cards, `done`.
   - **In progress:** any other open status.
   - **Not started:** no card yet (still only in a report, or waiting for a decision).
   - Ignore `rejected` cards, and count their issues as not started.
6. **Storybook cards:** cards titled 'Storybook coverage' owned by Lior (from the daily Storybook schedule). For each: the plain names of its components (a card holds up to 3; read them from the progress headline and executive summary), the card status, the PR link, and whether a fix card was opened for the product. Status groups: **Added to Storybook** = `merged`, `deployed` or `done`; **Waiting for Lior's review** = an open review gate for Lior; **Waiting for approval** = PR ready for review and not merged; **In progress** = anything else open. Ignore rejected cards. Also read the latest Storybook gaps list (`storybook-gaps.csv` on the latest roll-up card, or `005-storybook-gaps.csv` on card 5854 before the first roll-up) for the total number of components missing from Storybook.
7. **Engineering-only work:** the Engineering only findings in each audit's latest report (new findings only), and the cards they were routed to, from the latest roll-up's `routing-plan.md` (card status as in item 5; team from the card's `team` field). Before the first roll-up there are no cards: show the findings only, with team "Not assigned yet".
8. **Lior's pull requests:** merge two sources and remove duplicates by PR URL.
   - `metadata.prLinks` on every card owned by lior.haruvi@valencesecurity.com, any status, any track. Page through all of them with `offset` until `hasMore` is false.
   - GitHub search in the `valencesec` org for PRs authored by or assigned to `liorharuvi-valence`, using the REST search API (`/search/issues?q=org:valencesec+type:pr+author:liorharuvi-valence`, then the same with `assignee:`). Page through all results. Never print credentials.
   - If the count may still be incomplete (a search hit the page limit, a call failed, a card couldn't be read), say so under "Data gaps".
9. **Storybook list:** read `storybook-gaps.csv` from the newest of: the card titled "Storybook gaps: find duplicates and shorten the list", or the latest "UI audit roll-up" card. When the deduped list exists, show the before → after count (the roll-up's list, then the shortened one).

## Counting rules

- An issue shared by several screens counts **once** in the totals (the roll-up merged it), but appears on every screen it affects in the per-screen table.
- Before the first roll-up, there are no fix cards: show every issue as "Not started" and say so in one line.
- A finding Lior marked Won't fix or Not an issue is not counted.
- **Bug fixes** and **Engineering only** are always counted and shown separately. Never add them into one number.
- A finding fixed by a PR from "Fixed from the audits" counts as **fixed** when the PR is merged and **in progress** when it's open, even when there's no roll-up card for it. Count it in the totals and on its screen. A finding settled by a DESIGN.md rule counts as **Decided**. A finding counts once, even if several PRs cover it.
- Never guess. If a number can't be read, show "?" and list the reason under "Data gaps".

## Storybook finish-date estimate

- **Components left:** from the latest Storybook gaps list, count the components the daily schedule will pick: used on 2 or more screens (`screens`), not built for a single screen, not a layout wrapper or internal building block, not the bulk-action bar (being redesigned). Subtract the components that already have a Storybook card that isn't rejected (added or in progress); a card with 3 components subtracts 3. A rejected Storybook card removes its components from the count.
- **Planned pace:** 15 components a week. The schedule opens one card per workday, Sunday to Thursday (Asia/Jerusalem), with up to 3 components per card.
- **Actual pace:** components added to Storybook (components in cards merged, deployed or done; count components, not cards) per week over the last 4 weeks, or since the first Storybook card if that is less than 4 weeks. Round to one decimal.
- **Finish date:** the workday on which the last component would be opened, counting from today and only Sunday to Thursday as workdays (Friday and Saturday are skipped). Planned pace is 3 components per workday; at the actual pace, workdays needed = components left / (actual pace / 5), rounded up. If the actual pace is 0, show no date and say so. If a number can't be read, follow "Never guess" above.

## Fixed from the audits

Shows the PRs that fixed something an audit found, including ones with no roll-up card. Go through every PR of Lior's (item 8 of Sources). A PR matches when any of these is true:
- its card is a `[UI fix]` card from the roll-up;
- its card or the PR names an audit card, a finding, an issue kind or a screen;
- it fixes an issue kind that is listed in an audit report on that screen;
- it's a DESIGN.md PR that settled audit findings.

For each matching PR list: PR (linked), card (linked), what it fixed in plain words, the screens, and the audit findings it covers (screen + finding number). Merged PR = fixed, open PR = in progress, DESIGN.md rule = Decided.

If you're not sure a PR matches a finding, don't count it: list it under **Possible matches, not counted**, with the reason you're unsure. Never guess.

## Engineering-only work

Shows what the Engineering only tasks are, how much they matter, and which team has each one.

- **Summary** above the chart: total Engineering only tasks, tasks by team, and how many are Must fix.
- **Chart:** a horizontal bar chart of Engineering only findings grouped by **kind** (for example "No screen-reader name", "Identical copies of the same element", "Missing from Storybook"), each bar split by status (fixed / in progress / not started) with the same fill patterns and legend as "Issues by type", so it works in grayscale. Inline SVG.
- **Impact:** for each kind, show severity (Must fix / Should fix / Consider), how many screens it affects, and the Accessibility tag where it applies. Sort kinds by impact: Must fix first, then by number of screens.
- **Table:** one row per Engineering only task (one row per card once cards exist, otherwise one per finding): what it is in one plain sentence (what changes for users or developers), kind, severity, screens affected, team ("Not assigned yet" when there is no card), card (linked), status.

## Lior's work: pull requests

Shows all the work Lior has driven, so her contribution is visible. Source: item 8 of Sources.

- **Tiles:** PRs opened, PRs merged, PRs open, PRs closed without merging.
- **Chart:** PRs merged per week (bars), since the first one.
- **Table** (newest first): PR title, repo, type (Storybook story / UI fix / Design rule (DESIGN.md) / Audit skills / Other, from the repo and title), status (Open / Draft / Merged / Closed), opened date, merged date, ZenOps card (linked), PR link.
- **Summary line:** "Since <first date>: N PRs opened, M merged: X Storybook components added, Y UI fixes, Z design rules."

## Output (save to `artifacts/`)

`ui-audit-status-<YYYY-MM-DD>.html`: self-contained (inline CSS, no external links except to cards and reports), light background, readable on a laptop, printable. Plain design language, no code names. Sections, in order:

1. **Headline numbers** (8 tiles): screens audited / total screens; then four tiles, never summed into one "issues found" number: **Bug fixes** (Bug: work for developers) and **Engineering only** (behind-the-scenes work for developers), each showing found / fixed / in progress; **Decisions** (Trivial decision: yes/no questions for Lior), with its fixed (unique) count and the number Decided; **Design tasks** (UX/UI process: design work for Lior), with its fixed (unique) count; issues fixed (merged); screens left; components added to Storybook / components missing (e.g. "3 / 71"), with the before → after count when the deduped list exists.
2. **Fixed from the audits** (right after the headline numbers; see "Fixed from the audits" below), with "Possible matches, not counted" under it.
3. **Issues by type** (chart, right after the headline numbers): a horizontal bar chart drawn as inline SVG (no external libraries), one bar per type in this order: Bug, Engineering only, Trivial decision, UX/UI process. Each bar is split into fixed / in progress / not started (using the progress rules in Sources and the counting rules, so audit fixes from "Fixed from the audits" are included), with the number on each part and the total at the end of the bar. Add a legend. Show the Accessibility count (unique issues tagged Accessibility) as a small note under the chart; it is a tag, not a type. It must be readable when printed: give each part a distinct fill pattern (for example solid, diagonal stripes, empty with outline) as well as a colour, so it also works in grayscale. Do not draw any other progress bar of mixed issues.
4. **Screens audited** (table): screen (linked to the live screen), section, audit card (linked), audit date, Bug, Engineering only, Trivial decision, UX/UI process, Accessibility, repeats, fixed, in progress. Sorted by section, then screen.
5. **Screens left to audit** (table): screen (linked), section. Group by section.
6. **Storybook coverage:** a short progress bar (added, waiting for review or approval, in progress, not started = missing minus all cards); right under the bar: "About N components left. At the planned pace (15 a week): done around <date>. At the actual pace (X a week): done around <date>." (see "Storybook finish-date estimate"; if the actual pace is 0, say so instead of a date), then one line: "The list grows when the roll-up adds components from new audits, so the date can move."; then a table: component (plain name), card (linked), status, PR (linked), fix card opened for the product (linked, or "No"). Newest first.
7. **Engineering-only work** (see "Engineering-only work" below).
8. **Lior's work: pull requests** (see "Lior's work: pull requests" below).
9. **Open decisions for Lior:** count of items waiting for her yes/no (decisions card, open questions in reports), with links.
10. **Data gaps:** anything you couldn't read, and why.
11. Footer: date and time generated, and "Generated by the ui-audit-status skill on card N".

Also save `ui-audit-status-<YYYY-MM-DD>.md` with the same numbers as plain tables, including the Bug fixes / Engineering only / Decisions / Design tasks tiles, the "Fixed from the audits" section, a small "Issues by type" table (rows: Bug, Engineering only, Trivial decision, UX/UI process; columns: fixed, in progress, not started, total), the Accessibility count, the screens-left tile, the Storybook coverage table, the same finish-date estimate lines, the Engineering only summary line and table, and the PR tiles, summary line and table, for pasting into Slack or a doc.

Set the executive summary to 9 short lines, in the skill's own format, each one short and clear: screens audited / total, "Bug fixes X (fixed Y, in progress Z) · Engineering only X (fixed Y, in progress Z) · Decisions X · Design tasks X" (unique counts), "Fixed from the audits: N PRs, M findings", fixed, screens left, components added to Storybook / missing, the Storybook estimate line: "Storybook: N left, done around <planned date> (actual pace: <date>)", "Engineering only: N tasks, M Must fix, by team: …", and "PRs: N opened, M merged". Then complete the session as the card's track expects.

## Keeping the screen list current

If you see a screen in the product's side menu (T1, read-only) or in an audit card that isn't in `references/screens.md`, list it under "Data gaps" as "New screen not in the list". Don't edit `screens.md` yourself; Lior adds screens through a pull request.
