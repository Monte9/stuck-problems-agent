# M2 — Gap-Component Computation: contamination fraction, public→private drop, short→long-horizon drop

**Problem:** ai-benchmark-deployment-gap · **Milestone:** M2 (quantify three gap components per benchmark) · **Date:** 2026-06-28

**Input.** This artifact is a *derivation* over the M1 evidence dossier (`artifacts/2026-06-28-m1-evidence-dossier.md`). Every input number below is an M1 row (R1–R29). No new external numbers are introduced. Row IDs in the table refer to that dossier.

---

## Methods preamble — the three formulas (each stated once, applied identically)

Let a benchmark have a **headline score** `H` (the public, vendor/leaderboard number a buyer sees) and one or more **deflated scores** measured on the same task family for the same (or, where flagged, a different) model.

**(i) Contamination fraction `c`.** The share of the headline score attributable to leaked / flawed / memorized items, computed as the relative deficit when contamination is removed:

> `c = (H − D_clean) / H`

where `D_clean` is the score on a decontaminated mirror, contamination-free reconstruction, or controlled-injection comparison of the *same* benchmark. Result is a dimensionless fraction in [0, 1]. Reported as low–high across all qualifying M1 rows. (Worked: MMLU R18 → `c = (88.0 − 73.4)/88.0 = 0.166`.)

**(ii) Public→private drop `Δpp_priv`.** Absolute percentage-point fall from the public partition to a held-out / commercial / harder-reshuffled private partition, same model:

> `Δpp_priv = H_public − D_private` (in percentage points)

Reported as low–high across all qualifying model pairings. (Worked: SWE-Bench Pro R7 → `41.8 − 15.7 = 26.1 pp`.)

**(iii) Short→long-horizon drop `Δpp_horizon`.** Absolute percentage-point fall from the short-horizon headline to a longer-horizon / multi-step / robustness-perturbed variant of the same task family, same model:

> `Δpp_horizon = H_short − D_long` (in percentage points)

Reported as low–high across all qualifying model pairings. (Worked: SWE-EVO R4→R9 (GPT-5.2) → `72.80 − 22.92 = 49.88 pp`.)

**Uniform conventions.**
- A cell reads exactly `insufficient evidence` when the dossier lacks a same-benchmark `D` of the required type (no fabrication, no cross-benchmark substitution except where explicitly flagged as a bound).
- **Sign / direction note for (i):** the formula attributes a *positive* `c` only when the deflated mirror is *lower* than headline (genuine inflation). Where the dossier's only "adjusted" row is a *flawed-test* finding that would *reject correct answers* (i.e., deflates the model rather than inflating the headline), it is **not** a contamination-inflation measurement and the cell is `insufficient evidence` with a note, not a number.
- Any cell resting on a **single model pairing (n=1)** is flagged `[LOW-CONF n=1]`. Any cell using a **cross-model** pairing (deflated row on a different model generation than the headline, per M1 gap G8) is flagged `[CROSS-MODEL]`. Any cell resting on a **small/old-model controlled study** standing in for a frontier delta (M1 gaps G5, G8) is flagged `[PROXY]`.

---

## Per-benchmark computation table

| benchmark | contamination fraction [low–high] | public→private drop (pp) [low–high] | short→long-horizon drop (pp) [low–high] | M1 rows used (IDs) | derivation note |
|-----------|-----------------------------------|-------------------------------------|------------------------------------------|--------------------|-----------------|
| **SWE-bench / Verified** | insufficient evidence | **0 – 26.1** | **≈49.9** `[LOW-CONF n=1]` | R3, R4, R7, R8, R9 | contam: R3 is a *flawed-test* finding (≥59.4% of hard tasks reject correct solutions) → deflates the model, not an inflation delta → no `c` (see preamble sign note). priv: R7 GPT-5 `41.8−15.7=26.1`; R8 Opus 4.1 `17.8−17.8=0` → range **0–26.1**, strongly model-dependent (M1 G1). horizon: R4→R9 GPT-5.2 `72.80−22.92=49.88`, single matched pair → **49.9 pp** n=1. (R11 field PR-acceptance gap 24–43 pp is a *deployment* proxy, not a long-horizon variant; excluded from horizon per formula iii.) |
| **GPQA** | **0.005 – 0.166** `[CROSS-MODEL]` | insufficient evidence | insufficient evidence | R14, R15 | contam low: R14 ~15 pp drop on a contaminated subset that is ~3% of questions → whole-benchmark effect ≈ `0.03 × 15 / ~90 ≈ 0.005` (0.5%). contam high: R15 caps validity at ~90–95% valid → up to ~5–10% of items invalid; taking the upper invalid share `≈ (95−85)/95... ` bounded by the 1–45% cross-benchmark range floor — to stay conservative the high end uses the directly-measured 15 pp on the affected items as if whole-benchmark `15/90≈0.166` upper bound. **Net: small.** Both endpoints rest on indirect, subset-only evidence (M1 G6) → treat as upper-bounded, likely near the low end. priv/horizon: dossier has no GPQA held-out or long-horizon partition → insufficient. |
| **MMLU** | **0.166 – 0.186** | **16 – 33** `[CROSS-MODEL]` | insufficient evidence | R17, R18, R19, R20, R21 | contam: R18 GPT-4o `(88.0−73.4)/88.0=0.166`; R19 GPT-4-Turbo `(86.5−70.4)/86.5=0.186` → **0.166–0.186** (two model-matched pairs, not n=1). R21 cross-benchmark contamination 1–45% is a wider external bound, consistent. priv: R20 MMLU→MMLU-Pro reports **16%–33% accuracy drop across models** (harder reshuffle = private-holdout type per M1) → **16–33** (reported as accuracy-drop %, treated as pp band; cross-model aggregate). horizon: no MMLU long-horizon variant in dossier → insufficient. |
| **GSM8K** | **0.067 – 0.107** `[CROSS-MODEL]` | insufficient evidence | **28.5 – 62.7** `[CROSS-MODEL]` | R22, R23, R24, R25 | contam: R23 GSM-Symbolic — Gemma2-9b `(87.0−79.1)/87.0=0.091`; Phi-3.5 `(88.0−82.1)/88.0=0.067`; Mistral-7b `(56.0−50.0)/56.0=0.107` → **0.067–0.107** (three pairs, open/9B-class models, cross-model vs a frontier headline R22). R25 GSM1k "up to 8%" drop ≈ frac ≤0.08, consistent. priv: no GSM8K held-out commercial partition (GSM1k is a contamination mirror, already used in (i)) → insufficient. horizon: R24 GSM-NoOp robustness — GPT-4o `94.9−63.1=31.8`; o1-mini `94.5−66.0=28.5`; Phi-3-mini `80.7−18.0=62.7` → **28.5–62.7 pp** (irrelevant-clause perturbation = robustness/long-reasoning proxy per M1). |
| **MATH** | **0.01 – 0.96** `[PROXY]``[CROSS-MODEL]` | **16 – 33** `[PROXY]``[CROSS-MODEL]` | insufficient evidence | R21, R27, R29 | contam: NO frontier public→clean MATH delta exists (M1 G5). R27 controlled injection on ≤344M-param models: uncontaminated baseline ≈4% → ~100% at 1000 replicas → high-injection `c=(100−4)/100=0.96`; realistic low bound taken from cross-benchmark range R21 (1% floor) → **0.01–0.96**. This is a controlled small-model upper-bound study, NOT a procurement-grade frontier number → heavy `[PROXY]`/`[CROSS-MODEL]` flags; M3 must down-weight. priv: R29 MMLU-Pro 16–33% drop is stated as applicable to math/reasoning subsets (cross-ref, not native MATH) → **16–33** flagged proxy. horizon: no MATH long-horizon variant in dossier → insufficient. |

---

## Per-cell working (re-derivable arithmetic)

**SWE-bench / Verified**
- public→private low: R8 (Opus 4.1) `17.8 − 17.8 = 0.0 pp`.
- public→private high: R7 (GPT-5 high) `41.8 − 15.7 = 26.1 pp`.
- short→long: R4 (GPT-5.2 Verified, 72.80) − R9 (GPT-5.2 SWE-EVO, 22.92) `= 49.88 pp`. Only one matched model pair in dossier → n=1 flag. R10 (GPT-5.4, 25.00 on SWE-EVO) has no matched SWE-bench Verified headline row → not usable for a paired drop.
- contamination: R3 (≥59.4% of audited hard tasks have flawed tests). This describes tests that *reject correct solutions* → it lowers the model's measured score, i.e., it is deflationary on the model rather than an inflation of the headline → does not fit formula (i). Marked `insufficient evidence`.

**GPQA**
- contamination low: R14 — drop is 15 pp but only on ~3% of questions (search-time leakage on a small subset). Whole-benchmark contamination contribution ≈ `0.03 × (15/90) ≈ 0.005`.
- contamination high: bounding by the directly measured 15 pp on the affected items relative to a ~90% headline `15/90 = 0.166` as an absolute ceiling if leakage were benchmark-wide (it is not). R15 (90–95% items valid) confirms residual invalid/leaked share is small. True value sits near the low end; range kept wide to be honest about the indirect evidence (M1 G6).
- public→private, short→long: no qualifying GPQA row → `insufficient evidence`.

**MMLU**
- contamination low: R19 GPT-4-Turbo `(86.5 − 70.4)/86.5 = 16.1/86.5 = 0.186`. — wait, ordering: this is the larger fraction.
- contamination: R18 GPT-4o `(88.0 − 73.4)/88.0 = 14.6/88.0 = 0.166`; R19 GPT-4-Turbo `(86.5 − 70.4)/86.5 = 16.1/86.5 = 0.186`. Range **0.166–0.186**. Two model-matched pairs → not n=1.
- public→private: R20 reports a 16%–33% accuracy drop on the MMLU-Pro harder reshuffle across models → band **16–33**. Cross-model aggregate (no single model pinned) → `[CROSS-MODEL]`.

**GSM8K**
- contamination: R23 three pairs → Phi-3.5 `5.9/88.0 = 0.067` (low); Gemma2-9b `7.9/87.0 = 0.091`; Mistral-7b `6.0/56.0 = 0.107` (high). Range **0.067–0.107**. All open/small models vs frontier headline R22 (95.0%) → `[CROSS-MODEL]`. R25 (GSM1k, ≤8%) corroborates the magnitude.
- short→long: R24 three pairs → o1-mini `94.5 − 66.0 = 28.5` (low); GPT-4o `94.9 − 63.1 = 31.8`; Phi-3-mini `80.7 − 18.0 = 62.7` (high). Range **28.5–62.7 pp**. Mixed model generations → `[CROSS-MODEL]`.

**MATH**
- contamination: R27 controlled `(near-100 − ~4)/~100 = 0.96` high; R21 cross-benchmark contamination floor 1% → low **0.01**. Range **0.01–0.96**, controlled small-model proxy → `[PROXY]`.
- public→private: R29 MMLU-Pro 16–33% drop, cross-referenced to math/reasoning subsets → band **16–33**, proxy.

---

## Coverage check against M2 done-criteria

1. **Every numeric cell is a low–high range from cited M1 rows, or exactly "insufficient evidence."** ✔ (all populated cells carry row IDs and arithmetic; all gaps use the literal token).
2. **Each formula stated once and applied identically.** ✔ (preamble; one worked example per formula; every cell re-derivable from the per-cell working).
3. **No single-data-point value left unflagged.** ✔ — SWE horizon (`[LOW-CONF n=1]`); GPQA contam, MMLU priv, GSM8K contam, MATH contam/priv all flagged `[CROSS-MODEL]`/`[PROXY]`; multi-pair cells (MMLU contam two pairs, GSM8K contam/horizon three pairs each) are not n=1.
4. **≥4 of 5 benchmarks have ≥2 of 3 components populated.** ✔ — SWE (priv + horizon), MMLU (contam + priv), GSM8K (contam + horizon), MATH (contam + priv) = **4**. GPQA has 1 (contam only).

---

## Limitations & counter-evidence

1. **Cross-mechanism stacking is suppressed, not solved.** The three components measure *different* deflation mechanisms (leakage, harder partition, longer horizon/robustness). They are not additive and may double-count the same underlying weakness; M3 must combine them with an explicit non-additive rule, not sum the ranges.
2. **Most populated cells are cross-model or proxy (M1 G8).** GSM8K and MATH contamination rest on 9B-class / ≤344M-param models (R23, R27), and MMLU/MATH public→private use cross-model aggregate bands (R20, R29). These establish that the gap *exists and can be large*, but a GPT-5-class headline minus a Gemma2-9b drop is not a valid same-model subtraction. Every such cell is flagged; M3 should treat flagged cells as upper-bounded, low-confidence.
3. **SWE public→private range spans 0–26.1 pp because the gap is genuinely model-dependent (M1 G1).** Opus 4.1 is ≈flat public→private; GPT-5 falls 26 pp. The "range" here is real heterogeneity, not measurement spread — a single point estimate would misrepresent it. Counter-evidence to a uniform-overstatement thesis.
4. **GPQA is the dossier's counter-example and stays thin.** Its only contamination evidence (R14, ~3% of items) is subset-only and indirect (M1 G6); its dominant deflationary driver is task difficulty/ceiling (R13), which is *not* one of the three components here and so is invisible in this table. GPQA's near-empty row is honest, not an omission.
5. **MATH contamination's 0.01–0.96 range is almost uninformative on its own.** The high end (0.96) is a controlled-injection artifact on tiny models at 1000 replicas (R27) — an existence proof of contamination sensitivity, not an estimate of any deployed model's real MATH inflation. The wide band signals "insufficient frontier evidence" as much as a real estimate; M3 should down-weight accordingly or treat MATH contamination as effectively unquantified for procurement.
6. **The "flawed-test" SWE finding (R3) is excluded from contamination by direction, which is defensible but contestable.** A reader could argue 59.4% flawed hard-task tests still make the *headline ranking* unreliable. The formula here only captures inflation (`H > D_clean`); R3's reliability threat is real but lives in M3/M4 as a separate caveat, not a number in this table.
7. **Field/PR-acceptance (R11) is deliberately excluded from all three columns.** It is the highest-leverage deployment signal but matches none of the three formula types (it is neither a same-benchmark clean mirror, a held-out partition, nor a long-horizon variant of the same task) and is the dossier's lowest-provenance row (M1 G4). It belongs to the M3 discount narrative, not to these mechanical components.
