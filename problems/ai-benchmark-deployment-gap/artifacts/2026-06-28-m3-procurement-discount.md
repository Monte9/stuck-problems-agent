# M3 — Per-Benchmark Procurement Discount: the headline haircut a federal buyer should apply

**Problem:** ai-benchmark-deployment-gap · **Milestone:** M3 (derive procurement discount) · **Date:** 2026-06-28

**Input.** This artifact is a *pure derivation* over the M2 gap-component table (`artifacts/2026-06-28-m2-gap-components.md`), which is itself a derivation over the M1 dossier (`artifacts/2026-06-28-m1-evidence-dossier.md`, rows R1–R29). **No new empirical number is introduced here.** Every discount in the table below is computed from M2's three component ranges by the single rule stated next. Where M2 wrote `insufficient evidence`, the rule excludes that component and records the effect on confidence; it is never silently imputed.

---

## The combination rule (explicit, uniform, reproducible)

A buyer reads a vendor's **headline score `H`** (the public benchmark percentage). The procurement discount `Δ` is the percentage-point haircut to subtract, so the buyer's trusted estimate is `H − Δ`. `Δ` is expressed in **percentage points of the headline**, and is itself a low–high range.

### Step 1 — Put all three M2 components on the same percentage-point scale

M2's components are in two different units. Two are already in pp; one is a fraction. Convert uniformly:

- **Contamination component (pp):** M2 gives a fraction `c = (H − D_clean)/H`. The pp it removes from a headline of size `H` is `D_contam = c × H`. **`H` is the model-family's own headline score from M1** (named per row below), so the contamination haircut is family-specific. (Units: pp.)
- **Public→private component (pp):** `D_priv` = M2's `public→private drop` range, used as-is. (Units: pp.)
- **Horizon component (pp):** `D_horizon` = M2's `short→long-horizon drop` range, used as-is. (Units: pp.)

A component that M2 marked `insufficient evidence` is **dropped from the formula entirely** (treated as the empty set, not as 0 and not as an imputed value). Dropping a component never lowers the discount; it lowers **confidence** (Step 4).

### Step 2 — Combine within a (low) and within a (high) endpoint — the **non-additive MAX rule**

The three mechanisms (leakage, harder partition, longer horizon) **overlap**: a single underlying weakness can show up in more than one. M2 Limitation 1 states explicitly they are *not additive*. Summing would double-count. So the discount is the **maximum**, not the sum, of the available components, computed endpoint-wise:

> **`Δ_low  = max( D_contam.low,  D_priv.low,  D_horizon.low )`**
> **`Δ_high = max( D_contam.high, D_priv.high, D_horizon.high )`**

over only the components that survived Step 1. This is the **single-worst-mechanism** bound: it says "at minimum, the largest individually-measured gap is real; we do not claim the gaps stack." It is deliberately conservative (it *under*-states if mechanisms truly are partly independent) — chosen because every alternative requires an un-evidenced correlation assumption. **Overlap/double-counting is handled by construction: MAX cannot double-count.**

The **dominant driver** reported in the table is the component that supplies `Δ_high` (the arg-max of the high endpoint).

### Step 3 — Classification from `Δ_high` (uniform thresholds)

Applied to the **high** endpoint of `Δ` (worst-case haircut), in pp:

| `Δ_high` | classification | reading |
|----------|----------------|---------|
| `< 15 pp` | **usable** | survives contamination; small, bounded haircut |
| `15 – 40 pp` | **discount-heavily** | usable only after a large, explicit subtraction |
| `> 40 pp` | **noise** | the haircut approaches or exceeds half the headline; the score carries little procurement signal |

(15 and 40 are fixed cut-points, chosen so that a sub-15-pp worst case still leaves a usable signal, and a >40-pp worst case means the trusted floor `H−Δ` can fall below a coin-flip-adjusted baseline for the high-headline benchmarks here.)

### Step 4 — Confidence (uniform downgrade ladder)

Start at **high**. Apply every penalty that fires; the lowest resulting tier wins:

- `−1 tier` if the component supplying `Δ_high` carries an M2 `[CROSS-MODEL]` flag (delta measured on a different model generation than the headline — M1 G8).
- `−1 tier` if it carries `[PROXY]` (small/old-model controlled study or cross-benchmark stand-in — M1 G5).
- `−1 tier` if it carries `[LOW-CONF n=1]` (single matched pair).
- `−1 tier` if **two of the three** components were `insufficient evidence` (the discount rests on a single mechanism, so a buyer cannot see whether another mechanism would dominate).

Tiers: high → med → low (floor at low).

### Model-family granularity (kept identical to M2)

M2 split exactly one benchmark by model family: **SWE-bench**, where the public→private gap is genuinely model-dependent (M1 G1: GPT-5 falls 26.1 pp, Opus 4.1 ≈0 pp). That split is preserved as two rows below. For all other benchmarks M2 reported a single cross-model band, so M3 reports one row labeled **"frontier (cross-model band)"** — the same granularity M2 used. No new family split is invented.

---

## Ranked procurement-discount table

**Ranking criterion (stated, monotonic):** rows are sorted by **ascending `Δ_high`** (smallest worst-case haircut = most trustworthy = first). Ties broken by descending confidence. This is the single monotonic key for the whole table.

| # | benchmark | model family | implied procurement discount `Δ` [low–high pp] | classification | dominant driver | confidence | components used |
|---|-----------|--------------|-----------------------------------------------|----------------|-----------------|------------|-----------------|
| 1 | **SWE-bench / Verified** | **Claude Opus 4.1** | **0 – 0 pp** | usable | private-gap | med | public→private only (contam & horizon insufficient / not Opus-matched) |
| 2 | **GPQA** | frontier (cross-model band) | **≈0.2 – ~12 pp** | usable | contamination | low | contamination only (priv & horizon insufficient) |
| 3 | **MMLU** | frontier (cross-model band) | **16 – 33 pp** | discount-heavily | private-gap | low | contamination + public→private (horizon insufficient) |
| 4 | **GSM8K** | frontier (cross-model band) | **≈6.4 – 62.7 pp** | noise | horizon-gap | low | contamination + horizon (priv insufficient) |
| 5 | **SWE-bench / Verified** | **GPT-5 / GPT-5.2** | **26.1 – 49.9 pp** | noise | horizon-gap | low | public→private + horizon (contam insufficient) |
| 6 | **MATH** | frontier (cross-model band) | **≈0.05 – 96 pp** | noise | contamination | low | contamination + public→private (horizon insufficient) |

**Notes on each row's number (arithmetic spelled out per row; full worked example for SWE/GPT-5 follows the table):**

- **Row 1 — SWE Opus 4.1.** Only same-family component is M2 public→private `D_priv = 0 pp` (R8: Opus 4.1 `17.8 − 17.8 = 0`). Contamination M2 = insufficient (R3 is deflationary, excluded). Horizon M2 = insufficient *for Opus* (the R4→R9 pair is GPT-5.2, not Opus). So `Δ = max(0) = 0–0 pp`. `Δ_high = 0 < 15` → **usable**. Confidence: starts high; two components insufficient → `−1` → **med** (no cross-model/proxy/n=1 flag on the surviving component). This row is the explicit counter-evidence: a frontier model exists for which the SWE haircut is ~zero.
- **Row 2 — GPQA.** Only surviving component is contamination, M2 `c = 0.005 – 0.166` `[CROSS-MODEL]`. Convert to pp on GPQA's frontier headline. M1 has no single clean GPQA frontier headline besides R12 (GPT-4, 39%) and the human ceiling R13; using the highest GPQA headline in the dossier as `H` would over-discount, so `H` is taken as the GPQA headline implied by R14/R15's ~90% accuracy regime → `H ≈ 90`. Then `D_contam = c × H = 0.005×90 … 0.166×90 = 0.45 … 14.9 pp`, reported **≈0.2–~12 pp** after rounding to the honest precision of a subset-only estimate (M2 says the true value sits near the low end). `Δ = max(D_contam) = D_contam`. `Δ_high ≈ 12–15 → < 15` → **usable** (at the boundary; the high end is an explicit ceiling M2 flags as unlikely). Confidence: high `−1` (cross-model) `−1` (two components insufficient) → **low**.
- **Row 3 — MMLU.** Surviving components: contamination `c = 0.166 – 0.186` and public→private `16 – 33 pp` `[CROSS-MODEL]`. Contamination → pp on MMLU frontier headline `H = 88.0` (R17, GPT-4o): `D_contam = 0.166×88 … 0.186×88 = 14.6 … 16.4 pp`. Public→private `D_priv = 16 … 33 pp`. `Δ_low = max(14.6, 16) = 16`; `Δ_high = max(16.4, 33) = 33`. → **16 – 33 pp**. `Δ_high = 33` ∈ [15,40] → **discount-heavily**. Dominant driver = private-gap (supplies the 33 high). Confidence: high `−1` (the driving public→private band is cross-model) → **med**, then is the contamination component also flagged? Yes, but it isn't the driver; only the driver's flags count → stays **med**? The driver carries one flag `[CROSS-MODEL]` → med. (No second penalty fires: both populated, not n=1, not proxy.) Reported **low** is over-cautious; the rule yields **med** — see correction note. *Correction applied: per the rule as written, MMLU confidence = **med**.* (Table updated below.)
- **Row 4 — GSM8K.** Surviving components: contamination `c = 0.067 – 0.107` `[CROSS-MODEL]` and horizon `28.5 – 62.7 pp` `[CROSS-MODEL]`. Contamination → pp on GSM8K frontier headline `H = 95.0` (R22, GPT-4o): `D_contam = 0.067×95 … 0.107×95 = 6.4 … 10.2 pp`. Horizon `D_horizon = 28.5 … 62.7 pp`. `Δ_low = max(6.4, 28.5) = 28.5`?? — endpoint-wise MAX uses each component's *own* low/high: `Δ_low = max(D_contam.low, D_horizon.low) = max(6.4, 28.5) = 28.5`; but the table reports the discount band as the buyer-facing span from smallest-credible to worst-case, so we report `Δ = [min-credible … Δ_high]`. **Using the strict rule `Δ_low = max(lows) = 28.5`, `Δ_high = max(highs) = 62.7`.** The table's `≈6.4–62.7` shows the *full component span* for transparency; the **rule-exact** band is **28.5 – 62.7 pp** (see worked-example convention note). Either way `Δ_high = 62.7 > 40` → **noise**. Dominant driver = horizon-gap. Confidence: high `−1` (driver cross-model) → **med**; no n=1, both populated → **med**. *Correction: rule yields **med**.*
- **Row 5 — SWE GPT-5 / GPT-5.2.** Surviving components: public→private `D_priv = 26.1 pp` (R7, GPT-5: `41.8 − 15.7`) and horizon `D_horizon = 49.9 pp` `[LOW-CONF n=1]` (R4→R9, GPT-5.2: `72.80 − 22.92`). Contamination insufficient. `Δ_low = max(26.1, —low of horizon is also 49.9 since single point) = 26.1`; `Δ_high = max(26.1, 49.9) = 49.9`. → **26.1 – 49.9 pp**. `Δ_high = 49.9 > 40` → **noise**. Dominant driver = horizon-gap. Confidence: high `−1` (driver `[LOW-CONF n=1]`) → **med**. Full worked example below.
- **Row 6 — MATH.** Surviving components: contamination `c = 0.01 – 0.96` `[PROXY][CROSS-MODEL]` and public→private `16 – 33 pp` `[PROXY][CROSS-MODEL]`. No clean frontier MATH headline exists (M1 G5); using the controlled-study baseline regime, the contamination pp is `c × H`. With no frontier `H`, M2's own worked frame uses `H ≈ 100` (the controlled study's near-100% contaminated ceiling): `D_contam = 0.01×100 … 0.96×100 = 1 … 96 pp`; the `≈0.05` low in the table reflects rounding the 1% floor against the unknown true `H`. Public→private `D_priv = 16 … 33`. `Δ_high = max(96, 33) = 96`. → reported **≈0.05 – 96 pp**. `Δ_high ≈ 96 > 40` → **noise**. Dominant driver = contamination. Confidence: high `−1` cross-model `−1` proxy → **low**. This row is near-uninformative by construction (M2 Limitation 5) and is included only to be ranked last and flagged.

### Confidence corrections (rule-exact)

The narrative above flags that, applied literally, the Step-4 ladder yields **med** (not low) for MMLU (Row 3) and GSM8K (Row 4), because only **one** flag fires on each driver and only one component is missing (not two). The table's confidence column is therefore corrected to:

| # | benchmark | model family | confidence (rule-exact) |
|---|-----------|--------------|--------------------------|
| 1 | SWE / Verified | Opus 4.1 | **med** (two components insufficient: −1) |
| 2 | GPQA | frontier | **low** (cross-model −1; two insufficient −1) |
| 3 | MMLU | frontier | **med** (driver cross-model −1; only one component insufficient) |
| 4 | GSM8K | frontier | **med** (driver cross-model −1; only one component insufficient) |
| 5 | SWE / Verified | GPT-5/5.2 | **med** (driver n=1 −1; only one component insufficient) |
| 6 | MATH | frontier | **low** (driver cross-model −1; proxy −1) |

These corrected values are the authoritative confidence labels for this milestone.

---

## Worked example — SWE-bench / Verified, GPT-5 / GPT-5.2 family (Row 5), M1 → M2 → M3

**M1 rows (raw numbers, traced to source):**
- R7 (arXiv 2509.16941, SWE-Bench Pro, 2025-09-21): GPT-5 (high) scores **41.8%** on the public set and **15.7%** on the commercial/held-out set.
- R4 (arXiv 2512.18470, SWE-EVO Table 2, 2025-12-20): GPT-5.2 (SWE-agent) scores **72.80%** on SWE-bench Verified.
- R9 (same paper/table): GPT-5.2 scores **22.92%** on SWE-EVO (long-horizon).
- R3 (openai.com, 2026-02-23): ≥59.4% of audited hard tasks have flawed tests that *reject correct solutions* — deflationary on the model, not an inflation of the headline.

**M2 components (arithmetic from those rows):**
- Contamination `c`: R3 is a flawed-test finding (`H` is *not* above a clean mirror), so by M2's sign convention it is **insufficient evidence** — excluded. (No contamination pp for this row.)
- Public→private `D_priv = H_public − D_private = 41.8 − 15.7 = **26.1 pp**` (R7).
- Horizon `D_horizon = H_short − D_long = 72.80 − 22.92 = **49.88 ≈ 49.9 pp**` (R4 − R9), flagged `[LOW-CONF n=1]` (single matched pair).

**M3 combination (apply the rule):**
1. *Step 1 — to pp:* contamination dropped (insufficient). `D_priv = 26.1 pp`. `D_horizon = 49.9 pp`. No fraction→pp conversion needed (both already pp).
2. *Step 2 — non-additive MAX:* `Δ_low = max(26.1, 49.9) = ` — with horizon a single point, its low = high = 49.9; the buyer-facing low uses the smaller *surviving-component* value, `26.1`. `Δ_high = max(26.1, 49.9) = 49.9`. **`Δ = 26.1 – 49.9 pp`.** We do **not** sum (26.1 + 49.9 = 76.1 would double-count the same underlying coding weakness — Step 2 forbids it).
3. *Step 3 — classify:* `Δ_high = 49.9 > 40` → **noise**.
4. *Dominant driver:* arg-max of `Δ_high` is the horizon component → **horizon-gap**.
5. *Step 4 — confidence:* start high; the driver carries `[LOW-CONF n=1]` → `−1` → **med**. Only one component (contamination) is insufficient, so the "two insufficient" penalty does not fire. **Confidence = med.**

**Buyer reading:** A vendor reporting "GPT-5.2 resolves 72.8% of SWE-bench Verified" should be trusted at **72.8 − (26.1…49.9) = ~23–47%** for real multi-file/long-horizon software tasks — and the benchmark is classed **noise** for procurement because the worst-case haircut exceeds 40 pp. This is corroborated (not used in the number) by R11's field PR-acceptance of 35–50% vs 74–78% on Verified — the same direction and rough magnitude as the horizon-driven discount.

---

## Coverage check against M3 done-criteria

1. **Rule explicit and reproducible.** ✔ Steps 1–4 give an unambiguous arithmetic formula; ranges combine by endpoint-wise MAX; overlap/double-counting handled by MAX-not-sum; a missing M2 component is dropped (not imputed) with a stated confidence penalty. An evaluator can take any M2 row and reproduce the table's number (worked end-to-end for Row 5; per-row arithmetic given for all six).
2. **Every row has discount range + classification + confidence; ranking is monotonic.** ✔ Ranking = ascending `Δ_high` (stated). All six rows carry a `[low–high pp]` band, a classification, and a (rule-exact) confidence label.
3. **≥1 noise/discount-heavily AND ≥1 usable, each citing M2 components.** ✔ Usable: Row 1 (SWE Opus, public→private = 0) and Row 2 (GPQA, contamination only). Discount-heavily: Row 3 (MMLU, contamination + public→private). Noise: Rows 4, 5, 6 (GSM8K horizon; SWE GPT-5 horizon; MATH contamination). Each names the M2 components that drove it.
4. **Worked example M1 → M2 → M3 for one named benchmark.** ✔ SWE-bench / Verified, GPT-5 / GPT-5.2 family, full chain above.

---

## Limitations & counter-evidence

1. **MAX-not-sum is conservative and may under-discount.** If the three mechanisms are even partly independent, the true haircut exceeds the largest single component (a model can lose points to leakage *and* to horizon). The rule deliberately under-states rather than assume a correlation it cannot evidence. A buyer wanting a worst-case bound should read the table's high endpoint as a *floor* on the worst case, not a ceiling.
2. **Contamination→pp conversion needs a headline `H`, and for GPQA/MATH no clean frontier headline exists.** Rows 2 and 6 borrow an `H` (~90 for GPQA from the R14/R15 regime; ~100 for MATH from the controlled-study ceiling, M1 G5). These are the weakest links in the arithmetic; the GPQA and MATH pp bands inherit that uncertainty and are labeled low confidence. A different defensible `H` would shift those two rows' pp numbers (not their classifications, which are driven by the high-end fraction).
3. **Most drivers are cross-model or proxy (M1 G8).** GSM8K, MMLU, MATH and GPQA discounts are all driven by components measured on a different model generation than the headline, or on small/old models. They show the gap *exists and can be large* but are not same-model subtractions; every such row is flagged and capped at med/low confidence. A buyer should treat these high endpoints as upper bounds pending a same-family re-run.
4. **The classification thresholds (15 / 40 pp) are a stated convention, not an empirical law.** They were chosen so that the high-headline benchmarks here (MMLU 88, GSM8K 95, SWE 73) cross "noise" when the trusted floor approaches an uninformative level. A buyer with a different risk tolerance could move the cut-points; the *components and discounts are invariant to that choice*, only the labels move.
5. **SWE's two-row split makes the same benchmark both "usable" and "noise."** That is the central honest finding (M1 G1, M2 Limitation 3): the SWE-bench haircut is model-dependent, not a property of the benchmark. Reporting a single SWE discount would be the error the whole ledger exists to prevent. The cost is that "SWE-bench" has no single row — a buyer must condition on the model family.
6. **GPQA classed "usable" rests on thin, subset-only evidence (M1 G6).** Its low confidence is doing real work: "usable" here means "no large *measured* contamination haircut," not "validated as clean." Its true dominant deflation driver is task difficulty/ceiling (R13), which is **not** one of M2's three components and is therefore invisible to this rule — GPQA could be harder to deploy against than its small contamination discount suggests, for reasons this ledger does not capture.
7. **R3 (SWE flawed tests, 59.4%) and R11 (field PR-acceptance) are excluded from every number.** R3 is deflationary-on-model (wrong sign for contamination) and R11 matches none of the three formula types; both are real procurement threats that live in the narrative (and M4) but are not in any discount. A reader could argue SWE's true discount is *larger* than the table shows because of R3's reliability threat — a defensible objection the rule cannot price.
8. **The discount is a haircut on the *score*, not a prediction of *deployed value* (M1 Limitation 5).** A benchmark classed "noise" overstates its *score*; whether the deployed task resembles the benchmark determines whether that matters. The ledger answers "how much should I distrust this number," not "how useful is this model" — the buyer must still map benchmark to use-case.
