# Issue kinds

The catalog of known issue kinds, from the first 7 screen audits and Lior's review (roll-up card 5854). Match every finding to a kind and reuse its ID and category.

- A finding that matches no kind gets a category from `triage-rules.md` and is marked **"Proposed new kind"**. Only Lior adds kinds to this file.
- **Decision status** applies to Trivial decisions. "Approved" means it's now a rule in frontglance `DESIGN.md`, so a new occurrence is a **Bug**. "Pending" means Lior hasn't answered the yes/no yet: list it under "Decisions needed". "Per component" means it never becomes a general rule: every occurrence is its own yes/no under "Decisions needed".

## Active kinds

| ID | Kind | Category | Tag | Decision status | Notes |
|---|---|---|---|---|---|
| T01 | Small gray text lighter than gray_700 used for readable text (under 4.5:1) | Trivial decision | Accessibility | Approved | Rule: gray_700 (#727a86) is the approved colour for attribute labels and small secondary text. T01 flags only grays lighter than gray_700 used for readable text |
| T02 | Lightest grays used for readable text (hints, "No Information") | Trivial decision | Accessibility | Approved | Rule: lightest grays only for borders and disabled items; one placeholder color at 4.5:1 or more. Empty or unavailable values ("No Information", "Unknown", "None") in gray_600 (#969da9) are allowed by DESIGN.md and are not a finding |
| T03 | Status and accent colors too light for text or icons | Trivial decision | Accessibility | Per component | Not a general rule: Lior decides each component separately. Every occurrence goes to the decisions card with the component, the color and its contrast |
| T04 | Same element in different sizes, or text under 10px | Bug | | | Breaks existing size rules |
| T05a | Side panel breaks the drawer rules (heading sizes and colours, label and value styles, pinned area) | Trivial decision | | Approved | Rule: title is the largest text; headings semibold black; attribute labels regular gray_700 #727a86 with no colon, values black; only title, close and tabs stay pinned. Example: Identities panel "Title" label is black and its value gray (reversed) |
| T05b | Area built without a design process needs a redesign | UX/UI process | | | Activity Monitoring side panel |
| T06 | Icon-only button without a tooltip | Trivial decision | | Approved | Now a rule, so new occurrences are Bugs |
| T07 | Control or meaningful icon without a screen-reader name | Engineering only | Accessibility | | Name = tooltip or visible label; severity stays Must fix |
| T10 | Cut-off data text without "…" or full value on hover | Trivial decision | | Approved | Search hints and non-essential text are exempt (see design decisions). Includes a platform shown only as a logo whose hover doesn't show the platform and instance name, e.g. "Sophos Primary" (DESIGN.md rule). The "platform + instance" hover is needed only when the logo stands alone; when the instance name is shown next to it, a platform-only hover is fine |
| T12 | Last side-panel tab cut off mid-word | Trivial decision | | Approved | Rule: whole tabs move into the "…" menu, never half a tab |
| T13 | Small alignment and spacing slips | Bug | | | Fix to the existing pattern next to it |
| T14 | Pop-up taller than 80% of the window | Bug | | | Breaks the pop-up rule |
| T15 | Page taller than the window, so the whole page scrolls slightly | Bug | | | |
| T16 | Disabled link not in the design-system disabled color | Trivial decision | | Approved | Rule: a disabled link stays visible, in the design-system disabled color, with the reason in a tooltip |
| T19 | Active filter's options below the fold | Trivial decision | | Approved | Rule: the filter sidebar opens scrolled to the active filter |
| T21a | Copies of the same element that look the same | Engineering only | | | Merge into the one to keep |
| T21b | Copies of the same element that already look or behave differently | Trivial decision | | Approved | Keep the version the report names; if none is clearly right, UX/UI process |
| T23 | Item detail side panel width differs from 800px | Bug | | | Doesn't apply to filter pickers (e.g. Add-filter drawer) |
| T24 | Full-page logo while loading instead of the widget and table skeletons | Bug | | | Found on Integrations Inventory (card 6111) |
| T25 | Outlined icon-only button with a teal stroke instead of gray | Bug | | | Rule: gray stroke #cbd0d7 for every outlined icon-only button (card 6123, finding #5). The gray stroke is for the resting state; a teal stroke on hover is fine |
| T26 | Active filter shows no options | Bug | | | Card 6129, finding #6 |
| T27 | Widget row icon left empty | Bug | | | Card 6129, finding #9. When the icons don't exist yet it's UX/UI process |
| T28 | Same value in different letter case on one screen | Bug | | | Card 6128, "discovered" vs "Discovered" |
| T31 | Heading, tab or button not in Title Case | Bug | | | Breaks DESIGN.md: every button, heading, tab and attribute label capitalizes every word, except short words (to, of, in, on, at, by, for, and, or, the, a, an) unless first: "Export to PDF". Approved by Lior on card 6576 |
| T32 | Empty value shown as a dash | Bug | | | Approved by Lior on card 6576 |
| T33 | Count shows 0 while loading | Bug | | | Approved by Lior on card 6576 |
| T34 | Label ends with a colon | Bug | | | Breaks DESIGN.md: labels never end with a colon, anywhere in the product. Approved by Lior on card 6576 |
| T35 | Layout jumps while the screen loads (a skeleton the wrong size, overflowing or drawn over, or an element that appears late and pushes others) | Bug | | | Cards 6577, 6580, 6128 |
| T36 | Column opens too narrow (a flexible column squeezed by fixed columns) | Bug | | | Cards 6580, 6130 |
| T37 | Same thing named differently on one screen | Bug | | | Card 6580 |
| T38 | Table toolbar has no result count | Bug | | | Card 6741 (Tags), approved by Lior 2026-11-10 |
| T39 | Row highlights on hover but opens nothing | Bug | | | Card 6741 (Tags), approved by Lior 2026-11-10 |
| T40 | Chart order changes between loads | Engineering only | | | Card 6577 (AI Security), finding #7, approved by Lior 2026-11-09 |
| T41 | Side menu doesn't mark the current page | Bug | | | Card 6575 (Boards), finding #7, approved by Lior 2026-11-10 |
| T42 | Status icon without a label or tooltip | Bug | | | Card 6575 (Boards), finding #9, approved by Lior 2026-11-10. A status icon with no text label shows its meaning in a tooltip |
| U01 | Widgets row breaks at smaller widths | UX/UI process | | | One responsive rule for every screen. Symptom: platform names squeezed out of instance labels |
| U02 | Table toolbar overflows at smaller widths | UX/UI process | | | Designed once on the shared toolbar component |
| U04 | Page scrolls in several nested layers | UX/UI process | | | Needs a scroll model for table screens |
| U05 | Empty state not built from the empty-state component (Regular or Mini), or the wrong size for its place | UX/UI process | | | Needs one empty-state system |
| U07 | Links don't show where they lead | UX/UI process | | | Needs a product-wide link convention |
| U08 | Row opens a side panel but shows no pointer cursor | Bug | | | Other inventory tables already do it |
| U09 | Active filter isn't shown in the widget | UX/UI process | | | Needs a selected state for widget rows |
| U10 | Confirmation dialogs built several ways | Trivial decision | | Approved | Keep the design-system pop-up the report names |
| U12 | Element built without a design; replace with an existing design-system component | UX/UI process | | | Card 6126, finding #11 |
| U11 | Element not documented in Storybook | Engineering only | | | A card drafts the Storybook entry for Lior to approve |

## Won't fix or not an issue (don't report)

| ID | Kind | Why |
|---|---|---|
| T08 | Click targets under 24px | Won't fix |
| T09 | Keyboard access (hover-only icons, Enter on rows, focus ring) | Won't fix for now |
| T11 | Cut-off search box hint | Won't fix: fits on larger screens, shows "…", not needed for the task |
| T22 | Trash icon removes a filter | By design |
| U03 | Side panel covers the table | By design |
| U06 | No table error state | Global error pop-up already handles failed requests |
| T29 | Disabled sanction dropdown in the side-panel header | Won't fix | Card 6128: by design |
| T30 | Table search applies on Enter | Won't fix | Card 6128: by design |
| T17 | Empty value shows nothing | By design: empty values stay empty, or show a "no info" tag in some places |

## Retired

| ID | Kind | Why |
|---|---|---|
| T18 | Loading placeholder layout differs from the loaded page | False finding: evidence didn't hold up |
| T20 | Instance names shown without their platform | Merged into U01 as a symptom |
