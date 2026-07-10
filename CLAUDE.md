# Claude Code — Portfolio Context

**Read HANDOFF.md first.** It has the full technical state, audit status, token reference, and pending tasks.

## This project

Single-page static portfolio for Davide Scognamiglio (Bioinformatician, IRCCS IOR + UNIBO PhD). GitHub Pages target. No build, no framework, no backend. Everything is in `index.html` (inline CSS + JS, ~1420 lines).

## Design system

Full design system in DESIGN.md. Impeccable sidecar in `.impeccable/design.json`. Key constraints:

- **Impeccable-enforced bans** (match-and-refuse): side-stripe borders >1px, gradient text, glassmorphism, hero-metric template, identical card grids, numbered section eyebrows.
- **One accent only**: Instrument Teal `oklch(37% 0.13 185)` light / `oklch(74% 0.08 185)` dark. Never >10% viewport.
- **No shadows.** No hardcoded hex/rgb — OKLCH tokens only.
- **Dark mode** is a committed alternate world (cool blue-black), not a tonal inversion.

## Critical technical knowledge

**DO NOT add `overflow:hidden` to `#hero`** — it breaks `position:sticky` on `.hero-inner` (CSS spec: overflow:hidden creates a scroll container that captures sticky even when non-scrolling). The fix is `overflow:visible; clip-path:inset(0)` in the `@supports(animation-timeline:scroll())` block. This is documented in HANDOFF.md → Hero Overdrive section.

**`console.warn` calls are intentional** — ORCID/GitHub API error handlers, not debug artifacts. Do not remove.

## What ships

Only `index.html` + `assets/` (resized_avatar.png, slow_video.mp4). Everything else is dev context.

## Highest-priority pending task

GitHub projects live pull — replace 4 static `.proj` cards with GitHub API fetch. Full spec in HANDOFF.md → Projects section.

## Impeccable skill

If this project has the impeccable plugin loaded:
```
/impeccable craft GitHub projects live pull
/impeccable critique index.html
/impeccable polish index.html
```
