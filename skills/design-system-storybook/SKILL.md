---
name: design-system-storybook
description: Use when adding, moving or classifying anything in the frontglance design-system Storybook - component stories, icons, pictograms, illustrations.
---

# Adding items to the design-system Storybook

Applies to the `frontglance` repo (`/workspace/frontglance`). Every path below is relative to it.

The Storybook mirrors the Figma library ("Valence Platform"). Every item has exactly one home, named and ordered as in
Figma, so a designer's reference maps straight to the thing a developer imports. Work through the steps in order.

## 1. Decide what the item is

| The item is...                                                        | It goes in                          |
| --------------------------------------------------------------------- | ----------------------------------- |
| A token or a raw asset (color, type, spacing, elevation, an SVG file) | **Foundations** (section 3)         |
| A reusable component from `src/frontend/vaila` (`@vaila`, V-prefixed) | **Design System / Vaila**           |
| A generic component from `src/frontend/components/shared`             | **Design System / \<category\>**    |
| A component from a feature folder (`components/Platforms/...`, etc.)  | **Product / \<area\>**              |

Read the component's path and implementation before deciding. A `shared/` path does not make a component generic, and
a feature folder never belongs in Design System.

**Deprecated items** (listed in `agents/deprecated.md`): never add a new story for one. If you are documenting an existing
one, put it in a `(deprecated)` group (see `Design System/Layout/Spacers (deprecated)`) and name its replacement in the
story description.

**No new designs.** If the item exists in neither Figma nor the code, stop and say so; a design-system task must come
first (AGENTS.md).

## 2. Components: title, folder, order

| Section                       | Title                                    | File                                        |
| ----------------------------- | ---------------------------------------- | ------------------------------------------- |
| Vaila component               | `Design System/Vaila/<Category>/<Name>`  | `src/stories/designsystem/vaila/`           |
| Generic shared component      | `Design System/<Category>/<Name>`        | `src/stories/designsystem/shared/` (+ `charts/`, `layout/`) |
| Feature component             | `Product/<Area>/<Name>`                  | `src/stories/product/<area>/`               |

Design System categories, in sidebar order:

| Category        | What belongs                                                            |
| --------------- | ----------------------------------------------------------------------- |
| Buttons & Links | buttons, links                                                          |
| Tags & Badges   | tags, badges, chips                                                     |
| Forms           | inputs, selects, switches, form items                                   |
| Data Display    | tables, charts (`Data Display/Charts/...`), labeled values, trees, info blocks, icon components |
| Feedback        | loading, skeletons, empty states, notices, error modals                 |
| Layout          | structure and layout primitives                                         |
| Overlays        | modals, tooltips, drawers, popovers                                     |

Vaila uses the same categories, plus `Typography` and `Navigation`.

- Reuse an existing category or Product area. A new one must also be added to `storySort` in `.storybook/preview.tsx`;
  otherwise it falls to the end of the sidebar.
- Name the story after the component (`VSelect`, `BaseLineChart`). For a page about a family, use the Figma name in
  sentence case (`Value Primitives`, `Empty States`).
- A component that needs app state is wrapped in `StoryWrapper` from `src/stories/testingcontexts.tsx` (react-query,
  upToDate interceptors, feature flags). Put mock data in `src/stories/mocks/`.
- Write the file with **storybook-creation** (CSF3, args-based stories).

## 3. Foundations: assets and tokens

Sidebar order (`storySort`): Colors → Typography → Spacing → Elevation & Radii → **Icons** → **Pictograms** →
**Illustrations**.

Icons is a folder: System icons → Navigation icons → Object icons → Inventory icons → Status & Severity → Logos →
Needs review.

### Which set an SVG belongs to

Classify by **visual style first, usage second**, the way Figma does. Open the file and check its canvas and colors:

| Signature                                                                       | Set                                       |
| ------------------------------------------------------------------------------- | ----------------------------------------- |
| Monochrome line drawing, ~20px, `currentColor` or black                          | **System icons** (pick the section by meaning) |
| 14px filled grey, used by the settings menu (`AccountSettings/TabsMenu`)         | **Navigation icons**                      |
| ~20px filled teal `#6FCAD3` shape that stands for a thing (file type, record)    | **Object icons**                          |
| Fixed status colors (red / green / orange) as a small trend or state indicator   | **System icons > Status & indicators**    |
| Severity bars                                                                    | **Status & Severity**                     |
| Third-party brand mark                                                           | **Logos > Brand glyphs** (full libraries live in `assets/platforms`, `assets/endpointaiagents`, `assets/valence`) |
| Pink `#F45687` or status color **with teal `#6FCAD3` accent strokes**, canvas ≥ 44px | **Pictograms** (pick the set below)   |
| Pale grey `#E5E8EC` / `#B2B9C3`, large canvas                                    | **Illustrations** (empty states)          |
| Matches none of these                                                            | **Needs review**, and tell the user       |

Pictograms are three Figma component sets, each with its own single variant axis:

- **Pictogram:** feature and concept images (`Name=...`).
- **Status pictogram:** the visual at the top of a modal. `Info`, `Success`, `Attention` (confirmations), `Warning`
  (destructive), `Error`.
- **Landing page pictogram:** the 155px hero of a full-page result screen (e.g. the auth success page).

Inventory icons are not files. They are drawn from `src/frontend/constants/inventory/InventoryAdditionDetails.mapping.tsx`, so a new
inventory type appears on its own.

### Register the SVG

- Add the file name, without extension, to its set in `src/stories/foundations/icons/iconSets.ts`. That file is the
  only place set membership lives.
- **Do not move SVG files** into set folders. Over a thousand import sites use the current paths.
- An unlisted SVG shows up on **Needs review** automatically. Never leave a new file there: assign it, or ask.
- Status and landing pictograms are listed as `{ figma, file }` pairs, in Figma order, so tiles show the Figma name.

### SVG checks before committing a new or edited file

- **Unique ids.** `clipPath`, `mask` and gradient ids must be unique to the file (e.g. `id="my-icon-clip"`, not
  `id="a"`). Two inlined SVGs sharing an id clip or recolor each other.
- **No embedded `<style>` blocks** (Illustrator `.cls-1 { fill: ... }`). Inlined side by side, the last block recolors
  every other SVG. Convert them to attributes, or show the file as `<img>`, as the Valence logos do.
- **Color.** Monochrome icons use `currentColor`. A `currentColor` pictogram or illustration needs a `color` on its gallery
  grid matching what the product uses.
- **White-only marks** need a dark backing on the page, or they are invisible in the light theme.
- Logo sourcing, cropping and dark-mode handling: use **create-svg-logo**.

## 4. Verify

Pass an explicit timeout on every command.

1. `npx prettier --write <files>`, then `npx eslint --max-warnings 0 <files>`, then `npx tsc --noEmit -p tsconfig.json`.
2. Open every page you touched, with no page errors. Storybook runs as a service on `:6006`: start it with
   `/app/scripts/start-storybook.sh`, and start the viewable desktop with `/app/scripts/start-desktop.sh` (Playwright
   needs it). Story URL: `http://localhost:6006/iframe.html?id=<story-id>&viewMode=story`. The id is the title
   lowercased, with `/` and spaces as `-` and `&` dropped, e.g. `foundations-icons-status-severity--status-and-severity`.
3. Assets: the **Needs review** page must not grow, and every SVG under `assets/svgs` must appear on exactly one page.
4. Screenshot the result and look at it. A blank tile or a black shape where Figma shows color is a failure.

## Page conventions (for new foundation pages)

- One file per set, titled `Foundations/<Section>/<Set>`, with `tags: ['!autodocs']` and a single story named like the
  set. It then shows as one sidebar entry, not a folder.
- Build galleries with `iconGallery.tsx` (`IconGrid`, `Section`, `Intro`, `svgItems`). The tile tooltip carries the import
  path, or the JSX for components.
- Keep page copy short. Say what the set is for and when not to use it.
