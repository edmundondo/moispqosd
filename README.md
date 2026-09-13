# moispqosd

Public demo for the Mozambique ISP Tracker — crowdsourced quality-of-service ratings,
live status reports and speed tests for Mozambique's internet providers, sourced from
company disclosures and press reporting (INCM does not publish a consolidated
operator report we could source for this build).

Sibling of [zwispqosd](https://github.com/edmundondo/zwispqosd) (Zimbabwe),
[bwispqosd](https://github.com/edmundondo/bwispqosd) (Botswana) and
[saispqosd](https://github.com/edmundondo/saispqosd) (South Africa) — same codebase
pattern, same shared Supabase backend (multi-tenant via a `site` column, `mz` for
this site), different country data. See `zwispqosd`'s README/SETUP docs for the full
technical background on how the backend, live feeds (IODA) and speed test work —
nothing about that plumbing is Mozambique-specific.

Formatted report exports (PDF/CSV/EPUB) will live on a privileged `moispqosp`
backend once it's built — not here. This demo, like its siblings, ships with no
export/download options anywhere on the page.

## Provider data

Four ISPs/operators, in order. The regulator is **INCM** (Instituto Nacional das
Comunicações de Moçambique, https://www.incm.gov.mz/), which does not publish a
consolidated operator directory or per-operator subscriber table we could find for
this build — so unlike the Zimbabwe/Botswana sites, most of this list's figures are
`null` with an honest note, rather than a regulator-sourced number.

1. **Vodacom Moçambique** — majority owned by Vodacom Group (South Africa; itself
   majority-owned by Vodafone Group plc, UK); local shareholders include Intelec
   Holdings and the Emotel consortium (exact stakes unconfirmed). Mobile & fixed
   (2G/3G/4G/5G, fixed broadband, M-Pesa mobile money). The only operator on this
   list with a published subscriber figure: **12.4 million customers as of 31 March
   2025** (FY2025 results), reported by 360mozambique.com on 2025-05-26 — a
   company-published number, not an INCM-verified count, and flagged as such in the
   page's `note`/`subLabel`.
2. **Movitel** — joint venture of Viettel Group (Vietnam, state-owned) and SPI
   Gestão e Investimentos (Mozambican company); exact ownership split unconfirmed.
   Mobile & fixed wireless, with the widest rural/district coverage of any operator
   (127+ district centers) and its own fiber backbone. No published current
   subscriber count found.
3. **Tmcel** (Moçambique Telecom, S.A.) — 100% Mozambican state-owned. Formed
   January 2019 from the merger of TDM (fixed) and Mcel (mobile) — these are **not**
   two separate current companies, and this site doesn't list them as such. Mobile,
   fixed-line voice and fixed broadband. No published current subscriber count
   found.
4. **TVCABO Moçambique** — majority-owned by Visabeira Group (Portugal); a 2024
   report referenced Visabeira "seeking an 80% stake," implying it wasn't yet fully
   consolidated at that level as of that report — exact current stake unconfirmed.
   Fixed/fibre & cable broadband plus pay-TV, primarily in urban areas (Maputo,
   Beira, Matola, Nampula). No published subscriber count found.

Because the data model here only has two filterable categories (`Mobile` and
`Fixed/Wireless`), Vodacom Moçambique, Movitel and Tmcel are all tagged `Mobile`
(their primary consumer service), and TVCABO Moçambique is tagged `Fixed/Wireless` —
the same simplification the other three sites already use for operators with more
than one line of business. The fuller service description for each stays in its
`note` field.

All seed/sample QoS ratings, live-status reports, speed tests and switch/signup
stories are small, clearly-illustrative sample data (5–8 entries per category) for a
fresh site with no real users yet — not fabricated as if they were real crowdsourced
history. Vodacom Moçambique's entries reflect its real published 12.4M-subscriber
scale only in the `note`/`subLabel` text; the individual seed rows themselves are
still illustrative samples.

## Languages

Portuguese is Mozambique's **sole official language** (Constitution, Article 10).
Emakhuwa, Xichangana, Cinyanja, Elomwe, Cisena, Echuwabo, Cindau and Xitswa are
recognised **national languages** (Constitution, Article 9) that the state promotes
as part of the country's cultural and educational heritage — they are **not**
official languages, and this site is careful not to blur that distinction anywhere
in its copy. The eight national languages (plus their approximate 2017-census
speaker counts) are sourced from Wikipedia's "Languages of Mozambique" article; the
underlying primary source (Mozambique's INE 2017 census) could not be independently
verified in this research pass.

All nine ship as chips (English + Portuguese + the eight national languages above):

- **Portuguese (`pt`)** ships with a genuine, hand-written best-effort draft
  translation of every UI string — none reviewed by a native speaker yet, flagged
  as such in the code, exactly like every other non-English language in this
  family, even a well-resourced one like Portuguese.
- **Cinyanja (`ny`)** reuses `zwispqosd`'s existing Chewa (`ny`) I18N block
  verbatim — Chewa and Cinyanja/Nyanja are the same standard language (ISO 639-3
  `nya`), so this is legitimate reuse, not fabrication. Only the outward-facing
  label changed ("Cinyanja" instead of "Chewa"); the language code stays `ny` so
  the reused content slots straight in.
- **Xichangana (`ts`)** reuses `zwispqosd`'s existing Shangani (`ts`) I18N block
  verbatim, flagged explicitly as **lower confidence** — Xichangana and Shangani
  are closely related Tswa-Ronga cluster languages, not a confirmed identical
  standard, the same treatment `saispqosd` already gives its own Xitsonga/Shangani
  reuse. The language code stays `ts`.
- **Cindau (`ndc`)** was *meant* to reuse `zwispqosd`'s existing Ndau (`ndc`)
  content — the Ndau people span the Zimbabwe–Mozambique border, so this would have
  been legitimate reuse. However, `zwispqosd`'s own `ndc` block is itself still an
  empty placeholder in the v1.2.0 baseline this site was built from — there was
  nothing yet to reuse. Cindau therefore ships blank too, with a code comment
  explaining why, rather than a guessed translation.
- **Emakhuwa (`vmw`), Elomwe (`ngl`), Cisena (`seh`), Echuwabo (`chw`) and Xitswa
  (`tsc`)** have no cross-border shortcut and no verified translation source, so
  they ship as chips with literally empty I18N objects. They fall back cleanly to
  English via the existing `tt()`/`t()` helper with the standard "🚧 need
  translation" badge — nothing was guessed to fill the gap.
- **Important:** Xitswa (Tswa) is a **distinct** language from Xichangana/Tsonga
  despite the similar-sounding name, and is deliberately **not** filled in from the
  Xichangana/Shangani content — conflating the two would repeat a known mistake
  pattern from earlier in this project (Zimbabwe's Ndebele vs. South Africa's
  isiNdebele).

The suggest/endorse community-translation flow covers all nine languages today.

## What's different about this site (v1.0.0 scope)

- **No backbone (RIPEstat/ASN) badges.** `ISP_ASN` is intentionally empty — no
  verified ASN-to-operator mapping has been compiled for Mozambique yet. The badge
  simply doesn't render for any ISP without an entry, the same graceful fallback
  the Zimbabwe site already relies on for its own untracked ISPs.
- **No Cloudflare Radar national benchmark.** That feature calls a Supabase Edge
  Function that's hardcoded server-side to Zimbabwe's numbers only (and is a
  separately-tracked, not-fully-verified feature even there) — rather than build a
  second country-specific proxy sight-unseen, it's simply never invoked on this
  site (`refreshRadarBenchmark()` stays defined but uncalled at the bottom of
  `index.html`).
- **No phone-prefix ISP detection.** `PHONE_ISP_PREFIXES` starts empty — no
  verified INCM numbering-plan-to-carrier mapping was available for this build.
  `normalizePhone`/`isValidPhone` do understand Mozambique's numbering shape
  (9-digit mobile numbers starting with `8`, dialled internationally as `+258`).
- Provider list is intentionally small (4 tracked providers) and seed
  ratings/status/speed data is small and clearly illustrative (5–8 entries per
  category), not a real crowdsourced history — this is a fresh site with no real
  users yet.
- No export/download options anywhere on this page — matches the established,
  export-free public-demo pattern across the whole family.

See `CHANGELOG.md` for version history.
