# Changelog

All notable changes to the Mozambique ISP Tracker are recorded here. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning follows
[Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

The version number shown here matches the `<meta name="app-version">` tag in
`index.html` and the `v{version}` badge in the page's footer.

## [1.0.0] — 2026-09-13

Baseline versioned release. Built from `zwispqosd`'s v1.2.0 (no-exports) template,
following the same pattern already validated for `bwispqosd` (Botswana) and
`saispqosd` (South Africa).

### Added
- `index.html` — full interactive tracker for Mozambique: 4 tracked providers
  (Vodacom Moçambique, Movitel, Tmcel, TVCABO Moçambique), crowdsourced QoS
  ratings, live status reports, 24h-rolling speed rankings, and a "proof of
  impact" switch/signup panel — all backed by the shared Supabase project
  (`site: "mz"`).
- Nine-language translate panel: English (base/fallback) + Portuguese (official)
  + Emakhuwa, Xichangana, Cinyanja, Elomwe, Cisena, Echuwabo, Cindau and Xitswa
  (national languages). See README.md "Languages" for exactly which languages
  ship with a genuine draft, which reuse existing family content, and which are
  intentionally blank.
- Cross-browser compatibility banner (unchanged from the shared template):
  feature-detects `fetch`, `Promise`, `localStorage`, and CSS grid/flexbox
  support; points visitors to `lite.html` if anything's missing.
- `mz_`-prefixed localStorage keys throughout (device id, submit log, cached
  reports/conversions/status/speed/translations/referrals, language
  preference) so this site's local data never collides with a sibling site's
  in a shared browser.
- Version tracking: `<meta name="app-version">` on `index.html`, a footer
  version badge, and this changelog.

### Scope notes (intentional, not bugs)
- `ISP_ASN` and `PHONE_ISP_PREFIXES` ship as empty objects — no verified
  ASN-to-operator or numbering-plan-to-carrier mapping was available for this
  build. Both degrade gracefully (no badge / no phone-based suggestion) exactly
  as designed.
- The Cloudflare Radar national-bandwidth benchmark is **not** enabled on this
  site: the underlying Supabase Edge Function is hardcoded server-side to
  Zimbabwe's numbers only, so `refreshRadarBenchmark()` is left defined but is
  never called at the bottom of `index.html`.
- INCM does not publish a consolidated operator/subscriber report, so three of
  the four providers carry `subscribers: null` with an explanatory `note`
  rather than a guessed figure. Only Vodacom Moçambique has a citable
  subscriber count, and it's a company-published number (FY2025 results via
  360mozambique.com), flagged as such rather than presented as INCM-verified.
- Seed QoS ratings, live-status reports, speed tests and switch/signup stories
  are small (5–8 entries per category) and clearly illustrative sample data for
  a fresh site with no real users yet — not a real crowdsourced history.
- No export/download options anywhere on this page, matching the established
  export-free public-demo pattern across the whole `*ispqosd` family.

### Not yet translated
Emakhuwa, Elomwe, Cisena, Echuwabo, Cindau and Xitswa are not yet available as
translations on `index.html` — see README.md for why (either no reliable
translation source exists yet, or, for Cindau specifically, the Zimbabwe-site
content it was meant to reuse is itself still an empty placeholder as of this
build). They're listed as chips and dropdown options but fall back to English
with a "🚧 need translation" badge until real drafts exist.

<!--
Template for the next entry — copy this when you ship a change:

## [1.1.0] — YYYY-MM-DD
### Added / Changed / Fixed / Removed
- ...
-->
