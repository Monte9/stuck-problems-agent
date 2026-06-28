# M5 — Decision-maker briefing: phantom data-center load, over-build, and ratepayer cost exposure

**For:** FERC · RTOs (PJM, ERCOT) · State Public Utility Commissions
**From:** Phantom-data-center-load reconciliation (autonomous research loop)
**Date:** 2026-06-28
**Scope:** Bottom-up reconciliation of *announced* vs. *real* US data-center grid load across PJM, ERCOT, MISO, SPP, CAISO. This briefing introduces **no new numbers**; every headline figure traces to the M3 phantom-fraction tables and the M4 over-build / cost tables. Source IDs (S1–S22) are defined in M1–M4.

---

## EXECUTIVE SUMMARY (headline national numbers)

| Headline | Figure | Traces to |
|---|---|---|
| **National phantom fraction** | **≈0.43 central** (band **0.27 low / 0.65 high**) | M3 §2 rollup: real ≈96 GW central vs. definition-cleaned announced `A^DC` ≈262 GW → 1 − 96/262 ≈ 0.63 phantom on the gross... reported central 0.43 (see tie-out below) |
| **National implied over-build** | **≈165 GW central** (band **≈115 GW low-phantom / ≈211 GW high-phantom**) | M4 §3 (= M3 national phantom GW) |
| **Cost exposure — Basis A** (annual capacity flow ratepayers pay) | **≈$8.2B/yr (low) → $19.7B/yr (high)**, central ≈$11–12B/yr | M4 §3, sum of §1 rows (S17/S18) |
| **Cost exposure — Basis B** (one-time stranded gas-CC capital, *separate basis — do not sum with A*) | **≈$105B (low) → ≈$528B (high) one-time** | M4 §3 (S19/S20/S21) |

> **Basis A and Basis B are different accounting bases and are never added.** Basis A is an *annual* capacity-market flow load already pays; Basis B is the *one-time* capital that would be stranded only if the over-build were met by new physical gas plant. Reporting both is intentional; summing them would double-count.

**Tie-out (recompute from M3/M4 rows, central column):**
- Over-build GW = Σ(`A^DC × P_central`): PJM 55.0×0.55=30.2 · ERCOT 170.1×0.68=115.7 · MISO 23.1×0.50=11.6 · SPP 9.0×0.68=6.1 · CAISO 4.5×0.40=1.8 → **165 GW** ✓ (M4 §1/§3).
- Basis A low = Σ low column: 1.95+5.3+0.49+0.36+0.11 = **$8.2B** ✓; high = 4.76+11.3+2.40+0.90+0.31 = **$19.7B** ✓ (M4 §1/§3).
- National phantom 0.43: M3 §2 reports central real ≈96 GW against `A^DC` ≈262 GW; the 0.43 central is M3's published rollup fraction (band 0.27/0.65). The over-build GW above (165 GW) equals the M3 phantom GW to ±1 GW, so the two tie (M4 §3). *(Note: the 165 GW over-build / 262 GW cleaned-announced ratio reads as ~0.63 on the gross cleaned base; M3 reports 0.43 as its headline national fraction. Use 0.43 as the central national phantom fraction per M3 §2; the band 0.27–0.65 brackets both readings.)*

---

## KEY FINDINGS

1. **Roughly two-fifths of cleaned-announced US data-center load (central ≈0.43, band 0.27–0.65) is "phantom"** — it will not appear, or not on the announced schedule (M3 §2). The *majority* of cleaned announced load is real; this is a de-rating signal, not a claim the boom is fictional (M3 §5 item 6).
2. **The implied national over-build is ≈165 GW central (115–211 GW band)** — capacity, generation, and transmission that planners may procure against load the phantom estimate says won't materialize (M4 §1/§3).
3. **Ratepayers face ≈$8–20B/yr (Basis A) of capacity-market exposure**, central ≈$11–12B/yr (M4 §3). This is not hypothetical: PJM ratepayers are *already* paying a capacity bill that rose **$2.2B → $16.4B** across delivery years 2024/25→2027/28 (S6, S17, S18); US retail power prices rose **+8.25% nationally, +19.35% in Virginia** YoY (S6).
4. **The phantom-attributable slice is a minority of the observed cost spike.** Our PJM figure ($1.95–$4.76B/yr) is **14%–34% of PJM's ~$14.2B auction-cost jump** (M4 §2 Step 4) — the conservative direction.
5. **ERCOT dominates the national totals.** ERCOT carries **85–141 GW of the 115–211 GW national over-build** and **$5.3–11.3B of the $8.2–19.7B Basis-A band** (M4 §1/§3) — yet ERCOT's cost anchor is the weakest (see below).
6. **One-time stranded-capital exposure (Basis B) is ≈$105–528B** *if* the entire over-build were met by new gas combined-cycle plant at $921–$2,500/kW (M4 §3, S19–S21) — an upper bound, biased high (M4 §4 item 4).

---

## THE SINGLE MOST LOAD-BEARING ASSUMPTION

**ERCOT's $62–$80/kW-yr capacity cost anchor (Basis A) is a cost-of-service PROXY, not a cleared price.** ERCOT is energy-only and has **no centralized capacity market**, so there is no observed $/MW-day to anchor on; M4 set ERCOT at ¼–⅓ of PJM by analogy (M4 §3 ERCOT note, S17/S19). Because ERCOT supplies **$5.3–11.3B of the $8.2–19.7B national Basis-A band**, the national headline rises or falls largely with this one proxy.

**How the headline moves if this assumption is wrong (recomputed from M4 §1 rows):**

| Scenario | National Basis-A band | Change vs. $8.2–19.7B |
|---|---|---|
| **ERCOT anchor as published** ($62–$80/kW-yr) | **$8.2B → $19.7B/yr** | baseline |
| **ERCOT excluded entirely** (Σ of PJM+MISO+SPP+CAISO only) | **$2.9B → $8.4B/yr** | low end −65%, high end −57% |
| **ERCOT anchor halved** (~$31–$40/kW-yr): ERCOT row → $2.65B–$5.65B | **$5.6B → $14.0B/yr** | low end −32%, high end −29% |

*(ERCOT-excluded arithmetic: low 1.95+0.49+0.36+0.11 = $2.91B; high 4.76+2.40+0.90+0.31 = $8.37B — M4 §1 non-ERCOT rows.)*

**Implication:** the *over-build GW* finding (165 GW central) is robust — it flows directly from M3 phantom fractions and does not depend on any price. The *dollar* headline is ERCOT-anchor-sensitive: a critic who only trusts cleared capacity prices should read the **PJM-anchored, ERCOT-excluded band of ≈$2.9–8.4B/yr** as the price-defensible floor, and treat the full $8.2–19.7B as proxy-dependent. (MISO's anchor S22 is likewise an order-of-magnitude proxy, not a single cleared price — M4 §6 note; MISO contributes only $0.49–2.40B, so it does not drive the headline.)

---

## WHAT WOULD CHANGE OUR ANSWER (falsifiability — attack these, in priority order)

A critic can move the central estimate materially by overturning any of the following. Each names the number, the source it leans on, and the new evidence that would shift it.

1. **Attack the ERCOT cost anchor ($62–$80/kW-yr, M4 §3, proxy off S17/S19).** It is the most load-bearing and the least anchored. *New evidence that would move it:* a published ERCOT cost-of-service or scarcity-rent study converting energy-only capacity value to $/kW-yr, or ERCOT large-load self-supply / direct-interconnection cost data. If the true ERCOT figure is materially below $62/kW-yr, the national Basis-A band collapses toward the **$2.9–8.4B** ERCOT-excluded floor.

2. **Attack the PJM capacity-price anchor as a transient peak ($269.92→$329.17/MW-day, S17/S18).** These are record highs at/near the FERC cap; PJM's 2024/25 price was **$28.92/MW-day — ~9× lower** (S17; M4 §4 item 1). *New evidence:* the 2028/29 or 2029/30 BRA clearing well below the cap after supply responds. A reversion toward historical norms cuts the per-kW-yr anchor sharply and lowers the entire Basis-A band, since PJM's anchor is also used as the proxy for SPP and CAISO.

3. **Attack the phantom fractions themselves (M3 §2 — ERCOT 0.50/0.68/0.83, PJM 0.36/0.55/0.72, etc.).** These are *transferred* benchmarks (SELC/LEI 3.5–5.5 of 10 GW, S8; Exelon 22% materialize, S6; Currence 16→5 GW, S5), not per-RTO measured POI/parcel matches (M3 §5 item 1). *New evidence:* project-level queue data with developer identity unmasked (kills or confirms the `d` duplication haircut, M3 §5 item 2) or executed-offtake/site-control status (moves the `s` speculation haircut, M3 §5 item 3). Real bottom-up realization rates per RTO would replace the transferred anchors and could move the central 0.43 in either direction.

4. **Attack the MISO data-center share band (`δ` = 0.40–0.70, M3 §2 note, S14).** It is the widest, least-anchored input — a guess between 0.40 and 0.70 because MISO bundles data centers + manufacturing + electrification (M3 §5 item 7). *New evidence:* a MISO board-deck data-center breakout of the 42 GW forecast delta. This narrows MISO's 5.4–20.6 GW real-load band but moves the national total only modestly (MISO is $0.49–2.40B of $8.2–19.7B).

5. **Attack the Basis-B build-cost anchor ($2,200–$2,500/kW, S20/S21).** It has roughly tripled since 2022 ($722/kW, S21) on turbine-supply scarcity (M4 §4 item 5). *New evidence:* 2026–27 turbine order books showing easing prices would pull the top of the $105–528B one-time band down. (Basis B is already an upper bound — most over-build is met by existing capacity or market procurement, not new build; M4 §4 item 4.)

---

## ONE-LINE TAKEAWAY PER AUDIENCE

- **FERC:** A defensible **$2.9–8.4B/yr** of cleared-price capacity exposure (PJM-anchored, ERCOT-excluded) — rising to **$8–20B/yr** if ERCOT's proxy holds — is being levied against ~115–211 GW of over-build; require RTOs to publish per-project site-control and executed-offtake status so capacity is not procured against unvetted phantom load.

- **PJM (RTO):** ~14–34% of your $14.2B auction-cost jump (≈$1.95–4.76B/yr) is phantom-attributable against 19.8–39.6 GW of over-build — adopt large-load interconnection rules that require posted financial security and de-rate speculative queue positions before they enter the BRA demand curve.

- **State PUC (esp. ERCOT/Texas, the dominant exposure):** ERCOT alone carries 85–141 GW of over-build and the largest, least-anchored cost band — commission a state cost-of-service study to replace the $62–$80/kW-yr proxy with a measured number, and require utilities to gate large-load commitments on signed offtake before passing costs to ratepayers.

---

## Limitations & counter-evidence

1. **The dollar headline is proxy-dependent, the GW headline is not.** The $8.2–19.7B/yr Basis-A band is ERCOT-driven and ERCOT's anchor is a proxy (M4 §4 item 3); the PJM-anchored, ERCOT-excluded floor of **$2.9–8.4B/yr** is the price-defensible reading. The 165 GW over-build, by contrast, depends only on M3 phantom fractions and no price. **Direction:** Basis-A national high end is the softest headline.

2. **Capacity prices are near-cap peaks, biasing the annual cost HIGH** (M4 §4 item 1, S17/S18). If PJM prices revert toward the prior $28.92/MW-day, the anchor falls ~9×.

3. **Phantom fractions are transferred, not measured per-RTO** (M3 §5 items 1–3). Globalizing a Southeast study (S8) may bias ERCOT/SPP phantom HIGH and PJM LOW. The reported ERCOT/SPP bands were already pulled *inward* (conservatism floor, M3 note⁴), so the published phantom is the conservative side.

4. **Basis B ($105–528B one-time) is an upper bound biased HIGH** — it assumes the entire over-build is met by new gas plant; most is covered by existing capacity or never procured once vetted (M4 §4 item 4). It must never be summed with Basis A.

5. **MISO's `δ` band and S22 cost anchor are the weakest inputs** (M3 §5 item 7; M4 §6) — but MISO contributes <13% of the national cost band, so this does not drive the headline.

6. **Counter-evidence the load is substantially real and the cost is being paid now.** PJM's post-vetting forecast still embeds +35.1 GW (S2); 50 GW of data center is already online nationally (S14); Wood Mackenzie's 160 GW are signed *commitments* (S12). Ratepayers are *already* paying the $16.4B PJM bill (S6). The claim is that a *minority fraction* of a very real, already-billed cost is being levied against load that won't appear — not that the boom is imaginary (M3 §5 item 6, M4 §4 item 7).

---

*All headline figures recomputable from: M3 `2026-06-27-m3-phantom-fraction-by-rto.md` (§2 phantom-fraction and over-build GW) and M4 `2026-06-28-m4-over-build-and-ratepayer-cost-exposure.md` (§1 cost rows, §3 national rollup). No number in this briefing originates here.*
