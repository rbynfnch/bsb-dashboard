# Brooks Steel Buildings monthly dashboard

Monthly SEO / AEO / GEO and lead report for brookssteelbuildings.com.
Open `index.html` in a browser (no server needed). **Brooks report** is the client view; **Audit** is internal.
"Save report as PDF" prints only the Brooks view (choose "Save as PDF" in the print dialog).

## Each month
1. `npm i googleapis` (once), then `node scripts/pull-google.mjs YYYY-MM` writes GA4 + Search Console data to `data/auto/`.
   Credentials come from `GOOGLE_APPLICATION_CREDENTIALS_JSON` (single-line service-account key) or
   `GOOGLE_APPLICATION_CREDENTIALS_BASE64`. Defaults: GA4 property `542996053`, Search Console `sc-domain:brookssteelbuildings.com`,
   quote event `form_submit`, phone event `contact_link_click` (override with `QUOTE_EVENT` / `PHONE_EVENT`).
   Add `--diagnose` to list events and check what the quote and phone events really count.
2. Copy `data/TEMPLATE.json` to `data/manual/YYYY-MM.json` and fill in: Google Business Profile numbers,
   PageSpeed / index / backlink numbers, the AI-answer prompt panel results, Brooks's lead outcomes
   (`"leads": {"received":0,"qualified":0,"won":0}`; leave `null` until he reports), and the narrative bullets.
3. `node scripts/build-data.mjs` then reload `index.html`.

## Sample data
`node scripts/make-sample.mjs` fills `data/` with clearly flagged sample data for layout review.
Delete `data/auto/*` and `data/manual/*` before real use.

## Privacy
`data/` is git-ignored so real metrics and credentials are never committed. Never commit service-account keys.
The pull script is untested against live APIs until its first real run.

## Metric split
Brooks sees outcomes (quote requests, calls, conversion, search clicks, AI answer visibility, Business Profile
actions, lead-to-customer) plus the narrative. The Audit view holds diagnostics (form funnel, spam, landing pages,
striking-distance keywords, technical health, AI crawler hits, competitor citations).
