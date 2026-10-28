# Triage rules

Give every finding one **category**. Add the **Accessibility** tag when it applies. Lior owns the design system; her calls are final, and design-system decisions need no other sign-off.

Severity (Must fix / Should fix / Consider) is separate from category. Category says who does the work and whether a decision is needed; severity says how much it matters. Keep both.

## Categories

**Bug**: broken, no decision needed. Includes anything that breaks a rule in `design-decisions.md`, or a pattern the rest of the product already follows.
- A pop-up taller than 80% of the window.
- Low/No Code rows open a panel but show no pointer cursor, while the other inventory tables do.

**Trivial decision**: a yes/no, or a choice between two options that are already defined. Once Lior approves it, it becomes a rule in `design-decisions.md`, and from then on anything that breaks it is a Bug.
- Every icon-only button shows a tooltip with its action name (approved; now a rule).
- The same element is built more than once and the copies already look or behave differently: the report names the version to keep (the one in Storybook, the most used, or the most complete) and Lior approves it. If no version is clearly right, say so, and it becomes a UX/UI process.

Some Trivial decisions can't become general rules because the answer depends on the component (e.g. how a too-light status color is fixed). These are marked "Per component" in `issue-kinds.md`: each occurrence is its own yes/no for Lior, and approving one doesn't make the others Bugs.

**UX/UI process**: needs design work first. A new pattern, state, layout or copy; several options with real trade-offs; a behavior change across screens; or input from PM or users.
- How the widgets row behaves at smaller widths (wrap, scroll, shrink, minimum width).
- A widget doesn't show which row the active filter came from, so widget rows need a selected state.

**Engineering only**: nothing a user sees changes, or no design decision is left.
- Screen-reader names: they use the tooltip or visible label text, and the severity stays Must fix.
- An element missing from Storybook: a card drafts the entry for Lior to approve.

**Won't fix**: Lior decided not to work on it. Don't raise it again (see "Never flag" in `design-decisions.md`).

**Not an issue (by design)**: the finding describes an approved choice. Don't report it.

## Accessibility tag

Tag findings that only affect accessibility: contrast, screen-reader names, keyboard access, target size. The tag is separate from the category (gray text contrast is a Trivial decision; screen-reader names are Engineering only).

## Grouping

- **Shared component:** report one component-level issue and list the affected screens under it, not one issue per screen (e.g. the table toolbar overflow is designed once on the shared toolbar).
- **Caused by another issue:** merge it into that issue as a symptom (e.g. instance names losing their platform name because the widgets row is too narrow).
- **Area built without a design process that also breaks rules:** split it. Align it with the existing rules now (Trivial decision) and open a separate UX/UI process item for its redesign (e.g. the Activity Monitoring side panel).
- **Evidence:** screenshots must clearly show the problem. If they don't, drop the finding. A layout shift needs before-and-after screenshots.
