# Trackcor Tools Design System

Tokens, components and screen references for **Trackcor Tools**, the managed tooling platform for mine sites. Modern SaaS ERP register: clean, calm, plenty of white.

**Live site:** [trackcor.github.io/tools-design-system](https://trackcor.github.io/tools-design-system/)

| What | Where |
|---|---|
| **The design system** | [index.html](https://trackcor.github.io/tools-design-system/) — the Claude Design canvas itself, rendered |
| **The mobile canvas** | [mobile/](https://trackcor.github.io/tools-design-system/mobile/) — the same system on iOS and Android |
| Tokens, the source of truth for the app | `project/tokens.css` |
| Component classes | `project/components.css` |
| Mobile delta, tokens and classes | `project/mobile/mobile.css` |
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
├── support.js      ← the canvas runtime it loads, shared with the mobile canvas
├── tokens.css      ← start here for code, every --tc-* token
├── base.css        ← reset, type roles, focus, tabular numerals
├── components.css  ← .tc-* product UI
├── tokens.html     ← CSS reference page, built from the tokens
├── favicon.svg
└── mobile/
    ├── index.html        ← the mobile canvas, iOS and Android side by side
    ├── mobile.css        ← the --tcm-* delta and .tcm-* classes, layered on tokens.css
    ├── ios-frame.jsx     ← device chrome the canvas draws the screens inside
    └── android-frame.jsx
```

`index.html` is the authored design and is the thing to look at. The three CSS files are the same decisions expressed as code, for the Angular app to vendor; they are derived from the canvas, not the other way round. If the two ever disagree, **the canvas is the design and the CSS is the bug.**

The canvas published here has client names replaced (the primary blue is named Foreman rather than a client site, and sample rows use generic sections). The unedited original is in the private [trackcor/tools](https://github.com/trackcor/tools) repo under `design/canvas/`.

---

## Mobile

The field app is a **sibling, not a second system**. Same tokens, same semantics, same voice. [mobile/index.html](https://trackcor.github.io/tools-design-system/mobile/) is the canvas: five screens, each drawn on both platforms, with the platform delta named beside it.

The app is deliberately narrow. It carries only the jobs that cannot wait for a signal: the counter, recovery capture in the field, section audit, and a read-only view for a person holding tools. There is no dashboard here, no reporting, no admin and no client portal. Those assume a desk and a signal.

**The one rule that governs the whole app: never block the person in front of you.** Not on network, not on sync, not on a photo upload, not on a confirmation. If the app cannot do something now, it says so, queues it, and lets them carry on.

### Shared, and not negotiable

- Foreman blue `#2A5EBF` for action and navigation, **never for status**. Same rule as the web.
- Status is a **circle plus a sentence-case word**, 12px dot, 17px word, with the derivation printed beneath it.
- The commit bar is **56px and full width, in the bottom third** on both platforms.
- Geist and Geist Mono, and no layout that depends on their metrics.

### iOS owns

- The 34px home indicator, which the commit bar clears with padding rather than a spacer.
- Back as a labelled chevron in the top left, mirroring the swipe.
- A white on grey numeric pad with a 1px key lip.
- The status bar, which our header sits 60px below.

### Android owns

- The gesture pill, drawn in the frame, so the commit bar clears 14px and no more.
- Back as a bare arrow, because the gesture is the real affordance.
- A flat Gboard numeric pad with no key shadow.
- No app bar. The Trackcor title block replaces it, so the two products read alike.

### What changes from the web, and why

The environment is the constraint, not the screen size. Direct equatorial sun, dust, gloves, one free hand, a twelve-hour shift and no signal for hours at a time.

- **Touch targets are 56px on anything that commits custody**, not the 48px the web allows, and never adjacent to another target. Secondary actions are 52px and outlined.
- **Primary actions live in the bottom third.** This inverts the web, where the primary sits top right. Nothing that matters goes in a top corner.
- **The type scale steps up.** 16px body, 17px status word, 25px screen title, 32px mono for an asset number under confirmation.
- **Offline is a state, not an error.** A persistent band with a queue count. Never a toast, never a full-screen spinner, never a raw backend error.
- **The queue is counted in two lanes.** Custody transactions are recorded on the device the moment the clerk confirms; photos are large, sync last and block nothing. The split is visible so a photo backlog never reads as unrecorded custody.
- **A refusal takes the commit slot.** Blocked is not an error, so there is no red background and no error iconography. It is not an iOS alert and not an Android dialog, because both can be dismissed without choosing a path.
- **The camera is a component, not a screen.** 196px, cornered, torch pill inside it, with manual entry visible in the same glance. Typing an asset number is not a fallback: 408 tools carry no tag at all.
- **Battery discipline.** The camera surface only warms while its step is on screen, and nothing repaints when the screen is idle.

### For coding agents working in the mobile app

Load `project/tokens.css` first, then `project/mobile/mobile.css`. The delta file redefines **no colour**, because the palette does not change between platforms. It defines `--tcm-*` sizes, insets and targets, and `.tcm-*` classes for the shell: commit bar, offline band, status line, refusal panel, capture surface, queue lanes.

The two device frames in `mobile/` are canvas scaffolding, the OS chrome the screens are drawn inside. They are not product components and nothing in the app should import them.

---

Design by Claude Design, September 2026.
