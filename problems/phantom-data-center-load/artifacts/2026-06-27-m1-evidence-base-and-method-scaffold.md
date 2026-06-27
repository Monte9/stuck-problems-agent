# M1 — Evidence base and method scaffold

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M1 (evidence base + reconciliation method).
**Date:** 2026-06-27.
**Author:** generator (autonomous loop).

This artifact does two things and only two things: (1) it assembles a sourced, reachability-checked inventory of the open datasets and reports the later milestones (M2–M5) will draw on, and (2) it defines the reconciliation *method* — the explicit phantom categories, the source-derived signal that detects each, and a formula/decision rule linking inputs to a phantom-fraction estimate. **No phantom fraction or GW estimate is computed here**; that is M2/M3 work. Numbers below appear only to characterize the sources and to calibrate the method's benchmark haircuts.

---

## 1. Source inventory

All URLs checked for reachability on 2026-06-27 via `curl` (HTTP status code shown) and, where the body was machine-readable, via WebFetch content extraction. "Access status" = `yes` if the canonical public URL returned a usable document. Two LBNL host mirrors (`emp.lbl.gov`, `escholarship.org`) return **HTTP 403 to automated user-agents** (bot-block, not paywall); the **same report is fully public at OSTI (HTTP 200)**, which is listed as the primary LBNL URL. That distinction is flagged honestly in the table.

| # | Source name | Publisher | Date | URL | Geographic / RTO coverage | What variable it supplies | Access (reachable yes/no) |
|---|---|---|---|---|---|---|---|
| S1 | *Queued Up: 2025 Edition* (Tech. Report, OSTI biblio 3008763) | Lawrence Berkeley National Laboratory (Rand, Seel, Wiser et al.) | 2025-12-15 | https://www.osti.gov/biblio/3008763 | National (~50+ grid operators, ~97% of US capacity) | **Generation** queue completion/withdrawal base rates (13% / 77% / 10%, 2000–2019 cohort); active queue GW by tech | yes (200) |
| S1b | *Queued Up: 2025 Edition* landing page | LBNL Energy Markets & Planning (EMP) | 2025-12-15 | https://emp.lbl.gov/publications/queued-2025-edition-characteristics | National | Same report (landing/abstract) | **no (403 to bots)** — bot-blocked, not paywalled; use S1 (OSTI) |
| S2 | 2026 PJM Load Forecast Report | PJM Interconnection | 2026-01-14 | https://www.pjm.com/-/media/DotCom/library/reports-notices/load-forecast/2026-load-report.pdf | PJM RTO (13 states + DC) | PJM **large-load forecast adjustments** in GW; near-term downward revisions after data-center vetting | yes (200) |
| S3 | "ERCOT's large load queue jumped almost 300% last year" | Utility Dive (reporting Dec 2025 ERCOT board data) | 2026-01-06 | https://www.utilitydive.com/news/ercots-large-load-queue-jumped-almost-300-last-year-official/808820/ | ERCOT (Texas) | ERCOT **large-load queue total GW (~233 GW)**, % data center (>70%), YoY growth (~300%), official "won't all materialize" statement | yes (200) |
| S4 | System Planning & Weatherization Update, item 16.2 (ERCOT board) | ERCOT | 2025-12-02 | https://www.ercot.com/files/docs/2025/12/02/16.2-System-Planning-and-Weatherization-Update_Revised.pdf | ERCOT (Texas) | Primary-source ERCOT large-load queue GW + tech/stage composition (data center 72.9% of ~225.8 GW) | yes (200; PDF binary, machine-parse needed in M2) |
| S5 | Data Center Outlook ("Stop Saying Half…" research) | Currence (formerly Sightline Climate); author O. Wang | 2026-02-24 | https://www.currence.ai/blog/data-center-outlook | National (project-level, ~777 projects) | **Announced-vs-under-construction GW** gap by year (2026: ~16 GW announced / ~5 GW building; 2027 peak ~31 GW; 190 GW total) | yes (200; 301 redirect from sightlineclimate.com) |
| S6 | "Phantom data centers didn't break the power grid…" | POWER Magazine; author Tom Bailey (VP Energy, Flexential) | 2026-05-15 | https://www.powermag.com/phantom-data-centers-didnt-break-the-power-grid-they-proved-it-was-already-broken/ | National + PJM + Houston (CenterPoint) | Benchmark anchors: PJM auction $2.2B→$16.4B; Exelon 22%-materialize; CenterPoint 1→25 GW; retail +8.25% US / +19.35% VA | yes (200) |
| S7 | "US Data Centers: How Much Energy Do They Really Use?" | World Resources Institute (WRI) | 2025-09-17 | https://www.wri.org/insights/us-data-centers-electricity-demand | National | Qualitative mechanism of duplicate/speculative filings (same project, multiple utilities); defines "phantom" load | yes (200) |
| S8 | LEI Data Center Demand report (commissioned by SELC) | London Economics Intl. for Southern Environmental Law Center | 2025-07-07 | https://www.selc.org/wp-content/uploads/2025/07/LEI-Data-Center-Final-Report-07072025-2.pdf | Southeast (GA, AL, NC, SC) | Probabilistic materialization benchmark: ~10 GW utility projection vs **3.5–5.5 GW most-likely** (~0.2% / 1-in-500 odds for full 10 GW) | yes (200) |
| S9 | "FERC issues six show-cause orders on data-center interconnection" | Utility Dive | 2026-06-22 | https://www.utilitydive.com/news/ferc-doe-data-center-interconnection/823360/ | CAISO, ISO-NE, MISO, NYISO, PJM, SPP (FERC-jurisdictional RTOs) | Regulatory context: per-RTO large-load rules ordered 2026-06-18, 60-day response; cost-shift / co-location issues | yes (200) |
| S10 | "Experts say utilities' projected data center growth is speculative" | Southern Environmental Law Center | 2025 (press/news) | https://www.selc.org/news/experts-say-data-center-growth-is-speculative/ | Southeast US | Developer over-filing ratio ("5–10× more requests than centers built"); regulatory-incentive framing | partial (403 to bots; companion PDF S8 carries the numbers) |
| S11 | *Queued Up: 2025 Edition* (eScholarship mirror) | UC eScholarship / LBNL | 2025-12-15 | https://escholarship.org/uc/item/7gt1c2gh | National | Same report (secondary mirror) | **no (403 to bots)** — listed for provenance; use S1 |

**Inventory self-check vs. M1 done-criteria:**
- Distinct sources with a *working public URL*: S1, S2, S3, S4, S5, S6, S7, S8, S9 = **9 reachable** (≥ 8 required). S1b, S10, S11 are listed for honesty/provenance but are not counted toward the 8.
- PJM RTO-specific source: **S2** (and S6 for PJM auction). ✔
- ERCOT RTO-specific source: **S3 + S4** (S4 is primary ERCOT board material). ✔
- LBNL Queued Up 2025 with specific stats: **S1**, quoted verbatim in §2. ✔

---

## 2. LBNL *Queued Up: 2025 Edition* — exact statistics (the completion/withdrawal base rate)

Quoted from S1 (LBNL, *Queued Up: 2025 Edition*, OSTI 3008763, published 2025-12-15, data as of end of 2024):

> "Only **13%** of capacity that submitted interconnection requests from **2000–2019** had reached commercial operations by the end of 2024; **77%** of that capacity had been **withdrawn** and **10%** was still active." (S1)

Supporting figures from the same report (S1):
- "~**10,300 projects** actively seeking grid interconnection in the U.S., representing **1,400 GW of generation** and approximately **890 GW of storage**" as of end-2024. (S1)
- Total active queue volume fell **~12% year-over-year**; active natural gas capacity rose to **136 GW (+72% YoY)** while solar (956 GW, −12%), storage (890 GW, −13%) and wind (271 GW, −26%) fell. (S1)
- Median time from interconnection request to commercial operation "has doubled from <2 years for projects built in 2000–2007 to over 4 years for those built in 2018–2024." (S1)

**Critical scope caveat (load on the method):** the 13%/77% base rate is for **generation** interconnection, not **large-load** interconnection. Large-load (data-center) queues are newer; no comparable 20-year load-completion rate exists yet. The method (§3) therefore uses the LBNL generation rate only as an **upper-bound prior on developer-side attrition behavior**, blended with load-specific anchors (S5, S6, S8), never as a direct load haircut. This is the single most important methodological honesty point in M1.

---

## 3. Method — reconciliation of announced vs. real load

### 3.0 Notation (used by all categories; consumed in M2/M3)

- `A_r` = gross **announced** large-load / data-center figure for RTO `r`, in GW, before any de-duplication (built in M2 from S2/S3/S4).
- `P_r` = phantom fraction for RTO `r` ∈ [0,1]; `Real_r = A_r · (1 − P_r)`.
- Phantom is decomposed into three **non-overlapping** components combined as **survival (multiplicative) haircuts**, not additive, to avoid double-subtracting the same MW:

```
Real_r = A_r · (1 − d_r) · (1 − s_r) · (1 − b_r)
P_r    = 1 − (1 − d_r)(1 − s_r)(1 − b_r)
```

where `d_r` = duplication fraction, `s_r` = no-site-control/no-offtake speculative fraction, `b_r` = announced-vs-building double-count fraction. Each haircut is given as a **low / central / high** triple in M3; M1 fixes only the *rule* and the *benchmark anchor* for each.

Multiplicative composition is deliberate: a project that is a duplicate *and* lacks offtake must not be counted as phantom twice. Order of application is fixed (dedup → speculation → build-stage) so M3 is reproducible.

### 3.1 Category 1 — Duplicate filings across territories / multiple filings with one utility (`d_r`)

- **Mechanism (source):** "A developer can file the same project in multiple utility territories, or multiple times with one utility, because a queue position is cheap and powered land is a tradeable asset." (S7, WRI 2025-09-17)
- **Source-derived detection signal:** project-level cross-match on `{developer/parent company, parcel or substation/point-of-interconnection, requested MW, in-service year}` within and across RTO/utility queues (S2, S3, S4 supply the project rows; S4 is the most granular ERCOT set). A match on POI + MW + year across two filings = candidate duplicate.
- **Decision rule:**
  ```
  duplicate(project_i) = 1  if ∃ project_j (j≠i) with
        same POI/parcel  AND  |MW_i − MW_j| / max(MW_i,MW_j) ≤ 0.10
        AND  same developer-or-parent  AND  in-service year within ±1
  d_r = (Σ MW of all-but-one of each matched cluster) / A_r
  ```
  i.e., keep the largest single filing in each duplicate cluster, treat the rest as phantom. Where developer identity is masked (common in ERCOT large-load filings), fall back to POI+MW+year only and flag the result as a *lower bound* on `d_r`.
- **Benchmark anchor / sanity band:** SELC reports developers submit "**5–10× more requests than actual centers being built**" (S10) — an upper signpost on combined over-filing, used to sanity-check that `d_r` (duplication alone) does not exceed the share attributable to pure duplication vs. genuine speculation.

### 3.2 Category 2 — Projects lacking site control or signed offtake (speculative) (`s_r`)

- **Mechanism (source):** utilities receive "early-phase projects unlikely to be completed" and requests that are "speculative … 'phantom' load that will never be built." (S7). SELC/LEI quantify it: a ~10 GW utility projection had a "**roughly 0.2% chance**" (1-in-500) of fully occurring; the **most-likely** materializing need was **3.5–5.5 GW** (S8).
- **Source-derived detection signal:** queue-stage / milestone flags in RTO data — presence/absence of (a) executed interconnection or large-load agreement, (b) demonstrated site control, (c) financial-security deposit posted. ERCOT large-load tracking distinguishes study-stage from agreement-stage volume (S4); PJM applies its own "improved vetting of requested adjustments for data centers and large loads" which already removed near-term MW (S2).
- **Decision rule (applied to the post-dedup remainder):**
  ```
  s_r = 1 − (MW with executed agreement AND posted security) / (post-dedup MW)
  ```
  Central anchor when stage data is missing: derive from S8 — for the Southeast set, real/announced ≈ (3.5–5.5)/10 = **0.35–0.55**, implying `s_r ≈ 0.45–0.65` central. The LBNL **77% generation-withdrawal** rate (S1) is used only as a *high-end* prior on `s_r`, explicitly down-weighted because it is a generation, not load, statistic (see §2 caveat).
- **Direction of bias:** offtake/site-control status is frequently confidential, so observed "executed-agreement" MW understates real commitment → `s_r` likely **biased high** (over-counts phantom). Flagged in §4.

### 3.3 Category 3 — Capacity double-counted between "announced" and "under construction" (`b_r`)

- **Mechanism (source):** Currence/Sightline Climate finds that of "at least **16 GW** … slated to come online in 2026 … only about **5 GW** is currently under construction" (S5), with "**30–50% of that pipeline … unlikely to come online**" on schedule (S5). The problem brief's "12 GW announced vs 5 GW building" maps to this same dataset (the 12 GW was an earlier 2026 snapshot; current figure is ~16 GW — **see Limitations**).
- **Source-derived detection signal:** ratio of **under-construction GW** to **announced GW** for the same horizon year, from the project-stage tracker (S5). Distinct from `s_r`: this catches MW that is genuinely planned and contracted but timed later than the announced in-service year (a *timing* phantom, not a *will-never-exist* phantom), preventing it from being counted in the wrong year's baseline.
- **Decision rule (applied to the post-dedup, post-speculation remainder for the relevant horizon year):**
  ```
  b_r(year y) = 1 − (under-construction GW for year y) / (announced GW for year y)
  ```
  National anchor for 2026 from S5: `b ≈ 1 − 5/16 = 0.69` gross, bounded by the report's own "30–50% unlikely this year" framing → central `b ≈ 0.30–0.50` for the *current-year* horizon (the 5/16 gross figure includes MW that is real but slips to a later year, so the build-stage *phantom* is the smaller 30–50% band, not 69%). For later horizon years (2027+) the gap widens (S5: 2027 ~31 GW announced) and `b` is re-derived per year.
- **Direction of bias:** "under construction" is observed with a lag and excludes contracted-but-not-yet-broken-ground MW → `b_r` likely **biased high**. Flagged in §4.

### 3.4 Composition and per-RTO application (preview of M2/M3)

For each RTO `r`, M3 will populate the triple `(d_r, s_r, b_r)` low/central/high from the signals above, then compute `P_r` and `Real_r` via the multiplicative formula in §3.0. National roll-up = capacity-weighted aggregation across covered RTOs, with the LBNL ~97%-coverage figure (S1) used to state what fraction of US load the covered RTOs represent. M4 multiplies the *over-build* (announced − real) by cost anchors from S6 (PJM auction $2.2B→$16.4B; per-kW capacity cost). Every haircut in M3 must cite at least one of S1, S5, S6, S8, S10 as its empirical anchor — the method forbids an un-anchored haircut.

---

## 4. Limitations & counter-evidence

1. **LBNL 13%/77% is a generation rate, not a load rate.** The headline base rate (S1) describes power-plant interconnection 2000–2019. Applying it directly to data-center *load* would be a category error; large-load queues are <5 years old and may attrit differently (potentially *less*, because hyperscalers post real capital). The method (§3.2) uses it only as a down-weighted high-end prior. **Counter-evidence:** if data-center developers complete at a higher rate than generators (plausible — fewer permitting/land constraints once site is secured), the true phantom fraction is *lower* than an LBNL-anchored estimate; this biases our central estimate **high**.

2. **Duplicate detection is inferential and likely under-counts.** Developer identity is masked in many ERCOT large-load filings (S4), and the same project can appear under shell entities. POI+MW+year matching (§3.1) will miss split or relabeled filings → `d_r` is a **lower bound** (biases total phantom **low**).

3. **Offtake/site-control status is confidential** (S7, S8). "Executed-agreement MW" understates true commitment, so the speculation haircut `s_r` is likely **biased high** (over-counts phantom). The 0.2%/1-in-500 figure (S8) is a *probabilistic* statement about a specific Southeast utility projection, not a universal materialization rate — it must not be globalized.

4. **Queue snapshots are stale and inconsistently dated.** ERCOT figures are end-2025 board data (S3, S4 — Dec 2025/Jan 2026); PJM is Jan 2026 (S2); Currence is Feb 2026 (S5). Mixing as-of dates can double-count or miss MW. M2 must align horizon years explicitly.

5. **The "12 GW announced vs 5 GW building" anchor moved.** The problem brief cited 12 GW; the current Currence/Sightline Climate figure (S5, 2026-02-24) is **~16 GW announced / ~5 GW building**, and the source **rebranded from Sightline Climate to Currence** (domain redirect verified). The brief also conflated this with the **Sightline Institute** (sightline.org), a *different* organization. M2/M3 must cite the live Currence figure and not the stale brief number.

6. **Counter-evidence that load is real, not phantom.** PJM's own forecast (S2) still projects summer peak rising from 160 GW (2025) to 253 GW by 2046 *after* improved data-center vetting, and ERCOT officials (S3) and FERC (S9) are acting as if a large fraction is real. A robust phantom estimate must survive the fact that sophisticated grid operators, having every incentive to vet, still forecast large net growth — the method's job is to bound the *fraction* that is phantom, not to claim the boom is fictional.

7. **FERC scope vs. ERCOT.** ERCOT is **not FERC-jurisdictional**; FERC's June 2026 show-cause orders (S9) cover CAISO, ISO-NE, MISO, NYISO, PJM, SPP only. The brief's framing of a single "national interconnection standard ended" is imprecise; cost-allocation rules are being set per-RTO and, for ERCOT, by the Texas PUC/SB 6. This affects which decision-maker each milestone's findings address.

---

## 5. Self-verification against M1 done-criteria

- [x] ≥ 8 distinct sources with working public URLs, each with a one-line data note — **9 reachable** (S1–S9), reachability `curl`-checked 2026-06-27.
- [x] PJM (S2, S6) and ERCOT (S3, S4) each have ≥ 1 RTO-specific source.
- [x] LBNL *Queued Up: 2025 Edition* cited with specific 13% / 77% / 10% (2000–2019) figures quoted verbatim (§2), plus 1,400 GW / 890 GW active-queue numbers.
- [x] Method defines 3 distinct phantom categories (§3.1–3.3); each names a specific source-derived signal **and** a formula/decision rule (boxed), with a cited benchmark anchor.
- [x] Every quantitative claim carries an inline (S#) citation; no number appears without a source. Nothing required a `[speculative]` tag in this milestone.
- [x] "Limitations & counter-evidence" section present (§4), with bias directions stated.
