---
name: Davide Scognamiglio Portfolio
description: "Single-page research portfolio for a bioinformatician; flat, type-forward, live-data-powered."
colors:
  bg: "oklch(97.5% 0.007 80)"
  bg-raised: "oklch(95.5% 0.009 80)"
  bg-float: "oklch(93% 0.010 80)"
  line: "oklch(88% 0.007 75)"
  line-2: "oklch(76% 0.009 75)"
  ink: "oklch(12% 0.009 80)"
  ink-2: "oklch(42% 0.008 80)"
  ink-3: "oklch(48% 0.007 80)"
  accent: "oklch(37% 0.13 185)"
  accent-bg: "oklch(37% 0.13 185 / 0.07)"
  accent-tag: "oklch(37% 0.13 185 / 0.09)"
typography:
  display:
    fontFamily: "system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif"
    fontSize: "clamp(2.9rem, 6.5vw, 6rem)"
    fontWeight: 600
    lineHeight: 1.0
    letterSpacing: "-0.04em"
  headline:
    fontFamily: "system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif"
    fontSize: "clamp(1.75rem, 3vw, 2.5rem)"
    fontWeight: 600
    lineHeight: 1.1
    letterSpacing: "-0.03em"
  body:
    fontFamily: "system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif"
    fontSize: "1rem"
    fontWeight: 400
    lineHeight: 1.7
  label:
    fontFamily: "ui-monospace, 'SF Mono', SFMono-Regular, Menlo, Consolas, monospace"
    fontSize: "0.6875rem"
    fontWeight: 400
    letterSpacing: "0.04em"
rounded:
  sm: "6px"
  md: "10px"
  pill: "20px"
spacing:
  section: "96px 0"
  prose: "64ch"
  wrap: "1080px"
components:
  button-solid:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.bg}"
    rounded: "{rounded.md}"
    padding: "0.6rem 1.1rem"
  button-solid-hover:
    backgroundColor: "{colors.ink-2}"
    textColor: "{colors.bg}"
  button-outline:
    backgroundColor: "transparent"
    textColor: "{colors.ink-2}"
    rounded: "{rounded.md}"
    padding: "0.6rem 1.1rem"
  button-outline-hover:
    backgroundColor: "{colors.bg-raised}"
    textColor: "{colors.ink}"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.ink-3}"
    rounded: "{rounded.md}"
    padding: "0.6rem 0.25rem"
  proj-card:
    backgroundColor: "{colors.bg}"
    rounded: "{rounded.md}"
    padding: "1.5rem"
  proj-card-hover:
    backgroundColor: "{colors.bg}"
  tag:
    backgroundColor: "transparent"
    textColor: "{colors.ink-3}"
    rounded: "{rounded.pill}"
    padding: "0.2rem 0.5rem"
  tag-accent:
    backgroundColor: "{colors.accent-tag}"
    textColor: "{colors.accent}"
    rounded: "{rounded.pill}"
    padding: "0.2rem 0.5rem"
---

# Design System: Davide Scognamiglio Portfolio

## 1. Overview

**Creative North Star: "The Lab Notebook"**

This system reads like a working research document: precise, analytical, every element functional. The visual grammar is flat surfaces, ruled separations, monospace metadata, and type hierarchy that does all the lifting. No shadows. No gradients. No chrome that is not also content. The accent color is a measurement marker; it appears where something needs to be noted, not where something wants to look good.

Typography is system-native (SF Pro on Apple, Segoe on Windows, the best sans available everywhere else) used with intent: one tight scale, two weights, one mono stack for labels. The design defers to the platform on rendering quality while controlling scale, spacing, and color absolutely. Two themes exist as fully committed alternate worlds, not tonal inversions: light is warm (hue 80 ivory), dark is cool (hue 255 near-midnight blue-black).

This system explicitly rejects startup SaaS aesthetics (glassmorphism, gradient text, hero stat grids), developer portfolio templates (neon glow, numbered section eyebrows, purple-teal gradients), and flashy futuristic portfolios (canvas motifs, animated scan lines, grain overlays). The correct reference is peer-reviewed confidence: the work is the proof, the format stays out of the way.

**Key Characteristics:**
- Flat by default: depth comes from whitespace and type scale, never from shadows.
- Tonal warmth via background tint (hue 80), not via warm accent colors.
- Dark mode is a fully committed alternate world, not a color inversion.
- Live data (ORCID + GitHub APIs) means graceful skeleton states, never blank sections.
- Motion is purposeful: staggered load entrance, scroll reveals, scroll-driven parallax. All disabled cleanly under `prefers-reduced-motion`.

## 2. Colors: The Instrument Palette

Restrained strategy: warm-tinted near-white base, near-black ink, one muted accent used sparingly.

### Primary
- **Instrument Teal** (`oklch(37% 0.13 185)`): The single accent. Active nav states, publication year labels, project card hover borders, research track labels, email link. Its rarity is structural: if it appears in more than ~10% of any viewport, it has lost its role. Dark mode version: `oklch(74% 0.08 185)` (lighter, lower chroma on the dark surface).

### Neutral
- **Warm Vellum** (`oklch(97.5% 0.007 80)`): Page background. Warm-tinted near-white (hue 80, chroma 0.007) — enough warmth to read as deliberate, not enough to read as ivory. Dark mode: `oklch(9.2% 0.005 255)` — near-midnight blue-black.
- **Raised Surface** (`oklch(95.5% 0.009 80)`): Elevated backgrounds, hover states. Gains meaning next to Warm Vellum; nearly indistinguishable in isolation.
- **Float Surface** (`oklch(93% 0.010 80)`): Tinted sections (About, Contact use `.tinted`). Third step of tonal layering.
- **Near-Black Ink** (`oklch(12% 0.009 80)`): Headings and high-priority text. Warm-tinted to avoid harshness against Warm Vellum.
- **Body Ink** (`oklch(42% 0.008 80)`): Body prose. Meets WCAG AA against Warm Vellum.
- **Muted Ink** (`oklch(48% 0.007 80)`): Subheadings, captions, metadata. Meets WCAG AA.
- **Primary Line** (`oklch(88% 0.007 75)`): Section dividers, card borders, timeline separators.
- **Secondary Line** (`oklch(76% 0.009 75)`): Stronger borders (button outlines, avatar border).

### Named Rules
**The One-Accent Rule.** Instrument Teal is the only accent. Never as a background for large regions, never in gradients, never at full opacity on surfaces. Its sole role is annotation: it marks something to notice. When in doubt, use `var(--ink)` weight contrast instead of adding a second hue.

**The Dual-World Rule.** Light and dark mode are not tonal inversions. Light is warm (hue 80); dark is cool (hue 255, near-midnight blue-black). Do not create "warm dark mode" variants.

## 3. Typography

**Display Font:** System UI (`system-ui, -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Arial, sans-serif`) — SF Pro on Apple, Segoe UI on Windows.
**Body Font:** Same system stack.
**Label/Mono Font:** `ui-monospace, 'SF Mono', SFMono-Regular, Menlo, Consolas, monospace`

**Character:** One family in two weights (400 body, 600 headings), one mono stack for data labels. No decorative faces. The design trusts the platform to render the native typeface at its best; it controls scale, spacing, and color absolutely. Mono appears only where data-like precision is needed: year labels, language tags, metadata chips.

### Hierarchy
- **Display** (600, `clamp(2.9rem, 6.5vw, 6rem)`, line-height 1.0, letter-spacing -0.04em): Hero headline only. One per page. Often contains an italic weight-300 `<em>` for the qualifier clause.
- **Headline** (600, `clamp(1.75rem, 3vw, 2.5rem)`, line-height 1.1, letter-spacing -0.03em): Section h2. The italic `<em>` pattern applies here too.
- **Title** (500-600, 1rem-1.0625rem, line-height 1.4-1.5): Card titles, publication titles, nav brand name.
- **Body** (400, 1rem, line-height 1.7, max 64ch): Prose sections. `text-wrap: pretty` encouraged for widow control.
- **Label** (400, 0.625rem-0.75rem, letter-spacing 0.02em-0.04em, mono): Publication years, language tags, metadata, chip/tag text. Always mono stack.

### Named Rules
**The Italic Em Rule.** Section headings (h2) often split into a weight-600 plain clause and a weight-300 italic qualifier via `<em>`. This is a structural move: confident statement, poetic qualifier. Limit to one `<em>` per heading; do not use italic emphasis on body prose for decoration.

**The Mono-for-Data Rule.** Monospace appears only on data-derived labels: ISO years, programming language names, statistical metadata. Not on navigation, not on body prose, not on headings.

## 4. Elevation

This system is flat. No `box-shadow` declarations exist on cards, containers, or hover states. Depth comes from:
- Tonal surface layering (`--bg` → `--bg-raised` → `--bg-float`), ~2-4 lightness points per step
- `1px solid var(--line)` borders to establish containment without elevation
- Whitespace and section padding (96px) to separate content zones

The navigation bar uses `0 1px 0 var(--line)` as a bottom border at rest; `backdrop-filter: blur(20px)` for the frosted overlay. No other blur or shadow exists.

### Named Rules
**The No-Shadow Rule.** If you reach for `box-shadow` on a card or hover state, use a border transition to `var(--line-2)` instead. The only permitted blur is `backdrop-filter` on the nav and mobile drawer, where it is structural (signals the fixed overlay), not decorative.

## 5. Components

### Buttons
Small, functional, visually quiet. Three variants sharing font, size, and padding. Shape: gently rounded at 10px, not pill, not square.
- **Solid:** `background: var(--ink); color: var(--bg)`. Hover: opacity 0.85. Press: `transform: scale(0.98)`.
- **Outline:** `background: transparent; color: var(--ink-2); border: 1px solid var(--line-2)`. Hover: background `var(--bg-raised)`, color `var(--ink)`.
- **Ghost:** No background, no border. `color: var(--ink-3)`. Used for low-priority inline actions.
- **Focus:** Global `outline: 2px solid var(--accent); outline-offset: 3px` on `:focus-visible`.

### Tags / Chips
Two variants; both display-only (no hover, no press state).
- **Default:** Transparent background, `1px solid var(--line)`, `var(--ink-3)` text, 20px pill radius, mono 0.625rem, letter-spacing 0.02em.
- **Accent** (research track labels): `background: var(--accent-tag); color: var(--accent); border: none`. Signals a named category within the work, not a generic keyword.

### Project Cards
- **Corner Style:** 10px radius.
- **Background:** `var(--bg)`.
- **Border:** `1px solid var(--line)` at rest; on hover, `border-top: 1.5px solid var(--accent)`. The top-border accent on hover is the primary hover signal. No background change, no shadow.
- **Shadow Strategy:** None.
- **Internal Padding:** 1.5rem (24px).
- **Language dot:** 8px circle, color-coded per language family: Python blue, Nextflow/Groovy teal (same as accent), JS/TS amber, R steel-blue.

### Publication Rows
- **Style:** Two-column grid (54px year column + 1fr content). Year in mono accent. Title + authors + journal in the content column. Full-width `1px solid var(--line)` separators top and bottom (no card wrapper).
- **Hover:** Background shifts to `var(--bg-raised)` with a 0.15s transition.

### Navigation
- **Height:** 52px desktop, 48px mobile. Fixed top, full width.
- **Background:** `color-mix(in oklch, var(--bg) 85%, transparent)` with `backdrop-filter: blur(20px)`.
- **Links:** 0.8125rem system font, weight 400, 6px radius hover/active backgrounds. Active link: color `var(--accent)`, weight 500.
- **Mobile drawer:** Uses `opacity + visibility + pointer-events` (not `display:none`). Opens from top with 0.18s ease-out, `translateY(-6px)` entry.
- **Scroll progress bar:** 1px height, `var(--accent)` color, `transform: scaleX()` driven by scroll position (not `width` — avoids layout reflow).

### Skeleton Shimmer (Signature Component)
All three live-data sections show shimmer skeletons while fetching (publications, projects, career).
- **Keyframes:** `@keyframes shimmer` — linear-gradient from `var(--bg-raised)` through `var(--bg-float)` back to `var(--bg-raised)`, `background-size: 200%`. Animated 1.4s linear infinite.
- Publication skeleton: two rows of gradient bars at 40% and 90% width.
- Project skeleton: three card-shaped placeholder blocks.
- Career skeleton: two timeline-row-shaped blocks.
- Skeletons are replaced in-place when the API response arrives; the render function adds `.in` class directly to bypass the IntersectionObserver (which runs once at load and cannot see dynamically injected elements).

## 6. Do's and Don'ts

### Do:
- **Do** use `var(--accent)` (Instrument Teal) on a maximum of ~10% of any viewport's visual surface. Rarity is structural.
- **Do** express depth via tonal surface steps (`--bg` → `--bg-raised` → `--bg-float`) and ruled `1px var(--line)` borders.
- **Do** use the italic `<em>` pattern on display and headline elements for qualifier clauses only; one `<em>` per heading maximum.
- **Do** restrict mono (`--fm`) to data-derived labels: years, language names, numeric metadata.
- **Do** add `.in` directly in JavaScript when rendering dynamic content from ORCID or GitHub APIs, since the IntersectionObserver reveal fires once at load.
- **Do** verify WCAG AA (at least 4.5:1) for any new text color in both light and dark themes.
- **Do** provide skeleton shimmer states for any section that loads asynchronously.
- **Do** use `transform: scaleX()` (not `width`) for animated progress bars and horizontal reveals.
- **Do** use `opacity + visibility + pointer-events` (not `display:none`) for drawers and overlays that need smooth transitions.

### Don't:
- **Don't** add `box-shadow` to cards, containers, or hover states. Use a `1px solid var(--line-2)` border transition instead.
- **Don't** use gradient text (`background-clip: text` combined with a gradient). Use `var(--accent)` as a solid color.
- **Don't** use glassmorphism decoratively. `backdrop-filter` is structural on the nav and mobile drawer only.
- **Don't** add numbered section markers (01 / 02 / 03) or tiny all-caps tracked eyebrows above section headings.
- **Don't** use canvas-motif backgrounds, neon glows, animated scan lines, grain overlays, or particle systems.
- **Don't** write startup SaaS copy ("powerful", "seamless", "next-generation", "cutting-edge"). The voice is specific and measured.
- **Don't** introduce a second accent color. Instrument Teal is the only one. Use weight contrast for additional emphasis.
- **Don't** use `border-left` or `border-right` greater than 1px as a colored accent stripe on cards, callouts, or list items.
- **Don't** toggle mobile nav visibility with `display:none`. Use the `opacity + visibility` pattern with `pointer-events`.
- **Don't** make dark mode warm-tinted. Dark mode uses cool hue 255 (near-midnight blue-black), not dark warm ivory.
