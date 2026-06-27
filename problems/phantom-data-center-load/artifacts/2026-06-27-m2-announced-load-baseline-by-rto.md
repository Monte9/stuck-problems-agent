# M2 — Announced load baseline by RTO

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M2 (gross "announced" data-center / large-load baseline per RTO, before any de-duplication).
**Date:** 2026-06-27.
**Author:** generator (autonomous loop).

This artifact builds the **gross announced** large-load / data-center figure for each covered RTO/ISO — the numerator that M3 will haircut. It does **no de-duplication and applies no phantom fraction**; that is M3 work. Every figure carries an explicit as-of date and horizon year, because (as M1 §4 item 4 warned) mixing snapshots is itself a source of double-counting. Where a row uses an RTO's interconnection/queue figure and another uses a forecast, the reconciliation paragraph (§2) flags the definitional mismatch explicitly so M3 does not treat them as like-for-like.

A core honesty point up front: **these are different kinds of numbers across RTOs** — a study/interconnection *queue* (ERCOT, SPP), a utility *commitment / forecast* of large-load growth (PJM, MISO), and a *transmission-planning study volume* (CAISO). They are deliberately listed side-by-side here as the "announced" baseline, but they are **not summed naively** without the caveats in §2–§3.

---

## Sources used in this milestone

Carried from the M1 inventory: **S1** (LBNL *Queued Up: 2025*), **S2** (2026 PJM Load Forecast), **S3** (Utility Dive, ERCOT queue), **S4** (ERCOT board System Planning update), **S6** (POWER Magazine), **S9** (FERC show-cause). Newly added in M2 (with URLs, reachability noted 2026-06-27):

- **S12 — Wood Mackenzie press release, "US utility large-load commitments reach 160 GW amid unprecedented PJM demand surge."** Wood Mackenzie, 2025-10-27. https://www.woodmac.com/press-releases/us-utility-large-load-commitments-reach-160-gw-amid-unprecedented-pjm-demand-surge/ — supplies national large-load *commitment* total (>160 GW, "22% of 2024 US peak load") and **PJM** large-load growth (55 GW by 2030, 100 GW by 2037).
- **S13 — "MISO expects load to jump 35% by 2035 on data center growth."** Utility Dive, 2026-04-20. https://www.utilitydive.com/news/miso-long-range-forecast-data-center/817917/ — supplies MISO 2025 peak (121 GW) → 2035 peak (163 GW), and "8 GW to 14 GW of data centers will come online in 2026–2027."
- **S14 — "FERC approves SPP non-firm, large-load transmission service."** Utility Dive, 2026-06-08 (reporting SPP figures). https://www.utilitydive.com/news/ferc-spp-chills-large-load-transmission-service/822211/ — supplies **SPP** "26.4 GW in large load study requests since 2020," of which "9 GW have been disclosed as data centers."
- **S15 — "CAISO requests input on large load considerations report."** Utility Dive, 2026-01 (companion to CAISO *Large Load Considerations Issue Paper*, 2026-01-30, https://www.caiso.com/documents/issue-paper-large-load-consideration-jan-20-2026.pdf). https://www.utilitydive.com/news/caiso-california-grid-data-centers-transmission-large-loads/812440/ — supplies **CAISO** ~4.5 GW data-center demand in the 2025–2026 transmission-planning study cycle; California Energy Commission forecast +1.8 GW data-center by 2030 / +4.9 GW by 2040.
- **S16 — Grid Strategies, *National Load Growth Report 2025* ("Power Demand Forecasts Revised Up for Third Year Running").** Grid Strategies LLC, published Dec 2025. https://gridstrategiesllc.com/wp-content/uploads/Grid-Strategies-National-Load-Growth-Report-2025.pdf — supplies the **national** 5-year peak-growth forecast (~166 GW by 2030, of which ~90 GW data-center-linked) used as the denominator/cross-check for the coverage-fraction statement in §4. (PDF; figures via Utility Dive summary https://www.utilitydive.com/news/shocking-forecast-us-electricity-load-could-grow-128-gw-over-next-5-years-Grid-Strategies/734820/ and search-indexed report text, both 2025.)

All S12–S16 URLs returned usable documents on 2026-06-27 (S16 is a binary PDF; its figures are corroborated by the indexed Utility Dive summary cited alongside).

---

## 1. Announced data-center / large-load baseline by RTO

One row per RTO. "Announced load GW" is the **gross figure before de-duplication** — exactly the `A_r` input defined in M1 §3.0. The *type* of figure (queue / commitment / study-cycle) is stated in the Notes column because it governs how M3 must treat it.

| RTO / ISO | Announced data-center / large-load (GW) | As-of date | Horizon year | Source | Notes on scope / definition |
|---|---|---|---|---|---|
| **ERCOT** | **~233 GW** total large-load interconnection queue; **>70% data center → ~163 GW data-center-attributable** | End-2025 (board data) | No single horizon; in-service requests span ~2026–2031 | S3, S4 | **Interconnection/study queue** (every request ≥ ~25 MW that has entered the queue). Broadest, least-vetted definition here — ERCOT VP Kristi Hobbs: "We don't expect all of those will materialize" (S3). Includes study-stage and agreement-stage; **not** filtered for site control or offtake. ERCOT is **not FERC-jurisdictional** (M1 §4.7). |
| **PJM** | **~55 GW** new large-load growth by 2030; **100 GW by 2037** (data-center-dominated) | 2025-10-27 (Wood Mackenzie); PJM 2026 forecast posted 2026-01-14 | 2030 (55 GW) / 2037 (100 GW) | S12; S2 | **Utility commitment / forecast** of large-load growth in the PJM footprint, not a raw queue. PJM defines "large load" as an individual addition ≥ 50 MW (S2). PJM's own 2026 forecast already applied "improved vetting" and trimmed near-term MW (−4 GW summer 2027, −4.4 GW summer 2028 vs. 2025 forecast) (S2) — so 55 GW is **partially pre-vetted**, unlike ERCOT's raw queue. |
| **MISO** | **~8–14 GW** data centers online 2026–2027; **~42 GW** total peak growth 2025→2035 (121→163 GW), data-center-led; MTEP25 includes **11.6 GW** large-load additions | 2026-04-20 (forecast); MTEP25 (2025) | 2027 (8–14 GW); 2035 (42 GW peak growth) | S13 | **Forecast / transmission-plan** figure, not a raw interconnection queue. The 42 GW is *total* peak growth (data-center-led but not 100% data center); the 8–14 GW is the cleanest data-center-specific near-term number. MISO mid-case: data centers ≈ one-fifth of consumption by 2030 (S13). |
| **SPP** | **~26.4 GW** large-load study requests (≥100 MW) since 2020; **~9 GW disclosed as data center** | As of 2026-06 reporting (cumulative since 2020) | Cumulative; in-service spread; ~90 GW of forecast peak growth (all large load) over 10 yr | S14 | **Study-request queue** (≥100 MW). Only ~9 GW *disclosed* as data center; the rest is mixed industrial/manufacturing/undisclosed. SPP's own conversion history is telling: in 2022 it received 10.1 GW of requests but signed agreements for just 3.9 GW that year (S14) — a built-in attrition signal for M3. |
| **CAISO** | **~4.5 GW** data-center demand in 2025–2026 transmission-planning study cycle; CEC forecast **+1.8 GW by 2030 / +4.9 GW by 2040** | 2026-01-30 (issue paper) | 2030 (+1.8 GW) / 2040 (+4.9 GW) | S15 | **Transmission-planning study volume** + state forecast. Much smaller than Eastern RTOs; California is not a primary data-center build-out region in this cycle. The 4.5 GW (study cycle) and 1.8/4.9 GW (CEC forecast) are **different metrics** — listed together but not additive. |

**Notes on figure selection:**
- For ERCOT and PJM (the two RTOs the spec requires), the headline `A_r` carried into M3 will be **ERCOT ~163 GW data-center-attributable** (233 GW × >70%, S3/S4) and **PJM ~55 GW by 2030** (S12). These are the two largest and best-documented baselines.
- Where a range is given (MISO 8–14 GW), M3 will carry the range, not a midpoint, to avoid manufacturing false precision.

---

## 2. Reconciliation: definitional differences across RTOs

The five rows above are **not measuring the same thing**, and pretending they are would be the first way an analyst double-counts or compares apples to oranges. At least four definitional inconsistencies, of which the first two are the load-bearing ones the spec asks to be flagged:

**Inconsistency 1 — Raw queue vs. vetted forecast (the biggest apples-to-oranges).** ERCOT's ~233 GW (S3, S4) and SPP's ~26.4 GW (S14) are **raw interconnection/study queues**: any request that entered, with little or no filter for site control, offtake, or duplicate filings. PJM's ~55 GW (S12) and MISO's 8–14 GW / 42 GW (S13) are **forecasts/commitments that have already been partly vetted** — PJM explicitly trimmed near-term MW after "improved vetting" (S2). Summing a raw queue (ERCOT, SPP) with a pre-vetted forecast (PJM, MISO) treats unvetted and vetted MW as equivalent. **Consequence:** the phantom fraction `P_r` in M3 must be *larger* for the raw-queue RTOs (ERCOT, SPP) than for the partly-vetted ones (PJM, MISO), or we will over-haircut PJM/MISO and under-haircut ERCOT/SPP. This is exactly why M1 §3 made `P_r` per-RTO rather than a single national number.

**Inconsistency 2 — Different horizon years and accumulation windows (a timing double-count).** ERCOT's queue is a *snapshot of all in-queue requests* (in-service dates spanning ~2026–2031); PJM's 55 GW is *growth by a fixed year (2030)*; SPP's 26.4 GW is *cumulative since 2020*; CAISO's 1.8/4.9 GW are *2030/2040 forecast levels*. Adding a cumulative-since-2020 figure (SPP) to a snapshot (ERCOT) to a by-2030 growth figure (PJM) mixes stocks and flows over different windows. **Consequence:** the same calendar MW can appear in two RTOs' figures for different horizon years, and M3's category `b_r` (announced-vs-building / timing phantom, M1 §3.3) must be applied per-horizon-year, not to the blended total.

**Inconsistency 3 — "Data center" vs. "all large load."** ERCOT (>70% data center, S3), SPP (~9 of 26.4 GW disclosed as data center, S14), and MISO (42 GW is *total* peak growth, only "data-center-led", S13) bundle non-data-center industrial load into the headline number to varying, inconsistently-reported degrees. The data-center-*attributable* share is explicit for ERCOT and SPP but only approximate for MISO/PJM. M3 must use the data-center-attributable sub-figure where disclosed (ERCOT 163 GW, SPP 9 GW) and flag MISO/PJM as "large-load incl. data center."

**Inconsistency 4 — Minimum-size threshold differs.** "Large load" is ≥50 MW in PJM (S2), ≥100 MW for the SPP study-request figure (S14), and effectively ~25 MW for ERCOT's queue. A lower threshold sweeps in more (and smaller, more speculative) projects, inflating ERCOT's count relative to SPP's on definition alone.

---

## 3. Why these figures are *not* simply summed

Because of Inconsistencies 1–4, a naive sum of the announced column would (a) add raw queues to vetted forecasts, (b) mix cumulative, snapshot, and by-year figures, and (c) blend data-center-only with all-large-load numbers. The national total in §4 is therefore presented **two ways** — a wide naive sum (clearly labeled as an over-count ceiling) and an independent national anchor (Wood Mackenzie / Grid Strategies) — so the reader can see the gap that M3's de-duplication must close.

---

## 4. National total and coverage fraction

**Naive sum of the data-center-attributable rows (labeled as an over-count ceiling, NOT a de-duplicated estimate):**

- ERCOT ~163 GW (data-center share of queue, S3/S4) + PJM ~55 GW by 2030 (S12) + MISO ~8–14 GW near-term data-center, or ~42 GW total peak growth (S13) + SPP ~9 GW disclosed data-center (S14) + CAISO ~1.8–4.5 GW (S15)
- **≈ 237 GW (using MISO 8 GW near-term) to ≈ 274 GW (using MISO 42 GW total peak growth).**

**This naive sum is explicitly an upper-bound ceiling, not a load estimate.** It double-counts across the inconsistencies in §2 and mixes horizons; M3 exists precisely to deflate it.

**Independent national anchors (for cross-check and coverage):**
- Wood Mackenzie (S12, 2025-10-27): US utility large-load *commitments* total **>160 GW, ≈ 22% of 2024 US peak load** — across all RTOs.
- Grid Strategies (S16, Dec 2025): 5-year national peak-growth forecast **~166 GW by 2030, of which ~90 GW data-center-linked** (~55% of growth).

**Coverage fraction of US load represented by these rows:** The five RTOs here — ERCOT, PJM, MISO, SPP, CAISO — are five of the seven FERC-recognized/major US grid operators. Per LBNL (S1), interconnection-queue data spans grid operators covering **~97% of US generation capacity**; the major RTOs/ISOs together serve roughly **two-thirds of US electricity load** (the rest is in non-RTO regions of the Southeast, West, and Mountain states). The two RTOs **not** included here are **NYISO** and **ISO-NE**, both relatively small data-center markets and both named in the FERC June-2026 show-cause orders (S9). 

A defensible coverage statement: **the five RTOs in this table capture the large majority — on the order of 85–90% [speculative, see Limitations] — of *announced US data-center large-load*, because announced data-center load is heavily concentrated in ERCOT, PJM, and MISO**, the three largest figures above. This concentration is corroborated by the national anchors: if national data-center-linked growth is ~90 GW by 2030 (S16) and committed large load is ~160 GW (S12), the ERCOT+PJM data-center figures alone (~218 GW gross queue/forecast) already exceed those de-duplicated national totals — which is itself direct evidence of the phantom/over-count problem this project exists to quantify. **The fact that the un-deduplicated RTO rows sum to more than the best national de-duplicated estimate (160–166 GW) is the headline finding that M3 will turn into a phantom fraction.**

---

## 5. Limitations & counter-evidence

1. **The naive sum is a deliberate over-count, not an estimate.** Per §2–§3, summing raw queues, vetted forecasts, cumulative figures, and snapshots across different horizon years and size thresholds inflates the total. The ~237–274 GW ceiling should never be quoted as "announced US data-center load" without the de-duplication M3 supplies. Direction of bias: **high**.
2. **RTO figures are different metric *types*** (queue vs. commitment vs. study-cycle vs. CEC forecast). This is the central apples-to-oranges risk (§2, Inconsistency 1) and the reason M3 applies per-RTO phantom fractions rather than one national haircut.
3. **The 85–90% coverage fraction is [speculative].** It is inferred from the concentration of large figures in ERCOT/PJM/MISO and from the LBNL ~97%-capacity-coverage and Grid Strategies national figures (S1, S16), not from a published per-RTO data-center-load census (which does not exist — that absence is the problem this project addresses). NYISO and ISO-NE are omitted as small data-center markets but were not quantified here; their inclusion would raise the total modestly. Direction: omission biases the sum **low**, but only slightly.
4. **As-of dates are not aligned.** ERCOT is end-2025 board data (S3, S4); PJM commitment figure is 2025-10-27 (S12) with the 2026 forecast 2026-01-14 (S2); MISO is 2026-04-20 (S13); SPP is mid-2026 cumulative (S14); CAISO is 2026-01-30 (S15). All are within ~9 months and all < 12 months old, so none is stale, but M3 must not treat them as a single instant.
5. **MISO's 42 GW is total peak growth, not pure data center.** Using it as the data-center figure over-states MISO's data-center baseline; the 8–14 GW near-term (S13) is the cleaner data-center-specific number, but covers only 2026–2027. The honest MISO data-center horizon-2035 figure is **not cleanly published** — a genuine gap.
6. **SPP's 9 GW is "disclosed" data center only.** Some of the remaining ~17 GW of its 26.4 GW study requests are likely data centers filed without disclosure (S14), so 9 GW may **under-state** SPP's data-center baseline. Direction: **low** for SPP specifically.
7. **Counter-evidence that the baselines are real, not phantom.** Wood Mackenzie's independent ~160 GW *commitment* figure (S12) and Grid Strategies' ~90 GW data-center-linked national growth (S16) are large even after the vetting that operators have already applied. Sophisticated grid operators with every incentive to filter (PJM's "improved vetting," S2) still forecast 55 GW by 2030. The M2 baseline is genuinely large; M3's task is to bound the phantom *fraction*, not to claim the announced load is fictional.
8. **PJM "55 GW by 2030" is a forecast, not a queue total.** A raw PJM interconnection-queue large-load number (analogous to ERCOT's 233 GW) is not cleanly published as a single figure; using the vetted forecast makes PJM's baseline *more conservative* (smaller) than ERCOT's raw queue — which means cross-RTO phantom fractions in M3 are not directly comparable and must be read with each row's definition.

---

## 6. Self-verification against M2 done-criteria

- [x] **≥ 4 RTOs/ISOs including PJM and ERCOT, each with a GW figure, as-of date, and horizon year:** 5 RTOs (ERCOT, PJM, MISO, SPP, CAISO); PJM and ERCOT both present. Each row has GW, as-of date, horizon year (§1).
- [x] **Every announced-load figure cites a source:** ERCOT (S3, S4), PJM (S12, S2), MISO (S13), SPP (S14), CAISO (S15); national anchors (S12, S16). No figure unsourced. The one [speculative] number (85–90% coverage fraction) is explicitly tagged.
- [x] **Reconciliation paragraph flags ≥ 2 definitional inconsistencies:** §2 flags four (raw-queue-vs-vetted-forecast, horizon/accumulation-window, data-center-vs-all-large-load, size threshold), with the double-counting consequence stated for each.
- [x] **Clearly-labeled national total with coverage-fraction statement:** §4 gives a naive sum (~237–274 GW, labeled an over-count ceiling), independent national anchors (160 GW / 166 GW), and a coverage statement (~85–90% of announced US data-center load, [speculative]), plus the key finding that the un-deduplicated rows exceed the de-duplicated national total.
- [x] **Limitations & counter-evidence section present** (§5), with bias directions.
