# M4 — Over-build and ratepayer cost exposure

**Problem:** Phantom data-center load — bottom-up reconciliation of *announced* vs. *real* US data-center electricity demand.
**Milestone:** M4 (translate M3 real-load ranges into implied generation/transmission over-build in GW, and into a ratepayer cost-exposure range in dollars, against cited cost anchors).
**Date:** 2026-06-28.
**Author:** generator (autonomous loop).

This artifact takes the M3 per-RTO phantom GW (`2026-06-27-m3-phantom-fraction-by-rto.md`) **as given** — it does **not** re-derive phantom fractions — and does two things: (1) defines an **implied over-build GW** band per RTO directly from M3's phantom GW, and (2) maps that over-build to a **ratepayer cost-exposure dollar band** using cited cost anchors. Source IDs (S1–S16) carry forward from M1–M3; new cost-anchor sources are labelled **S17–S21** with working public URLs verified 2026-06-27/28.

---

## 0. Definitions and method (read before the table)

**Over-build GW (definition).** Over-build is the **phantom GW** from M3 — the announced data-center capacity (definition-cleaned to `A^DC`) that the central/high phantom estimate says will *not* appear, and against which planners may nonetheless procure capacity, build generation, or commit transmission. Formally, for RTO `r`:

```
OverBuild_r = A^DC_r − Real_r  =  A^DC_r · P_r
```

where `A^DC_r`, `Real_r`, and the phantom fraction `P_r` are read straight from the M3 §2 table. The over-build **range** runs from M3's **low-phantom** case (least over-build) to M3's **high-phantom** case (most over-build). The M3 *central* phantom is reported as the central over-build. This is the same `phantom GW = A^DC − Real` quantity M3 already computed; M4 adds no new haircut.

> **Worked check that over-build = M3's phantom GW (PJM):** `A^DC = 55.0 GW`, `Real` band = 35.2 / 24.8 / 15.4 GW (M3 §2). Over-build = 55.0 − {35.2, 24.8, 15.4} = **19.8 / 30.2 / 39.6 GW** (low-phantom / central / high-phantom). Equivalently 55.0 × `P` = 55.0 × {0.36, 0.55, 0.72} = {19.8, 30.2, 39.6}. The two routes agree, so the chain off M3 is exact.

**Cost-exposure (definition and the two anchors).** "Ratepayer cost exposure" is the **annual dollars ratepayers would pay to procure/serve capacity that the phantom estimate says is not real load**, plus, as an upper bound, the **capital that would be stranded if generation is physically built against it.** Two clearly-separated cost bases are used, and each table row states which:

- **Basis A — capacity-market exposure ($/kW-year).** What load pays *per year* through the capacity market (or its IRP/cost-of-service equivalent) to hold capacity available for the phantom GW. Anchored on the **PJM Base Residual Auction (BRA) clearing prices**: **$269.92/MW-day** for 2025/26 and **$329.17/MW-day** for 2026/27 (S17, S18). Converted to annual $/kW-year:
  - $269.92/MW-day × 365 days = **$98,520/MW-year = $98.52/kW-year** (low capacity anchor).
  - $329.17/MW-day × 365 days = **$120,147/MW-year = $120.15/kW-year** (high capacity anchor).
  This is an **annual** flow. It is the most defensible anchor because it is an actually-cleared market price load is already paying.
- **Basis B — stranded generation capital ($/kW, one-time).** What it costs to *build* a gas combined-cycle plant for the phantom GW — a one-time capital figure, relevant only to the fraction of over-build that is met with new physical generation rather than market procurement. Anchored on **EIA AEO2025 overnight capital cost ≈ $921/kW (2023$)** (S19) at the low end and **observed 2025 market build cost ≈ $2,200–2,500/kW** (S20, S21) at the high end. This is reported as a **separate, clearly-labelled bound**, not added to Basis A, to avoid double-counting an annual flow with a one-time capital figure.

For the headline cost-exposure $ column I use **Basis A (annual capacity exposure)**, because it is (a) an actually-cleared price, (b) the quantity FERC/PUCs are litigating now, and (c) conservative relative to lifetime capital. Basis B is given per-RTO as the stranded-capital upper bound. **The headline column is one year of capacity exposure**; a multi-year cumulative is given in §3 with its assumption stated.

**Conservatism rule (carried from M3).** Where an anchor is weak, the band is pulled *inward*. PJM's own market price is the strongest anchor and is used at face value; ERCOT (no centralized capacity market) is anchored to a *lower* cost-of-service proxy and the band is widened to reflect that, not narrowed to flatter the headline.

---

## 1. Main table — implied over-build and ratepayer cost exposure

Over-build GW = `A^DC × P` from M3 §2 (low-phantom → high-phantom). Cost-exposure $ = over-build GW × cost basis. **Headline $ column = Basis A, one year of capacity exposure**, low = (low-phantom GW × low capacity anchor $98.52/kW-yr), high = (high-phantom GW × high capacity anchor $120.15/kW-yr). Stranded-capital (Basis B) bound in the notes column.

| RTO/ISO | `A^DC` GW (M3) | Phantom `P` low/cen/high (M3) | **Implied over-build GW** (low-phantom / central / high-phantom) | **Cost-exposure $/yr** (Basis A, low → high) | Cost basis / citation |
|---|---|---|---|---|---|
| **PJM** | 55.0 | 0.36 / 0.55 / 0.72 | **19.8 / 30.2 / 39.6 GW** | **$1.95B → $4.76B /yr** | Basis A: PJM BRA $269.92–$329.17/MW-day = $98.52–$120.15/kW-yr (S17, S18). Stranded-capital bound (Basis B): 19.8–39.6 GW × $921–$2,500/kW = **$18B–$99B one-time** (S19–S21). |
| **ERCOT** | 170.1 | 0.50 / 0.68 / 0.83 | **85.0 / 115.7 / 141.2 GW** | **$5.3B → $11.3B /yr** | Basis A (proxy): ERCOT has no centralized capacity market; anchored to a *lower* cost-of-service capacity proxy of **$62–$80/kW-yr** (¼–⅓ of PJM, see §3 note) (S17, S19). Stranded-capital bound: 85–141 GW × $921–$2,500/kW = **$78B–$353B one-time** (S19–S21). Band deliberately wide — weakest anchor. |
| **MISO** | 16.8 / 23.1 / 29.4 | 0.30 / 0.50 / 0.68 | **5.0 / 11.6 / 20.0 GW** | **$0.49B → $2.40B /yr** | Basis A: MISO PRA prices far below PJM; anchored to **$98.52/kW-yr PJM proxy as a high bound, $40/kW-yr MISO-PRA-style low bound** (S17, S22). Stranded-capital bound: 5–20 GW × $921–$2,500/kW = **$4.6B–$50B one-time**. |
| **SPP** | 9.0 | 0.50 / 0.68 / 0.83 | **4.5 / 6.1 / 7.5 GW** | **$0.36B → $0.90B /yr** | Basis A: PJM $98.52–$120.15/kW-yr used as upper proxy; SPP has no comparable capacity market, so band pulled inward (S17, S18). Stranded-capital bound: 4.5–7.5 GW × $921–$2,500/kW = **$4.1B–$19B one-time**. |
| **CAISO** | 4.5 | 0.24 / 0.40 / 0.58 | **1.1 / 1.8 / 2.6 GW** | **$0.11B → $0.31B /yr** | Basis A: PJM capacity proxy $98.52–$120.15/kW-yr (CAISO RA market broadly comparable order of magnitude) (S17, S18). Stranded-capital bound: 1.1–2.6 GW × $921–$2,500/kW = **$1.0B–$6.5B one-time**. |

**Over-build GW arithmetic (recompute from M3's own numbers, central column):**
PJM 55.0×0.55 = 30.2 ✓ · ERCOT 170.1×0.68 = 115.7 ✓ · MISO 23.1×0.50 = 11.6 ✓ · SPP 9.0×0.68 = 6.1 ✓ · CAISO 4.5×0.40 = 1.8 ✓. (MISO uses the M3 `δ`-banded `A^DC`: low-phantom over-build = 16.8×0.30 = 5.0; high-phantom = 29.4×0.68 = 20.0, matching M3's two-axis treatment.)

---

## 2. Fully worked calculation — PJM (every input and multiplier cited)

PJM is worked end-to-end because it has the strongest anchor (an actually-cleared capacity price) and a published auction-cost jump to sanity-check against. A skeptical evaluator can reproduce every dollar by hand from the lines below.

**Step 1 — Over-build GW (from M3, no new haircut).**
- Input `A^DC = 55.0 GW` (M3 §2; PJM utility commitment by 2030, S12, data-center share ≈1.0).
- Input phantom fraction `P` = 0.36 / 0.55 / 0.72 (low / central / high), from M3 §2/§3.
- Over-build = `A^DC × P`:
  - low-phantom: 55.0 × 0.36 = **19.8 GW**
  - central: 55.0 × 0.55 = **30.25 ≈ 30.2 GW**
  - high-phantom: 55.0 × 0.72 = **39.6 GW**

**Step 2 — Capacity cost anchor, converted to $/kW-year (Basis A).**
- Input: PJM 2025/26 BRA cleared at **$269.92/MW-day** for most of the footprint, up from **$28.92/MW-day** the prior year; total cost to load **$14.7 billion**, up from **$2.2 billion** (S17, Utility Dive / S&P Global).
- Input: PJM 2026/27 BRA cleared at **$329.17/MW-day**; total auction value **$16.1 billion** (S18, PJM Inside Lines / POWER).
- Annualize (× 365 days/year, the BRA delivery-year basis):
  - $269.92/MW-day × 365 = $98,520/MW-year. Divide by 1,000 kW/MW → **$98.52/kW-year** (low anchor).
  - $329.17/MW-day × 365 = $120,147/MW-year → **$120.15/kW-year** (high anchor).

**Step 3 — Annual cost exposure = over-build GW × $/kW-year.** (1 GW = 1,000,000 kW.)
- **Low end** (least phantom × cheapest year): 19.8 GW × $98.52/kW-yr
  = 19,800,000 kW × $98.52 = **$1,950,696,000 ≈ $1.95 billion/year.**
- **High end** (most phantom × dearest year): 39.6 GW × $120.15/kW-yr
  = 39,600,000 kW × $120.15 = **$4,757,940,000 ≈ $4.76 billion/year.**
- **Central** (central phantom × low anchor, the conservative central): 30.2 GW × $98.52/kW-yr
  = 30,200,000 × $98.52 = **$2,975,304,000 ≈ $2.98 billion/year.**

**PJM headline: ratepayers pay roughly $1.95B–$4.76B per year of capacity cost for data-center load that the phantom estimate says will not appear (central ≈ $3.0B/yr).**

**Step 4 — Sanity check against the published auction-cost jump.** PJM's *total* capacity cost to load rose from **$2.2B → $14.7B → $16.1B → $16.4B** across the 2024/25 → 2027/28 delivery years (S17, S18, S6). The increment is **≈ $14.2B/year** of new capacity cost. PJM and analysts attribute the bulk of that jump to data-center-driven demand and a tightened reserve margin (S18: forecast peak rose >5,400 MW year-on-year "driven largely by data center expansion"). Our PJM phantom-attributable slice of **$1.95–$4.76B/yr** is **14%–34% of the $14.2B total auction-cost increase** — i.e., we are claiming that between one-seventh and one-third of the auction-cost spike is being paid against load that the central/high phantom estimate says will not materialize. That is a *conservative fraction of the observed jump*, not larger than it, which is the defensible direction.

**Step 5 — Stranded-capital upper bound (Basis B, one-time, reported separately).**
- If the 19.8–39.6 GW of PJM over-build were met with **new gas combined-cycle generation** rather than market procurement:
  - low: 19.8 GW × $921/kW (EIA AEO2025, 2023$, S19) = 19,800,000 kW × $921 = **$18.2 billion** one-time.
  - high: 39.6 GW × $2,500/kW (observed 2025 market build cost, S20/S21) = 39,600,000 × $2,500 = **$99.0 billion** one-time.
- So **$18B–$99B** of generation capital is the stranded-asset exposure if planners physically build against the high phantom band. This is a *one-time capital* figure and is **not** added to the annual Basis-A number.

---

## 3. National rollup (consistent with the rows)

**Implied national over-build (sum of rows, central column):** 30.2 (PJM) + 115.7 (ERCOT) + 11.6 (MISO) + 6.1 (SPP) + 1.8 (CAISO) = **≈ 165 GW central**, band **≈ 115 GW (low-phantom) / 211 GW (high-phantom)**. This equals the M3 national phantom GW (M3 §2 central real ≈ 96 GW against `A^DC` ≈ 262 GW → phantom ≈ 166 GW central), so the rollup is internally consistent with M3 to ±1 GW (rounding).

**National annual capacity cost exposure (Basis A, sum of rows):** **≈ $8.2B/year (low) → $19.7B/year (high)**, central **≈ $11–12B/year**. (Sum of low column: 1.95+5.3+0.49+0.36+0.11 = $8.2B; sum of high column: 4.76+11.3+2.40+0.90+0.31 = $19.7B.) ERCOT dominates the band because of its 85–141 GW over-build, and ERCOT's anchor is the weakest (no capacity market) — so the national band is itself ERCOT-driven and should be read with the ERCOT caveat in §4.

**National stranded-generation-capital upper bound (Basis B, one-time):** summing the per-row Basis-B bounds gives **≈ $105B (low, $921/kW × 115 GW) → ≈ $528B (high, $2,500/kW × 211 GW)** if the entire national over-build were met with new gas plant. This is the headline "over-build capital" figure for M5, reported as a one-time capital bound, not an annual flow.

**Multi-year framing (assumption stated):** capacity exposure is annual; a single delivery year is the most defensible unit. If the phantom over-build persisted across a **3-year forward capacity commitment** (PJM auctions 3 years ahead), the cumulative ratepayer exposure is **3 × the annual figure ≈ $25B–$59B nationally** over the commitment window — stated only as a scaling, with the 3-year assumption explicit and load-bearing.

**ERCOT cost-anchor note (why its band is wide and its $/kW-yr is below PJM).** ERCOT has **no centralized capacity market**; it is energy-only with an Operating Reserve Demand Curve. There is no cleared $/MW-day to anchor on, so Basis A for ERCOT is a *cost-of-service capacity proxy* set deliberately **below** PJM at **$62–$80/kW-yr** (≈ ¼–⅓ of PJM's $98–$120/kW-yr, reflecting that energy-only markets recover capacity value through scarcity energy prices, not a capacity charge, and that much ERCOT large load may self-supply or pay interconnection cost directly). ERCOT cost exposure = 85.0 GW × $62/kW-yr = **$5.27B** (low) to 141.2 GW × $80/kW-yr = **$11.30B** (high). This is the least-anchored row and is flagged first in Limitations.

---

## 4. Limitations & counter-evidence

Each item names the **direction of bias** on the cost figure (does it push the headline cost-exposure number **too high** or **too low**?).

1. **Capacity-market prices are transient peaks, not a permanent cost.** The PJM $269.92→$329.17/MW-day prices are **record highs** at or near the FERC price cap (S18: 2026/27 hit the cap; 2027/28 cleared at the cap $333.44/MW-day, S6). PJM's 2024/25 price was **$28.92/MW-day** — ~9× lower (S17). If new supply responds and prices revert toward historical norms, the per-kW-yr anchor falls sharply. **Direction: using near-cap prices biases the annual cost figure HIGH.** This is the single most load-bearing caveat on the headline dollar number.

2. **Annual capacity exposure ≠ permanent stranded cost; some "phantom" load is delayed, not absent.** M3's phantom band includes a **build-stage timing component (`b`)** — MW that is real but slips its in-service year (M3 §1, S5). Capacity procured a year early for load that arrives a year late is a *timing* cost, not a total loss. Counting the full phantom GW as cost-exposure therefore **biases the cost HIGH** for the timing slice. Offsetting partially: capacity once procured is paid regardless of whether the load shows, so the ratepayer *does* bear it in that year.

3. **ERCOT anchor is a proxy, not a cleared price → its band is the least reliable, and it dominates the national total.** ERCOT has no capacity market, so its $62–$80/kW-yr is an analyst proxy, not an observed clearing price (S17 used only by analogy). Because ERCOT carries 85–141 GW of the 115–211 GW national over-build, **the national cost band is ERCOT-driven and inherits ERCOT's anchor uncertainty.** Direction: **indeterminate** — the proxy could be too low (ERCOT scarcity-energy costs in tight years have spiked far above $80/kW-yr equivalent) or too high (much ERCOT large load self-supplies or pays its own interconnection). Flagged as the first target for refinement.

4. **Stranded-capital (Basis B) assumes new-build, but much over-build is met by market procurement or existing capacity → Basis B biases the capital figure HIGH.** The $18B–$99B (PJM) / $105B–$528B (national) one-time figures assume the *entire* over-build is met with newly built gas plant at $921–$2,500/kW (S19–S21). In reality a large share is covered by existing capacity, demand response, or never procured at all once the phantom is vetted out. **Direction: Basis B is an upper bound and biases the capital exposure HIGH;** it is reported separately for exactly this reason.

5. **Gas build-cost anchor has tripled recently and may not hold → Basis B band is wide and possibly HIGH at the top.** The $2,200–$2,500/kW market figure (S20/S21) reflects 2025 turbine-supply scarcity ("roughly tripled" vs. a few years prior; EIA's own AEO2025 overnight cost is ~$921/kW, 2023$, S19; EIA reported $722/kW as recently as 2022, S21). If turbine supply eases, the high anchor falls. **Direction: the top of the Basis-B band is biased HIGH.**

6. **Over-build inherits all of M3's phantom-fraction uncertainty.** Because over-build = `A^DC × P` with `P` taken directly from M3, every M3 limitation propagates: transferred (not measured) haircuts, masked duplicate filings (`d` biased low → phantom and over-build LOW), confidential offtake (`s` biased high → over-build HIGH), and the MISO `δ` band. **Direction: net indeterminate, but the over-build GW range is at least as wide as M3's phantom range — never narrower.** M4 adds no precision M3 did not have.

7. **Counter-evidence that the cost is real and being paid now.** This is not a hypothetical exposure: PJM ratepayers **are** paying the $14.7B→$16.4B capacity bill today (S17, S18, S6), and US retail electricity prices rose **8.25% nationally and 19.35% in Virginia** year-on-year (S6), in a footprint where data-center load is the dominant new driver (S18). The phantom critique is that a *fraction* of this very-real bill is being levied against load that won't appear — not that the bill is imaginary. Our claim that **14%–34% of PJM's auction-cost jump** is phantom-attributable (§2 Step 4) is a *minority* slice of an undisputed, already-billed cost increase, which is the conservative and defensible framing.

---

## 5. Self-verification against M4 done-criteria

- [x] **Over-build GW range AND cost-exposure $ range for ≥3 RTOs including PJM, each low/high not a point** — §1 table gives all five (PJM, ERCOT, MISO, SPP, CAISO), each with a low-phantom→high-phantom over-build GW band and a low→high $/yr exposure band, plus a separate stranded-capital bound. PJM, ERCOT, MISO satisfy the ≥3-including-PJM minimum with margin.
- [x] **At least one RTO fully worked, every multiplier and input shown and individually cited, reproducible by hand** — PJM, §2: `A^DC=55.0` (S12/M3) → `P`=0.36/0.55/0.72 (M3) → over-build 19.8/30.2/39.6 GW → ×$98.52–$120.15/kW-yr (=$269.92–$329.17/MW-day × 365, S17/S18) → **$1.95B–$4.76B/yr**, with the full kW-level multiplication shown (19,800,000 kW × $98.52 = $1,950,696,000) and a sanity check against the $14.2B auction-cost jump.
- [x] **Cost anchors quoted with numbers and cited, not paraphrased** — PJM BRA $2.2B → $14.7B → $16.1B → $16.4B; clearing $28.92 → $269.92 → $329.17 → $333.44/MW-day (S17, S18, S6); retail +8.25% US / +19.35% VA (S6); gas capex $921/kW (S19) and $2,200–$2,500/kW (S20/S21), with $722/kW (2022, S21) for context.
- [x] **Limitations states ≥2 reasons with direction of bias** — §4 lists **seven**, each with HIGH / LOW / indeterminate direction (near-cap prices→HIGH; timing slice→HIGH; ERCOT proxy→indeterminate & dominant; Basis-B new-build→HIGH; gas-cost peak→HIGH; inherited M3 uncertainty→indeterminate; plus counter-evidence the cost is real and being billed now).
- [x] **Chains off M3, no re-derivation of phantom fractions** — §0 and §2 take `A^DC` and `P` verbatim from M3 §2; over-build = `A^DC × P`; the §0 PJM check shows the two computation routes agree. No new haircut is introduced.

---

## 6. New sources added (cost anchors; not in M1–M3 inventories; URLs verified 2026-06-27/28)

| ID | Source | Publisher | Date | URL | Supplies |
|---|---|---|---|---|---|
| S17 | "PJM capacity prices hit record highs, sending build signal to generators" (corroborated by S&P Global market report) | Utility Dive / S&P Global Commodity Insights | 2024-07-30 | https://www.utilitydive.com/news/pjm-interconnection-capacity-auction-vistra-constellation/722872/ | PJM 2025/26 BRA: clearing **$269.92/MW-day** (vs **$28.92** prior year); total cost to load **$14.7B** (up from **$2.2B**); zonal caps to $466.35/MW-day (BGE) and $444.26/MW-day (Dominion). |
| S18 | "PJM Auction Procures 134,311 MW of Generation Resources; Supply Responds to Price Signal" / "PJM's Record-High Capacity Prices…" | PJM Inside Lines / POWER Magazine | 2025-07-22 | https://insidelines.pjm.com/pjm-auction-procures-134311-mw-of-generation-resources-supply-responds-to-price-signal/ | PJM 2026/27 BRA: clearing **$329.17/MW-day** (UCAP, full footprint, at FERC cap; uncapped est. $389); total value **$16.1B** (+9.5% vs $14.7B); peak forecast +>5,400 MW "driven largely by data center expansion." |
| S19 | "Capital Cost and Performance Characteristics for Utility-Scale Electricity Generating Plants" (AEO2025 capital cost study) | U.S. Energy Information Administration | 2025 | https://www.eia.gov/analysis/studies/powerplants/capitalcost/pdf/capital_cost_AEO2025.pdf | New gas combined-cycle overnight capital cost ≈ **$921/kW (2023$)** (Sargent & Lundy basis; ~$1,058/kW by 2030 at 2% escalation). Low-end generation-capex anchor (Basis B). |
| S20 | "The New Reality of Power Generation: An Analysis of Increasing Gas Turbine Costs" | GridLab | 2025-09 | https://gridlab.org/wp-content/uploads/2025/09/GridLab_Gas-Turbine-Costs-Report-1.pdf | 2025 observed build cost ≈ **$2.2M–$2.5M/MW = $2,200–$2,500/kW** for new gas CC, roughly **tripled** vs. a few years prior. High-end generation-capex anchor (Basis B). |
| S21 | "Construction Costs for Gas-fired Power Remains Well Below Those for Solar and Wind" (citing EIA generator-cost data) | Institute for Energy Research | 2024 | https://www.instituteforenergyresearch.org/fossil-fuels/gas-and-oil/construction-costs-for-gas/ | EIA-reported combined-cycle construction cost **$722/kW (2022)** — historical low-end context point for the gas-capex range. |
| S22 | MISO Planning Resource Auction (PRA) results context — used only as an order-of-magnitude low proxy ($/kW-yr well below PJM) | MISO (PRA results, public) | 2025 | https://www.misoenergy.org/markets-and-operations/RPM/ | MISO capacity prices historically far below PJM; used as the **low ($40/kW-yr-class) proxy bound** for the MISO Basis-A band. [Order-of-magnitude proxy; not a single cited clearing price — band widened accordingly.] |

**Cost anchors repeated from M1/M3 (S6, load-bearing here):**
- **S6** — POWER Magazine / Tom Bailey, 2026-05-15, https://www.powermag.com/phantom-data-centers-didnt-break-the-power-grid-they-proved-it-was-already-broken/ — PJM auction "**$2.2 billion** for 2024-25 … **$16.4 billion** in 2027-28"; retail electricity "**+8.25% nationally**, **+19.35% in Virginia**"; Exelon 22%-materialize; CenterPoint 1→25 GW. (Quotes verified verbatim 2026-06-27/28.) The 2027/28 BRA $16.4B / $333.44-MW-day cap figure is independently confirmed (PJM Inside Lines, 2025-12-17, https://insidelines.pjm.com/pjm-auction-procures-134479-mw-of-generation-resources/).

**Note on S22:** the MISO low proxy is the only anchor in this artifact that is *not* a single cited clearing price; per the conservatism rule, the MISO Basis-A band is correspondingly widened ($40–$98.52/kW-yr) rather than presented as precise. A reader wanting the firmest MISO number should pull the latest MISO PRA auction summary directly.
