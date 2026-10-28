# Known design decisions

Rules Lior has approved. Treat them as facts. Never flag what they allow. Anything that breaks one of them is a **Bug**, not a decision.

To add a rule: Lior approves it (usually a Trivial decision), and it's added here through a pull request.

## Visual rules

- **Smallest text:** 10px is the smallest approved text style (Pass/Fail chips, category tags). Don't question the size. Contrast rules still apply. Anything smaller than 10px is a Bug.
- **Category tags** are the same size everywhere. A size difference (e.g. table vs side panel) is a Bug.
- **Lightest grays** are only for borders and disabled items. Every input uses one placeholder color with at least 4.5:1 contrast. Readable text in the lightest grays is a Bug.
- **Pop-ups** are never taller than 80% of the window. The title and buttons stay fixed and only the content scrolls. Anything taller is a Bug.
- **Side panels (drawers):** the panel title is the largest text, and only the title and close button stay pinned.
- **Small gray secondary text** uses the darker secondary gray (#5f6672, 5.8:1). Lighter gray for small readable text is a Bug.
- **Inventory side panels** overlap the table by design and are 800px wide. A panel with a different width is a Bug.

## Behavior and content rules

- **Icon-only buttons** always show a tooltip with the action name ("Download", "Sort direction", "Settings"). A missing tooltip is a Bug.
- **Screen-reader names:** a control's name is its tooltip or visible label text. A severity icon's name is "<Severity> severity".
- **Cut-off text** is fine when it (1) shows "…", (2) fits at wider screen sizes, and (3) isn't needed to complete a task, like a search hint. Data people need to read (table values, names, IPs) must show its full value on hover.
- **Side-panel tabs:** when tabs don't fit, whole tabs move into the "…" menu. A tab cut off mid-word is a Bug.
- **Disabled links** stay visible, in the design-system disabled color, with the reason in a tooltip.
- **Filter sidebar** opens scrolled to the active filter, so its selected options are visible.
- **Empty values** stay empty, or show a "no info" tag where that's already used. Don't flag blank values.
- **Rows that open a side panel** show a pointer cursor, like the other inventory tables.
- **Summary widget rows** lock while a filter is on, by design; Clear filters is the way out. Do flag a widget that doesn't show which row the active filter came from.
- **Failed requests** open the global pop-up "An error has occurred" ("Please try refreshing the page. If the issue persists, contact support."), so tables don't need their own error state.
- **The light-teal filled "Save View" button** is an approved button variant.
- **The bulk-action bar** (Actions, Change Severity, Track/Untrack) is being redesigned. Skip it until told otherwise.
- **Shared UI behaves the same on every screen.** If a shared element works on some screens and breaks on others, flag it once and list the screens.

## Never flag

- Target size (click areas under 24px)
- Keyboard access (hover-only icons, rows that don't open with Enter, missing focus ring)
- Missing error states on tables
- The trash icon that removes a filter
- A side panel covering the table
- Cut-off search box hints
- Blank (empty) values
