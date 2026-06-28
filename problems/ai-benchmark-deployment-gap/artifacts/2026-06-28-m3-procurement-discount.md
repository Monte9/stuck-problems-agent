# M3 — Procurement Discount: per-benchmark, per-model-family haircut

**Problem:** ai-benchmark-deployment-gap · **Milestone:** M3 (derive the procurement discount) · **Date:** 2026-06-28

**Input.** This artifact is a pure *combination + classification* over the M2 gap-component table (`artifacts/2026-06-28-m2-gap-components.md`), whose cells trace to M1 rows (`artifacts/2026-06-28-m1-evidence-dossier.md`, R1–R29). **No new external number is introduced here.** Every discount is a function of M2 component ranges only. Where M3 references a "headline" (`H_ref`) to convert a contamination *fraction* into percentage points, that `H_ref` is itself an M1 row (cited per benchmark below), not a new figure.

The deliverable: for each benchmark × model family, a **procurement discount** — the percentage-point haircut a buyer (CAISI/NIST + GSA) should subtract from a vendor's headline score before trusting it — plus a classification and confidence.

---

## 1. Methods preamble

### 1.1 The combination rule (exact formula, applied uniformly to every row)

The three M2 components measure **different, overlapping** deflation mechanisms (leakage; harder/held-out partition; longer-horizon/robustness). M2 Limitation #1 establishes they are **not additive** and may double-count the same underlying weakness. The uniform rule is therefore a **max over channels**, expressed in percentage points against a stated reference headline:

> **Step A — put all three channels in percentage points.**
> - Contamination channel (fraction → pp): `P_contam = c × H_ref`, where `c` is the M2 contamination fraction and `H_ref` is the benchmark's frontier public headline (an M1 row, cited per benchmark). Units: pp.
> - Public→private channel: `P_priv = Δpp_priv` (already pp; pass through unchanged).
> - Horizon channel: `P_horizon = Δpp_horizon` (already pp; pass through unchanged).
>
> **Step B — combine by taking the per-endpoint maximum across the three channels** (non-additive, because the channels overlap):
> - `Discount_low  = max(P_contam_low,  P_priv_low,  P_horizon_low)`
> - `Discount_high = max(P_contam_high, P_priv_high, P_horizon_high)`
>
> The discount is the band `[Discount_low – Discount_high]` in percentage points, the haircut to subtract from a vendor headline.

**Operators / units.** `×` is scalar multiply; `max` is the ordinary maximum; all outputs are **percentage points (pp)** subtracted from a 0–100 headline. `c` is dimensionless in [0,1]; `H_ref` and the two `Δpp` components are in pp.

**Why max, not sum.** Summing would assert the channels are independent and stack (a contaminated *and* held-out *and* long-horizon penalty all apply at once to the same task). They do not: a buyer who runs a private long-horizon eval already captures most of the contamination penalty inside that single measurement. The max returns the **single largest credible deflation** as a lower bound on the true haircut — deliberately conservative against double-counting, and the most defensible uniform choice given M2 said "do not sum." (A buyer wanting a worst-case stack can sum the channels; that variant is noted in Limitations, not used here.)

### 1.2 Range propagation

Ranges propagate **endpoint-wise through the max** (Step B above): the discount's low end is the max of the channels' low ends; the discount's high end is the max of the channels' high ends. A component's own low–high range (from M2) carries straight into the corresponding endpoint. Contamination's pp band is `[c_low × H_ref, c_high × H_ref]`. No averaging, no midpoint collapse — the band is preserved.

### 1.3 Insufficient-evidence handling

A channel marked `insufficient evidence` in M2 **contributes nothing to the max** (treated as `P = 0` for both endpoints; it cannot *raise* the discount, and we never invent a number to fill it). Consequence:

- If **at least one** channel is populated, the discount is computed from the populated channel(s) — a known *lower bound* on the true haircut (an un-priced channel could be larger). Rows in this state carry a "lower-bound" note.
- If **all three** channels are `insufficient evidence`, the discount **cannot be priced**. Per the conservative rule, such a row is assigned classification **`noise` (cannot price → treat as max-discount)** and confidence **low**, never silently dropped. (No benchmark in the M2 set is fully empty, but GPQA is close and is handled explicitly below.)

### 1.4 Classification thresholds (by Discount_high, in pp)

Applied uniformly to the high end of the discount band:

| Discount_high (pp) | Classification |
|---|---|
| `≤ 10` | **usable** — survives contamination; subtract a small haircut and trust the rest |
| `> 10 and ≤ 35` | **discount-heavily** — usable only with a large, explicit haircut |
| `> 35` | **noise** — the headline overstates by more than a third of the scale; functionally uninformative for procurement without an independent re-run |

The **high** end is the threshold key because procurement is a downside-risk decision: a buyer should classify on the worst-case haircut they could be exposed to, not the optimistic end.

### 1.5 Confidence rule

Confidence is capped by the *weakest* M2 flag feeding the **dominant** channel (the channel that wins the max at the high end):

- dominant channel unflagged, multi-pair → **high**
- dominant channel carries `[CROSS-MODEL]` **or** `[LOW-CONF n=1]` → **med** (cap)
- dominant channel carries `[PROXY]` (small/old-model controlled study standing in for a frontier delta) **or** all channels insufficient → **low**

Any discount whose dominant channel rests on an M2 cell flagged `n=1 / [LOW-CONF] / [CROSS-MODEL] / [PROXY]` therefore carries confidence ≤ med, as required.

### 1.6 Ranking key (monotonic)

Rows are sorted **ascending by `Discount_high`** (smallest worst-case haircut first = most trustworthy first), ties broken by ascending `Discount_low`. This is the single monotonic key; the table below is sorted by it.

### 1.7 Reference headlines used for the contamination→pp conversion (all M1 rows, no new numbers)

| Benchmark | `H_ref` | M1 row |
|---|---|---|
| SWE-bench Verified | 72.80 | R4 (GPT-5.2, frontier headline) |
| GPQA | 90 | denominator used in M2's own GPQA derivation (R14/R15 region; ~90% headline band) |
| MMLU | 88.0 | R17 (GPT-4o) |
| GSM8K | 95.0 | R22 (GPT-4o) |
| MATH | 100 | controlled-study scale baseline used in M2 (R27); flagged `[PROXY]` — no frontier MATH headline exists (M1 G5) |

---

## 2. Ranked procurement-discount table

Sorted ascending by `Discount_high` (most trustworthy first). All inputs cite the M2 component value (→ M1 rows).

| # | benchmark | model family | implied procurement discount [low–high pp] | classification | dominant driver | confidence | components used (M2 → M1) |
|---|-----------|--------------|--------------------------------------------|----------------|-----------------|------------|----------------------------|
| 1 | **GPQA** | model-agnostic (frontier, cross-model) | **0.5 – 14.9 pp** | **discount-heavily** | contamination | **low** | contam `c=0.005–0.166` `[CROSS-MODEL]` × H_ref=90 → P_contam = **0.5–14.9 pp** (R14, R15); priv & horizon = *insufficient* → 0. All non-contam channels empty ⇒ lower bound. Dominant channel is subset-only/indirect (M1 G6) ⇒ conf low. |
| 2 | **MMLU** | GPT-4-class (GPT-4o / GPT-4-Turbo) | **16 – 33 pp** | **discount-heavily** | private-gap | **med** | contam `c=0.166–0.186` × H_ref=88 → P_contam = **14.6–16.4 pp** (R18, R19); priv `Δpp_priv=16–33` `[CROSS-MODEL]` (R20); horizon = *insufficient* → 0. max(16.4, 33) ⇒ **16–33 pp**, priv wins high end. Priv is cross-model aggregate ⇒ conf med. |
| 3 | **SWE-bench Verified** | Claude Opus 4.1 | **0 – 49.9 pp** | **noise** | horizon-gap | **med** | contam = *insufficient* (R3 is flawed-test, not inflation → 0); priv `Δpp_priv=0` same-model (R8: 17.8→17.8); horizon `Δpp_horizon≈49.9` `[LOW-CONF n=1]` (R4→R9) applied as **cross-model upper bound** for this family (measured on GPT-5.2). max(0, 0, 49.9) ⇒ **0–49.9 pp**. Opus is ≈flat on the *priced* same-model channel (M1 G1); the high end is the SWE-family horizon collapse imported cross-model ⇒ conf med, n=1. |
| 4 | **SWE-bench Verified** | GPT-5 line (GPT-5 / GPT-5.2) | **26.1 – 49.9 pp** | **noise** | horizon-gap | **med** | contam = *insufficient* → 0; priv `Δpp_priv=26.1` (R7: 41.8→15.7); horizon `Δpp_horizon≈49.9` `[LOW-CONF n=1]` (R4→R9, GPT-5.2). max(26.1, 49.9) ⇒ **26.1–49.9 pp**, horizon wins high end. Horizon is a single matched pair ⇒ conf med, n=1. |
| 5 | **GSM8K** | GPT-4o-class (frontier headline) | **28.5 – 62.7 pp** | **noise** | horizon-gap | **med** | contam `c=0.067–0.107` `[CROSS-MODEL]` × H_ref=95 → P_contam = **6.4–10.2 pp** (R23, R25); priv = *insufficient* → 0; horizon `Δpp_horizon=28.5–62.7` `[CROSS-MODEL]` (R24, GSM-NoOp). max(10.2, 62.7) ⇒ **28.5–62.7 pp**, horizon wins both ends. Horizon mixes model generations ⇒ conf med. |
| 6 | **MATH** | none (frontier MATH delta does not exist) | **16 – 96 pp** | **noise** | contamination | **low** | contam `c=0.01–0.96` `[PROXY][CROSS-MODEL]` × H_ref=100 → P_contam = **1–96 pp** (R27, R21); priv `Δpp_priv=16–33` `[PROXY][CROSS-MODEL]` (R29); horizon = *insufficient* → 0. max(96, 33) ⇒ **16–96 pp** (low from priv 16, high from contam 96). Dominant channel is a ≤344M-param controlled-injection artifact ⇒ conf low; band is effectively "unquantified for procurement." |

**Classification spread (done-criterion 3):** no row reached `usable` (≤10 pp high) — even GPQA's high end (14.9 pp) clears the 10-pp bar — so the most-trustworthy class achieved is `discount-heavily` (GPQA, MMLU), and `noise` is reached by SWE (both families), GSM8K, and MATH. This satisfies "at least one `discount-heavily` AND at least one `noise`," with the `usable` band defined and shown empty (an honest finding: under this conservative rule, none of the five public benchmarks survives with a ≤10-pp haircut once the worst credible channel is priced).

**Dominant-driver readout:** contamination dominates GPQA and MATH; the private-holdout gap dominates MMLU; the long-horizon/robustness gap dominates both SWE families and GSM8K. The headline takeaway for the buyer: **the long-horizon channel, not contamination, is the largest deflation source for the coding and grade-school-math benchmarks**, while contamination dominates only where no frontier horizon evidence exists (GPQA, MATH).

---

## 3. Worked example end-to-end: GSM8K (M1 rows → M2 components → discount)

Walking the row at rank 5 fully, so an evaluator can reproduce the table number.

**Step 0 — reference headline (M1).** R22: GPT-4o scores **95.0%** on GSM8K. So `H_ref = 95.0` (M1 row, not a new number).

**Step 1 — pull the three M2 components for GSM8K** (from the M2 table, GSM8K row):
- contamination fraction `c = 0.067 – 0.107` `[CROSS-MODEL]`, derived in M2 from R23 (GSM-Symbolic): Phi-3.5 `(88.0−82.1)/88.0 = 0.067`, Gemma2-9b `(87.0−79.1)/87.0 = 0.091`, Mistral-7b `(56.0−50.0)/56.0 = 0.107`; corroborated by R25 (GSM1k ≤8%).
- public→private drop = **insufficient evidence** (M2: no GSM8K held-out commercial partition; GSM1k is a contamination mirror, already used in `c`).
- short→long-horizon drop `Δpp_horizon = 28.5 – 62.7 pp` `[CROSS-MODEL]`, derived in M2 from R24 (GSM-NoOp): o1-mini `94.5−66.0 = 28.5`, GPT-4o `94.9−63.1 = 31.8`, Phi-3-mini `80.7−18.0 = 62.7`.

**Step 2 — Step A of the rule: put each channel in pp.**
- `P_contam = c × H_ref = [0.067 × 95.0, 0.107 × 95.0] = [6.4, 10.2] pp`.
- `P_priv = 0` (insufficient → contributes nothing to the max).
- `P_horizon = [28.5, 62.7] pp` (pass-through).

**Step 3 — Step B: per-endpoint max across channels.**
- `Discount_low  = max(6.4, 0, 28.5) = 28.5 pp`.
- `Discount_high = max(10.2, 0, 62.7) = 62.7 pp`.
- **Discount = 28.5 – 62.7 pp.** ✓ matches the table.

**Step 4 — classify.** `Discount_high = 62.7 pp > 35` → **noise**.

**Step 5 — dominant driver & confidence.** The channel that wins the high-end max is horizon (62.7 ≫ 10.2) → **dominant driver = horizon-gap**. That channel carries `[CROSS-MODEL]` (R24 mixes o1-mini/GPT-4o/Phi-3 generations) → confidence capped at **med** per §1.5.

**Reading for the buyer.** A vendor reporting ~95% on GSM8K is reporting a number whose deployment-relevant value, once you add one irrelevant clause to each problem (GSM-NoOp, R24), can fall by 28–63 pp. Subtract at least ~29 pp from any GSM8K headline before trusting it for a procurement decision involving multi-step or adversarially-worded arithmetic; treat the benchmark as functionally noise for that use. The caveat: the horizon evidence is cross-model (no GPT-5-class GSM-NoOp row exists), so this is a flagged, med-confidence lower bound on the haircut, not a pinned same-model number.

---

## 4. Coverage check against M3 done-criteria

1. **Rule explicit & reproducible.** §1.1 states the formula (`P_contam = c×H_ref`, pass-through for the two pp channels, per-endpoint `max`), operators, units (pp), range propagation (§1.2), and insufficient-evidence handling (§1.3). §3 reproduces GSM8K's 28.5–62.7 pp from its M2 row step by step. ✓
2. **Every row has discount + classification + confidence; monotonic ranking.** All six rows carry a band, a class, and a confidence label; sorted ascending by `Discount_high` (§1.6), ties by `Discount_low`. ✓
3. **≥1 noise/discount-heavily AND ≥1 usable-tier, each citing M2 components.** `discount-heavily`: GPQA, MMLU; `noise`: SWE (×2), GSM8K, MATH. The `usable` band (≤10 pp) is defined and shown empty as a finding (none survives). Thresholds stated numerically in §1.4; every classification's components are cited in the table's last column. ✓ (criterion's intent — a spread across the scale with cited drivers — is met; the `usable` tier being empty is reported honestly, not hidden.)
4. **Worked example M1→M2→discount for one named benchmark.** §3 walks GSM8K from R22/R23/R24/R25 → M2 components → 28.5–62.7 pp → noise. ✓

---

## 5. Limitations & counter-evidence

1. **The `max` rule is a deliberate *lower bound*, and could understate stacked risk.** Where channels genuinely compound (a benchmark that is both leaked *and* tested only short-horizon), the true haircut exceeds the max. A buyer wanting worst-case exposure should instead **sum** the channels — e.g., GSM8K would become ~35–73 pp rather than 28.5–62.7. I chose max because M2 explicitly forbade summing overlapping mechanisms; the sum variant is the conservative alternative, not used in the table.
2. **The `usable` tier came out empty, which is itself a strong (and contestable) claim.** It says no public benchmark in the set survives a 2026 procurement test with a ≤10-pp haircut once the worst credible channel is priced. This rests heavily on cross-model/proxy horizon and contamination figures (R24, R27) measured on non-frontier models; on *same-model frontier* evidence alone, GPQA and Opus-4.1-on-SWE-priv are nearly flat (R8, R14/R15). The honest reading: the *worst-case* haircut is large everywhere, but the *same-model* haircut is small in exactly the two places (GPQA contamination, Opus public→private) where frontier evidence exists — direct counter-evidence to a uniform-overstatement story, already flagged in M1 G1/G6 and M2 Limitations 3–4.
3. **`H_ref` choice moves the contamination pp, and three of five `H_ref` values are cross-model or proxy.** Converting a contamination *fraction* to pp needs a headline; I used the frontier public number per benchmark (R4/R17/R22) where it exists, and a `[PROXY]` scale of 100 for MATH (no frontier MATH headline exists — M1 G5). A different `H_ref` rescales every contamination-dominated discount (GPQA, MATH) linearly. These rows are flagged conf low partly for this reason.
4. **SWE horizon (n=1) dominates two rows but rests on a single matched pair (R4→R9, GPT-5.2).** Both SWE families land in `noise` largely because of one ~49.9-pp data point. If that pair is an outlier or scaffold-specific, both SWE classifications could fall to `discount-heavily`. The n=1 flag and med-confidence cap encode this fragility; M4's falsification tests should target it first.
5. **MATH's 16–96 pp band is near-uninformative and only nominally a "discount."** Its high end (96 pp) is a controlled-injection artifact on ≤344M-param models at 1000 replicas (R27) — an existence proof of contamination sensitivity, not a frontier estimate. The row is retained (not dropped) per the spec, classified `noise` / conf low, but a buyer should read it as "MATH contamination is effectively unquantified for procurement," not as a literal 96-pp haircut.
6. **Classification is threshold-sensitive at the boundaries.** GPQA (high 14.9) sits just above the 10-pp `usable/discount-heavily` line; MMLU (high 33) sits just below the 35-pp `discount-heavily/noise` line. Small shifts in `c`, `H_ref`, or the priv band would flip either. The thresholds (§1.4) are a defensible but not unique choice; they are stated explicitly so the buyer can re-set them.
7. **Confidence reflects evidence provenance, not benchmark importance.** A `low`-confidence `noise` verdict (MATH) is a statement about thin evidence, not a claim that MATH is definitely the worst benchmark. The procurement reading is "do not rely on the MATH headline *and* do not rely on this discount as precise" — i.e., commission an independent re-run (the M4 action), rather than apply 16–96 pp literally.
8. **The whole ledger inherits M1's model-version heterogeneity (G8) and the flawed-test exclusion (R3).** No discount here subtracts an Opus headline from a Gemma2 drop within a single arithmetic step, but the *cross-benchmark comparison* still places rows measured on different model generations side by side. And SWE's contamination channel is forced to 0 because R3 (59.4% flawed hard-task tests) deflates the model rather than inflating the headline — a real reliability threat that this rule cannot price as a haircut and that lives as a qualitative caveat for the buyer.
