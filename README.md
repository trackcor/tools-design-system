# Trackcor Tools Design System

Tokens, components and screen references for **Trackcor Tools**, the managed tooling platform for mine sites. Modern SaaS ERP register: clean, calm, plenty of white.

**Live site:** [trackcor.github.io/tools-design-system](https://trackcor.github.io/tools-design-system/)

| What | Where |
|---|---|
| Design system reference | [index.html](https://trackcor.github.io/tools-design-system/) |
| Tokens, the source of truth | `project/tokens.css` |
| Component classes | `project/components.css` |
| Original Claude Design canvas | Private, in `trackcor/tools` at `design/canvas/` |

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
├── tokens.css      ← start here, every --tc-* token
├── base.css        ← reset, type roles, focus, tabular numerals
├── components.css  ← .tc-* product UI
├── index.html      ← the reference page rendered from the tokens
└── favicon.svg
```

The original Claude Design canvas (`.dc.html` plus `support.js`) is kept in the private [trackcor/tools](https://github.com/trackcor/tools) repo under `design/canvas/`, because it carries client names that do not belong in a public repository.

---

Design by Claude Design, September 2026. Built by [Obsydian Technologies](https://obsydiantechnologies.com) for Trackcor Africa.
