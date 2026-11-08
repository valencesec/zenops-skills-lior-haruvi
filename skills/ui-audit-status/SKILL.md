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
6. **Storybook cards:** cards titled 'Storybook coverage' owned by Lior (from the daily Storybook schedule). For each: the component's plain name (from the progress headline or executive summary), the card status, the PR link, and whether a fix card was opened for the product. Status groups: **Added to Storybook** = `merged`, `deployed` or `done`; **Waiting for Lior's review** = an open review gate for Lior; **Waiting for approval** = PR ready for review and not merged; **In progress** = anything else open. Ignore rejected cards. Also read the latest Storybook gaps list (`storybook-gaps.csv` on the latest roll-up card, or `005-storybook-gaps.csv` on card 5854 before the first roll-up) for the total number of components missing from Storybook.

## Counting rules

- An issue shared by several screens counts **once** in the totals (the roll-up merged it), but appears on every screen it affects in the per-screen table.
- Before the first roll-up, there are no fix cards: show every issue as "Not started" and say so in one line.
- A finding Lior marked Won't fix or Not an issue is not counted.
- Never guess. If a number can't be read, show "?" and list the reason under "Data gaps".

## Storybook finish-date estimate

- **Components left:** from the latest Storybook gaps list, count the components the daily schedule will pick: used on 2 or more screens (`screens`), not built for a single screen, not a layout wrapper or internal building block, not the bulk-action bar (being redesigned). Subtract the components that already have a Storybook card that isn't rejected (added or in progress). A rejected Storybook card removes that component from the count.
- **Planned pace:** 5 components a week. The schedule opens one card per workday, Sunday to Thursday (Asia/Jerusalem).
- **Actual pace:** components added to Storybook (cards merged, deployed or done) per week over the last 4 weeks, or since the first Storybook card if that is less than 4 weeks. Round to one decimal.
- **Finish date:** the workday on which the last component would be opened, counting from today and only Sunday to Thursday as workdays (Friday and Saturday are skipped). Planned pace is 1 component per workday; at the actual pace, workdays needed = components left / (actual pace / 5), rounded up. If the actual pace is 0, show no date and say so. If a number can't be read, follow "Never guess" above.

## Output (save to `artifacts/`)

`ui-audit-status-<YYYY-MM-DD>.html`: self-contained (inline CSS, no external links except to cards and reports), light background, readable on a laptop, printable. Plain design language, no code names. Sections, in order:

1. **Headline numbers** (7 tiles): screens audited / total screens; then three tiles, each with its fixed (unique) count under it and never summed into one "issues found" number: **Fixes** (Bug + Engineering only: work for developers), **Decisions** (Trivial decision: yes/no questions for Lior), **Design tasks** (UX/UI process: design work for Lior); issues fixed (merged); screens left; components added to Storybook / components missing (e.g. "3 / 71").
2. **Issues by type** (chart, right after the headline numbers): a horizontal bar chart drawn as inline SVG (no external libraries), one bar per type in this order: Bug, Engineering only, Trivial decision, UX/UI process. Each bar is split into fixed / in progress / not started (using the progress rules in Sources), with the number on each part and the total at the end of the bar. Add a legend. Show the Accessibility count (unique issues tagged Accessibility) as a small note under the chart; it is a tag, not a type. It must be readable when printed: give each part a distinct fill pattern (for example solid, diagonal stripes, empty with outline) as well as a colour, so it also works in grayscale. Do not draw any other progress bar of mixed issues.
3. **Screens audited** (table): screen (linked to the live screen), section, audit card (linked), audit date, Bug, Engineering only, Trivial decision, UX/UI process, Accessibility, repeats, fixed, in progress. Sorted by section, then screen.
4. **Screens left to audit** (table): screen (linked), section. Group by section.
5. **Storybook coverage:** a short progress bar (added, waiting for review or approval, in progress, not started = missing minus all cards); right under the bar: "About N components left. At the planned pace (5 a week): done around <date>. At the actual pace (X a week): done around <date>." (see "Storybook finish-date estimate"; if the actual pace is 0, say so instead of a date), then one line: "The list grows when the roll-up adds components from new audits, so the date can move."; then a table: component (plain name), card (linked), status, PR (linked), fix card opened for the product (linked, or "No"). Newest first.
6. **Open decisions for Lior:** count of items waiting for her yes/no (decisions card, open questions in reports), with links.
7. **Data gaps:** anything you couldn't read, and why.
8. Footer: date and time generated, and "Generated by the ui-audit-status skill on card N".

Also save `ui-audit-status-<YYYY-MM-DD>.md` with the same numbers as plain tables, including the Fixes / Decisions / Design tasks tiles, a small "Issues by type" table (rows: Bug, Engineering only, Trivial decision, UX/UI process; columns: fixed, in progress, not started, total), the Accessibility count, the screens-left tile the Storybook coverage table and the same finish-date estimate lines, for pasting into Slack or a doc.

Set the executive summary to 6 short lines: screens audited / total, "Fixes X (fixed Y) · Decisions X · Design tasks X" (unique counts; Y = fixed Fixes), fixed, screens left, components added to Storybook / missing, and the Storybook estimate line: "Storybook: N left, done around <planned date> (actual pace: <date>)". Then complete the session as the card's track expects.

## Keeping the screen list current

If you see a screen in the product's side menu (T1, read-only) or in an audit card that isn't in `references/screens.md`, list it under "Data gaps" as "New screen not in the list". Don't edit `screens.md` yourself; Lior adds screens through a pull request.
