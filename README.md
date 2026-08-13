# AGM Real Estate Group | Product Design & Development | Team Overview

**INTERNAL. Team overview material. Private repository. Do not make public.**

A micro-site version of the AGM Product Design & Development team overview (July 2026). Each
section is a page in a single-file static site (`index.html`). There is no build step and no
dependencies. Fonts load from Google Fonts; everything else is inline. The repository reuses the
design system built for the AGM proposal micro-sites (multi-family, commercial, HOA).

## Contents
Ten sections:

1. Overview
2. Operating Model
3. Tool Stack
4. Adoption Risks
5. Open Items
6. AppFolio Database API
7. Claude Premium Seats
8. In Production
9. In Development
10. Planned Work

Sections 3 through 5 carry the budget request. Section 3 states list pricing for every tier of
Slack, Granola, and Figma, the capability differences between tiers, and the basis for the tier
selected, each followed by the argument against it and by what the tier does not address. Section 4
states the risks to consistent use and the maintenance time proposed against them. Section 5
records the two items already discussed verbally: Claude API credits and the AppFolio Database API.

Copy is adapted from the source team overview document. Layout, palette (navy `#00202F`, brand blue
`#3A8DDE`, serif and sans pairing), and the rail-and-content structure follow the shared AGM
micro-site design system. Each page carries a per-page summary rail, reveal-on-scroll, prev and
next paging, a reading-progress bar, and a light and dark toggle.

Pricing footnotes, source lists, and counterarguments are collapsed into labeled `<details>`
disclosures (`.disc`) so the main line of each section stays readable. They are native elements
with no JavaScript behind the toggle. A `beforeprint` handler expands every one of them and an
`afterprint` handler restores the previous state, so printing or exporting to PDF captures the full
document rather than the summary labels alone.

## Editorial standard
This deck is read by leadership for a budget decision and retained afterward as reference. Copy
follows a fixed standard. Any edit should hold to it:

- No em dashes.
- Section labels name their subject. Headings are noun phrases with no verb, no colon and tagline,
  and no implied argument.
- Body copy states a fact and its source, then stops. Clauses that exist to land a point rather
  than carry information are cut.
- Tables use one unit per column, stated in the header. Feature strings separated by dots are split
  into the dimensions being compared.
- Measured, estimated, and assumed figures are distinguished explicitly. Costs are stated per seat
  and annualized.
- Vendor tier language is quoted and attributed to the vendor rather than adopted. "Unlimited" is
  the vendor's word.
- Every recommendation names its strongest counterargument and what it does not solve.
- Supporting detail sits in collapsible disclosures rather than inline blocks. The summary label
  states what is inside, so a counterargument is visible as present without being read. Labels
  therefore have to be literal: "Argument against Pro, and what it does not address", never a
  neutral word like "Details" or "More". A disclosure that hides the existence of a counterargument
  breaks the rule above.

## No access gate
Unlike the proposal micro-sites, this overview is not password-protected. There is no
`functions/_middleware.js` cover or login screen; `index.html` is served directly as a static page.
If access control becomes necessary, front the Cloudflare Pages project with Cloudflare Zero Trust
Access, which is email-verified and tied to AGM Google Workspace, rather than re-adding a
shared-password gate.

## Local preview
Open `index.html` in a browser. Deep-link a section with the URL hash, for example
`index.html#appfolio`. The hash is read on page load only; changing it without a reload does not
switch sections.

## Deploy: Cloudflare Pages
1. Cloudflare dashboard, then **Workers & Pages > Create > Pages > Connect to Git**, then select
   this repository.
2. Settings: Framework preset **None**, Build command **(empty)**, Build output directory **/**
3. Every push to `main` deploys production, **provided the project's production branch is set to
   `main`**. Check this under Settings, Build, Production branch. If it points at a feature branch,
   pushes to `main` build successfully but are labeled Preview and the live site does not change.
   Every other branch and pull request receives a preview URL.

## Analytics (PostHog), optional
The site is instrumented for PostHog and is off by default. To enable it, paste the Project API Key
into the marked block in the `<head>` of `index.html` (`window.AGM_POSTHOG_KEY`). Until a real key
is set, no analytics requests are made. Events are tagged with `proposal: aiengineering-overview`.

Tracked once the key is set:
- **Visits.** A virtual `$pageview` per section. The URL carries the `#section` hash.
- **Tab navigation.** A `tab_click` event with `to`, `from`, and `method`.
- **Time per section.** A `section_time` event when a section is left.
- Autocapture, session replays, and click and scroll heatmaps.

## Operational notes
- `_headers` enforces `noindex` and security headers at the edge.
- Bracketed placeholders mark figures that are not yet filled in: `[ estimate ]`,
  `[ decision date ]`, `[ hours per month ]`, `[ amount ]`. Section 5 requires a usage baseline for
  the monthly Claude credit figure and the current balance for the top-off figure. Section 6
  requires measured hours of manual AppFolio entry.
- Section 3 costs the three licenses at 5, 10, and 35 seats. Only the 5-seat case corresponds to a
  known list of users, being current development team headcount; the other two are comparison
  scenarios with no agreed scope. Totals are the per-seat rate multiplied by seat count. If a rate
  changes after a vendor quote, both the annual and the monthly table need updating, along with the
  month-to-month comparison in the footnote beneath them.
- Figma is costed at the Full seat rate only. Figma also sells Dev and Collab seats at lower rates
  within the same plan, which is disclosed in the section 3 Figma footnote and flagged in the
  scenario note as a reason the 35-seat Figma figure runs high.
- Third-party pricing in section 3 is vendor list pricing, verified 13 August 2026 against vendor
  pricing pages and cross-checked against independent pricing summaries. Every tool section links
  its vendor pricing page in the footnote, and section 3 closes with a consolidated source list
  recording what was confirmed and what was not. Re-verify at renewal and before any presentation.
- Claude API rates in section 5 come from the Anthropic rate card rather than a summary. Sonnet 5
  is $2.00 input and $10.00 output; the previously scheduled increase to $3.00 and $15.00 was
  cancelled and the introductory rate is now standard.
- The least corroborated figures in the deck are the two Granola Basic-plan limits, 30-day rolling
  note access and a 25-meeting lifetime cap. Both come from third-party summaries and are marked as
  such in the Granola footnote.
- AppFolio and Claude seat costs reflect the source document. Update against current quotes before
  circulating.
- Section 2 carries an itemized tooling spend table taken from the source team overview document.
  The annual column is computed from the monthly figures rather than quoted, giving a total of
  $7,440 to $8,040. The approximately $8,000 per year figure used in the Overview metrics is the
  upper end of that range. The additional Premium seat in section 7 and the three licenses in
  section 3 are outside that table, which its disclosure states.
- The vendor cost range in section 1 cites 2026 US agency pricing surveys from Clutch and
  GoodFirms, plus list pricing for Glean, Birdeye, Buildout, Proposify, PandaDoc, Domo, and Prophia
  as commercial equivalents. The per-product build estimates that backed this range lived on a
  Vendor Cost Basis appendix page, removed deliberately in commit `1a1c293`. Only the source
  attribution was carried forward; the page was not restored.
- The 31 July 2026 target dates in section 9 come from the source document and have passed. Four
  items need status reconfirmed before the deck is presented, which the note under the table says.
- Section 4 carries four unfilled placeholders for the maintenance block: `[ day ]`, `[ hours ]`,
  `[ who ]`, and `[ owner ]`. The cadence has not been agreed, and neither the block nor the
  quarterly review has been costed in staff hours.
- The access control table in section 8 has `[ add link ]` in every Live URL cell. Credentials are
  distributed separately and must not be committed here.
- The footer logos are shared AGM brand assets at `/assets/agm-logo-black.svg` and
  `/assets/agm-logo-white.svg`.
