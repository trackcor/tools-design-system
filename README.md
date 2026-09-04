# Trackcor Tools Design System

Tokens, components and screen references for **Trackcor Tools**, the managed tooling platform for mine sites. Modern SaaS ERP register: clean, calm, plenty of white.

**Live site:** [trackcor.github.io/tools-design-system](https://trackcor.github.io/tools-design-system/)

| What | Where |
|---|---|
| **The design system** | [index.html](https://trackcor.github.io/tools-design-system/) — the Claude Design canvas itself, rendered |
| Tokens, the source of truth for the app | `project/tokens.css` |
| Component classes | `project/components.css` |
| CSS reference page | [tokens.html](https://trackcor.github.io/tools-design-system/tokens.html) — the same tokens as plain CSS |

---

## For coding agents

**Read `project/tokens.css` before introducing any colour, spacing or typography in [trackcor/tools](https://github.com/trackcor/tools).**

The Angular app vendors these tokens into `src/styles.scss`. When the app and this repo diverge, **the app wins**: backport the change here.

### The two rules that govern everything

**1. The primary blue never carries status meaning.** Foreman blue `#2A5EBF` was chosen from three candidates because it holds as an 11px label, a 6px progress fill and a 1px focus ring without reading as a state. `#27406E` sits too near ink so the focus ring stops registering on a sunlit screen; `#3B7DE8` is bright enough that a blue progress fill starts reading as a status of its own.

**2. Semantic colour and rigging period colour are separated by shape, not hue.** Period colours are physical tape on a sling, so they cannot be recoloured to suit the palette.

- A **period** is a 16px **square** plus a mono period name, and only ever appears inside a band or a cell labelled as a period.
- A **status** is a **circle** plus a sentence-case word, and never a square.

A red square means the item passed inspection in the red quarter. A red dot means the item is withheld. **The two never appear in the same column.**

### The brand device

Marketing uses a red short rule, a gold long rule and heavy condensed caps. Red there competes with *withheld*, and gold at that weight competes with *warning*. The device survives into the product; the red does not.

The short rule becomes ink, gold darkens to `#B08A2E`, and it is permitted in **exactly one place**: a 2px rule under a page title. Gold never appears as a fill, a dot, text or a background, and warning never appears as a rule. The two cannot be mistaken because they never share a shape.

### Fonts and icons

**Geist** and **Geist Mono** (Vercel), loaded from Google Fonts. Geist Mono is for asset numbers, stage names, system values and timestamps. **Tabular lining numerals everywhere**, non-negotiable.

**Lucide** icons at 1.75 stroke width. Icons appear in navigation, buttons, empty states and affordances. **An icon never carries status on its own**, because a supervisor on a sunlit screen needs the dot and the word.

### Not in this system

No dark mode in v1: tokens are structured so it is possible later, but do not implement it. No component library in feature screens. No landing dashboard (Today replaces it), no tile grids of counts, no charts that do not change a decision, no chat interface, no illustrations inside the app, and no red as a decorative or background colour anywhere.

### Source layout

```
project/
├── index.html      ← the Claude Design canvas, the design system itself
├── support.js      ← the canvas runtime it loads
├── tokens.css      ← start here for code, every --tc-* token
├── base.css        ← reset, type roles, focus, tabular numerals
├── components.css  ← .tc-* product UI
├── tokens.html     ← CSS reference page, built from the tokens
└── favicon.svg
```

`index.html` is the authored design and is the thing to look at. The three CSS files are the same decisions expressed as code, for the Angular app to vendor; they are derived from the canvas, not the other way round. If the two ever disagree, **the canvas is the design and the CSS is the bug.**

The canvas published here has client names replaced (the primary blue is named Foreman rather than a client site, and sample rows use generic sections). The unedited original is in the private [trackcor/tools](https://github.com/trackcor/tools) repo under `design/canvas/`.

---

Design by Claude Design, September 2026. Built by [Obsydian Technologies](https://obsydiantechnologies.com) for Trackcor Africa.
