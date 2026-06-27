# M3 — Phantom-fraction estimation by RTO

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M3 (per-RTO phantom fraction, low/central/high, decomposed by category).
**Date:** 2026-06-27.
**Author:** generator (autonomous loop).

This artifact applies the M1 multiplicative method (`2026-06-27-m1-evidence-base-and-method-scaffold.md`, §3.0) to the M2 announced baselines (`2026-06-27-m2-announced-load-baseline-by-rto.md`, §1) to produce, for each of the five covered RTOs/ISOs, a **phantom fraction as a low/central/high range**, decomposed into the three M1 categories — duplication (`d`), no-site-control/no-offtake speculation (`s`), and announced-vs-building double-count (`b`) — with **every haircut anchored to a named, cited empirical benchmark**. Source IDs (S1–S15) are defined in M1/M2.

---

## 0. Method recap and composition rule (so the arithmetic is reproducible)

From M1 §3.0, the three category haircuts compose **multiplicatively** (as survival fractions), **not additively**, so the same MW is never subtracted twice:

```
Real_r = A_r · (1 − d_r) · (1 − s_r) · (1 − b_r)
P_r    = 1 − (1 − d_r)(1 − s_r)(1 − b_r)
```

`A_r` = announced GW (M2). `d_r`, `s_r`, `b_r` ∈ [0,1] are the duplication, speculation, and build-stage haircuts. Order of application (dedup → speculation → build-stage) is irrelevant to the product but fixed for auditability. Each of `d`, `s`, `b` is itself a **low/central/high triple** (§2); the row's `P_low` is built from the three *low* haircuts, `P_central` from the three central, and `P_high` from the three *high* (a conservative bracketing — see Limitation 6 on correlation). **The §1 and §3 tables are the same computation**: §1 reports the rounded outputs, §3 shows the full per-haircut composition and hand-verifies it.

**Baseline GW used per row (`A_r`).** Per the M2 reconciliation, the announced rows are *not* data-center-pure and *not* on a common definition, so M3 applies the M2 cleaning **before** haircutting, and states `A_r` explicitly:
- **ERCOT:** `A = 163 GW` (= 233 GW large-load queue × 0.73 data-center share, S3/S4) — not the raw 233.
- **PJM:** carried as **two definitional variants** per the M2 flag — `A = 55 GW` (Wood Mackenzie utility commitment, S12) and `A = 35.1 GW` (PJM post-vetting embedded adjustment, S2). Both are haircut and reported.
- **MISO:** `A = 25 GW` central (= 42 GW total peak-load growth × ~0.60 data-center share; the share is **inferential** — M2 Limitation 2 flags MISO has no cleanly published DC share, so a 0.50–0.70 band gives 21–29 GW). The 42 GW gross is shown for transparency.
- **SPP:** `A = 9 GW` (data-center-**disclosed** portion of the 26.4 GW large-load study requests since 2020, per the corrected SPP HILL source). The full 26.4 GW is large-load, not data-center; using it as a data-center baseline would itself be a phantom inflation, so 9 GW is the defensible data-center `A`.
- **CAISO:** `A = 4.5 GW` (data-center load under study, S15).

**Carry-forward fixes applied (M2 evaluator):** (1) the SPP figures are re-attributed to the **SPP HILL (High Impact Large Load) integration page** — `https://www.spp.org/markets-operations/high-impact-large-load-hill-integration/` (HTTP 200, curl-checked 2026-06-27; transient 503 on WebFetch body only) — which states "since 2020, SPP has received **26.4 GW of load interconnection requests larger than 100 MW, including 9 GW disclosed as data centers**" (corroborated by Wright & Talisman, *The HILLs Have Ayes*, 2026-01, and Perkins Coie). This is **not** attributed to S13 (Ascend, ERCOT-specific). (2) The incoherent M2 "~90 GW of the 49 GW" SPP forecast phrasing is **dropped** — it was never used in any baseline and is not used here.

---

## 1. Per-RTO phantom-fraction table

Phantom fraction is low/central/high; real-load GW = `A_r · (1 − P_r)`. The fractions and real-load GW below are the **exact outputs of the multiplicative composition of the §2 haircut triples**, computed in full in §3 (this table reports P rounded to 2 decimals, GW to 1 decimal). **Higher phantom fraction → lower real load** (range inverts correctly: low ≤ central ≤ high for P; high ≥ central ≥ low for real GW — verified every row).

| RTO/ISO | Announced GW (A_r, cleaned, from M2) | Phantom fraction **low** | Phantom fraction **central** | Phantom fraction **high** | Real-load GW **high** (= A·(1−P_low)) | Real-load GW **central** | Real-load GW **low** (= A·(1−P_high)) |
|---|---|---|---|---|---|---|---|
| **ERCOT** | 163 (233 × 0.73 DC share, S3/S4) | 0.51 | 0.71 | 0.83 | 79.2 | 48.1 | 27.9 |
| **PJM (var. A: WoodMac 55)** | 55 (S12) | 0.32 | 0.55 | 0.74 | 37.2 | 24.7 | 14.5 |
| **PJM (var. B: PJM 35.1)** | 35.1 (S2, post-vetting) | 0.16 | 0.39 | 0.60 | 29.4 | 21.4 | 14.0 |
| **MISO** | 25 (42 × ~0.60 DC share; band 21–29) | 0.46 | 0.67 | 0.80 | 13.5 | 8.4 | 5.1 |
| **SPP** | 9 (DC-disclosed of 26.4, SPP HILL) | 0.36 | 0.58 | 0.75 | 5.8 | 3.8 | 2.2 |
| **CAISO** | 4.5 (S15) | 0.17 | 0.38 | 0.59 | 3.7 | 2.8 | 1.8 |

**National roll-up (central, using PJM variant A = 55 to be conservative-high on announced):**
announced (cleaned) = 163 + 55 + 25 + 9 + 4.5 = **256.5 GW**; real-load central = 48.1 + 24.7 + 8.4 + 3.8 + 2.8 = **87.8 GW**.
Implied **national central phantom fraction = 1 − 87.8/256.5 = 0.658 (~66%)**.
Low-phantom case (all rows at `P_low`): real = 79.2 + 37.2 + 13.5 + 5.8 + 3.7 = **139.4 GW** → national phantom ≈ **46%**.
High-phantom case (all rows at `P_high`): real = 27.9 + 14.5 + 5.1 + 2.2 + 1.8 = **51.5 GW** → national phantom ≈ **80%**.
**National phantom-fraction range: ~46% (low) / ~66% (central) / ~80% (high).** Using PJM variant B (35.1) instead of A gives announced = 236.6 GW and real central = 84.5 GW → central ~64% — the headline is robust to the PJM definitional choice (M2 Limitation 6 concern resolved).

*Independent cross-check:* the M2 naïve gross was ~361 GW and Wood Mackenzie's independent national *commitment* figure was ~160 GW (S12). A ~66% central phantom on the cleaned 256.5 GW gives ~88 GW real, **below** WoodMac's 160 GW commitment — consistent, because a "commitment" still contains speculation and timing slip; our real-load central sitting under the commitment figure is the expected ordering and a sanity pass, not a contradiction.

---

## 2. Per-category haircut breakdown, with anchoring citation

Each haircut triple (low/central/high) below is the `d`, `s`, `b` applied to the row above. **No haircut is asserted without a named cited benchmark.** These triples are the exact inputs to the §3 composition that produces §1.

### 2.1 Category `d` — duplication (cross-territory + within-utility multiple filings)

| RTO | `d` low | `d` central | `d` high | Anchoring benchmark (cited) |
|---|---|---|---|---|
| ERCOT | 0.10 | 0.20 | 0.30 | SELC: developers file "**5–10× more requests than centers built**" (S10); WRI mechanism of multi-territory filing (S7). Raw open queue (S4) → high `d`. Capped well below the 5–10× signpost because that ratio bundles duplication *and* speculation; `d` is the duplication-only slice. |
| PJM (A) | 0.05 | 0.15 | 0.25 | Within-PJM evidence: WoodMac 55 GW (S12) vs PJM post-vetting 35.1 GW (S2) = ~20 GW / ~36% gap, part of which is dedup/vetting → central `d` set below that combined gap. |
| PJM (B) | 0.02 | 0.08 | 0.15 | Lower because the 35.1 GW (S2) is *already post-vetting*, so most cross/within-utility duplication is removed; residual only. |
| MISO | 0.10 | 0.18 | 0.28 | SELC 5–10× over-filing (S10) applied to a bundled large-load forecast; cross-RTO shopping into PJM/SPP plausible (S7). |
| SPP | 0.10 | 0.20 | 0.30 | SELC 5–10× (S10); SPP study-request queue is raw (SPP HILL page) and the same developers shop ERCOT/MISO (S7). |
| CAISO | 0.03 | 0.08 | 0.15 | Small, relatively well-vetted study set (S15); low duplication. SELC 5–10× (S10) is a national upper signpost, down-weighted here. |

### 2.2 Category `s` — no site control / no signed offtake (speculation)

| RTO | `s` low | `s` central | `s` high | Anchoring benchmark (cited) |
|---|---|---|---|---|
| ERCOT | 0.40 | 0.55 | 0.65 | SELC/LEI: ~10 GW utility projection had a **~0.2% (1-in-500) chance** of fully occurring; **most-likely 3.5–5.5 GW** → real/announced ≈ 0.35–0.55, i.e. `s` ≈ 0.45–0.65 (S8). Exelon: only **~22% of its 36 GW data-center pipeline has executed agreements / "will materialize"** (S6) → supports a high `s` for raw queues. LBNL **77% generation-withdrawal** (S1) used **only** as a down-weighted high-end prior (M1 §2 caveat), never applied directly. |
| PJM (A) | 0.25 | 0.40 | 0.55 | Exelon (a PJM-zone utility) **22%-materialize** statement (S6) — ~78% not yet under firm agreement, taken as a *high* prior; LEI 0.35–0.55 real/announced (S8). Lower than ERCOT because 55 GW is a utility *commitment*, partly screened (S12). |
| PJM (B) | 0.12 | 0.28 | 0.45 | Lower still: 35.1 GW is PJM's *post-vetting* figure (S2), so much speculation already removed; Exelon 22% (S6) and LEI (S8) bound the residual. |
| MISO | 0.35 | 0.52 | 0.62 | LEI 3.5–5.5 of 10 → `s` ≈ 0.45–0.65 (S8); MISO row is a *forecast* delta (S14), less vetted than PJM's. Exelon 22% (S6) as high prior. |
| SPP | 0.25 | 0.40 | 0.55 | LEI (S8); only 9 of 26.4 GW even *disclosed* as data centers (SPP HILL), so the DC slice is self-selected toward more-serious projects → `s` below ERCOT's raw queue. |
| CAISO | 0.12 | 0.25 | 0.40 | CEC forecast **+1.8 GW by 2030 vs 4.5 GW under study** (S15) → real/announced ≈ 0.40 gross; but most of that gap is *timing* (captured in `b`), so the pure speculation slice is the smaller 0.12–0.40. LEI (S8) bounds. |

### 2.3 Category `b` — announced-vs-building double-count (timing phantom)

| RTO | `b` low | `b` central | `b` high | Anchoring benchmark (cited) |
|---|---|---|---|---|
| ERCOT | 0.10 | 0.18 | 0.30 | Currence/Sightline Climate: of ~16 GW slated for 2026 only ~5 GW under construction, with "**30–50% of the pipeline unlikely to come online**" on schedule (S5). National 30–50% timing band applied; ERCOT mid because Texas builds fast once interconnected. CenterPoint **1→25 GW** Houston request growth (S6) shows announced-vs-real timing inflation in ERCOT specifically. |
| PJM (A) | 0.05 | 0.12 | 0.22 | Currence 30–50% unlikely-this-year (S5), applied to the *post-speculation* remainder; lower band because PJM 55 GW is a 2030 horizon (S12), not a current-year figure, so less of the timing gap remains. |
| PJM (B) | 0.03 | 0.08 | 0.15 | Lowest: 35.1 GW already on PJM's vetted forecast schedule (S2); residual timing slip only, bounded by Currence (S5). |
| MISO | 0.08 | 0.15 | 0.25 | Currence 30–50% (S5) on a 2035 horizon (S14); modest because the horizon is distant (timing phantom smaller per year). |
| SPP | 0.05 | 0.12 | 0.22 | Currence 30–50% (S5); SPP HILL's new 90-day-to-agreement process compresses the build-stage gap for disclosed projects. |
| CAISO | 0.03 | 0.10 | 0.20 | CEC +1.8 GW by 2030 vs 4.5 GW under study (S15) is largely a *timing/horizon* gap → most of the CAISO announced-vs-real gap lives here; Currence (S5) bounds. |

---

## 3. Composition arithmetic (authoritative recompute — every row reproducible from its own haircuts)

Using `P = 1 − (1−d)(1−s)(1−b)` and `Real = A·(1−P)`, with the §2 triples. Worked to 3 decimals; §1 rounds. **This table is identical in inputs to §1/§2 and governs.**

| RTO | A | (d,s,b) low | P_low | (d,s,b) central | P_central | (d,s,b) high | P_high | Real_high =A(1−P_low) | Real_central =A(1−P_cent) | Real_low =A(1−P_high) |
|---|---|---|---|---|---|---|---|---|---|---|
| ERCOT | 163 | .10/.40/.10 | 0.514 | .20/.55/.18 | 0.705 | .30/.65/.30 | 0.829 | 79.2 | 48.1 | 27.9 |
| PJM-A | 55 | .05/.25/.05 | 0.323 | .15/.40/.12 | 0.551 | .25/.55/.22 | 0.737 | 37.2 | 24.7 | 14.5 |
| PJM-B | 35.1 | .02/.12/.03 | 0.163 | .08/.28/.08 | 0.391 | .15/.45/.15 | 0.602 | 29.4 | 21.4 | 14.0 |
| MISO | 25 | .10/.35/.08 | 0.462 | .18/.52/.15 | 0.665 | .28/.62/.25 | 0.795 | 13.5 | 8.4 | 5.1 |
| SPP | 9 | .10/.25/.05 | 0.359 | .20/.40/.12 | 0.578 | .30/.55/.22 | 0.754 | 5.8 | 3.8 | 2.2 |
| CAISO | 4.5 | .03/.12/.03 | 0.171 | .08/.25/.10 | 0.379 | .15/.40/.20 | 0.592 | 3.7 | 2.8 | 1.8 |

**Five worked checks (an evaluator can repeat each by hand):**
- ERCOT low: (1−.10)(1−.40)(1−.10) = 0.90 × 0.60 × 0.90 = 0.486 → P = **0.514**; Real = 163 × 0.486 = **79.2**. ✓
- ERCOT central: 0.80 × 0.45 × 0.82 = 0.2952 → P = **0.705**; Real = 163 × 0.2952 = **48.1**. ✓
- PJM-A high: 0.75 × 0.45 × 0.78 = 0.26325 → P = **0.737**; Real = 55 × 0.26325 = **14.5**. ✓
- SPP high: 0.70 × 0.45 × 0.78 = 0.2457 → P = **0.754**; Real = 9 × 0.2457 = **2.2**. ✓
- CAISO central: 0.92 × 0.75 × 0.90 = 0.621 → P = **0.379**; Real = 4.5 × 0.621 = **2.8**. ✓

**National roll-up (authoritative; using PJM-A):**
- Announced cleaned = 163 + 55 + 25 + 9 + 4.5 = **256.5 GW.**
- Real central = 48.1 + 24.7 + 8.4 + 3.8 + 2.8 = **87.8 GW** → national central phantom = 1 − 87.8/256.5 = **0.658 (~66%).**
- Real high (rows at P_low) = 79.2 + 37.2 + 13.5 + 5.8 + 3.7 = **139.4 GW** → national phantom **~46% (low).**
- Real low (rows at P_high) = 27.9 + 14.5 + 5.1 + 2.2 + 1.8 = **51.5 GW** → national phantom **~80% (high).**
- **National phantom-fraction range: ~46% / ~66% / ~80% (low / central / high).** With PJM-B (35.1) substituted: announced = 236.6 GW, real central = 84.5 GW → central ~64% — robust to the PJM choice. (Downstream note for M4: the over-build base is announced 256.5 − real ≈ 117–205 GW depending on tier; M4 should pick a single tier per use and not mix.)

---

## 4. Limitations

1. **The LBNL 13%/77% prior is generation, not load (biases central HIGH).** The 77% withdrawal rate (S1) is a 2000–2019 *generation*-interconnection statistic and is used here only as a down-weighted high-end prior on `s`, never as a direct load haircut (M1 §2). If hyperscaler data-center load completes at a *higher* rate than merchant generators — plausible, since land is often already secured and capital committed — then `s` (and the central phantom fraction) is **over-stated**. Direction: **over-states phantom.**

2. **Duplication detection is inferential and developer identity is masked (biases `d` LOW → biases total phantom LOW).** ERCOT large-load filings often mask the parent entity (S4), and projects reappear under shell entities, so POI+MW+year matching (M1 §3.1) misses split/relabeled filings. The `d` haircuts here are conservative **lower bounds**; true duplication — especially cross-RTO shopping (the same project filed in ERCOT *and* SPP/MISO, which no single RTO's number can see, S7) — is likely higher. Direction: **under-states phantom.**

3. **Offtake / site-control status is confidential (biases `s` HIGH → over-states phantom).** "Executed-agreement MW" is not fully public (S7, S8); the Exelon 22%-materialize figure (S6) is a snapshot of *currently executed* agreements, not a ceiling on what will ever execute, and the LEI 0.2%/1-in-500 figure (S8) is a *probabilistic statement about one specific Southeast utility projection* that must not be globalized. Treating low executed-agreement counts as permanent speculation **over-states** `s`. Direction: **over-states phantom.**

4. **Queue snapshots are stale and dated inconsistently (direction ambiguous).** ERCOT is end-2025 board data (S3/S4), PJM Jan-2026 (S2/S12), MISO late-2025 (S14), Currence Feb-2026 (S5), CAISO Jan-2026 (S15). A project withdrawn after a snapshot is still counted as announced (over-states the phantom denominator) while new filings after the snapshot are missed (under-states). Net direction is **ambiguous**, but staleness widens true uncertainty beyond the stated low/high band.

5. **The MISO data-center share (0.60) and the SPP "9 of 26.4 GW disclosed" split are estimates (biases `A`, hence real-load GW).** ERCOT's 72.9% DC share is firm (S4); MISO's ~0.60 is **inferential** (no clean published DC share, M2 Limitation 2; band 0.50–0.70). SPP's 9 GW is the *disclosed* DC portion — undisclosed large-load could include further data centers (under-states SPP `A`) or none (the 9 GW is right). If MISO's true DC share is lower, its `A` and real-load GW are **over-stated**, propagating to the national roll-up. Direction for MISO: likely **over-states** the data-center baseline.

6. **Low/high are bracketed by composing same-tier haircuts, assuming positive correlation across categories.** `P_low` uses all three *low* haircuts and `P_high` all three *high*, i.e. it assumes `d`, `s`, `b` errors move together. If they are independent, the true band is *narrower* than shown (joint extremes are less likely); multiplicative composition (M1 §3.0) prevents double-subtracting the same MW but cannot fully eliminate estimate-error interaction near the boundaries. Direction: the **stated band is likely wider than the true 1-sigma band** (conservative on uncertainty, not on the central point).

---

## 5. Self-verification against M3 done-criteria

- [x] **Every RTO row gives phantom fraction as explicit low/central/high (three numbers), not a point** — §1 and §3, six rows (ERCOT, PJM-A, PJM-B, MISO, SPP, CAISO), each with three ordered fractions (low ≤ central ≤ high verified every row).
- [x] **Each category haircut tied to ≥1 named cited benchmark** — §2.1 (`d`: SELC 5–10× S10, WRI S7, PJM 55-vs-35.1 S12/S2), §2.2 (`s`: LEI 3.5–5.5/10 & 0.2% S8, Exelon 22% S6, LBNL 77% S1 down-weighted), §2.3 (`b`: Currence 16/5 GW & 30–50% S5, CenterPoint 1→25 GW S6, CAISO CEC +1.8 GW S15). No un-anchored haircut.
- [x] **Real-load GW arithmetically consistent with announced GW and stated fraction** — §3 is the authoritative composition; five rows hand-verified; `Real = A·(1−P)` reproduces every cell; §1 and §3 use identical inputs. Composition stated explicitly as **multiplicative** (M1 §3.0) so no MW is double-subtracted. Ranges invert correctly (high P → low real).
- [x] **Limitations names ≥3 specific error sources with direction** — §4 gives six: LBNL-prior (over), masked-duplication (under), confidential-offtake (over), stale snapshots (ambiguous), MISO/SPP-share (over), correlation/bracketing (band-width).
- [x] **Carry-forward fixes applied** — SPP re-attributed to the SPP HILL page (not S13/Ascend); 9 GW DC-disclosed used as SPP baseline; incoherent "~90 GW of the 49 GW" phrasing dropped (§0).
- [x] **PJM dual baseline carried** — both 55 GW (S12) and 35.1 GW (S2) haircut and reported; national headline shown robust to the choice (§1, §3).
- [x] **Limitations & counter-evidence subsection present** (§4).
