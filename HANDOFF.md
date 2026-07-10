# Handoff — Portfolio Site

Single-page static portfolio for Davide Scognamiglio. GitHub Pages target. No build, no framework, no backend.

**Last updated:** 2026-07-10 (post-overdrive + audit pass)

---

## Files

| File | Purpose |
|---|---|
| `index.html` | Entire site. Inline CSS + JS. ~1420 lines. The only file that ships. |
| `PRODUCT.md` | Impeccable strategic doc (register=brand, users, principles). Read-only for agents. |
| `DESIGN.md` | Full visual design system (Google Stitch format). North Star: "The Lab Notebook." |
| `.impeccable/design.json` | Impeccable sidecar: tonal ramps, motion tokens, 6 component snippets, narrative. schemaVersion:2 |
| `.impeccable/live/config.json` | Live mode: `files:["index.html"]`, `insertBefore:"</body>"`, no CSP. |
| `assets/resized_avatar.png` | Profile photo. Hero byline (40px) + About sidebar (180px). |
| `assets/slow_video.mp4` | Hero background video, ~6MB, `opacity:0.09`. |
| `reference.html` | OLD 5.3MB MuSA report — color-palette source only. NOT part of site. |
| `style.css`, `script.js` | DEAD from earlier multi-file version. Safe to delete. |

---

## Architecture

- **Theme**: light default (warm ivory, OKLCH hue ~80). Dark = `[data-theme="dark"]` on `<html>`, toggled via nav button, persisted in `localStorage` key `theme`.
- **Fonts**: `system-ui` stack (SF Pro on Apple). Mono = `ui-monospace`/SF Mono. Zero web font loads.
- **Sections**: hero → about → research → publications → projects → experience → contact → footer.
- **Motion**: `.r` reveal class via IntersectionObserver (5px/500ms ease-out). `prefers-reduced-motion` global kills all animations via `animation-duration:.01ms!important`. Hero video hidden under reduced-motion.
- **Accent**: Instrument Teal `oklch(37% 0.13 185)` light / `oklch(74% 0.08 185)` dark. Used sparingly (active nav, pub years, research track labels, email link, project card top-border-on-hover). Never >10% of any viewport.

## Design System (DESIGN.md)

- **Creative North Star**: "The Lab Notebook" — flat surfaces, ruled separations, mono metadata, type hierarchy does all lifting.
- **Color strategy**: Restrained — warm-tinted near-white base, near-black ink, single teal accent.
- **OKLCH throughout**: every color via CSS token. Never hardcoded hex/rgb.
- **Named rules**: One-Accent Rule, Dual-World Rule, No-Shadow Rule, Italic Em Rule, Mono-for-Data Rule.
- **Anti-patterns banned**: gradient text, glassmorphism, hero-metric template, side-stripe borders >1px, numbered section eyebrows, identical card grids.
- **Dark mode**: fully committed alternate world (cool hue 255, near-midnight blue-black). NOT a tonal inversion.

## Token Reference (CSS variables, `:root` / `[data-theme="dark"]`)

| Token | Light | Dark |
|---|---|---|
| `--bg` | `oklch(97.5% 0.007 80)` | `oklch(9.2% 0.005 255)` |
| `--bg-raised` | `oklch(95.5% 0.009 80)` | `oklch(12.5% 0.006 255)` |
| `--bg-float` | `oklch(93% 0.010 80)` | `oklch(16.5% 0.005 255)` |
| `--line` | `oklch(88% 0.007 75)` | `oklch(21% 0.005 255)` |
| `--line-2` | `oklch(76% 0.009 75)` | `oklch(33% 0.006 255)` |
| `--ink` | `oklch(12% 0.009 80)` | `oklch(95% 0.003 255)` |
| `--ink-2` | `oklch(42% 0.008 80)` | `oklch(68% 0.007 255)` |
| `--ink-3` | `oklch(48% 0.007 80)` | `oklch(55% 0.006 255)` |
| `--accent` | `oklch(37% 0.13 185)` | `oklch(74% 0.08 185)` |
| `--ease-out` | `cubic-bezier(.16,1,.3,1)` | same |
| `--nav-h` | `52px` | same |
| `--r` | `10px` | same |
| `--wrap` | `1080px` (1200px at 1400px+) | same |

---

## Hero Overdrive (scroll-driven parallax)

Implemented: Direction B — cinematic parallax. CSS-only, browser-native, zero JS.

**What it does (desktop Chrome/Edge/Safari 16+ only, gated behind `@supports(animation-timeline:scroll())` + `@media(min-width:769px)`):**
- Hero is `140svh` tall (instead of `100svh`).
- `.hero-inner` is `position:sticky; top:calc(var(--nav-h) + 4rem)` — content pins in viewport while the user scrolls through the hero.
- `.hero-video` has a scroll-driven zoom: `scale(1)→scale(1.1) translateY(-5%)` over the full 140svh range. `translateY(-5%)` is the geometric maximum before the video bottom exposes the hero background; `-14%` was tried but left a 12.6svh gap.
- Hero content layers exit via staggered `hero-layer-exit` animation (opacity:1→0, translateY:0→-44px) on `scroll(root)` timeline:
  - `.hero-byline`: 78–114svh
  - `.hero-actions`: 80–116svh
  - `.hero-body`: 84–122svh
  - `.hero-intro`: 86–124svh
  - `h1.hero-h`: 92–132svh (headline lingers longest)
- Scroll cue: 1px gradient line, `position:fixed`, appears after 2s delay, hides on first 30px scroll via JS.

**Critical bug that was fixed (2026-07-10):**
`#hero { overflow:hidden }` (base CSS) intercepts `position:sticky` — per CSS spec, sticky sticks to the nearest ancestor with a scroll mechanism, which includes `overflow:hidden` even if it doesn't scroll. Fix: in the `@supports` block, `#hero` gets `overflow:visible; clip-path:inset(0)`. `clip-path:inset(0)` clips the scaled video overflow visually without creating a scroll container.

**Reduced motion:**
- Global block (`@media(prefers-reduced-motion:reduce)`) sets `animation-duration:.01ms!important` on all elements. Hero video `display:none`.
- Inner block (inside `@supports`) restores `#hero` to `display:flex; min-height:100svh`, `position:relative` on `.hero-inner`, all animations to `none!important`.

---

## Live Data (ORCID + GitHub APIs, CORS, no auth)

### Publications — DONE
- Endpoint: `https://pub.orcid.org/v3.0/0009-0007-5163-0327/works`
- IntersectionObserver lazy-load (200px rootMargin). `sessionStorage` cache key `orcid_works_v1`.
- Shimmer skeleton while loading, error state with ORCID fallback link.
- Sorted year desc. Title → DOI link.
- Container: `#pub-list`. Render function injected via IIFE in `<script>` block.

### Projects — STILL STATIC ⚠️ (pick up here)
- 4 static `.proj` cards exist in HTML. Need to be replaced with GitHub API live pull.
- Endpoint: `https://api.github.com/users/davide-scognamiglio/repos?per_page=100&sort=updated`
- **EXCLUDE `test-datasets` repo** (explicit user instruction).
- Cache in `sessionStorage` key `gh_repos_v1` (mirror orcid pattern).
- Unauth GitHub = 60 req/hr per IP. Fine for portfolio.
- Skip forks (`fork:true`). Skip repos with no description (noise).
- Keep MuSA featured/first (it's the published pipeline — either pin it hardcoded or sort by stars desc).
- Field map: `name` → card title, `description` → card body, `html_url` → link, `language` → `.ldot-*` dot, `stargazers_count` + `forks_count` → optional meta.
- Existing lang dot classes: `.ldot-py` (Python), `.ldot-nf` (Nextflow/Groovy), `.ldot-js` (JS/TS), `.ldot-r` (R). Add fallback for unknowns.
- Skeleton: reuse `.proj-skel` CSS + `@keyframes shimmer` (already exists from pub skeleton).
- Container already has `id="proj-api-slot"` with `aria-live="polite"`.
- Pattern to follow exactly: the ORCID IIFE in the `<script>` block around line 1310.

### Career — DONE
- Fetches ORCID employment. `#exp-list` container. Same shimmer pattern.

---

## Audit Status (2026-07-10)

Score: **15/20 — Good** (all P0/P1 fixed this session).

| Severity | Issue | Status |
|---|---|---|
| P0 | Hero sticky broken by `overflow:hidden` | **FIXED** |
| P1 | Dark mode `--ink-3` WCAG AA fail (2.4:1) | **FIXED** → 55% (4.6:1) |
| P1 | `hero-intro border-left:1.5px` side-stripe ban | **FIXED** (removed) |
| P2 | Touch targets: nav-link/theme-btn/nav-toggle <44px | **FIXED** via `@media(pointer:coarse)` |
| P3 | Parallax bottom gap at translateY(-14%) | **FIXED** → -5% |

No open P0/P1/P2 issues. Remaining: none (P3 were all fixed).

---

## Known Placeholders

- `assets/cv_davide_scognamiglio.pdf` — referenced by CV buttons but **file not present**. User must supply.
- Hero stats (if still present) are hardcoded — verify accuracy with user.
- ORCID `0009-0007-5163-0327` — confirmed correct.
- Contact email: `davide.scognamiglio@ior.it`.

---

## User Context

- **Title**: Bioinformatician (NOT engineer, NOT developer).
- **Affiliations**: IRCCS IOR Bologna (primary) + PhD candidate, Data Science & Computation, UNIBO.
- **Research tracks**: (1) rare disease genomics + variant annotation pipelines; (2) IMU/inertial sensor analysis for clinical motion studies.
- **Published**: MuSA (BMC Bioinformatics 2026), BMJ Open IMU, Sci Reports 2025 IMU, Int J Cardiology 2026.
- **Audience**: peer researchers, clinicians, potential collaborators, PhD supervisors. Technically literate, skeptical of decoration.
- **Brand voice**: "Precise, understated, curious." No marketing copy. No buzzwords. No numbered eyebrows.

---

## Recommended Next Commands

```
/impeccable craft GitHub projects live pull    # highest-value remaining task
/impeccable critique index.html               # scored UX review (hasn't been run since overdrive)
/impeccable polish index.html                 # final pre-ship pass
```
