# M3 — State-by-State Shortage / Sidelined-IMG Match

**Milestone:** M3 (sidelined-immigrant-physicians)
**Date:** 2026-06-25
**Input artifacts:** [M1 crosswalk](./2026-06-25-m1-provisional-licensure-crosswalk.md) (50-state + DC provisional-licensure status) and [M2 stranding analysis](./2026-06-25-m2-stranding-defect-analysis.md) (which laws have supply-capping defects).

## What this artifact does

M1/M2 established *where the laws are clean*. This artifact establishes *where the need and the sidelined supply both sit*, so the packet can tell a legislator not just "fix the statute" but "here is how many physicians a clean statute could plausibly unlock in your state, and how that ranks against your shortage." It joins three public datasets:

1. **Shortage** — HRSA's primary-care Health Professional Shortage Area (HPSA) statistics: the population living in designated shortage areas, the percent of need met, and **the number of additional primary-care practitioners HRSA says are needed to remove every HPSA designation in the state**. That last figure is the cleanest available "size of the hole."
2. **Sidelined supply** — the national estimate of **~65,000 fully-trained foreign physicians who cannot practice** (MIRA Coalition figure, as reported by the Massachusetts Medical Society), allocated to states by a transparent proxy because **no measured per-state count of sidelined physicians exists**.
3. **The allocation proxy** — each state's share of the US **foreign-born population** (2024 ACS, via CRS). Sidelined IMGs are overwhelmingly foreign-born and tend to settle near existing immigrant communities, so foreign-born share is the best available distributional proxy. It is an *allocation, not a measurement* — see Methodology and Limitations.

**Headline caveat, stated up front:** the "Plausible unlocked-physician estimate" column is a **capacity-constrained upper-bound plausibility figure, not a forecast.** It says "the shortage could absorb at most this many, and at most this many sidelined IMGs plausibly live here" — it does *not* predict how many will actually be licensed and placed, which depends on board rulemaking, employer willingness, and supervisor availability (the M2 caveats).

---

## State-by-state table (50 rows)

Columns:
- **PC HPSAs** — number of designated primary-care HPSAs in the state (HRSA, as of 3/31/2026).
- **Pop. in HPSA / % need met** — population living in designated primary-care HPSAs, and the percent of primary-care need currently met (lower = worse shortage). (HRSA, 3/31/2026.)
- **Practitioners needed** — additional primary-care physicians HRSA says are needed to remove all the state's HPSA designations (HRSA, 3/31/2026). This is the shortage-size figure used for ranking.
- **Est. sidelined IMGs (basis)** — national 65,000 × (state foreign-born share). **No state-level measured count exists; this is a derived allocation** (formula in Methodology). State foreign-born share shown in parentheses.
- **Shortage-severity rank** — 1 = largest "practitioners needed" (worst absolute hole); 50 = smallest. (Computed.)
- **Plausible unlocked estimate** — `min(est. sidelined IMGs, practitioners needed)` — capacity-constrained match (formula in Methodology). Upper-bound plausibility, not forecast.
- **Notes** — M1/M2 statute status where it bears on whether the unlock can actually happen.

| State | PC HPSAs | Pop. in HPSA / % need met | Est. sidelined IMGs (basis) | Shortage-severity rank | Plausible unlocked est. | Notes (M1/M2 status) | Source(s) |
|---|---|---|---|---|---|---|---|
| Alabama | 132 | 2,468,157 / 63.9% | 299 (national 65k × 0.46% FB share; **no state count — allocated**) | 20 | 287 | M1: **none** (no pathway) — unlock requires passing a law first | HRSA¹; CRS²; MIRA³ |
| Alaska | 338 | 300,563 / 27.5% | 74 (× 0.11% FB; allocated) | 39 | 67 | M1: **none** | HRSA¹; CRS²; MIRA³ |
| Arizona | 302 | 4,735,060 / 41.3% | 1,320 (× 2.03% FB; allocated) | 5 | 889 | M2: Low defect (HB2435, rural-targeted, pending) | HRSA¹; CRS²; MIRA³ |
| Arkansas | 155 | 1,148,837 / 53.0% | 234 (× 0.36% FB; allocated) | 29 | 183 | M2: Low (enacted, HPSA-targeted by design) | HRSA¹; CRS²; MIRA³ |
| California | 682 | 7,613,682 / 53.5% | 14,137 (× 21.75% FB; allocated) | 3 | 1,147 | M2: Low (MPP limited + AB2386 pending); supply far exceeds hole | HRSA¹; CRS²; MIRA³ |
| Colorado | 146 | 1,340,894 / 47.9% | 815 (× 1.25% FB; allocated) | 24 | 227 | M1: **none** | HRSA¹; CRS²; MIRA³ |
| Connecticut | 67 | 1,318,825 / 63.0% | 758 (× 1.17% FB; allocated) | 33 | 152 | M2: bill failed (SB1054) | HRSA¹; CRS²; MIRA³ |
| Delaware | 13 | 518,742 / **9.6%** | 158 (× 0.24% FB; allocated) | 32 | 158 | M1: **none**; worst % need met in 50 states | HRSA¹; CRS²; MIRA³ |
| Florida | 322 | 7,038,468 / 39.9% | 6,992 (× 10.76% FB; allocated) | 1 | **1,446** | M2: Low (enacted SB7016); biggest absolute hole | HRSA¹; CRS²; MIRA³ |
| Georgia | 243 | 2,778,075 / 39.1% | 1,729 (× 2.66% FB; allocated) | 11 | 572 | M2: Medium (enacted SB427, long path + appropriation trigger) | HRSA¹; CRS²; MIRA³ |
| Hawaii | 34 | 605,759 / 66.0% | 349 (× 0.54% FB; allocated) | 40 | 59 | M1: **none** | HRSA¹; CRS²; MIRA³ |
| Idaho | 106 | 510,995 / 47.0% | 163 (× 0.25% FB; allocated) | 37 | 87 | M2: **None found** — cleanest enacted statute | HRSA¹; CRS²; MIRA³ |
| Illinois | 334 | 3,900,461 / 42.3% | 2,538 (× 3.91% FB; allocated) | 7 | 725 | M2: Medium (enacted); MPI: ~12k health-degree brain-waste in IL⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| Indiana | 174 | 2,887,519 / 52.8% | 632 (× 0.97% FB; allocated) | 13 | 436 | M2: None found (enacted, underserved-targeted) | HRSA¹; CRS²; MIRA³ |
| Iowa | 187 | 1,085,543 / 40.5% | 264 (× 0.41% FB; allocated) | 27 | 206 | M2: None found (enacted) | HRSA¹; CRS²; MIRA³ |
| Kansas | 172 | 666,724 / 41.1% | 301 (× 0.46% FB; allocated) | 34 | 121 | M2: None found (HB2251 pending, broadest sponsor) | HRSA¹; CRS²; MIRA³ |
| Kentucky | 265 | 1,842,632 / 30.8% | 309 (× 0.48% FB; allocated) | 14 | 309 | M2: None found (enacted SB137); supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Louisiana | 198 | 2,536,598 / 72.0% | 310 (× 0.48% FB; allocated) | 25 | 223 | M2: Low (enacted, hospital-owned) | HRSA¹; CRS²; MIRA³ |
| Maine | 97 | 249,364 / 57.6% | 85 (× 0.13% FB; allocated) | 46 | 33 | M2: Medium (LD105 pending, rural-GME single channel) | HRSA¹; CRS²; MIRA³ |
| Maryland | 57 | 1,178,186 / 28.6% | 1,389 (× 2.14% FB; allocated) | 21 | 287 | M2: **High** (HB598 academic-tie / SB489 no-conversion, pending) | HRSA¹; CRS²; MIRA³ |
| Massachusetts | 68 | 702,128 / 61.3% | 1,735 (× 2.67% FB; allocated) | 36 | 89 | M2: Medium (enacted); large supply, modest hole | HRSA¹; CRS²; MIRA³ |
| Michigan | 292 | 3,315,162 / 44.9% | 1,010 (× 1.55% FB; allocated) | 10 | 614 | M2: Medium (HB4925 pending); MPI state profile state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| Minnesota | 243 | 1,895,121 / 53.9% | 679 (× 1.04% FB; allocated) | 22 | 272 | M2: Low (enacted HF2, rural/underserved-targeted) | HRSA¹; CRS²; MIRA³ |
| Mississippi | 161 | 1,389,696 / 34.5% | 103 (× 0.16% FB; allocated) | 17 | 103 | M2: High (SB2441, UMMC-tie) vs broad HB313, pending; supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Missouri | 344 | 1,826,146 / **21.0%** | 400 (× 0.62% FB; allocated) | 12 | 400 | M2: bill failed (HB1198); 2nd-worst % need met; supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Montana | 139 | 340,302 / 41.9% | 32 (× 0.05% FB; allocated) | 41 | 32 | M1: **none**; tiny FB pop caps allocation | HRSA¹; CRS²; MIRA³ |
| Nebraska | 137 | 263,455 / 49.1% | 235 (× 0.36% FB; allocated) | 45 | 37 | M2: Medium (enacted LB1212, ~6-yr runway) | HRSA¹; CRS²; MIRA³ |
| Nevada | 79 | 993,903 / 44.8% | 842 (× 1.30% FB; allocated) | 30 | 182 | M2: Low (enacted SB124, underserved-targeted) | HRSA¹; CRS²; MIRA³ |
| New Hampshire | 27 | 196,758 / 78.1% | 109 (× 0.17% FB; allocated) | 49 | 14 | M2: **High** (SB457 residency-tie, pending) | HRSA¹; CRS²; MIRA³ |
| New Jersey | 44 | 795,788 / 83.4% | 3,082 (× 4.74% FB; allocated) | 43 | 39 | M2: None found (A3987 broad, pending); huge supply, small hole | HRSA¹; CRS²; MIRA³ |
| New Mexico | 104 | 997,702 / 35.0% | 276 (× 0.42% FB; allocated) | 26 | 210 | M1: **none** | HRSA¹; CRS²; MIRA³ |
| New York | 203 | 5,143,725 / 34.6% | 5,993 (× 9.22% FB; allocated) | 4 | **1,115** | M2: Medium (enacted hospital-only permit + A7319 pending); MPI state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| North Carolina | 252 | 3,777,750 / 47.7% | 1,418 (× 2.18% FB; allocated) | 9 | 658 | M2: Low (enacted HB67, rural-targeted) | HRSA¹; CRS²; MIRA³ |
| North Dakota | 94 | 199,521 / 36.8% | 54 (× 0.08% FB; allocated) | 44 | 38 | M2: bill failed (SB2270) | HRSA¹; CRS²; MIRA³ |
| Ohio | 254 | 4,148,315 / 48.9% | 849 (× 1.31% FB; allocated) | 8 | 699 | M2: None found (HB763 pending); MPI state profile state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| Oklahoma | 200 | 1,351,920 / 29.9% | 353 (× 0.54% FB; allocated) | 16 | 340 | M2: **High** (enacted HB2050, residency-tie); supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Oregon | 177 | 1,664,148 / 44.2% | 556 (× 0.86% FB; allocated) | 18 | 307 | M2: Medium (enacted SB476, FQHC-anchored); MPI state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| Pennsylvania | 144 | 526,759 / 51.8% | 1,414 (× 2.18% FB; allocated) | 35 | 99 | M2: Medium (HB1066/2121 pending); large supply, small hole | HRSA¹; CRS²; MIRA³ |
| Rhode Island | 17 | 257,218 / 74.3% | 227 (× 0.35% FB; allocated) | 48 | 22 | M2: Medium (enacted, primary-care-only to full) | HRSA¹; CRS²; MIRA³ |
| South Carolina | 113 | 2,924,569 / 79.4% | 455 (× 0.70% FB; allocated) | 28 | 194 | M2: None found (S376 pending, broad) | HRSA¹; CRS²; MIRA³ |
| South Dakota | 110 | 290,506 / 33.3% | 50 (× 0.08% FB; allocated) | 42 | 50 | M1: **none**; supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Tennessee | 171 | 2,927,729 / 57.8% | 613 (× 0.94% FB; allocated) | 15 | 408 | M2: **High → Medium** (TN defect; SB2366 fix eff. 1/31/2027) | HRSA¹; CRS²; MIRA³ |
| Texas | 441 | 8,415,032 / 50.4% | 7,472 (× 11.50% FB; allocated) | 2 | **1,331** | M2: Medium (enacted HB2038, residency-tie at issuance); MPI state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| Utah | 69 | 708,536 / 65.1% | 443 (× 0.68% FB; allocated) | 38 | 81 | M1: **none** | HRSA¹; CRS²; MIRA³ |
| Vermont | 17 | 50,210 / 82.6% | 38 (× 0.06% FB; allocated) | 50 | 3 | M2: Medium (S142 pending); smallest hole in 50 states | HRSA¹; CRS²; MIRA³ |
| Virginia | 184 | 2,303,622 / 57.6% | 1,548 (× 2.38% FB; allocated) | 19 | 307 | M2: Medium (enacted HB995, underserved renewal) | HRSA¹; CRS²; MIRA³ |
| Washington | 248 | 5,165,096 / 44.1% | 1,661 (× 2.56% FB; allocated) | 6 | 875 | M2: Medium (enacted SB5185 pilot, broad); MPI state profile state⁴ | HRSA¹; CRS²; MIRA³; MPI⁴ |
| West Virginia | 126 | 793,019 / 38.3% | 48 (× 0.07% FB; allocated) | 31 | 48 | M2: **High** (enacted HB5458, US-fellowship tie); supply ≈ hole | HRSA¹; CRS²; MIRA³ |
| Wisconsin | 181 | 2,014,921 / 65.4% | 424 (× 0.65% FB; allocated) | 23 | 230 | M2: None found (enacted AB954, broad) | HRSA¹; CRS²; MIRA³ |
| Wyoming | 47 | 243,465 / 56.8% | 27 (× 0.04% FB; allocated) | 47 | 27 | M2: None found (HB129 pending); tiny FB pop | HRSA¹; CRS²; MIRA³ |

**Row count: 50.** Every row has a HRSA shortage figure AND a sidelined-IMG estimate (all flagged "allocated" because no measured state count exists). National allocation sums to exactly 65,000 across the 50 states.

---

## Top-10 highest-leverage states

**Ranking rule (recomputable):** rank states by the **Plausible unlocked estimate = `min(estimated sidelined IMGs, practitioners needed)`**, descending. This single rule combines both inputs the milestone asks for: a state scores high only if it has *both* a large shortage (high "practitioners needed") *and* enough allocated sidelined-IMG supply to fill it. A state with a huge shortage but no immigrant supply (e.g., Missouri) is capped by supply; a state with huge immigrant supply but a small shortage (e.g., New Jersey, 83% need met) is capped by the hole. The `min()` is exactly the capacity-constrained match. Ties broken by lower percent-of-need-met (worse shortage ranks higher).

| Rank | State | Practitioners needed | Est. sidelined IMGs (allocated) | Plausible unlocked = min() | Binding constraint | M2 statute status |
|---|---|---|---|---|---|---|
| 1 | Florida | 1,446 | 6,992 | **1,446** | Shortage (supply ample) | Low-defect, enacted — near-ready |
| 2 | Texas | 1,331 | 7,472 | **1,331** | Shortage (supply ample) | Medium — residency-tie at issuance |
| 3 | California | 1,147 | 14,137 | **1,147** | Shortage (supply vastly ample) | Low-defect, expansion bill pending |
| 4 | New York | 1,115 | 5,993 | **1,115** | Shortage (supply ample) | Medium — hospital-only permit; broader bill pending |
| 5 | Arizona | 889 | 1,320 | **889** | Shortage (supply adequate) | Low-defect bill pending |
| 6 | Washington | 875 | 1,661 | **875** | Shortage (supply adequate) | Medium — broad pilot enacted |
| 7 | Illinois | 725 | 2,538 | **725** | Shortage (supply ample) | Medium-defect enacted |
| 8 | Ohio | 699 | 849 | **699** | Shortage (supply adequate) | Clean bill pending |
| 9 | North Carolina | 658 | 1,418 | **658** | Shortage (supply ample) | Low-defect, enacted (rural-targeted) |
| 10 | Michigan | 614 | 1,010 | **614** | Shortage (supply adequate) | Medium-defect bill pending |

**Reading this list.** In all top-10 states the binding constraint is the *size of the shortage*, not the supply of sidelined IMGs — every one has more allocated sidelined physicians than its HPSA hole. That means the leverage isn't "are there enough idle doctors" but "does the statute let them reach the shortage." Cross-referencing M2: **Florida, California, North Carolina, Ohio** pair a top-10 shortage with a clean/low-defect law — the fastest wins. **Texas, New York, Illinois, Washington, Michigan** pair top-10 leverage with a *Medium-defect* law — these are exactly the high-value targets for the M4 model-bill redline, because a statutory fix converts an already-large match. **Arizona** has only a pending bill. (Mississippi and Oklahoma are notable *outside* the top 10: both have a High-defect law and a shortage where supply ≈ hole, so a clean statute would unlock essentially their entire allocated supply — high *proportional* leverage even if absolute numbers are smaller.)

---

## Methodology & assumptions

### Datasets used (with access dates)

1. **HRSA, Bureau of Health Workforce — *Designated Health Professional Shortage Areas Statistics*, Second Quarter FY2026, Designated HPSA Quarterly Summary, data as of March 31, 2026** (report generated June 25, 2026). Table 3 (Primary Care HPSAs by State) is the source for the PC-HPSA count, population of designated HPSAs, percent of need met, and "practitioners needed to remove designations" columns. Accessed **2026-06-25**. https://data.hrsa.gov/default/generatehpsaquarterlyreport . National primary-care total in this report: 8,789 HPSAs, 101.7M population, 47.74% need met, **17,306** practitioners needed. (Note: this is *more current* than the KFF/HRSA Dec-31-2025 snapshot of 8,467 HPSAs / 92.3M / 15,604 needed, which I cross-checked: [KFF State Health Facts, primary-care HPSAs, data as of 12/31/2025, accessed 2026-06-25](https://www.kff.org/other-health/state-indicator/primary-care-health-professional-shortage-areas-hpsas/).)
2. **Congressional Research Service, R48940, *Current Foreign-Born Population by State and Congressional District*, Table 1 (one-year ACS estimates for 2024).** Source for state foreign-born population, used as the allocation proxy. Accessed **2026-06-25** via EveryCRSReport mirror. https://www.everycrsreport.com/reports/R48940.html . 50-state foreign-born sum used as the denominator: **50,126,316**.
3. **MIRA Coalition figure of ~65,000 sidelined foreign-trained physicians**, as reported by the **Massachusetts Medical Society, *The US Needs Foreign-Trained Physicians: Why Are We Making It So Tough for Them?*** Accessed **2026-06-25**. https://www.massmed.org/Publications/The-US-Needs-Foreign-Trained-Physicians--Why-Are-We-Making-It-So-Tough-for-Them-/ . This is the national sidelined-physician anchor that gets allocated.
4. **Migration Policy Institute — *Brain Waste among U.S. Immigrants with Health Degrees: A Multi-State Profile*** (state fact sheets for CA, FL, MI, NY, OH, OR, TX, WA; national figure ~263,000 immigrants with health degrees underemployed/out of work, of which physicians are a subset; ~12,000 health-degree-holders in Illinois cited). Used only as a *corroborating cross-check* on the order of magnitude and on which states have large sidelined health-professional populations — **not** as the primary allocation, because MPI's figure is all health degrees (nurses, therapists, doctors), not physicians alone, and covers only 8 states. Accessed **2026-06-25**. https://www.migrationpolicy.org/research/brain-waste-immigrants-health-degrees-multi-state-profile and https://www.migrationpolicy.org/news/health-care-untapped-immigrant-talent .

### The arithmetic (every number in the table is one of these or a direct HRSA cell)

- **Estimated sidelined IMGs (state s)** = `65,000 × (foreign-born population of s ÷ 50,126,316)`.
  Example (Texas): `65,000 × (5,762,477 / 50,126,316) = 65,000 × 0.1150 = 7,472`. (Florida: `65,000 × 0.1076 = 6,992`. California: `65,000 × 0.2175 = 14,137`.)
  The state foreign-born **share** shown in each cell is `foreign-born of s ÷ 50,126,316 × 100%`. By construction these allocations sum to 65,000.
- **Shortage-severity rank** = rank of "practitioners needed" in descending order (1 = most needed). Pure ordering of the HRSA column; ties broken by lower % need met.
- **Plausible unlocked estimate (state s)** = `min(estimated sidelined IMGs of s, practitioners needed of s)`.
  Example (Florida): `min(6,992, 1,446) = 1,446` (shortage-bound). New Jersey: `min(3,082, 39) = 39` (shortage-bound). Kentucky: `min(309, 413) = 309` (supply-bound).
- **Top-10 leverage** = the 50 states sorted by the Plausible unlocked estimate, descending.

### Key assumptions (stated explicitly)

- **A1 — No measured per-state sidelined-physician count exists.** FSMB, AMA, and HRSA publish *licensed* IMG counts, not *sidelined/unlicensed* physician counts by state. Every "Est. sidelined IMGs" cell is therefore an **allocation of the national 65,000**, not a state observation. This is labeled "allocated" in every cell.
- **A2 — Foreign-born population share is the chosen proxy** for where sidelined IMGs live. Rationale: sidelined IMGs are by definition foreign-trained and predominantly foreign-born, and immigrants cluster geographically; foreign-born share is the most directly relevant publicly-available distribution. (Alternative proxies — share of *already-licensed* IMGs, or MPI's 8-state health-degree counts — are discussed in Limitations.)
- **A3 — Primary-care HPSA "practitioners needed" is the shortage metric.** HRSA also publishes dental and mental-health HPSAs; this artifact uses **primary care** because that is where provisional-licensure pathways most plausibly place general physicians, and it is the metric with a clean "practitioners needed" figure. Using primary care *understates* total physician need (it excludes specialist shortages), so the shortage side is conservative.
- **A4 — The unlock is capacity-constrained, not additive.** A state cannot "unlock" more practicing physicians than (a) its shortage can absorb or (b) sidelined IMGs plausibly live there. The `min()` enforces both ceilings. This deliberately produces a *plausibility ceiling*, not a forecast.
- **A5 — Statute status (M1/M2) is a gate, not a multiplier.** The unlocked estimate assumes a *clean* statute exists. The Notes column flags states where no law exists (the unlock is purely hypothetical until one passes) or where an M2 defect would block placement (the unlock is contingent on the M4 fix). The number is "what a clean law could plausibly reach," consistent with the packet's purpose.

---

## Limitations & counter-evidence

**The allocation is the weakest link, by design.** The single largest limitation is **A1/A2**: there is no measured count of sidelined physicians by state, so the entire "Est. sidelined IMGs" column is a national figure spread across states by foreign-born share. This is an *allocation, not a measurement*, and it can be wrong in both directions:
- **Foreign-born share over-weights low-skill immigrant populations.** Sidelined *physicians* are a tiny, highly-educated slice of the foreign-born; states whose immigrant population skews toward physicians/professionals (e.g., metros with large South-Asian or Middle-Eastern medical diasporas) are *under*-counted by a raw foreign-born proxy, and states with large low-education immigrant populations are *over*-counted. A "share of already-licensed IMGs" proxy or a "share of immigrants with a health degree" proxy (MPI) would shift the distribution — likely toward IL, NY, MI, NJ and away from agricultural-immigration states. I used foreign-born share because it is complete for all 50 states and directly published; the others are partial (MPI covers 8 states) or would themselves need an allocation.
- **MPI cross-check suggests my allocation may understate some industrial-Midwest states.** MPI separately estimates ~12,000 immigrants with health degrees underemployed in Illinois alone (all health degrees, not just physicians) [MPI⁴]. My allocation gives Illinois 2,538 *physicians* — not directly comparable (different denominator: all health degrees vs. physicians; ~263,000 national vs. ~65,000), but it flags that immigrant *health-professional* concentration is not perfectly proportional to total foreign-born population. Treat the per-state IMG figures as order-of-magnitude, not precise.

**The 65,000 anchor is itself soft.** The MIRA/Mass-Medical-Society figure is "as many as 65,000," an advocacy estimate, not a census. The brief and this packet treat it as the working national number; if the true figure is, say, 40,000 or 90,000, every allocated cell scales linearly (multiply the column by 40/65 or 90/65). The *ranking* is unaffected by this scaling because it is monotonic — only the absolute "unlocked" numbers move, and only where supply (not shortage) is the binding constraint.

**"Plausible unlocked" is an upper bound, not a forecast — repeated because it matters.** The number assumes (1) a clean statute exists, (2) every sidelined IMG in the state is willing and able to enter the pathway, (3) employers in shortage areas hire them, and (4) supervisors are available. M2's central counter-evidence applies in full: Tennessee's law stalled in *board rulemaking*, and broad-sponsor states (ID, WI, KY) have not yet visibly produced large placement numbers. The realized number will be a fraction of the ceiling. This column answers "how big could the prize be," not "how many doctors will be practicing in 2028."

**Double-counting and mismatch risks.**
- *Specialty mismatch.* The shortage metric is *primary-care* HPSA need, but sidelined IMGs span all specialties. A sidelined cardiologist does not remove a primary-care HPSA designation. The `min()` match implicitly assumes interchangeability that does not strictly hold; the realized primary-care unlock is therefore *lower* than the ceiling for states whose sidelined IMGs skew specialist. (Conversely, specialist shortages — omitted here — mean the *total* physician unlock could be larger.)
- *Cross-state mobility.* Foreign-born residents of one state may take a provisional license in a neighboring state; the allocation pins supply to state of residence, which licensure mobility can violate.
- *No double-counting within the table* — the allocation partitions a single national figure, so a given sidelined physician is counted in exactly one state; the column sums to exactly 65,000.

**Counter-evidence to the artifact's framing.**
1. *The biggest shortages are in states that already have decent laws.* Florida, California, and North Carolina — top-3, top-3, and top-9 on leverage — already have low-defect enacted statutes (M2). This cuts against a "fix the law and unlock doctors" story for the very largest holes: there, the binding constraint is *implementation and placement*, not statutory text. The strongest *statutory*-fix case is the Medium-defect top-10 states (TX, NY, IL, WA, MI), and the High-defect states with supply ≈ hole (OK, MS, WV) where a clean law would unlock nearly the entire local supply.
2. *Percent-of-need-met tells a different story than absolute need.* Delaware (9.6%), DC (0.23%, excluded as non-state), Missouri (21.0%), and Maryland (28.6%) have the *worst* coverage ratios but rank mid-pack on absolute "practitioners needed" because they are small. A reader optimizing for *severity of deprivation* rather than *absolute hole size* would re-rank toward these states; the chosen rule optimizes for total physicians plausibly placed, which favors large states. Both rankings are defensible; the rule is stated so a reader can recompute either.
3. *HRSA "practitioners needed" counts physicians only, ignoring NPs/PAs.* HRSA's own footnote (7) notes the formula "does not take into account the availability of additional primary care services provided by nurse practitioners and physician assistants." Where NPs/PAs already fill gaps, the true unmet *physician-equivalent* need is smaller than the HRSA figure, so the shortage side may be overstated for scope-of-practice-friendly states.

**Nothing in the table is marked `[speculative]`:** every cell is either a directly-cited HRSA value, a directly-cited CRS foreign-born value, or the stated arithmetic (allocation / min / rank) applied to those cited values and the cited 65,000 anchor. The *judgment* embedded in the artifact — that foreign-born share is the right proxy and that primary-care HPSA need is the right shortage metric — is disclosed above as an assumption, not presented as a measured fact.

---

### Source key
¹ HRSA Bureau of Health Workforce, *Designated HPSA Statistics, Q2 FY2026*, data as of 3/31/2026, Table 3, accessed 2026-06-25 — https://data.hrsa.gov/default/generatehpsaquarterlyreport (cross-check: [KFF, data as of 12/31/2025](https://www.kff.org/other-health/state-indicator/primary-care-health-professional-shortage-areas-hpsas/))
² CRS R48940, *Current Foreign-Born Population by State*, Table 1 (2024 ACS), accessed 2026-06-25 — https://www.everycrsreport.com/reports/R48940.html
³ MIRA Coalition ~65,000 figure via Massachusetts Medical Society, accessed 2026-06-25 — https://www.massmed.org/Publications/The-US-Needs-Foreign-Trained-Physicians--Why-Are-We-Making-It-So-Tough-for-Them-/
⁴ Migration Policy Institute, *Brain Waste among U.S. Immigrants with Health Degrees: A Multi-State Profile* (8-state profiles; ~263,000 national health-degree figure; ~12,000 IL), accessed 2026-06-25 — https://www.migrationpolicy.org/research/brain-waste-immigrants-health-degrees-multi-state-profile
