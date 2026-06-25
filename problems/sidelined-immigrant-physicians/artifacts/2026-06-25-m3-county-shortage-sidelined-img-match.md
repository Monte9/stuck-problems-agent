# M3 — Shortage-Area / Sidelined-IMG Match: How Many Physicians a Clean Statute Could Unlock, and Where

**Milestone:** M3 (sidelined-immigrant-physicians)
**Date:** 2026-06-25
**Input artifacts:** [M1 — Provisional-Licensure Crosswalk](./2026-06-25-m1-provisional-licensure-crosswalk.md); [M2 — Stranding-Defect Analysis](./2026-06-25-m2-stranding-defect-analysis.md)

## What this artifact does

M1 catalogued which states have a clean (or defective, or no) provisional-licensure law. M2 graded the stranding defect in each enacted/proposed law. M3 supplies the **third leg**: it matches each state's **physician-shortage severity** (HRSA primary-care HPSA data) against an **estimate of the sidelined internationally-trained-physician (IMG) supply** living in that state, and produces a state-by-state estimate of how many additional physicians a *defect-free* statute could plausibly unlock and where the need is greatest. The leverage ranking that closes the artifact combines shortage severity, sidelined-IMG supply, and the M1/M2 finding of whether the state still needs a clean statute (or already has one).

**The honest headline:** the data to do this precisely at the *county* level for the *physician-specific* sidelined population **does not exist** in any single public dataset — the Federal Reserve Bank of Minneapolis stated flatly in January 2024 that "nationally representative data quantifying the underutilization of foreign-trained physicians is not yet available" ([Minneapolis Fed, 2024-01-19](https://www.minneapolisfed.org/article/2024/occupational-licensing-can-detour-immigrant-physicians-career-paths)). Every physician-specific state number below is therefore a **derived estimate** built by allocating a national physician figure across states using the best available *state-level* distribution (the Migration Policy Institute's brain-waste-by-state table). The arithmetic is shown in full in the Methodology section so a reader can substitute their own assumptions.

---

## Key national anchors (all sourced)

| Quantity | Figure | Source (dated) |
|---|---|---|
| Primary-care HPSA designations, US total | **8,467** | [KFF / HRSA Bureau of Health Workforce, data as of 2025-12-31](https://www.kff.org/other-health/state-indicator/primary-care-health-professional-shortage-areas-hpsas/) (accessed 2026-06-25) |
| Population in primary-care HPSAs, US total | **92,285,375** | KFF / HRSA, as of 2025-12-31 (same source) |
| Primary-care practitioners needed to remove all HPSA designations, US total | **15,604** | KFF / HRSA, as of 2025-12-31 (same source) |
| Immigrants (ages 25-64) with health-related undergraduate degrees who are underutilized ("brain waste"), US total | **263,000** | [MPI, *Brain Waste among U.S. Immigrants with Health Degrees*, July 2020](https://www.migrationpolicy.org/sites/default/files/publications/MPI-HealthCare-Brainwaste-by-State_Final.pdf), 2013-17 ACS (accessed 2026-06-25) |
| Of which: total immigrants with health-related undergraduate degrees, US | **1,069,000** (24.6% underutilized) | MPI, July 2020 (same source) |
| Unlicensed *foreign-trained physicians* in the US who cannot practice | **~65,000** | MIRA Coalition estimate, cited in [GBH/PRX, 2018-03-26](https://theworld.org/stories/2018-03-26/highly-trained-and-educated-some-foreign-born-doctors-still-can-t-practice) (older figure — see Limitations) |
| Share of immigrant physicians (2004-2022 arrivals) on track to practice in the US by early 2024 | **~1 in 3** | [Minneapolis Fed, 2024-01-19](https://www.minneapolisfed.org/article/2024/occupational-licensing-can-detour-immigrant-physicians-career-paths) |
| Immigrant share of all US physicians and surgeons | **~26%** | MPI, cited in [Niskanen Center, 2025-03-20](https://www.niskanencenter.org/unlocking-potential-how-states-can-remove-barriers-for-internationally-trained-physicians/) |

The two italicized rows are the load-bearing numbers for the physician-specific estimate: **~65,000 sidelined foreign-trained physicians nationally**, distributed across states in proportion to the **MPI state-level brain-waste shares**. Both are imperfect (see Methodology and Limitations); they are the best public figures available.

---

## State-by-state table (50 states)

Columns: **HPSA** = primary-care HPSA designations (count) / **Need** = primary-care practitioners needed to remove all HPSA designations (KFF/HRSA, 2025-12-31). **Sidelined IMGs** = estimated sidelined IMG *physicians* (derived; basis in next column). **Shortage rank** = rank of 1-51 by Need (1 = worst). **Unlocked est.** = plausible additional practicing physicians a clean statute could unlock over ~5 yrs (10-20% capture of the sidelined-IMG estimate; see Methodology). **Statute status** = from M1/M2 (clean / defective-needs-fix / none / pending).

DC is shown for completeness but excluded from the 50-state count and the leverage ranking (no state-level sidelined-IMG estimate and licensure is municipal).

| State | HPSA | Need | Est. sidelined IMG physicians (basis) | Shortage rank | Unlocked est. (10-20%) | M1/M2 statute status | Source(s) |
|---|---|---|---|---|---|---|---|
| Alabama | 124 | 239 | ~140 (national fallback; no MPI state figure) | 20 | 0-50 | none | KFF/HRSA; MPI residual |
| Alaska | 338 | 68 | ~140 (national fallback) | 40 | 0-50 | none | KFF/HRSA; MPI residual |
| Arizona | 284 | 776 | ~1,000 (MPI: 4,000 underutil. health-degree immigrants) | 5 | 100-200 | pending (HB2435, low-severity) | KFF/HRSA; MPI 2020 |
| Arkansas | 152 | 177 | ~140 (national fallback) | 28 | 0-50 | enacted, **clean** (HPSA-targeted) | KFF/HRSA; MPI residual |
| California | 661 | 1,045 | ~14,800 (MPI: 60,000 — largest in US) | 3 | 1,500-2,950 | enacted limited + pending AB2386 | KFF/HRSA; MPI 2020 |
| Colorado | 131 | 171 | ~1,000 (MPI: 4,000) | 29 | 100-200 | none | KFF/HRSA; MPI 2020 |
| Connecticut | 52 | 73 | ~700 (MPI: 3,000) | 39 | 50-150 | pending (SB1054 failed) | KFF/HRSA; MPI 2020 |
| Delaware | 12 | 122 | ~140 (national fallback) | 32 | 0-50 | none | KFF/HRSA; MPI residual |
| Florida | 320 | 1,434 | ~7,200 (MPI: 29,000) | 1 | 700-1,450 | enacted, low-severity | KFF/HRSA; MPI 2020 |
| Georgia | 233 | 563 | ~2,000 (MPI: 8,000) | 9 | 200-400 | enacted-2026, medium (appropriation-contingent) | KFF/HRSA; MPI 2020 |
| Hawaii | 34 | 58 | ~500 (MPI: 2,000) | 42 | 50-100 | none | KFF/HRSA; MPI 2020 |
| Idaho | 105 | 85 | ~140 (national fallback) | 36 | 0-50 | enacted, **clean** (cleanest comparator) | KFF/HRSA; MPI residual |
| Illinois | 304 | 597 | ~2,700 (MPI: 11,000) | 8 | 250-550 | enacted, medium | KFF/HRSA; MPI 2020 |
| Indiana | 169 | 431 | ~700 (MPI: 3,000) | 13 | 50-150 | enacted, **clean** (underserved-targeted) | KFF/HRSA; MPI 2020 |
| Iowa | 180 | 197 | ~140 (national fallback) | 24 | 0-50 | enacted, **clean** | KFF/HRSA; MPI residual |
| Kansas | 164 | 122 | ~140 (national fallback) | 33 | 0-50 | pending, **clean** (cleanest pending) | KFF/HRSA; MPI residual |
| Kentucky | 257 | 388 | ~500 (MPI: 2,000) | 14 | 50-100 | enacted-2026, **clean** | KFF/HRSA; MPI 2020 |
| Louisiana | 198 | 220 | ~140 (national fallback) | 22 | 0-50 | enacted, low-severity | KFF/HRSA; MPI residual |
| Maine | 87 | 26 | ~140 (national fallback) | 47 | 0-50 | pending, medium (rural-GME single channel) | KFF/HRSA; MPI residual |
| Maryland | 56 | 284 | ~1,700 (MPI: 7,000) | 19 | 150-350 | pending, **high-severity defect** (HB598/SB489) | KFF/HRSA; MPI 2020 |
| Massachusetts | 66 | 81 | ~1,200 (MPI: 5,000) | 37 | 100-250 | enacted, medium (long supervision) | KFF/HRSA; MPI 2020 |
| Michigan | 280 | 464 | ~1,500 (MPI: 6,000) | 12 | 150-300 | pending, medium | KFF/HRSA; MPI 2020 |
| Minnesota | 222 | 216 | ~700 (MPI: 3,000) | 23 | 50-150 | enacted, low-severity | KFF/HRSA; MPI 2020 |
| Mississippi | 159 | 303 | ~140 (national fallback) | 17 | 0-50 | pending, **high (SB2441)** / clean (HB313) | KFF/HRSA; MPI residual |
| Missouri | 344 | 475 | ~500 (MPI: 2,000) | 11 | 50-100 | pending (HB1198 failed; clean text) | KFF/HRSA; MPI 2020 |
| Montana | 137 | 57 | ~140 (national fallback) | 43 | 0-50 | none | KFF/HRSA; MPI residual |
| Nebraska | 136 | 36 | ~140 (national fallback) | 45 | 0-50 | enacted-2026, medium (6-yr runway) | KFF/HRSA; MPI residual |
| Nevada | 75 | 180 | ~1,000 (MPI: 4,000) | 27 | 100-200 | enacted, low-severity | KFF/HRSA; MPI 2020 |
| New Hampshire | 26 | 14 | ~140 (national fallback) | 50 | 0-50 | pending, **high-severity defect** (SB457) | KFF/HRSA; MPI residual |
| New Jersey | 40 | 24 | ~3,500 (MPI: 14,000) | 48 | 350-700 | pending, **clean** (A3987) | KFF/HRSA; MPI 2020 |
| New Mexico | 103 | 182 | ~140 (national fallback) | 26 | 0-50 | none | KFF/HRSA; MPI residual |
| New York | 194 | 1,036 | ~5,400 (MPI: 22,000) | 4 | 550-1,100 | enacted permit (medium) + pending | KFF/HRSA; MPI 2020 |
| North Carolina | 234 | 559 | ~1,500 (MPI: 6,000) | 10 | 150-300 | enacted, low-severity (rural-targeted) | KFF/HRSA; MPI 2020 |
| North Dakota | 93 | 37 | ~140 (national fallback) | 44 | 0-50 | pending (SB2270 failed; clean text) | KFF/HRSA; MPI residual |
| Ohio | 249 | 686 | ~1,200 (MPI: 5,000) | 6 | 100-250 | pending, **clean** (HB763) | KFF/HRSA; MPI 2020 |
| Oklahoma | 196 | 318 | ~140 (national fallback) | 16 | 0-50 | enacted, **high-severity defect** (residency tie) | KFF/HRSA; MPI residual |
| Oregon | 160 | 169 | ~500 (MPI: 2,000) | 30 | 50-100 | enacted, medium (FQHC-anchored) | KFF/HRSA; MPI 2020 |
| Pennsylvania | 142 | 91 | ~1,500 (MPI: 6,000) | 35 | 150-300 | pending, mixed (HB1066 clean / HB2121 medium) | KFF/HRSA; MPI 2020 |
| Rhode Island | 17 | 22 | ~140 (national fallback) | 49 | 0-50 | enacted, medium (primary-care-only) | KFF/HRSA; MPI residual |
| South Carolina | 111 | 189 | ~200 (MPI: 1,000) | 25 | 0-50 | pending, **clean** (cleanest comparator) | KFF/HRSA; MPI 2020 |
| South Dakota | 107 | 59 | ~140 (national fallback) | 41 | 0-50 | none | KFF/HRSA; MPI residual |
| Tennessee | 169 | 383 | ~700 (MPI: 3,000) | 15 | 50-150 | enacted, **HIGH (named defect; mid-fix)** | KFF/HRSA; MPI 2020 |
| Texas | 418 | 1,147 | ~5,700 (MPI: 23,000) | 2 | 550-1,150 | enacted, medium (residency tie at issuance) | KFF/HRSA; MPI 2020 |
| Utah | 67 | 79 | ~500 (MPI: 2,000) | 38 | 50-100 | none | KFF/HRSA; MPI 2020 |
| Vermont | 16 | 2 | ~140 (national fallback) | 51 | 0-50 | pending, medium | KFF/HRSA; MPI residual |
| Virginia | 181 | 298 | ~1,500 (MPI: 6,000) | 18 | 150-300 | enacted, medium (shortage-aligned renewal) | KFF/HRSA; MPI 2020 |
| Washington | 238 | 685 | ~2,000 (MPI: 8,000) | 7 | 200-400 | enacted-2026 pilot (medium legacy route) | KFF/HRSA; MPI 2020 |
| West Virginia | 126 | 163 | ~140 (national fallback) | 31 | 0-50 | enacted-2026, **high-severity defect** (US-fellowship tie) | KFF/HRSA; MPI residual |
| Wisconsin | 175 | 223 | ~140 (national fallback) | 21 | 0-50 | enacted, **clean** (cleanest comparator) | KFF/HRSA; MPI residual |
| Wyoming | 46 | 29 | ~140 (national fallback) | 46 | 0-50 | pending, **clean** | KFF/HRSA; MPI residual |
| *District of Columbia* | *12* | *96* | *no state-level estimate; derived only via national fallback ~140* | *34* | *0-50* | *none (eminence-only)* | *KFF/HRSA; MPI residual* |

**Row count: 50 states + DC = 51 rows.** Every row carries a HPSA/Need figure (KFF/HRSA) and a sidelined-IMG figure. The 22 states (+ DC) MPI does not break out are explicitly flagged **"national fallback"** — meaning *no state-level estimate is available; derived from the national figure via the residual-share method in the Methodology* (the ~12,000 of the MPI 263,000 not attributed to a named state, and the corresponding ~3,000 of the 65,000 physician figure, spread thin across 22 states + DC ≈ 130-140 each).

---

## Methodology & assumptions

### External datasets used (each named, with access date 2026-06-25)

1. **HRSA Bureau of Health Workforce — Designated HPSA Quarterly Summary**, surfaced via **KFF State Health Facts**, "Primary Care Health Professional Shortage Areas (HPSAs)," **data as of 2025-12-31** ([link](https://www.kff.org/other-health/state-indicator/primary-care-health-professional-shortage-areas-hpsas/)). Supplies, per state: HPSA designation count, percent of need met, and **practitioners needed** to remove all designations. *Practitioners-needed* is the shortage-severity metric used here because it is denominated in physicians, directly comparable to a sidelined-physician supply, rather than in designation counts (which vary with how a state draws its service areas).
2. **Migration Policy Institute — *Brain Waste among U.S. Immigrants with Health Degrees: A Multi-State Profile*, July 2020** ([PDF](https://www.migrationpolicy.org/sites/default/files/publications/MPI-HealthCare-Brainwaste-by-State_Final.pdf)), Table 1, based on **pooled 2013-17 American Community Survey** microdata. Supplies the national total (263,000 underutilized immigrants with health-related undergraduate degrees, of 1,069,000) and the **28 named-state breakdown** used to distribute the physician estimate. MPI's "underutilized" = degree-holders ages 25-64 working in jobs requiring ≤ a high-school diploma, unemployed, or out of the labor force.
3. **MIRA Coalition ~65,000 figure** for unlicensed foreign-trained physicians, as reported in **GBH/PRX, 2018-03-26** ([link](https://theworld.org/stories/2018-03-26/highly-trained-and-educated-some-foreign-born-doctors-still-can-t-practice)). Used as the national *physician-specific* anchor.
4. **Federal Reserve Bank of Minneapolis, 2024-01-19** ([link](https://www.minneapolisfed.org/article/2024/occupational-licensing-can-detour-immigrant-physicians-career-paths)) — the "1 in 3 on track to practice" finding and the explicit statement that state-by-state physician-underutilization data does not yet exist. Used as the capture-rate sanity check and the central caveat.
5. **Niskanen Center, 2025-03-20** ([link](https://www.niskanencenter.org/unlocking-potential-how-states-can-remove-barriers-for-internationally-trained-physicians/)) — the 26%-of-physicians-are-immigrants figure and corroboration of the MPI ~270,000 health-degree estimate (a rounding of 263,000).
6. **M1 and M2 artifacts** (this packet) for each state's statute status, derived from the **FSMB key-issue chart, Last Updated May 2026**.

### The estimation chain (every number traceable)

**Step 1 — National sidelined-physician anchor.** Take **65,000** as the national count of sidelined foreign-trained physicians (MIRA via GBH/PRX 2018). This is deliberately distinct from MPI's 263,000, which counts *all health-degree* immigrants (nurses, therapists, technicians, dentists, etc.), not physicians. Using 65,000 rather than 263,000 is the conservative, physician-specific choice.

**Step 2 — State distribution.** No source distributes the 65,000 *physicians* by state. The best available state-level distribution of the closely-related *health-degree brain-waste* population is MPI Table 1. **Assumption (disclosed):** sidelined foreign-trained physicians are distributed across states in the same proportions as MPI's underutilized health-degree immigrants. Per state: `est_sidelined_physicians = (MPI_state_underutilized / 263,000) × 65,000`, rounded to the nearest 100. Worked example, California: `(60,000 / 263,000) × 65,000 = 14,829 ≈ 14,800`. Florida: `(29,000/263,000)×65,000 ≈ 7,200`. Texas ≈ 5,700; New York ≈ 5,400; New Jersey ≈ 3,500; Illinois ≈ 2,700; and so on down Table 1.
- **The 22 unbroken-out states + DC:** MPI names only 28 states (it suppresses small-sample states). Those 28 sum to 251,000 of the 263,000; the **residual 12,000** (4.6%) belongs to all other states combined, i.e. **~3,000 of the 65,000 physicians** spread across 22 states + DC ≈ **~130-140 each** as a flat "national fallback." These rows are flagged in the table; they are floors, not point estimates, and most are low-shortage states anyway.

**Step 3 — Capture rate → "unlocked" estimate.** Not every sidelined physician would obtain a license even under a perfect statute (English/USMLE gaps, age, family, competing careers, employer-matching frictions — see Limitations). The Minneapolis Fed "1 in 3 on track to practice" finding implies a large untapped fraction but also real attrition. **Assumption (disclosed):** a clean statute realistically converts **10-20%** of a state's sidelined-IMG pool into practicing physicians over a ~5-year window. Per state: `unlocked = est_sidelined × [0.10, 0.20]`, rounded to nearest 50. This yields a **national named-state total of roughly 6,000 (low) to 12,500 (high) additional practicing physicians** — set against a national primary-care shortfall of **15,604 practitioners** (KFF/HRSA). In other words, even on conservative assumptions, fully unlocking sidelined IMGs could close **~40-80% of the measured national primary-care practitioner gap** — the core leverage finding of this packet. (A 30% high-capture scenario reaches ~18,000, exceeding the gap; reported only as an upper bound.)

### The leverage ranking rule

"Leverage" = **shortage severity × sidelined-IMG supply**, with statute-status as a tie-breaker/qualifier. Concretely:

- **Composite score** = `sqrt( (Need / max Need) × (Sidelined-IMG / max Sidelined-IMG) )` — the geometric mean of each state's normalized practitioner-need and normalized sidelined-IMG estimate. The geometric mean (rather than a sum) enforces the *intersection* logic the spec asks for: a state scores high only if it has **both** a real shortage **and** a real sidelined-IMG supply. A state with a huge shortage but no IMGs (or vice versa) scores low.
- Then **statute status (from M1/M2) modifies the action implication**, not the raw score: a high-leverage state that *already has a clean enacted statute* is a lower advocacy priority (the law is done; the bottleneck is implementation), while a high-leverage state with **no law or a high-severity defect** is where "a dollar of advocacy unlocks the most clinical capacity" — exactly the funder question the packet exists to answer. Both are shown.

---

## Top-10 highest-leverage states

Ranked by the composite score above (shortage severity × sidelined-IMG supply). The **"advocacy priority"** column applies the M1/M2 statute-status modifier: where the highest clinical payoff per advocacy dollar sits.

| Rank | State | Need (rank) | Est. sidelined IMG physicians | Composite | Unlocked est. | M1/M2 statute status | Advocacy priority |
|---|---|---|---|---|---|---|---|
| 1 | **California** | 1,045 (#3) | ~14,800 | 0.85 | 1,500-2,950 | enacted *limited* + AB2386 pending | **HIGH** — pass AB2386 to convert the legacy capped MPP into a real converting pathway; biggest single pool in the US |
| 2 | **Florida** | 1,434 (#1) | ~7,200 | 0.70 | 700-1,450 | enacted, low-severity | MEDIUM — law is fairly clean; priority is implementation + watching board discretion to exclude foreign schools |
| 3 | **Texas** | 1,147 (#2) | ~5,700 | 0.56 | 550-1,150 | enacted, **medium (residency tie at issuance)** | **HIGH** — large pool + worst-tier shortage + a fixable medium defect (broaden issuance beyond residency-operating hospitals) |
| 4 | **New York** | 1,036 (#4) | ~5,400 | 0.51 | 550-1,100 | enacted permit (medium) + pending bill | **HIGH** — pass A7319/S7840 to replace the hospital-only limited permit with a converting, shortage-area pathway |
| 5 | **Illinois** | 597 (#8) | ~2,700 | 0.28 | 250-550 | enacted, medium (long supervision) | MEDIUM — broaden closed sponsor list / shorten runway |
| 6 | **Washington** | 685 (#7) | ~2,000 | 0.25 | 200-400 | enacted-2026 pilot (legacy route medium) | MEDIUM — ensure the SB5185 pilot supersedes the narrow 1129 route in practice |
| 7 | **Georgia** | 563 (#9) | ~2,000 | 0.23 | 200-400 | enacted-2026, **medium (appropriation-contingent)** | **HIGH** — secure the appropriation; the law strands at $0 until funded |
| 8 | **North Carolina** | 559 (#10) | ~1,500 | 0.20 | 150-300 | enacted, low-severity (rural-targeted) | LOW-MEDIUM — implementation; law is shortage-aligned |
| 9 | **Ohio** | 686 (#6) | ~1,200 | 0.20 | 100-250 | **pending, clean (HB763)** | **HIGH** — clean bill + 6th-worst shortage + real pool; passage is the single highest-leverage legislative act outside the big-4 |
| 10 | **Arizona** | 776 (#5) | ~1,000 | 0.19 | 100-200 | **pending, low-severity (HB2435)** | **HIGH** — 5th-worst shortage, no enacted law yet; a clean bill is in reach |

**Reading the table for funders/legislators (the leverage rule applied):**
- **Biggest raw clinical payoff:** California, Texas, New York, Florida — the four states with both the deepest shortages and the largest sidelined pools account for the lion's share of the national unlocked estimate (~3,300-6,650 of the ~6,000-12,500 total).
- **Highest *advocacy* leverage (need + pool + a fixable statute gap):** **Texas** (fix the medium residency-tie defect), **New York** and **California** (pass the pending converting bills), **Ohio** and **Arizona** (pass clean pending bills in high-shortage states), and **Georgia** (fund an already-passed law). These are where statutory change, not just implementation, still moves the needle.
- **Cautionary high-severity-defect states to watch** (smaller pools, but the defect actively strands what supply exists): **Maryland** (#19 need, ~1,700 pool, high-severity pending defect), **Oklahoma** and **West Virginia** (enacted residency/fellowship ties), and **New Hampshire** (pending residency tie). These rank below the top 10 on the combined score but are the clearest M2→M4 "fix the defect" targets.

---

## Limitations & counter-evidence

**1. The physician-specific state distribution is an assumption, not a measurement.** The single most important caveat: there is **no public dataset that counts sidelined foreign-trained *physicians* by state.** Every physician number in the table is the national ~65,000 *allocated* using MPI's *health-degree* (all-occupations) state shares. If sidelined physicians cluster differently than sidelined nurses/therapists — plausibly more concentrated in immigrant-gateway metros (NY, CA, NJ) where IMGs historically settle — then the big-state estimates are *under*-stated and the fallback-state estimates *over*-stated. The Minneapolis Fed's January 2024 statement that such data "is not yet available" is the standing reason this whole estimate is a modeled approximation. ([Minneapolis Fed, 2024-01-19](https://www.minneapolisfed.org/article/2024/occupational-licensing-can-detour-immigrant-physicians-career-paths))

**2. The 65,000 figure is old and soft.** It traces to a MIRA Coalition estimate reported in 2018 ([GBH/PRX, 2018-03-26](https://theworld.org/stories/2018-03-26/highly-trained-and-educated-some-foreign-born-doctors-still-can-t-practice)) — more than 12 months old and methodologically opaque (it is an advocacy estimate, not a peer-reviewed tabulation). It is reported here as the best available physician-specific national anchor, **dated as a 2018 figure**, not as current state. If the true figure is materially different, every state estimate scales proportionally; the *relative* leverage ranking (which depends on shares, not the absolute level) is more robust than the absolute unlocked counts.

**3. The MPI state data is from 2013-17 ACS (July 2020 report).** The state shares are ~8-12 years old. Immigration patterns shift; the shares are presented as the best available *distribution*, dated accordingly, not as a current census. MPI suppressed 22 states + DC for small sample size — those rows are the weakest in the table and are flagged as national-fallback floors.

**4. HPSA "practitioners needed" measures primary-care shortage only.** KFF/HRSA's figure is *primary-care* HPSAs. Sidelined IMGs include many specialists (the MPI/Niskanen data is not specialty-resolved), and the leverage match implicitly assumes IMGs can be placed against primary-care need. Mental-health and dental HPSAs (separate HRSA series) are excluded; states with severe *specialty* shortages may be under-ranked here.

**5. The 10-20% capture rate is an analyst construct.** It is not drawn from any authority; it is a judgment about how many sidelined physicians a clean statute actually licenses, bracketed to show sensitivity. Real capture depends on USMLE/English attainment, the recency-of-practice floors documented in M1 (many statutes require 3-5+ recent years), age and family constraints, and — critically — **employer willingness and board administrative capacity**, which M2's counter-evidence flagged as possibly the *binding* constraint regardless of statute quality. If the bottleneck is administrative rather than statutory, the "unlocked" estimates are upper bounds and the M4 board-rulemaking comment matters as much as the bill redline.

**6. Counter-evidence to the leverage thesis itself.**
   - *A clean statute is necessary but not sufficient.* M1/M2 showed several states (ID, WI, KY) already have clean enacted laws yet no visible large placement numbers, and TN's implementation stalled in board rulemaking. The composite score rewards states with big pools and big shortages, but if those states' bottleneck is supervisor scarcity or employer hiring, the "unlocked" number will not materialize from a statute alone.
   - *Shortage and supply may not co-locate within a state.* The match is at the *state* level; the spec's "county-level" ambition is only partially met because the sidelined-IMG data has no sub-state geography. A state can rank high on combined state totals while its sidelined IMGs live in the metro and its HPSAs are rural — the within-state placement problem (precisely the stranding defect M2 analyzed) is not captured by a state composite.
   - *Some apparent low-leverage states are policy-ready, high-need rural states.* States like Mississippi (#17 need) and Oklahoma (#16 need) rank low here only because they fall in the MPI fallback bucket (no measured pool) — their true sidelined-IMG supply is unknown, not zero. Conversely, New Jersey has a large pool (~3,500) but a tiny measured shortage (#48), so its high pool buys little in-state leverage even though its clean pending bill (A3987) is a good model for *other* states.

**7. Marked-speculative items.** No number in the table is presented without a basis, but the following are the softest and should be treated as order-of-magnitude only: every "national fallback ~140" cell `[derived, not measured]`; the 65,000 national anchor `[2018 advocacy estimate]`; and the 10-20% capture band `[analyst assumption, disclosed]`. Nothing is presented as a precise count; all estimates are rounded and bracketed to signal their uncertainty.
