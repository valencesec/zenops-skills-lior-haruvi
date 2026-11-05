# Audit rules

Product design rules live in frontglance `DESIGN.md`. This file only says how to audit against them.

Lior Haruvi owns `DESIGN.md`. Treat its rules as facts: anything that breaks one is a **Bug**, not a decision. Never flag what `DESIGN.md` allows, including everything under its "Intentional behaviour".

## How to judge findings

- **Bug vs decision:** a finding that breaks a rule in `DESIGN.md` is a Bug. A finding no rule covers is a decision for Lior (Trivial decision or UX/UI process, see `triage-rules.md`); don't call it a Bug.
- **Shared UI behaves the same on every screen.** If a shared element works on some screens and breaks on others, flag it once and list the screens.
- **Widgets:** do flag a summary widget that doesn't show which row the active filter came from. Locked rows while a filter is on are by design.
- **Side panels:** besides the rules in `DESIGN.md`, each of these is a Bug: a gray section heading, a black or bold attribute label, a gray value, a colon after a label, or Title Case labels ("Admin Accounts").
- **Smaller than 10px** text is a Bug.
- **Panel width:** an item detail panel with a width other than 800px is a Bug. Filter pickers like the Add-filter drawer are exempt.
- **Cut-off text:** missing "…", not fitting at wider screen sizes, or hiding data people need to read (table values, names, IPs) without the full value on hover is a Bug. A cut-off search hint is never flagged.

## Never flag

- Target size (click areas under 24px)
- Keyboard access (hover-only icons, rows that don't open with Enter, missing focus ring)
- Missing error states on tables
- The trash icon that removes a filter
- A side panel covering the table
- Cut-off search box hints
- Blank (empty) values
- The bulk-action bar (Actions, Change Severity, Track/Untrack) until design says otherwise

## In the old file but not in DESIGN.md

Kept here until Lior decides whether they belong in `DESIGN.md`:

- Where the outlined icon-only button rule was found: Security Checks Dashboard (card 6123, finding #5) and Integrations Inventory (card 6111, finding #3, the Accounts-tab download button).
- Side-panel examples: section rows "Admin accounts 1" and "Threats 3"; the section link "View in activity monitoring"; the attribute row "Reports to manager@mail.com"; "No information" shown in gray.
- "Don't question the size" for the 10px text style.
