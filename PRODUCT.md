# Product

## Register

brand

## Users

Researchers, clinicians, and potential collaborators who land here via a publication link, a GitHub profile, or a conference mention. They're peers: technically literate, skeptical of decoration. They want to assess quickly whether Davide can solve a specific problem — data analysis, pipeline design, a stalled omics dataset — and decide whether to reach out. Secondary audience: hiring managers and PhD supervisors assessing research profile and software craft.

## Product Purpose

A personal portfolio that communicates scientific depth and software rigor without performing them. Visitors should leave with a clear picture of two research lines (genomics, IMU/motion), a feel for the tools Davide actually builds, and a frictionless way to reach him. Success: a collaborator emails within 48 hours of landing.

Publications and projects are retrieved live (ORCID + GitHub public APIs) so the page never goes stale without manual edits. The site stays a single static `index.html`, fully GitHub Pages compatible — no build step, no backend, no framework.

## Brand Personality

Precise, understated, curious. The voice of someone who thinks carefully and does not oversell.

## Anti-references

- Startup SaaS landing pages (glassmorphism, gradient text, "powerful/seamless/next-gen" copy)
- Developer portfolio templates (numbered section eyebrows, purple/teal neon glow, hero stat grids)
- Academic CVs dumped into HTML (no hierarchy, wall of text)
- Flashy "futuristic" portfolios (canvas motifs, neon glows, animated scan lines, grain overlays) — explicitly rejected during this build in favor of Apple-style restraint

## Design Principles

1. **Typography earns the weight.** Every visual decision routes through type: size, weight, spacing. Color and decoration are used only when type alone cannot do the job.
2. **The work is the proof.** Show real projects, real publications, real GitHub links — pulled live from ORCID and GitHub, not hand-curated marketing. No inflated claims.
3. **Respect the reader's time.** Every section should be skimmable in 10 seconds and deeper in 30. No intros that restate the heading.
4. **Light by default, dark by choice.** Default is a warm ivory light mode; dark mode is equally crafted, not an afterthought. Preference persists via localStorage.
5. **Restraint is not absence.** The accent color, the photo, the motion — all appear, all have a specific role, and all disappear when that role is done.

## Accessibility & Inclusion

WCAG AA minimum. System fonts ensure platform-native rendering quality. All color pairs checked for ≥4.5:1 contrast at body size in both themes. Reduced-motion alternative for all transitions.
