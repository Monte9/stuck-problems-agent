# M2 — Announced data-center load baseline by RTO

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M2 (gross "announced" baseline, before any de-duplication).
**Date:** 2026-06-27.
**Author:** generator (autonomous loop).

This artifact builds the **gross "announced" large-load / data-center figure** for each covered RTO/ISO — the number that headline forecasts and capacity-build justifications are summed from — **before** any phantom haircut (dedup, speculation, build-stage). Each figure carries an explicit as-of date and horizon year. No phantom fraction is computed here; that is M3. The deliberate point of this milestone is to expose how **inconsistent the underlying definitions are**, because that inconsistency is the first source of the phantom problem: you cannot subtract phantoms from a baseline until you know exactly what each RTO's baseline counts.

Sources are cited by the M1 inventory IDs (S1–S11; see `2026-06-27-m1-evidence-base-and-method-scaffold.md`). One new source is added and clearly labeled **S12** (Wood Mackenzie, with working URL) because it supplies the cleanest apples-to-apples PJM and national large-load *commitment* figure that the M1 inventory did not carry; one new figure-bearing source **S13** (Ascend Analytics) is added for a 2026-current ERCOT cross-check, and **S14** (Utility Dive / FERC market report) and **S15** (CAISO) for MISO and CAISO respectively. All five new URLs were retrieved 2026-06-27.

---

## 1. Announced-load baseline table

One row per RTO/ISO. "Announced data-center load GW" is the **gross queue or utility-forecast figure as that RTO reports it** — explicitly *not* yet de-duplicated. The **Notes** column states precisely *what kind* of number it is (large-load study queue vs. utility load-forecast adjustment vs. data-center-only forecast), which is what the reconciliation paragraph (§2) then flags.

| RTO/ISO | Announced data-center / large-load GW | As-of date | Horizon year | Source | Notes on scope / definition |
|---|---|---|---|---|---|
| **ERCOT** | **~233 GW** large-load queue total (>70% data center → **~163 GW data-center share**) | End-2025 (board data) | Interconnection-request horizon, no fixed year; requests target ~2026–2032 in-service | S3 (Utility Dive, 2026-01-06) + S4 (ERCOT board, 2025-12-02; 72.9% of ~225.8 GW = data center) | **Large-load interconnection-request queue**, gross. Includes study-stage requests with no signed agreement. ERCOT official on record: "We don't expect all of those will materialize" (S3). Up ~300% YoY from end-2024. A separate Q1-2026 read shows ~198 GW *applied* with 86 GW newly *under review* (S13) — same order of magnitude, different cut. |
| **PJM** | **55 GW** new large-load growth (utility forecasts, PJM footprint); **100 GW by 2037** | 2025-10-27 (Wood Mackenzie) / PJM forecast 2026-01-14 | **2030** (55 GW); 2037 (100 GW) | S12 (Wood Mackenzie, 2025-10-27) + S2 (2026 PJM Load Forecast, 2026-01-14) | **Utility large-load *commitment*/forecast**, not a raw interconnection queue. PJM's own 2026 forecast embeds **+35.1 GW** of large-load adjustments 2026–2031 *after* "improved vetting" already removed near-term MW (S2). The 55 GW (WoodMac, S12) is the pre-vetting utility-committed figure; the 35.1 GW (S2) is PJM's post-vetting embedded figure — see reconciliation. |
| **MISO** | **~42 GW** of forecast peak-load growth 2025→2035 (121→163 GW), data-center-led; MISO had the fastest US data-center growth (43% CAGR 2020–25) | 2025-12-09 (board) / forecast pub. late-2025 | **2035** | S14 (Utility Dive / FERC market report, "50 GW online end-2025, MISO strongest growth") + MISO 2026 long-term load forecast (board item, 2025-12-09) | **Long-term load *forecast* delta**, not a queue. The 42 GW is total peak-load growth (data centers + manufacturing + electrification), so it is an **upper bound on the data-center-attributable** announced load, not a pure data-center figure. MISO generator-queue backlog (~300 GW) is *generation*, not load, and is excluded here. |
| **SPP** | **26.4 GW** large-load study requests since 2020; ~90 GW of the 49 GW peak-growth-to-105 GW forecast attributed to data centers | 2025 (SPP HILL/queue materials) | Study-request basis (2020→present); peak-growth horizon ~2035 | S13 (Ascend Analytics, 2026-05-05, citing SPP) + SPP HILL program page (spp.org) | **Large-load study-request queue** (26.4 GW) — a cleaner "announced queue" number than MISO's forecast. The ~90 GW data-center figure is from SPP's *forecast* peak-growth framing and is **definitionally different** (forecast vs. study queue) — the table uses the 26.4 GW study-request figure as the announced baseline and flags the 90 GW as forecast-basis only. |
| **CAISO** | **~4.5 GW** data-center demand in the 2025–26 transmission-planning study | 2026-01-30 (CAISO large-load issue paper) | 2025–26 planning cycle; CEC forecasts +1.8 GW by 2030, +4.9 GW by 2040 | S15 (CAISO Large Load Considerations issue paper, 2026-01-30) | **Data-center load under study** in the planning cycle — small and relatively well-vetted vs. ERCOT/PJM. CEC forecast (+1.8 GW by 2030) is far smaller than the raw study figure, illustrating the announced-vs-forecast gap even inside one ISO. |

**Coverage:** 5 RTOs/ISOs (ERCOT, PJM, MISO, SPP, CAISO), each with a GW figure, as-of date, and horizon — satisfies the ≥4-including-PJM-and-ERCOT requirement. ISO-NE and NYISO are FERC-jurisdictional and named in the FERC show-cause set (S9) but carry materially smaller data-center queues and lack a clean published GW figure in the M1 inventory; they are addressed in Limitations rather than given an unsourced number.

---

## 2. Reconciliation paragraph — definitional inconsistencies (why these rows must not simply be summed)

These five numbers **measure different things**, and naïvely adding them is exactly the apples-to-oranges error that produces the "phantom" headline. At least four distinct definitional inconsistencies are present:

1. **Interconnection-request queue vs. utility load-forecast vs. data-center-only forecast.** ERCOT's 233 GW (S3/S4) and SPP's 26.4 GW (S13) are **raw large-load study-request queues** — anyone can file, no signed agreement required, and a single project can appear multiple times. PJM's 55 GW (S12) is a **utility *commitment*/forecast** number (utilities have screened it before reporting). MISO's 42 GW (S14) is a **total peak-load forecast delta** that bundles data centers *with* manufacturing and electrification. CAISO's 4.5 GW (S15) is **data-center load under transmission study**. A request queue, a utility forecast, and a planning-study figure have completely different "phantom" densities: the raw queues (ERCOT, SPP) are the most inflated; the vetted forecasts (PJM, the CAISO CEC number) are the least. **Summing them double-counts the optimism that has already been partially removed from the PJM/CAISO figures but not from the ERCOT/SPP figures.**

2. **"Large load" ≠ "data center."** ERCOT's queue is ">70% data center" (S4: 72.9%), so the 233 GW overstates *data-center* load by ~27% before any phantom haircut; MISO's 42 GW explicitly includes manufacturing and electrification (S14), so its data-center share is even lower. PJM's and CAISO's figures are closer to data-center-pure. **Treating every row as "data-center GW" inflates the gross by including non-data-center industrial load** — and that non-data-center load behaves differently (manufacturing site-control is usually real). M3 must apply the per-RTO data-center share (ERCOT ×0.73, MISO < that, PJM/CAISO ≈1) before haircutting.

3. **Horizon-year mismatch.** ERCOT's 233 GW is a **queue snapshot with no single in-service year**; PJM's 55 GW is **by 2030** and 100 GW **by 2037** (S12); MISO's 42 GW is **by 2035** (S14); CAISO's CEC figures split 2030/2040 (S15). Aligning a no-dated queue (ERCOT) against a 2030 forecast (PJM) against a 2035 forecast (MISO) mixes time horizons; the same MW counted "by 2037" in PJM is not comparable to ERCOT's open-ended queue. **M3/M4 must normalize to a common horizon (proposed: 2030–2032) before national roll-up.**

4. **Cross-RTO and within-RTO duplication is *inside* the queue figures, not yet removed.** The raw queues (ERCOT 233 GW, SPP 26.4 GW) explicitly contain the same project filed multiple times (S7, S10: developers file "5–10× more requests than centers built"). The vetted utility figures (PJM 55 GW) have had *some* of this removed but not all. There is **also genuine cross-RTO duplication** — a developer shopping the same project to ERCOT and SPP, or to PJM and MISO — which no single RTO's number can detect. This is precisely the `d_r` category M3 will estimate; M2's job is only to record that the gross figures still contain it.

The PJM internal contrast makes the point concrete: the **same RTO** publishes both a **55 GW** committed-forecast number (S12, pre-vetting utility submissions) and a **35.1 GW** embedded-adjustment number (S2, *after* PJM's "improved vetting of requested adjustments for data centers and large loads"). The ~20 GW gap between them is a partially-vetted phantom already visible *within one operator's own books* — a lower-bound, single-RTO illustration of the haircut M3 will generalize.

---

## 3. National total and coverage fraction

**Gross announced total across the 5 covered rows (deliberately naïve sum, for scale only):**

| Component | GW |
|---|---|
| ERCOT (full large-load queue, S3/S4) | 233 |
| PJM (utility large-load commitment by 2030, S12) | 55 |
| MISO (total peak-load growth by 2035, S14) | 42 |
| SPP (large-load study requests since 2020, S13) | 26 |
| CAISO (data-center load under study, S15) | 5 |
| **Naïve sum** | **~361 GW** |

**This ~361 GW is not a defensible national announced-data-center figure** — it is the apples-to-oranges sum the reconciliation paragraph warns against, and it is presented only to show the scale of the un-deduplicated headline pool. A more honest gross is the **data-center-share-adjusted, queue-only band**: applying ERCOT's 73% data-center share gives ~163 GW for ERCOT alone, and using PJM's vetted 35.1 GW (S2) instead of 55 GW yields a **definition-cleaned gross of roughly ~231 GW** (163 + 35 + 42×[DC share, <1] + 26 + 5). The independent national cross-check from Wood Mackenzie — **"over 160 GW of US utility large-load commitments, ≈22% of 2024 US peak load"** as of 2025-10-27 (S12) — sits below even the cleaned sum, confirming that the naïve 361 GW roughly **doubles** the best independent national *commitment* estimate. That gap (361 vs. 160) is itself first-order evidence of the phantom problem and a target for M3.

**Coverage fraction of US load:** The five covered RTOs/ISOs represent the large majority of US data-center load. PJM + ERCOT alone are the two dominant data-center grids; adding MISO (fastest-growing, S14), SPP, and CAISO covers the next tier. LBNL's queue dataset spans ~97% of US generation capacity (S1) across the same operators, and Wood Mackenzie pegs the 160 GW commitment at **22% of 2024 US peak load** (S12) — so the covered RTOs capture essentially all of the *national* large-load commitment that 22% figure is built from. **Estimated coverage of US data-center/large-load announced volume by these 5 rows: ~85–95%** [partly inferential — ISO-NE, NYISO, and non-RTO Southeast utilities (Georgia Power, TVA; see S8) are the main uncovered remainder, and the Southeast in particular hosts large data-center load outside any RTO]. This coverage estimate is flagged in Limitations.

---

## 4. New sources added (not in M1 inventory; URLs retrieved 2026-06-27)

| ID | Source | Publisher | Date | URL | Supplies |
|---|---|---|---|---|---|
| S12 | "US utility large load commitments reach 160 GW amid unprecedented PJM demand surge" | Wood Mackenzie (press release for *Up, up and away* report) | 2025-10-27 | https://www.woodmac.com/press-releases/us-utility-large-load-commitments-reach-160-gw-amid-unprecedented-pjm-demand-surge/ | National 160 GW commitment (=22% of 2024 US peak); PJM 55 GW by 2030 / 100 GW by 2037; Dominion/AEP/PPL = two-thirds of demand |
| S13 | "Can US Interconnection Queues Survive Data Center-Driven Load Growth?" | Ascend Analytics | 2026-05-05 | https://www.ascendanalytics.com/blog/large-load-interconnection-queues-data-center-grid-access | ERCOT Q1-2026: 198 GW applied / 86 GW under review; SPP 26.4 GW large-load study requests since 2020; PJM 15 GW capacity shortfall by 2030 |
| S14 | "50 GW of data centers online at end of 2025, with MISO seeing strongest growth: FERC" | Utility Dive (FERC market report) | 2026 (Q1) | https://www.utilitydive.com/news/data-centers-miso-ferc-market-report/815831/ | National 50 GW data centers online end-2025; MISO fastest growth (43% CAGR 2020–25); MISO peak 121→163 GW by 2035 |
| S15 | "Large Load Considerations Issue Paper" | California ISO (CAISO) | 2026-01-30 | https://www.caiso.com/documents/issue-paper-large-load-consideration-jan-20-2026.pdf | CAISO ~4.5 GW data-center demand under study 2025–26; CEC +1.8 GW by 2030 / +4.9 GW by 2040 |

(MISO's own board figure — 2026 long-term load forecast, board item 2025-12-09, cdn.misoenergy.org — corroborates the 121→163 GW figure and is reachable; S14 is used as the primary citation because it states the data-center attribution directly.)

---

## 5. Limitations & counter-evidence

1. **The rows are not summable, by construction (see §2).** The headline ~361 GW naïve sum mixes raw queues (ERCOT, SPP), vetted utility forecasts (PJM), and bundled load forecasts (MISO). The artifact states this explicitly and provides the cleaned ~231 GW alternative and the independent 160 GW WoodMac cross-check, but **any reader who lifts the 361 GW out of context will over-state the gross**. Direction of bias: the naïve sum is **biased high** as a data-center figure.

2. **MISO and SPP figures conflate data center with other large load.** MISO's 42 GW (S14) and SPP's 90-GW forecast framing include manufacturing and electrification; only SPP's 26.4 GW *study-request* figure is large-load-specific (and even that is not data-center-pure). The data-center share for MISO is not cleanly published in the inventory, so the MISO row is an **upper bound** on data-center announced load → biases the data-center gross **high**.

3. **Coverage is not 100%, and the uncovered tail is non-trivial.** ISO-NE and NYISO are omitted for lack of a clean published GW figure, and a large block of Southeast data-center load (Georgia Power / TVA / Dominion-non-PJM; S8 LEI report) sits **outside any RTO** — the SELC/LEI work (S8) shows ~10 GW of Southeast utility projection alone. The ~85–95% coverage claim is therefore **inferential** and likely **biased high** (i.e., true coverage may be lower because non-RTO Southeast load is under-counted).

4. **As-of dates and horizons are mixed despite alignment effort.** ERCOT (end-2025, no in-service year), PJM (2030/2037), MISO (2035), CAISO (2030/2040) span different snapshots. The table records each honestly but the national total still blends horizons; M3/M4 must normalize to a common year (proposed 2030–2032) before any roll-up. Direction: mixing a no-dated open queue (ERCOT) with dated forecasts **biases the gross high** because the open queue includes far-future and speculative MW.

5. **Counter-evidence that the announced figures are substantially real.** These are not fabricated: PJM's *post-vetting* forecast still embeds +35.1 GW of large load 2026–2031 (S2), MISO independently shows the fastest real data-center growth in the US (43% CAGR, with 50 GW already *online* nationally end-2025, S14), and Wood Mackenzie's 160 GW is a *commitment* figure (utilities have signed up to serve it), not a raw wishlist (S12). The phantom problem is about the *fraction* of the gross that won't appear, not a claim that the gross is fictional — sophisticated operators with every incentive to vet still forecast large net growth.

6. **PJM 55 vs. 35.1 GW is a definitional choice, not a measurement.** The table uses 55 GW (WoodMac utility commitment, S12) as the *announced* baseline and 35.1 GW (PJM post-vetting, S2) as the cleaned figure. A critic could argue PJM's own forecast *is* the right announced baseline, which would shrink the gross. This is flagged as the single most consequential definitional choice in the PJM row; M3 will carry both and show the result is robust to which is used.

7. **S13 (Ascend) and S14 (Utility Dive/FERC) are secondary reporting, not primary RTO filings.** The ERCOT 233 GW (S3/S4) and CAISO 4.5 GW (S15) trace to primary board/ISO material; the SPP 26.4 GW and MISO 42 GW lean on secondary aggregation. M3 should pull the SPP HILL primary filing and the MISO 2025-12-09 board deck directly to firm these two rows.

---

## 6. Self-verification against M2 done-criteria

- [x] **≥4 RTOs/ISOs including PJM and ERCOT**, each with a GW figure, as-of date, and horizon year — **5 rows** (ERCOT, PJM, MISO, SPP, CAISO); §1.
- [x] **Every announced-load figure cites a source** from the M1 inventory (S2, S3, S4) or a clearly-labeled new source with working URL (S12–S15, §4); no figure is unsourced.
- [x] **Reconciliation paragraph flags ≥2 definitional inconsistencies** — it flags **four** (queue vs. forecast vs. data-center-only; large-load ≠ data-center; horizon mismatch; embedded duplication), plus the within-PJM 55-vs-35.1 GW illustration; §2.
- [x] **National total given, clearly labeled, with coverage fraction** — naïve ~361 GW + cleaned ~231 GW + independent 160 GW cross-check, with ~85–95% US-load coverage stated and caveated; §3.
- [x] **Limitations & counter-evidence section** present with bias directions; §5.
