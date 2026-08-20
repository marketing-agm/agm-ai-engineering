# AGM Real Estate Group | Product Design & Development | Team Overview

**INTERNAL. Team overview material. Private repository. Do not make public.**

A micro-site version of the AGM Product Design & Development team overview (July 2026). Each
section is a page in a single-file static site (`index.html`). There is no build step and no
dependencies. Fonts load from Google Fonts; everything else is inline. The repository reuses the
design system built for the AGM proposal micro-sites (multi-family, commercial, HOA).

## Contents
Eleven sections:

1. Overview
2. Operating Model
3. Corporate Library
4. Tool Stack
5. Adoption Risks
6. Open Items
7. AppFolio Database API
8. Claude Premium Seats
9. In Production
10. In Development
11. Planned Work

Section 3 carries the records standard for the Corporate Library: the proposed folder structure for
all three division trees, the document tagging system, the file naming convention, and the retention
clock. It is a proposal for review, not built work, and it closes on the two decisions it asks
leadership for: how far to take the naming convention, and confirmation of the tag list. Its
retention periods are the team's reading of Washington statute and are marked as unreviewed by
counsel.

Sections 4 through 6 carry the budget request. Section 4 opens each tool with what the product does
and where it is used today, then states list pricing for every tier of Slack, Granola, Figma, and
Asana, the capability differences between tiers, and the basis for the tier selected, each followed
by the argument against it and by what the tier does not address. The Slack request additionally
carries a comparison with Microsoft Teams and a table of the systems connected to the workspace.
Section 5 states the risks to consistent use and the maintenance time proposed against them.
Section 6 records the two items already discussed verbally: Claude API credits and the AppFolio Database API.

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
  `[ decision date ]`, `[ hours per month ]`, `[ amount ]`. Section 6 requires a usage baseline for
  the monthly Claude credit figure and the current balance for the top-off figure. Section 7
  requires measured hours of manual AppFolio entry.
- Section 4 costs the four licenses at 5, 10, and 35 seats. Only the 5-seat case corresponds to a
  known list of users, being current development team headcount; the other two are comparison
  scenarios with no agreed scope. Totals are the per-seat rate multiplied by seat count. If a rate
  changes after a vendor quote, both the annual and the monthly table need updating, along with the
  month-to-month comparison in the footnote beneath them.
- Section 5 was written before Asana was added as a fourth license, so its upkeep table originally
  named only Granola, Slack, Figma, and Claude. An Asana row was added when the two were merged.
  Any further tool added to section 4 needs a matching row here, or the deck requests a license
  with no stated upkeep.
- The Function and Current use pair that opens each tool in section 4 distinguishes measured use
  from prospective use. Slack and Granola are in use and are described as such. Figma is in use for
  marketing and business development only, and Asana has no seats in use; both say so, and their
  stated value is marked prospective. Move a tool out of prospective wording only when it is
  actually deployed.
- The Slack "Connected systems" table was read from the AGM workspace on 13 August 2026. The
  AppFolio row is recorded from the team's own description when the channel was created on 15 July
  2026, not from an observed message, which its disclosure states. Move the Monday.com and
  Cloudflare rows from Planned to Live as they are configured. The table deliberately quantifies
  nothing: no baseline was captured before the channels existed, so time saved cannot be stated.
- The Slack and Microsoft Teams comparison names no seat counts, deliberately. The workspace held 6
  members on 13 August 2026 while section 4 costs 5 seats as current development team headcount.
  Reconcile those two figures before presenting, and keep any headcount out of the comparison so
  the seat basis is stated in one place only.
- Figma is costed at the Full seat rate only. Figma also sells Dev and Collab seats at lower rates
  within the same plan, which is disclosed in the section 4 Figma footnote and flagged in the
  scenario note as a reason the 35-seat Figma figure runs high.
- Third-party pricing in section 4 is vendor list pricing, verified 13 August 2026 against vendor
  pricing pages and cross-checked against independent pricing summaries. Every tool section links
  its vendor pricing page in the footnote, and section 4 closes with a consolidated source list
  recording what was confirmed and what was not. Re-verify at renewal and before any presentation.
- Claude API rates in section 6 come from the Anthropic rate card rather than a summary. Sonnet 5
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
  upper end of that range. The additional Premium seat in section 8 and the three licenses in
  section 4 are outside that table, which its disclosure states.
- The vendor cost range in section 1 cites 2026 US agency pricing surveys from Clutch and
  GoodFirms, plus list pricing for Glean, Birdeye, Buildout, Proposify, PandaDoc, Domo, and Prophia
  as commercial equivalents. The per-product build estimates that backed this range lived on a
  Vendor Cost Basis appendix page, removed deliberately in commit `1a1c293`. Only the source
  attribution was carried forward; the page was not restored.
- The 31 July 2026 target dates in section 10 come from the source document and have passed. Four
  items need status reconfirmed before the deck is presented, which the note under the table says.
- Section 5 carries four unfilled placeholders for the maintenance block: `[ day ]`, `[ hours ]`,
  `[ who ]`, and `[ owner ]`. The cadence has not been agreed, and neither the block nor the
  quarterly review has been costed in staff hours.
- The access control table in section 9 has `[ add link ]` in every Live URL cell. Credentials are
  distributed separately and must not be committed here.
- Section 3 is transcribed from the team's Excalidraw working diagram. Three things in it are
  unresolved and stated as such in the section: legal sign-off on the retention schedule, which is a
  prerequisite to any automated destruction; the Records Owner role, which the section assumes
  throughout but which has not been assigned; and back-fill of documents already in the Library,
  which is unscoped. The schedule also carries a mandatory review before 1 January 2028, when the
  Washington association chapters are repealed. The folder trees, tag lists, retention codes, and the
  date rule live in `<details>` disclosures; the tag list is closed by design, so a new document type
  is added by the Records Owner rather than improvised at filing time.
- The section adds four style classes used nowhere else: `.pattern` for the file-name pattern,
  `.tree` for the three division trees, `.tag-cols` for the tag lists, and `.legend` for the
  added/unchanged/restricted key. `.tree` and `.legend` define their amber and red variants for
  light and dark separately, so a palette change needs both.
- Section 3 carries six hand-authored inline SVG figures: the four folder levels and the file name
  at the end of the path, the file name banded by which fields are machine-set and which are AI
  proposed, the tag stored in both the name and the metadata column with only the name surviving
  export, the two clocks on a dated timeline, the seven-step pipeline with the line where AI
  authority ends, and the clock-state machine. Every stroke and fill resolves to a design token, so
  the figures follow the light and dark toggle without a second copy, and marker fills are set by
  class because a `<marker>` does not inherit color from the element referencing it. Coordinates are
  hand-placed against the `viewBox`: moving a label means checking it still clears its neighbours,
  since nothing here reflows. Below 760px each figure keeps its drawn size and scrolls inside its own
  box, because scaling an 860-unit viewBox into a phone width renders the labels illegible.
- The figure wrapper class is `.diagram`, not `.fig`. `.fig` was already taken by the figure cell in
  a `comp-table` total row, and using it for the figures silently restyled those cells.
- The footer logos are shared AGM brand assets at `/assets/agm-logo-black.svg` and
  `/assets/agm-logo-white.svg`.
