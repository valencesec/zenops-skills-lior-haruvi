# Issue kinds

The catalog of known issue kinds, from the first 7 screen audits and Lior's review (roll-up card 5854). Match every finding to a kind and reuse its ID and category.

- A finding that matches no kind gets a category from `triage-rules.md` and is marked **"Proposed new kind"**. Only Lior adds kinds to this file.
- **Decision status** applies to Trivial decisions. "Approved" means it's now a rule in `design-decisions.md`, so a new occurrence is a **Bug**. "Pending" means Lior hasn't answered the yes/no yet: list it under "Decisions needed". "Per component" means it never becomes a general rule: every occurrence is its own yes/no under "Decisions needed".

## Active kinds

| ID | Kind | Category | Tag | Decision status | Notes |
|---|---|---|---|---|---|
| T01 | Small gray secondary text too light (under 4.5:1) | Trivial decision | Accessibility | Approved | Rule: small gray text uses the darker secondary gray (#5f6672, 5.8:1) |
| T02 | Lightest grays used for readable text (hints, "No Information") | Trivial decision | Accessibility | Approved | Rule: lightest grays only for borders and disabled items; one placeholder color at 4.5:1 or more |
| T03 | Status and accent colors too light for text or icons | Trivial decision | Accessibility | Per component | Not a general rule: Lior decides each component separately. Every occurrence goes to the decisions card with the component, the color and its contrast |
| T04 | Same element in different sizes, or text under 10px | Bug | | | Breaks existing size rules |
| T05a | Side panel breaks the drawer rules (heading sizes, pinned area) | Trivial decision | | Approved | Rule: title is the largest text; only title and close stay pinned |
| T05b | Area built without a design process needs a redesign | UX/UI process | | | Activity Monitoring side panel |
| T06 | Icon-only button without a tooltip | Trivial decision | | Approved | Now a rule, so new occurrences are Bugs |
| T07 | Control or meaningful icon without a screen-reader name | Engineering only | Accessibility | | Name = tooltip or visible label; severity stays Must fix |
| T10 | Cut-off data text without "…" or full value on hover | Trivial decision | | Approved | Search hints and non-essential text are exempt (see design decisions) |
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
| U01 | Widgets row breaks at smaller widths | UX/UI process | | | One responsive rule for every screen. Symptom: platform names squeezed out of instance labels |
| U02 | Table toolbar overflows at smaller widths | UX/UI process | | | Designed once on the shared toolbar component |
| U04 | Page scrolls in several nested layers | UX/UI process | | | Needs a scroll model for table screens |
| U05 | Empty states look different in different places | UX/UI process | | | Needs one empty-state system |
| U07 | Links don't show where they lead | UX/UI process | | | Needs a product-wide link convention |
| U08 | Row opens a side panel but shows no pointer cursor | Bug | | | Other inventory tables already do it |
| U09 | Active filter isn't shown in the widget | UX/UI process | | | Needs a selected state for widget rows |
| U10 | Confirmation dialogs built several ways | Trivial decision | | Approved | Keep the design-system pop-up the report names |
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
| T17 | Empty value shows nothing | By design: empty values stay empty, or show a "no info" tag in some places |

## Retired

| ID | Kind | Why |
|---|---|---|
| T18 | Loading placeholder layout differs from the loaded page | False finding: evidence didn't hold up |
| T20 | Instance names shown without their platform | Merged into U01 as a symptom |
