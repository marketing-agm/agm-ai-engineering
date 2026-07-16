# AGM Real Estate Group — Product Design & Development · Team Overview

**INTERNAL — team overview material. Private repository. Do not make public.**

A digital micro-site version of AGM Product Design & Development's *Team Overview* (July 2026).
Each section is its own page in a single-file static site (`index.html`, no build step, no
dependencies). Fonts load from Google Fonts; everything else is inline. This repo reuses the design
system built for AGM's proposal micro-sites (multi-family, commercial, HOA).

## What this is
The overview's ten sections, rebuilt as an institutional, navigable micro-site:

1. Overview (TL;DR) · 2. Shipped (with launch links + access) · 3. In Flight · 4. Pipeline ·
5. Tools & Stack · 6. How We Work (principles, where things are documented, why development takes
time) · 7. AI Costs (Anthropic breakdown) · 8. The AppFolio Database API · 9. Claude Premium Seats ·
10. Vendor Cost Basis (Appendix).

Copy is adapted from the source team-overview document. The layout, palette (navy `#00202F`, brand
blue `#3A8DDE`, serif/sans pairing), and rail-and-content structure follow the shared AGM micro-site
design system. Each page adds whitespace and interaction — a per-page navy/blue summary rail,
hover-reactive cards and pills, reveal-on-scroll, prev/next paging, a reading-progress bar, and a
light/dark toggle.

## No access gate
Unlike the proposal micro-sites, **this overview is not password-protected**. There is no
`functions/_middleware.js` cover/login screen — `index.html` is served directly as a static page.
If access control is ever needed, front the Cloudflare Pages project with Cloudflare Zero Trust
Access (email-verified, tied to AGM Google Workspace) rather than re-adding a shared-password gate.

## Local preview
Open `index.html` in a browser. That's it. Deep-link a section with the URL hash, e.g.
`index.html#appfolio`.

## Deploy — Cloudflare Pages (AGM standard pattern)
1. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git** → select this repo.
2. Settings: Framework preset **None** · Build command **(empty)** · Build output directory **/**
3. Every push to `main` auto-deploys production; every branch/PR gets its own preview URL.

## Analytics (PostHog) — optional
The site is instrumented for PostHog but **off by default**. To turn it on, paste your Project API
Key into the marked block in `index.html`'s `<head>` (`window.AGM_POSTHOG_KEY`). Until a real key is
set, no analytics requests are made. Events are tagged with `proposal: aiengineering-overview`.

What it tracks once the key is set:
- **Visits** — a virtual `$pageview` per section (URL carries the `#section` hash).
- **Tab navigation** — a `tab_click` event with `to`, `from`, and `method`.
- **Time on each section** — a `section_time` event when a section is left.
- Plus `autocapture`, session replays, and click/scroll heatmaps.

## Operational notes
- `_headers` enforces `noindex` and security headers at the edge.
- Several figures carry bracketed placeholders (`[ estimate ]`, `[ decision date ]`,
  `[ X hrs/mo ]`, `[ $X ]`, `[ one-liner in progress ]`) — fill these in as details are confirmed.
- **Shipped page:** each product has a `Launch ↗` link with `href="#"` and an `[ add link ]` note —
  drop in the live URLs before presenting. Login credentials are **not** stored in this repo; share
  them separately.
- **AI Costs page:** per-line `[ $X ]` figures come from the Anthropic Console (Usage & Billing).
- Cost figures (vendor cost basis, AppFolio API pricing, Claude seat pricing) reflect the source
  document; update per the latest quotes before circulating.
- The footer logos are shared AGM brand assets at `/assets/agm-logo-black.svg` and
  `/assets/agm-logo-white.svg`.
