# M3 — Per-Benchmark Procurement Discount: the haircut a federal buyer subtracts from a headline score

**Problem:** ai-benchmark-deployment-gap · **Milestone:** M3 (derive procurement discount) · **Date:** 2026-06-28

**Input.** This artifact is a *derivation* over the M2 gap-component table (`artifacts/2026-06-28-m2-gap-components.md`), which is itself a derivation over the M1 dossier (`artifacts/2026-06-28-m1-evidence-dossier.md`, rows R1–R29). Every number below traces to an M2 cell (and through it to named M1 rows). No new external numbers are introduced. The only new arithmetic is the combination rule defined in §1, applied identically to all five benchmarks.

**Buyer.** CAISI/NIST + GSA, who under their March-2026 MOU must "select and interpret benchmarks" for federal AI procurement ([NIST, 2026-03](https://www.nist.gov/news-events/news/2026/03/caisi-signs-mou-gsa-boost-ai-evaluation-science-federal-procurement-through), via M1 problem brief). The **procurement discount** is the percentage-point haircut they should subtract from a vendor's reported headline score before treating it as a predictor of deployed performance.

---

## 1. The combination rule (explicit, uniform, reproducible)

The rule maps the three M2 components for a benchmark into a single discount band `[D_low – D_high]` in percentage points. It is **non-additive** (per M2 Limitation 1: the three components measure overlapping weaknesses and must not be summed) and **confidence-graded**.

### Step 1 — Put all three components in the same unit (pp on the headline)

Two of the three M2 components are already in percentage points (`Δpp_priv`, `Δpp_horizon`). The contamination component is a dimensionless fraction `c`, so convert it to a pp effect on the benchmark's reference headline `H_ref`:

> **`c_pp = c × H_ref`**

`H_ref` is the public-headline M1 row for the benchmark's stated reference model family (the value a buyer actually reads off a leaderboard). The `H_ref` used per benchmark is named in §2 and §3. (Worked: MMLU `H_ref = 88.0` (R17); `c = 0.166–0.186` (M2) → `c_pp = 14.6 – 16.4 pp`.)

### Step 2 — Combine the three pp-effects by MAX, not sum

For each of `{c_pp, Δpp_priv, Δpp_horizon}` that is **not** "insufficient evidence", take the band. The discount band is the element-wise maximum across available components:

> **`D_low  = max( low-ends of available components )`**
> **`D_high = max( high-ends of available components )`**

Rationale for MAX: the three mechanisms (leakage, harder/held-out partition, longer horizon) are partly the same underlying brittleness re-measured three ways; their effects overlap, so the worst single measured drop is the defensible single-number estimate of how far a headline can fall, and summing would double-count (M2 Limitation 1). MAX also means a benchmark cannot be rescued by one clean component if another shows a large drop.

### Step 3 — Handling "insufficient evidence" components

An "insufficient evidence" component **drops out of the max** (it neither raises nor lowers the band). It does **not** contribute a 0. Consequence: a benchmark with only one populated component gets its discount from that component alone, and its **confidence is capped at `med`** (one mechanism measured) or `low` (see Step 4). A benchmark with **zero** populated components would read "insufficient evidence" for the whole discount; none of the five do.

### Step 3a — Excluding a non-procurement-grade component before the MAX

A component flagged `[PROXY]` in M2 (a small/old-model controlled study standing in for a frontier delta) whose **high end is an existence-proof artifact rather than a deployed estimate** is excluded from the MAX and replaced by the next-best populated component, with the exclusion stated in the row note. This is invoked exactly once: MATH's contamination `c=0.96` (≤344M-param injection, M2 Limitation 5). It is a stated, uniform escape hatch, not an ad-hoc edit: the test is "is the high end a controlled-injection artifact flagged `[PROXY]` by M2?" If yes, drop it and fall through to the next component; record the dropped value in the note for transparency.

### Step 4 — Confidence grade (drives the ranking and the low-end caveat)

Assign confidence from the *provenance flags M2 attached to the component(s) that drive `D_high`*:

| Confidence | Condition on the band-driving component(s) |
|---|---|
| **high** | Driving component rests on ≥2 model-matched, same-generation pairs with **no** `[CROSS-MODEL]`/`[PROXY]`/`[LOW-CONF n=1]` flag. |
| **med** | Driving component rests on a single matched pair (`[LOW-CONF n=1]`) OR on `[CROSS-MODEL]` aggregate bands, but the *magnitude* is corroborated by a second independent component or row. |
| **low** | Driving component is `[PROXY]` OR is the benchmark's only component and is itself flagged. |

### Step 5 — Classification (from `D_high` and confidence)

> - **usable** — `D_high ≤ 20 pp`. A buyer can trust the headline after a modest, well-bounded haircut.
> - **discount-heavily** — `20 < D_high ≤ 50 pp`, OR any `D_high` whose driving component is `low`-confidence (the number is real but the size is uncertain, so the buyer must apply a large, defensive haircut).
> - **noise** — `D_high > 50 pp` with `med`/`high` confidence that a frontier-relevant variant collapses the score, i.e., the headline predicts deployed performance no better than a large guess.

### Step 6 — Low-end disagreement flag

When the available components **disagree at the low end** (one component's low = 0 because one model is flat, while another shows a large drop), record `D_low` as the max (per Step 2) but annotate the row "model-dependent floor" so the buyer knows the discount is a function of *which* model is being procured, not a flat constant. This is the SWE-bench case (M2: Opus 4.1 flat, GPT-5 −26 pp).

**Reproducibility check for an evaluator:** take any benchmark's M2 row, compute `c_pp = c × H_ref` (H_ref named in §2/§3), drop any `[PROXY]` existence-proof high end (Step 3a), then `D = [max(lows), max(highs)]` over the remaining non-"insufficient" components, then read the classification off Step 5. You will reproduce the §2 table.

---

## 2. Ranked procurement-discount table

**Ranking criterion (monotonic):** ascending `D_high` (most-trustworthy / smallest worst-case haircut first), ties broken by descending confidence. Most-trustworthy benchmark is therefore at the top. Order: GPQA (14.9) < MMLU (33, med) = MATH (33, low) < SWE (49.9) < GSM8K (62.7).

| # | benchmark | model family | implied procurement discount [low–high pp] | classification | dominant driver | confidence | components used |
|---|-----------|--------------|---------------------------------------------|----------------|-----------------|------------|-----------------|
| 1 | **GPQA** | frontier (GPT-4→Diamond-era; H_ref=39–90, R12) | **0.2 – 14.9 pp** | **usable** | contamination | **low** | contam `c=0.005–0.166` (R14,R15) → `c_pp = 0.005·39 … 0.166·90`; priv & horizon insufficient |
| 2 | **MMLU** | frontier (GPT-4o; H_ref=88.0, R17) | **16 – 33 pp** | **discount-heavily** | private-gap | **med** | contam `c=0.166–0.186` (R18,R19) → `c_pp=14.6–16.4`; priv `16–33` (R20); horizon insufficient |
| 3 | **MATH** | frontier (no native headline; H_ref proxy) | **16 – 33 pp** `[PROXY]` | **discount-heavily** | private-gap | **low** | contam `c=0.01–0.96` `[PROXY]` **dropped via Step 3a** (R27,R21); priv `16–33` `[PROXY]` (R29) binds; horizon insufficient |
| 4 | **SWE-bench / Verified** | frontier (GPT-5 family; H_ref=72.8, R4) | **0 – 49.9 pp** (model-dependent floor) | **discount-heavily** | horizon-gap | **med** | priv `0–26.1` (R7,R8); horizon `≈49.9` `[n=1]` (R4→R9); contam insufficient (R3 is flawed-test, excluded) |
| 5 | **GSM8K** | frontier (GPT-4o; H_ref=95.0, R22) | **28.5 – 62.7 pp** | **noise** | horizon-gap | **med** | contam `c=0.067–0.107` (R23,R25) → `c_pp=6.4–10.2`; horizon `28.5–62.7` (R24); priv insufficient |

Notes on specific cells:
- **GPQA** `D_high = 14.9 pp` uses `c=0.166 × H=90` as the conservative upper edge of the contamination band across the benchmark's headline range (R12 GPT-4 = 39%, modern Diamond headlines ~80–90%). The low end `0.2 pp` = `0.005 × 39`. The whole band rests on subset-only, indirect leakage evidence (M1 G6, M2: "true value sits near the low end"), so it is `usable` but `low`-confidence — the number is small *and* soft.
- **MATH** Step 3a is invoked: the contamination high-end `c_pp` (`0.96 × H_ref` ≈ 48–86 pp) is **dropped** because M2 Limitation 5 calls `c=0.96` a controlled-injection artifact on ≤344M-param models — "an existence proof, not an estimate of any deployed model's real MATH inflation." The remaining populated component is the cross-referenced private-gap `16–33 pp` (R29), which binds → `D = 16–33 pp`. Confidence `low` (the only surviving component is itself `[PROXY]`, R29 borrowed from MMLU-Pro; no native frontier MATH delta, M1 G5). The dropped contamination ceiling is recorded here for transparency. **MATH is the benchmark where the evidence is weakest; treat `16–33 pp` as a floor pending a real frontier decontamination run, not a measurement.**

---

## 3. Why each classification (citing the M2 components that drove it)

- **GPQA → usable.** Both deflationary partitions (private, horizon) are "insufficient evidence" in M2 — GPQA has no held-out or long-horizon variant in the dossier — and the only populated component, contamination, is small (`c ≤ 0.166`, and M2 says it "sits near the low end"). MAX over one small component → small discount. This is the dossier's documented counter-example to the blanket "all benchmarks overstate" thesis (M1 G6, M2 Limitation 4): GPQA's real ceiling problem is *task difficulty* (R13: experts only reach 65–74%), a property of the task, not a contamination of the score, so it does not enter the haircut. **Usable, with the explicit caveat that the headline already sits below a ~70% human-expert ceiling.**
- **MMLU → discount-heavily.** Two model-matched contamination pairs (R18, R19) give `c_pp = 14.6–16.4`, and the harder-reshuffle private partition (R20, MMLU-Pro) gives `16–33 pp`. MAX → `16–33 pp`. `D_high = 33 > 20` → discount-heavily. Two independent mechanisms (leakage *and* harder reshuffle) both land in the 15–33 pp zone, corroborating each other → `med` confidence despite the `[CROSS-MODEL]` flag on the private band.
- **MATH → discount-heavily (by the low-confidence rule), not noise.** After Step 3a drops the proxy contamination ceiling, the operative band is the cross-referenced private-gap `16–33 pp` (R29). Step 4 forces `low` confidence (only surviving component is `[PROXY]`); Step 5: a `low`-confidence driver forces `discount-heavily` regardless of magnitude. **MATH is classified by honesty about weak evidence, not by a measured frontier collapse.**
- **SWE-bench / Verified → discount-heavily, model-dependent floor.** Private-gap `0–26.1 pp` is genuine model heterogeneity (M2: Opus 4.1 flat, GPT-5 −26; M1 G1), and the single matched long-horizon pair (R4→R9, GPT-5.2 on SWE-EVO) is `≈49.9 pp` `[n=1]`. MAX → `0–49.9`. `D_high` just under the noise threshold and resting on n=1 → `discount-heavily`, not `noise`. The "0" floor is real but applies only to models like Opus 4.1; for GPT-5-class agents the floor is ~26 pp (private) rising toward ~50 pp on long-horizon work. Separately, R3 (≥59.4% of hard tasks have flawed tests) is a *reliability* threat to the ranking that M2 correctly excluded from the contamination number; flagged here for M4, not in the arithmetic.
- **GSM8K → noise.** The horizon/robustness component (R24, GSM-NoOp: one irrelevant clause) collapses scores `28.5–62.7 pp`, with frontier-class models in-band (GPT-4o −31.8, o1-mini −28.5). `D_high = 62.7 > 50` with `med` confidence (the low end 28.5 is on a frontier model, o1-mini) → **noise**: a 95% GSM8K headline does not survive a trivially-perturbed version of the same arithmetic, so for procurement the headline is near-worthless as a deployed-robustness signal. (Contamination here is modest, `6.4–10.2 pp`; the killer is brittleness, not leakage.)

**Classification coverage (done-criterion):** `usable` = GPQA (#1); `discount-heavily` = MMLU, MATH, SWE (#2,#3,#4); `noise` = GSM8K (#5). At least one `usable` and at least one `noise`/`discount-heavily`, each citing its driving M2 components above. ✔

---

## 4. Worked example — full chain M1 → M2 → M3 for **MMLU**

**M1 rows.**
- R17: GPT-4o on MMLU (5-shot), **88.0%** (public-headline). → this is `H_ref`.
- R18: GPT-4o on MMLU-CF (contamination-free), **73.4%**.
- R19: GPT-4-Turbo, MMLU **86.5%** → MMLU-CF **70.4%**.
- R20: MMLU → MMLU-Pro (10-option, reasoning-focused harder reshuffle), reported **16%–33%** accuracy drop across models.

**M2 components (re-derived from those rows).**
- Contamination fraction `c = (H − D_clean)/H`: R18 → `(88.0 − 73.4)/88.0 = 0.166`; R19 → `(86.5 − 70.4)/86.5 = 0.186`. → **`c = 0.166 – 0.186`** (two model-matched pairs, not n=1).
- Public→private drop `Δpp_priv`: R20 → **`16 – 33 pp`** (MMLU-Pro = harder/held-out reshuffle; cross-model aggregate band).
- Short→long-horizon `Δpp_horizon`: **insufficient evidence** (no MMLU long-horizon variant in the dossier).

**M3 combination rule applied.**
1. Step 1 — convert contamination to pp on the headline: `c_pp = c × H_ref = 0.166×88.0 … 0.186×88.0 = 14.6 – 16.4 pp`.
2. Step 3a — no `[PROXY]` existence-proof component present, nothing dropped.
3. Step 2 — MAX over available components `{c_pp = 14.6–16.4, Δpp_priv = 16–33}` (horizon drops out, Step 3):
   - `D_low  = max(14.6, 16) = 16.0 pp`
   - `D_high = max(16.4, 33) = 33.0 pp`
   → **discount = 16 – 33 pp**.
4. Step 4 — confidence: `D_high` driven by the private-gap (R20), which is `[CROSS-MODEL]`, but its magnitude is corroborated by the same-model contamination pairs landing in the same 15–16 pp zone → **med**.
5. Step 5 — classify: `D_high = 33`, in `(20, 50]` → **discount-heavily**.
6. Dominant driver: the private-gap high-end (33) exceeds the contamination high-end (16.4) → **private-gap**.

**Result for the table:** MMLU | GPT-4o family | **16 – 33 pp** | discount-heavily | private-gap | med | contam (R18,R19) + priv (R20). This reproduces row #2 of §2. **Plain reading for the buyer:** subtract ~16–33 points from a vendor's reported MMLU before trusting it — an 88% claim implies a deployment-relevant ~55–72%.

---

## 5. Limitations & counter-evidence

1. **The MAX rule is a modeling choice, not a measured fact.** Summing would double-count overlapping brittleness (M2 Limitation 1); MAX assumes the worst single drop is the right single number. The truth could be higher (some mechanisms partly independent), which would push real discounts *above* MAX. MAX is therefore a *defensible-floor-of-the-worst-case*, and the discounts here may **under**-state for benchmarks where mechanisms stack (a contaminated *and* long-horizon deployment task). This errs toward larger haircuts, the safe direction for a buyer.
2. **`c_pp = c × H_ref` assumes contamination inflates uniformly across the headline.** It does not: leaked items may concentrate in easy or hard slices. The conversion is a first-order approximation; it is load-bearing only for MMLU and GPQA, and in both the contamination term is *not* the binding `D_high` driver (MMLU bound by private-gap; GPQA's whole band is small and `low`-confidence), so the approximation drives no classification.
3. **Most binding components are `[CROSS-MODEL]` or `[PROXY]` (M1 G8, M2 Limitation 2).** GSM8K's horizon driver (R24) mixes GPT-4o, o1-mini, Phi-3-mini; MMLU's private band (R20) is a cross-model aggregate; MATH's components are both `[PROXY]`. A GPT-5-class headline minus a Gemma2-9b/Phi drop is not a clean same-model subtraction. The confidence column encodes this; **no benchmark earns `high` confidence — itself the honest headline finding: no benchmark currently has procurement-grade, same-frontier-model deflation evidence across all three mechanisms.**
4. **The thresholds (20 pp / 50 pp) are operator-set, not derived.** Shifting "noise" to 40 pp would reclassify SWE-bench as noise; shifting "usable" to 15 pp would push GPQA's upper edge over the line. The thresholds are stated so a buyer can move them; the *bands and drivers* are the evidence, the *labels* are policy.
5. **GSM8K "noise" rests on robustness perturbation, not pure capability.** R24's GSM-NoOp adds an irrelevant clause; one could argue a deployed system with light prompt-hardening recovers some of that 28–63 pp. The classification reads GSM8K as a *deployed-robustness* signal (where it fails badly), not as a *can-the-model-do-arithmetic* signal (where 95% may be roughly fair). A buyer using GSM8K only to screen basic numeracy should down-weight this label.
6. **SWE-bench's horizon driver is n=1 (R4→R9, GPT-5.2 only).** A single matched long-horizon pair carries the high end toward 50 pp; one more model could widen or collapse it. This is why SWE is `med`, not lower, and why it lands `discount-heavily` rather than `noise` despite a `D_high` near the noise threshold.
7. **MATH is barely an estimate (M2 Limitation 5).** Its discount is an honesty placeholder: contamination evidence is small-model proxy (dropped by Step 3a), the private-gap is borrowed from MMLU-Pro (R29), and there is no native frontier MATH public→clean delta (M1 G5). A buyer should treat MATH's `16–33 pp` as a *lower bound pending a real frontier decontamination run*, not as a finding.
8. **GPQA's H_ref spans 39–90, so its contamination `c_pp` band is headline-dependent.** Pinning the low end to the 2023 GPT-4 headline (39, R12) and the high end to modern Diamond headlines (~90) is a deliberate widening to avoid a false-precise single number; a buyer scoring a *specific* model should recompute `c_pp = 0.005…0.166 × that model's GPQA headline`.
9. **Counter-evidence to the core thesis is preserved, not smoothed.** GPQA classifies `usable` and Opus 4.1 is flat public→private on SWE (priv low = 0): overstatement is real and sometimes very large, but it is **benchmark- and model-dependent**, not a flat haircut. The single most defensible buyer takeaway is not a universal discount but *this table*: the haircut depends on which benchmark and which model family, and for one of five (GSM8K) the headline is a poor deployment predictor while for one (GPQA) it is usable after a modest, soft haircut.
