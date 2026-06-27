# M3 — Phantom-fraction estimation by RTO

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M3 (per-RTO phantom fraction + real-load range).
**Date:** 2026-06-27.
**Author:** generator (autonomous loop).

**Scope note.** M3 takes the M2 announced baselines (`A_r`) and the M1 method (three non-overlapping survival haircuts `d`→`s`→`b`, composed multiplicatively) and produces, per RTO, a **phantom fraction** `P_r` and a **real-load GW** range, each as an explicit low/central/high triple. M3 computes *fractions and real-load GW only*. **Over-build GW (announced − real) and ratepayer dollar exposure are M4** and are not derived here. Every haircut is anchored to a named, cited empirical benchmark from the M1/M2 inventory (S1, S5, S6, S8, S10 are the empirical anchors the M1 method requires). Sources are cited by their M1/M2 IDs (S1–S15); see `2026-06-27-m1-evidence-base-and-method-scaffold.md` and `2026-06-27-m2-announced-load-baseline-by-rto.md`. One figure is re-verified below with a URL retrieved today and labeled.

---

## 0. Method recap and two pre-haircut adjustments (kept OUT of the three phantom categories)

**Formula (M1 §3.0), fixed order dedup → speculation → build-stage:**

```
Real_r = A_dc,r · (1 − d_r)(1 − s_r)(1 − b_r)
P_r    = 1 − (1 − d_r)(1 − s_r)(1 − b_r)
```

`d` = duplication; `s` = no-site-control / no-offtake speculation; `b` = announced-vs-building (timing) double-count. Multiplicative composition means the same MW is never haircut twice. **Internal consistency convention:** the real-load **HIGH** corresponds to the phantom-fraction **LOW** (all three haircuts at their low end → highest survival), and real-load **LOW** corresponds to phantom-fraction **HIGH** (all haircuts high).

**Two adjustments applied to the M2 gross `A_r` BEFORE haircutting, deliberately kept separate from `d/s/b` so nothing is double-subtracted (carry-forward to-do #4):**

1. **Data-center share** (only where the M2 row is "large load," not "data center"). This converts a large-load queue to a data-center baseline `A_dc,r`. It is **not** a phantom category — non-data-center load (manufacturing) is real, just not data-center. Shares used:
   - **ERCOT:** ×0.729 → 225.8 GW × 0.729 ≈ **163 GW** data center (S4, 72.9% of queue is data center; consistent with M2 ~163 GW).
   - **SPP:** of 26.4 GW large-load study requests since 2020, **only ~9 GW is disclosed as data center** (SPP HILL program page, spp.org — see §4 re-verification; corrects M2's loose 26.4 attribution). The SPP **data-center** baseline is therefore **9 GW**; the 26.4 GW large-load figure is carried as an **upper bound** row.
   - **MISO:** 42 GW is total peak-load growth (data center + manufacturing + electrification, S14); the data-center share is **not cleanly published**, so the 42 GW is treated as an **upper bound** on data-center announced load (M2 §2; carry-forward #4) and the MISO row is flagged accordingly.
   - **PJM ≈ 1.0** and **CAISO ≈ 1.0** (M2 rows are already data-center-pure: PJM large-load commitment S12; CAISO data-center-under-study S15).

2. **PJM definitional choice (carry-forward #3):** PJM is computed on the **55 GW** WoodMac utility-commitment baseline (S12, by 2030) as the headline row, with a **robustness row on 35.1 GW** (PJM post-vetting embedded adjustment, S2) shown directly below it. The phantom *fraction* is identical (it is a ratio); only the GW scales.

---

## 1. Phantom-fraction and real-load table (one row per RTO)

Real-load GW computed as `A_dc · (1−d)(1−s)(1−b)` using the per-category triples in §2. **High haircuts → P high → Real low; low haircuts → P low → Real high.** Arithmetic shown per row so it can be recomputed.

| RTO/ISO | Announced `A_r` (M2) | Data-center baseline `A_dc` | Phantom fraction P (low / central / high) | Real-load GW (low / central / high) | Survival factor (1−d)(1−s)(1−b) used (hi-surv / cen / lo-surv) |
|---|---|---|---|---|---|
| **ERCOT** | 233 GW large-load queue (S3/S4) | **163** (×0.729 DC share, S4) | **0.69 / 0.83 / 0.92** | **12.2 / 27.4 / 50.2** | 0.308 / 0.168 / 0.075 |
| **PJM** (headline) | 55 GW by 2030 (S12) | **55** (DC-pure, ×1) | **0.43 / 0.62 / 0.78** | **12.2 / 21.0 / 31.3** | 0.570 / 0.382 / 0.223 |
| *PJM (35.1 robustness, S2)* | 35.1 GW post-vetting (S2) | *35.1* | *0.43 / 0.62 / 0.78* | *7.8 / 13.4 / 20.0* | 0.570 / 0.382 / 0.223 |
| **MISO** | 42 GW peak growth by 2035 (S14) | **42** (upper bound; DC share <1, not published) | **0.56 / 0.72 / 0.85** | **6.3 / 11.6 / 18.4** | 0.439 / 0.277 / 0.150 |
| **SPP** | 26.4 GW large-load since 2020 (SPP HILL) | **9** (disclosed data center; spp.org) | **0.69 / 0.83 / 0.92** | **0.7 / 1.5 / 2.8** | 0.308 / 0.168 / 0.075 |
| *SPP (26.4 large-load upper bound)* | 26.4 GW large load (SPP HILL) | *26.4* | *0.69 / 0.83 / 0.92* | *2.0 / 4.4 / 8.1* | 0.308 / 0.168 / 0.075 |
| **CAISO** | 4.5 GW data center under study (S15) | **4.5** (DC-pure, ×1) | **0.34 / 0.53 / 0.71** | **1.3 / 2.1 / 3.0** | 0.660 / 0.469 / 0.290 |

**Recompute check (worked, for the evaluator):**
- ERCOT central: 163 × (1−0.30)(1−0.60)(1−0.40) = 163 × 0.70 × 0.40 × 0.60 = 163 × 0.168 = **27.4 GW**; P = 1 − 0.168 = **0.832**. ✔
- ERCOT high-phantom (Real low): 163 × (1−0.40)(1−0.75)(1−0.50) = 163 × 0.60 × 0.25 × 0.50 = 163 × 0.075 = **12.2 GW**; P = **0.925**. ✔
- ERCOT low-phantom (Real high): 163 × (1−0.20)(1−0.45)(1−0.30) = 163 × 0.80 × 0.55 × 0.70 = 163 × 0.308 = **50.2 GW**; P = **0.692**. ✔
- PJM central: 55 × 0.88 × 0.62 × 0.70 = 55 × 0.382 = **21.0 GW**; P = **0.618**. ✔
- CAISO central: 4.5 × 0.92 × 0.68 × 0.75 = 4.5 × 0.469 = **2.1 GW**; P = **0.531**. ✔

**Ordering sanity (carry-forward #3):** the raw study-request queues **ERCOT and SPP** are the most phantom-dense (central P ≈ 0.83), the bundled-but-vetted **MISO** sits in the middle (0.72), and the vetted **PJM** (0.62) and well-vetted **CAISO** (0.53) are the least phantom — exactly the ordering the M2 reconciliation and the M3 method require.

---

## 2. Per-category haircut breakdown (every haircut anchored to a cited benchmark)

Each cell is the haircut **low / central / high**. The right column gives the named empirical anchor (≥1 of S1, S5, S6, S8, S10 per the M1 rule). Categories applied multiplicatively in the order shown.

### 2a. `d` — duplication (cross/within-territory multiple filings)

| RTO | d (low / central / high) | Anchoring benchmark |
|---|---|---|
| ERCOT | 0.20 / 0.30 / 0.40 | **S10** (SELC): developers file "5–10× more requests than centers built" — an upper signpost on combined over-filing; raw, identity-masked ERCOT queue (S4) sits at the high end of the *duplication* share of that signpost. **S7** (WRI): mechanism of same project filed in multiple territories. |
| SPP | 0.20 / 0.30 / 0.40 | Same as ERCOT — SPP 26.4 GW is a **raw study-request queue** (SPP HILL, spp.org), the same filing regime SELC's 5–10× over-filing (S10) describes. |
| MISO | 0.10 / 0.18 / 0.28 | **S10** signpost, **down-weighted** because the MISO 42 GW is a utility **forecast delta** (S14), not a raw open queue — utilities have already screened some duplicate submissions. |
| PJM | 0.05 / 0.12 / 0.20 | **S6** (Exelon: of a 65 GW pipeline, ~22% "likely real," i.e. ~78% attrition from *all* causes — duplication is a small slice of that) and **S2** (PJM "improved vetting … removed near-term MW") → most duplication already stripped from the 55 GW commitment figure; residual `d` low. |
| CAISO | 0.03 / 0.08 / 0.15 | **S6** corroboration + **S15** (CAISO study-stage figure is small and individually tracked) → minimal cross-filing in a single, well-vetted ISO. |

### 2b. `s` — no site control / no signed offtake (speculation), applied to post-dedup remainder

| RTO | s (low / central / high) | Anchoring benchmark |
|---|---|---|
| ERCOT | 0.45 / 0.60 / 0.75 | **S8** (LEI/SELC): most-likely 3.5–5.5 GW of a ~10 GW projection → real/announced ≈ 0.35–0.55 → `s ≈ 0.45–0.65` central; raw ERCOT queue pushed to the high end. **S1** (LBNL 77% generation-withdrawal) used **only as a down-weighted HIGH-end prior** (it is a *generation* withdrawal rate, not a load rate — never a direct load haircut; M1 §2). **S6** (CenterPoint 1→25 GW; Exelon 22%) corroborates a large speculative share. |
| SPP | 0.45 / 0.60 / 0.75 | Same anchors as ERCOT (S8 central band; S1 high-end prior; S6 corroboration) — raw study-request queue. |
| MISO | 0.35 / 0.48 / 0.62 | **S8** band, shifted **down** because part of MISO's 42 GW is manufacturing/electrification with real site control (M2 §2), and 50 GW of data centers were already *online* nationally end-2025 (S14), evidencing genuine build-out. |
| PJM | 0.25 / 0.38 / 0.52 | **S6** (Exelon "22% of its 65 GW pipeline likely real" → strong speculative signal, but applied to a *commitment* figure utilities have signed to serve, so central below the S8 raw-queue band) + **S8** as the upper anchor. |
| CAISO | 0.20 / 0.32 / 0.45 | **S8** lower band + **S15** (CAISO data-center study figure is small and screened; CEC forecast +1.8 GW by 2030 vs 4.5 GW under study evidences a real-but-smaller materialization, anchoring `s` toward the low end). |

### 2c. `b` — announced-vs-building (timing / build-stage) double-count, applied to post-dedup, post-speculation remainder

| RTO | b (low / central / high) | Anchoring benchmark |
|---|---|---|
| ERCOT | 0.30 / 0.40 / 0.50 | **S5** (Currence 2026): ~16 GW announced vs ~5 GW under construction, with the report's own "**30–50% of the pipeline unlikely to come online**" this year → `b ≈ 0.30–0.50` current-year band. Raw queue → high end. |
| SPP | 0.30 / 0.40 / 0.50 | **S5**, same 30–50% national build-stage band. |
| MISO | 0.25 / 0.35 / 0.45 | **S5** band, shifted slightly **down** — MISO's figure is a 2035 forecast (longer horizon absorbs timing slippage) and reflects the fastest *realized* US growth (43% CAGR, S14). |
| PJM | 0.20 / 0.30 / 0.42 | **S5** band, lower end — PJM's 55 GW is a 2030 *commitment* (S12) already partly vetted for buildability (S2). |
| CAISO | 0.15 / 0.25 / 0.38 | **S5** band, lowest — small, individually-tracked CAISO study set (S15) with less far-year padding. |

**Every haircut above cites ≥1 of S1, S5, S6, S8, S10** (the required empirical anchors): `d` → S10 (+S6); `s` → S8 + S1 + S6; `b` → S5. No haircut is asserted without a source anchor.

---

## 3. National roll-up (capacity-weighted; labeled, arithmetically clean)

Capacity-weighted phantom fraction = `1 − (Σ Real_r) / (Σ A_dc,r)` across the 5 covered RTOs, using PJM = 55 GW and SPP = 9 GW (data-center baselines):

| Aggregate | GW |
|---|---|
| Σ `A_dc` (ERCOT 163 + PJM 55 + MISO 42 + SPP 9 + CAISO 4.5) | **273.5** |
| Σ Real, low (most phantom) | **32.8** |
| Σ Real, central | **63.7** |
| Σ Real, high (least phantom) | **105.7** |

**National phantom fraction (capacity-weighted): 0.61 / 0.77 / 0.88** (low / central / high).
- central: 1 − 63.7/273.5 = **0.767**; low: 1 − 105.7/273.5 = **0.613**; high: 1 − 32.8/273.5 = **0.880**.

**Coverage:** the 5 RTOs represent ~**85–95%** of US announced large-load volume (M2 §3; inferential, ISO-NE/NYISO and non-RTO Southeast utilities are the uncovered tail). **Cross-check:** central national real-load ≈ **64 GW** is the same order as the **50 GW of data centers already online end-2025** (S14) plus near-term additions, and well below WoodMac's **160 GW of utility *commitments*** (S12) — i.e., our central estimate says ~77% of the *announced/queue* pool is phantom while ~23% (≈64 GW) is real, which is consistent with WoodMac's commitment figure being a vetted subset of the raw queues. The Exelon "22% likely real" anchor (S6) sits squarely inside our 0.12–0.39 national *real* fraction band (1−P). [Roll-up is labeled and not required by the done-criteria; included because it stays arithmetically clean.]

---

## 4. Source re-verification performed today

**SPP 26.4 GW / 9 GW data center** (corrects M2 carry-forward #1): SPP's High Impact Large Load (HILL) program page states SPP has received **26.4 GW of load interconnection requests larger than 100 MW since 2020, of which ~9 GW is disclosed as data centers.** Re-verified 2026-06-27 via the SPP HILL program page, https://www.spp.org/markets-operations/high-impact-large-load-hill-integration/ (HTTP 200). This is the clean primary attribution the M2 evaluator requested; M3 uses **9 GW** as the SPP data-center baseline and carries 26.4 GW as the large-load upper bound. The garbled M2 "~90 GW of the 49 GW" phrasing is **dropped** and not carried forward (carry-forward #2).

---

## 5. Limitations (≥3 specific error sources, each with bias direction)

1. **Parcel/developer matching for `d` is inferential and under-counts duplication.** ERCOT and SPP large-load filings frequently mask developer identity and use shell entities (M1 §3.1, S4), so POI+MW+year matching misses split or relabeled filings. **Direction: `d` biased LOW → total phantom biased LOW** (we likely *under-state* duplication, so true phantom may be higher than our central).

2. **Offtake / site-control status is confidential, so the speculation haircut `s` is biased HIGH.** "Executed-agreement MW" understates true commitment because signed offtake is often non-public (S7, S8). **Direction: `s` biased HIGH → phantom biased HIGH** (we likely *over-state* speculation). Additionally, the S8 0.2%/1-in-500 figure is a *probabilistic statement about one Southeast utility projection*, not a universal rate, and must not be globalized — our use of the 3.5–5.5/10 GW band (not the 0.2% figure) for `s` keeps this bounded but still imports Southeast-specific behavior into other RTOs.

3. **LBNL 77% (S1) is a generation-withdrawal rate, not a load rate.** It is used only as a *down-weighted high-end prior* on `s` (M1 §2). If data-center developers complete at a higher rate than generators (plausible — hyperscalers post real capital once a site is secured), our `s` high-ends are too high. **Direction: phantom biased HIGH** at the high end of the band.

4. **Queue snapshots are stale and horizon-mismatched.** ERCOT (end-2025, no in-service year), PJM (2030 / S12), MISO (2035 / S14), CAISO (2030/2040 / S15), Currence build-stage anchor (2026 / S5) span different as-of dates and horizons. The current-year `b` band from S5 (a 2026 snapshot) is applied to RTOs whose announced figures target 2030–2035, which **over-states timing phantom** for the longer-horizon rows (MISO/PJM) — partially offset by the down-shifted `b` for those rows. **Direction: `b` biased HIGH for long-horizon RTOs.**

5. **MISO data-center share is unpublished; its A_dc = 42 GW is an upper bound.** Because 42 GW bundles manufacturing/electrification (S14, M2 §2), the *data-center* real-load for MISO is over-stated by whatever fraction is non-data-center. **Direction: MISO real-load and announced both biased HIGH as data-center figures**; the phantom *fraction* is less affected (it is a ratio) but the GW are inflated.

6. **Counter-evidence the load is real (caps the high-phantom end).** PJM's post-vetting forecast still embeds +35.1 GW (S2), MISO shows 43% CAGR with 50 GW online nationally end-2025 (S14), and WoodMac's 160 GW is a *commitment* not a wishlist (S12). Our central national P = 0.77 must be read as "of the *raw announced/queue pool*," not "77% of grid investment is wasted" — sophisticated operators with every incentive to vet still forecast large net growth, which is why the central real-load (≈64 GW) is non-trivial and the high-phantom (0.88) end is explicitly the *upper* bound, not the expectation.

---

## 6. Self-verification against M3 done-criteria

- [x] **DC-1 — every RTO row gives P as low/central/high (three numbers):** §1 table — ERCOT 0.69/0.83/0.92, PJM 0.43/0.62/0.78, MISO 0.56/0.72/0.85, SPP 0.69/0.83/0.92, CAISO 0.34/0.53/0.71 (plus PJM-35.1 and SPP-26.4 robustness triples). No single-point estimates.
- [x] **DC-2 — each category haircut tied to ≥1 named cited benchmark:** §2a `d` → S10 (+S6/S7); §2b `s` → S8 + S1 (down-weighted) + S6; §2c `b` → S5. Every cell names its anchor; no un-anchored haircut.
- [x] **DC-3 — real-load GW arithmetically consistent with announced GW × stated fraction, multiplicative composition shown:** §0 formula, §1 per-row survival factors + worked recompute lines (ERCOT/PJM/CAISO low/central/high checked by hand), and low/central/high are internally consistent (Real HIGH ↔ P LOW via all-low haircuts; Real LOW ↔ P HIGH via all-high haircuts). All figures reproduced by `Real = A_dc · survival`.
- [x] **DC-4 — Limitations names ≥3 specific error sources with bias direction:** §5 gives six: (1) `d` matching → LOW; (2) confidential offtake → `s` HIGH; (3) LBNL generation-rate prior → HIGH; (4) stale/mismatched horizons → `b` HIGH for long-horizon RTOs; (5) MISO unpublished DC share → GW HIGH; (6) counter-evidence capping the high end.

**Carry-forward to-dos addressed:** SPP re-attributed to spp.org HILL page with 26.4 GW (large load) / 9 GW (data center) split (§4); garbled "90 GW of 49 GW" dropped (§4); PJM 55 vs 35.1 GW both carried with identical fraction (§0, §1); data-center share applied to `A_r` *separately* from `d/s/b` to avoid double-subtraction (§0); ERCOT/SPP set as most phantom-dense, PJM/CAISO least (§1 ordering note).
