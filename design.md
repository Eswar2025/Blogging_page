# Design system for handbooks and codebase guides

Use this file whenever you generate a handbook, roadmap page, or detailed codebase walkthrough for this repo. The current local reference is `Project_Workflow.html`. Use these tokens consistently; do not depend on a reference file that is absent from the repository.

The look is near-black with warm cream text. Monochrome, quiet, soft corners, thin lines. Color comes from the palette below and nowhere else.

## Palette

| Token | Dark theme | Light theme | Used for |
|---|---|---|---|
| `--bg` | `#0a0a0a` | `#fffaf0` | Page background (the primary color) |
| `--surface` | `#1a1a1a` | `#faf5e8` | Code blocks, demo panels, stage nodes |
| `--surface-2` | `#1f1f1f` | `#ebe6d6` | Inner fills, inputs |
| `--line` | `#1f1f1f` | `#ebe6d6` | Hairline dividers and card borders |
| `--line-strong` | `#3a3a3a` | `#9a9a9a` | Hover borders, node borders, table frames |
| `--control-border` | `#6a6a6a` | `#6a6a6a` | Input boundaries and interactive outlines that need to be identifiable |
| `--text` | `#fffaf0` | `#0a0a0a` | Headings and emphasis |
| `--body` | `#e5e5e5` | `#1a1a1a` | Paragraph text |
| `--muted` | `#9a9a9a` | `#6a6a6a` | Secondary text on background/surface, meaningful chapter numerals |
| `--faint` | `#6a6a6a` | `#9a9a9a` | Decoration only: nonessential edges and ornaments |
| `--primary` | `#fffaf0` | `#0a0a0a` | Filled buttons, "done" state, focus ring |
| `--on-primary` | `#0a0a0a` | `#fffaf0` | Text on a primary fill |

The full set from the source swatch is `#0a0a0a #fffaf0 #faf5e8 #ebe6d6 #e5e5e5 #1f1f1f #3a3a3a #1a1a1a #6a6a6a #9a9a9a`. Do not add other colors, gradients, or colored shadows.

### Contrast and semantic use

- Meaningful normal text needs at least 4.5:1 against its actual background. Qualifying large text needs 3:1: at least 24 CSS px regular or about 18.67 CSS px bold. An 18px size alone does not qualify. These thresholds are accessibility requirements, not a recommended reading size.
- `--faint` is never for meaningful text, regardless of size. It is about 3.66:1 on the dark background and 2.70:1 on the light background. Use `--muted` or stronger for chapter numbers that identify the reading order.
- `--muted` passes on both themes' background and first surface, but the light theme's `#6a6a6a` on `--surface-2` is only about 4.33:1. Use `--body` for text, placeholders, and meaningful helper copy on that inner fill. Check ancestor backgrounds rather than assuming a token always passes.
- Decorative hairlines can stay subtle. When a boundary is necessary to identify an active control, use `--control-border` rather than `--line-strong`. The control border is above 3:1 against the defined background/surface fills in both themes. Focus and selected-state indicators must also remain distinguishable against adjacent colors. Not every decorative card border needs 3:1.
- Do not reduce meaningful text/control opacity without rechecking contrast. Keep disabled text understandable; accompany unavailable actions with a reason when helpful.
- Underline inline links. Navigation links and buttons may omit underlines when placement and shape already identify them.
- Communicate states using explicit labels such as "Saved", "Failed", "Learned", and "Unavailable", supported by shape or icons where useful. A monochrome fill or brightness change must not be the only state cue.

References: [WCAG text contrast](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html), [non-text contrast](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html).

The dark theme is the default. Offer a light/dark toggle and remember the choice in `localStorage` inside a try/catch.

## Typography

Use `Inter, "Segoe UI", system-ui, -apple-system, sans-serif`, with no remote font download so pages stay offline. Inter is used only when installed; the system fallback is intentional and must be checked for wrapping/readability. Do not claim every device renders Inter. One sans-serif family plus a monospace code stack is sufficient. Code uses `ui-monospace, "Cascadia Code", Consolas, Menlo, monospace`.

Use rem-based text sizes with the browser's default base size, normally 16px; do not override user font preferences with a fixed root size. Values below show that default equivalent. Keep unitless line heights. These sizes are design choices, not WCAG minimum font sizes.

| Token | Size / line height | Weight | Used for |
|---|---|---|---|
| display | `clamp(2rem, 5vw, 3rem)` / 1.1 | 600 | Page title, normally 32-48px |
| h2 | 1.75rem (28px) / 1.2 | 600 | Stage or chapter title |
| h3 | 1.25rem (20px) / 1.35 | 600 | Topic card title |
| lead | 1.125rem (18px) / 1.6 | 400 | Intro paragraph under a title |
| body | 1rem (16px) / 1.7 | 400 | Paragraphs, lists, form fields |
| small | 0.875rem (14px) / 1.5 | 400 | Captions, useful secondary text, buttons, node labels |
| label | 0.75rem (12px) / 1.4, uppercase, 0.08em tracking | 500 | Short eyebrows and table headers; use 14px sentence case for form labels |
| stat | 1.75rem (28px) / 1.1 | 600 | Numbers in the stat grid |
| numeral | 3rem (48px) / 1 | 600 | Meaningful stage numbers in `--muted` |
| code | 0.875rem (14px) / 1.6 | 400 | Blocks; inline code about 0.9em |

Limit ordinary prose to about 65-75 characters per line; default to `max-width: 72ch`. Allow tables, trees, diagrams, and demo controls to use more width. Do not shrink useful text on phones to make a dense layout fit: reflow the layout. Check text enlargement and browser zoom, including at 200%.

## Shape and spacing

- Base radius 12px for cards, panels, and stage nodes. 8px for small nodes, inputs, and code chips. Fully round (999px) for buttons and pills.
- Decorative borders are 1px; preserve the specified thicker focus rings, graph edges, and callout rules. Depth comes from borders and surface fills, never shadows.
- Spacing scale for padding, margin, and layout gaps: 4, 8, 12, 16, 24, 32, 48, 64 (px). Typography, line widths, reading measures, responsive dimensions, and accessibility sizing are separate rules.
- Primary buttons, form controls, disclosure triggers, and standalone navigation targets should have a minimum 48px hit height. Icon-only controls should have at least a 48 x 48px target. Expand the clickable label area for checkboxes; inline paragraph links do not need giant boxes. WCAG's 24 x 24px AA minimum has exceptions; 48px is this system's more comfortable design target. See [target-size guidance](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html).

## Signature motifs

1. Hairline grid. Stats and key facts sit in cells separated by 1px lines inside one rounded frame, like the swatch row in the reference image.
2. Roadmap graph. Chapters are nodes on a vertical spine joined by arrowed edges. Sub-topics are smaller nodes on either side, joined by dashed curves. This is inspired by roadmap.sh. Click a node to jump to its section.
3. Cards on a hairline. Discrete topics/comparisons have a `--line` border and no fill. On hover or `:target` the border becomes `--line-strong` or `--primary`. Do not put every explanatory paragraph in a card: use unboxed reading blocks for narratives and step-by-step explanations, with spacing and headings providing hierarchy.

## Components

| Component | Rules |
|---|---|
| Top bar | Sticky, minimum 56px, translucent `--bg` with blur, hairline underneath. Brand left, search and theme toggle right. Allow reflow at text enlargement; preserve control hit areas. |
| Table of contents | Sticky left column from 1100px up. Active chapter is `--text` with a `--primary` marker and `aria-current`. Below that width replace it with a labeled "Jump to chapter" selector, rather than removing chapter access. Keep an accessible skip link. |
| Stat grid | Four cells, 2 columns on phones. |
| Roadmap stage node | `--surface` fill, `--control-border` outline, 12px radius, number label above title. Done state is a `--primary` fill plus a "Learned" label. Active state has a `--primary` indicator and programmatic current state. |
| Roadmap branch node | `--bg` fill, 8px radius, 14px muted text, 48px minimum hit height. Hover/focus turns the outline `--primary`. |
| Edges | Spine edges are 2px solid `--muted` with an arrowhead. Branch edges are 1.5px dashed `--faint`. Phones show the spine only. |
| Stage header | Numeral, title, lead paragraph, and a "Mark learned" pill button on the right. |
| Topic card | 24px padding, 12px radius, h3, short paragraph or list, optional code block. |
| Code block | `--surface` fill, `--line` border, 12px radius, 14px text; long lines scroll inside the block. No syntax colors. |
| Callout | 3px `--primary` left rule on a `--surface` fill. |
| Demo panel | `--surface` fill, `--line-strong` border, controls above, result below, generated code underneath. |
| Table | Collapsed borders, `--line` row dividers, label-style header. Wrap in a scroll container on phones. |
| Buttons | `--control-border` outline pill by default; 14px text and 48px minimum hit height. Filled (`--primary`) marks chosen/finished state with a visible label. Toggles expose `aria-pressed`. |
| Form fields | 16px text, visible 14px label, 48px minimum hit height, `--control-border`, `--body` on `--surface-2`. Placeholders supplement labels and must remain readable. |
| Search | Filters topic cards and unboxed reading blocks; hides empty chapters, announces result count, provides empty-state recovery. `/` focuses it and Escape clears it. Chapter navigation restores filtered-out targets. |
| Pager | Previous and next chapter links at the end of each stage. |
| Status and feedback | Visible words for saved, failed, unavailable, learned, and selected states; concise live announcements for updates. Keep helpful errors near the relevant action. |

## Content rules

- Sentence-case headings. Plain words. No emoji.
- Each topic or reading block says what the thing is, why it exists, and what to look up next. Use cards for bounded topics and flowing prose for explanations; avoid excessive borders and repeated labels.
- Add a snippet only when 3 to 8 lines make the idea clearer.
- Every chapter ends with a "Go deeper" line pointing at a real next step.

## Technical rules

- One self-contained HTML file. No CDN scripts, no web fonts, no frameworks. Plain CSS and a small amount of vanilla JS.
- Content lives in static HTML so it reads without JavaScript. JS builds the roadmap, table of contents, pagers, search, and demos from that markup.
- Respect `prefers-reduced-motion`. Keep visible focus rings (2px `--primary`, 3px offset).
- Layout works at phone width with a 16px side gutter and no horizontal page scroll. Dense tables/code may scroll within their own labeled region. Navigation and focused targets must not hide beneath sticky bars.
- Verify both themes and actual text/background combinations, keyboard navigation, visible focus, readable fallback fonts, narrow layouts, and text enlargement. State what was checked; a token checklist alone is not a full accessibility audit.

## Verification handoff preference

Provide concise browser-check instructions and expected outcomes to the user. Do not take over their laptop/browser or use GUI automation unless explicitly requested later. Lightweight source/syntax/contrast checks can support the edit; clearly distinguish those checks from user-run rendering and interaction verification. A manual checklist is available at `docs/testing/manual-checklist.md`.
