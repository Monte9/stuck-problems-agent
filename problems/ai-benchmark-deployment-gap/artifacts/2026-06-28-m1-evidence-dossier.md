# M1 — Evidence Dossier: deployment-validity fragments per benchmark

**Problem:** ai-benchmark-deployment-gap · **Milestone:** M1 (evidence dossier) · **Date:** 2026-06-28

**Purpose.** Collect every reachable, primary-source-verified data point bearing on how much a public AI benchmark's headline score overstates real deployed performance, keyed by stable row ID for downstream milestones (M2 quantifies gap components, M3 derives the procurement discount). This is raw collection, not yet analysis — derivations belong to M2/M3.

**Verification method.** Every URL below was fetched or searched against during this run (2026-06-28) via WebFetch/WebSearch; exact numbers and dates were read from the primary source (arXiv abstract/HTML, vendor blog, or named research page). Where the problem brief's cited number could not be confirmed against its cited source, the row carries the *verified* number and the discrepancy is logged in "Gaps & contested points." No URL is included that did not resolve during this run.

**Metric-type legend.** `public-headline` = vendor/leaderboard score on the public benchmark · `private-holdout` = score on a held-out/commercial/unseen partition · `long-horizon` = score on a longer-horizon variant of the same task family · `contamination-adjusted` = score after removing/decontaminating leaked items or on a contamination-controlled mirror · `field/PR-acceptance` = real-deployment acceptance proxy.

**How "distinct benchmark" is counted.** Five core benchmark families each carry ≥3 rows: (1) SWE-bench / SWE-bench Verified, (2) GPQA, (3) MMLU, (4) GSM8K, (5) MATH. Two private/long-horizon variants of the SWE family — **SWE-Bench Pro** and **SWE-EVO** — are listed as their own labeled blocks because they are the deflationary evidence *for* SWE-bench Verified; their rows are also counted under the SWE-bench family for the ≥3-rows test. The ≥5-with-≥3-rows criterion is met by the five core families independently of how the SWE variants are bucketed.

---

## Evidence table

### Benchmark family 1 — SWE-bench / SWE-bench Verified (coding)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R1 | SWE-bench (original) | GPT-4o (best scaffold) | public-headline | 16% resolved | https://openai.com/index/introducing-swe-bench-verified/ | vendor (OpenAI) | 2024-08-13 |
| R2 | SWE-bench Verified | GPT-4o (best scaffold) | public-headline | 33.2% resolved (500-task human-validated subset) | https://openai.com/index/introducing-swe-bench-verified/ | vendor (OpenAI) | 2024-08-13 |
| R3 | SWE-bench Verified | (OpenAI internal audit of hard-fail subset) | contamination-adjusted | ≥59.4% of audited hard tasks have flawed test cases that reject correct solutions; audit covered 27.6% subset; OpenAI ceased reporting and now recommends SWE-bench Pro | https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/ | vendor (OpenAI) | 2026-02-23 |
| R4 | SWE-bench Verified | GPT-5.2 (SWE-agent) | public-headline | 72.80% resolved | https://arxiv.org/abs/2512.18470 | independent academic (SWE-EVO paper, Table 2) | 2025-12-20 |
| R5 | SWE-bench Verified | GLM-5 / Kimi-k2p5 / DeepSeek-v3p2 (SWE-agent) | public-headline | 72.80% / 70.80% / 70.00% resolved | https://arxiv.org/abs/2512.18470 | independent academic (SWE-EVO paper, Table 2) | 2025-12-20 |

### SWE-Bench Pro (private-holdout variant of the SWE family)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R6 | SWE-Bench Pro — public set (N=731) | Claude Opus 4.1 | public-headline | 17.8% resolved | https://arxiv.org/abs/2509.16941 | independent academic (Scale, SWE-Bench Pro) | 2025-09-21 |
| R7 | SWE-Bench Pro — commercial/held-out set (N=276) | GPT-5 (high) | private-holdout | 15.7% resolved (vs 41.8% on public set) | https://arxiv.org/abs/2509.16941 | independent academic (SWE-Bench Pro) | 2025-09-21 |
| R8 | SWE-Bench Pro — commercial/held-out set (N=276) | Claude Opus 4.1 | private-holdout | 17.8% resolved (≈ flat vs public 17.8%) | https://arxiv.org/abs/2509.16941 | independent academic (SWE-Bench Pro) | 2025-09-21 |

### SWE-EVO (long-horizon variant of the SWE family)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R9 | SWE-EVO (long-horizon, avg 21 files/task) | GPT-5.2 (SWE-agent) | long-horizon | 22.92% resolved (vs 72.80% on SWE-bench Verified, R4) | https://arxiv.org/abs/2512.18470 | independent academic (SWE-EVO, Table 2) | 2025-12-20 |
| R10 | SWE-EVO (long-horizon) | GPT-5.4 (best of both frameworks) | long-horizon | 25.00% resolved (best model on benchmark) | https://arxiv.org/abs/2512.18470 | independent academic (SWE-EVO, Table 2) | 2025-12-20 |
| R11 | SWE family — field deployment proxy | Top coding agents (Anthropic/OpenAI/Cognition + GitHub PR data + 25+ enterprise rollouts) | field/PR-acceptance | Production PR-acceptance 35–50% vs 74–78% on SWE-bench Verified | https://presenc.ai/research/coding-agent-benchmarks-2026 | independent (Presenc; mixed primary measurement + public reports) | 2026-05 (last updated) |

### Benchmark family 2 — GPQA (graduate-level science Q&A)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R12 | GPQA (full, 448 Q) | GPT-4 | public-headline | 39% accuracy | https://arxiv.org/abs/2311.12022 | independent academic (GPQA paper) | 2023-11-20 |
| R13 | GPQA (full) | Human PhD-domain experts (ceiling reference) | public-headline | 65% (74% discounting self-identified errors); skilled non-experts 34% | https://arxiv.org/abs/2311.12022 | independent academic (GPQA paper) | 2023-11-20 |
| R14 | GPQA / GPQA-Diamond + HLE + SimpleQA | Search-augmented agents (contaminated subset) | contamination-adjusted | ≈15 percentage-point accuracy drop on contaminated subset after HuggingFace blocked; ~3% of questions affected by search-time leakage | https://arxiv.org/abs/2508.13180 | independent academic (Search-Time Data Contamination) | 2025-08-12 |
| R15 | GPQA-Diamond | (validity audit of hardest items) | contamination-adjusted | ~90–95% of questions judged valid; ~2–3 of hardest 40 likely invalid (bad key/unsolvable) — caps the achievable ceiling | https://epoch.ai/gradient-updates/gpqa-diamond-whats-left | independent (Epoch AI, Greg Burnham) | 2025-05 |

### Benchmark family 3 — MMLU (multitask knowledge)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R16 | MMLU (original, 57 tasks) | GPT-3 (175B) | public-headline | ~+20 pp over random chance on average (i.e., far below expert level) | https://arxiv.org/abs/2009.03300 | independent academic (MMLU paper) | 2021-01-12 |
| R17 | MMLU (5-shot) | GPT-4o | public-headline | 88.0% | https://arxiv.org/abs/2412.15194 | independent academic (MMLU-CF, citing vendor-reported MMLU) | 2024-12-19 |
| R18 | MMLU-CF (contamination-free, 5-shot test set) | GPT-4o | contamination-adjusted | 73.4% (0-shot 71.9%); gap of 14.6 pp vs MMLU 88.0% | https://arxiv.org/abs/2412.15194 | independent academic (MMLU-CF) | 2024-12-19 |
| R19 | MMLU-CF (5-shot test set) | GPT-4-Turbo | contamination-adjusted | 70.4% vs 86.5% on MMLU; gap of 16.1 pp | https://arxiv.org/abs/2412.15194 | independent academic (MMLU-CF) | 2024-12-19 |
| R20 | MMLU → MMLU-Pro (10 options, reasoning-focused) | GPT-4o (best at time) | private-holdout (harder reshuffle) | 72.6% on MMLU-Pro; reframed MMLU causes 16%–33% accuracy drop across models | https://arxiv.org/abs/2406.01574 | independent academic (MMLU-Pro) | 2024-06-03 |
| R21 | QA benchmarks incl. MMLU (cross-benchmark contamination) | 15+ popular LLMs, 6 MCQA benchmarks | contamination-adjusted | Measured contamination 1%–45% across benchmarks; rising over time | https://arxiv.org/abs/2310.17589 | independent academic (Li, Guerin & Lin) | 2023-10-26 |

### Benchmark family 4 — GSM8K (grade-school math)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R22 | GSM8K | GPT-4o | public-headline | 95.0% accuracy | https://arxiv.org/abs/2410.05229 | independent academic (GSM-Symbolic, Table 1) | 2024-10-07 |
| R23 | GSM-Symbolic (templated rewrite of GSM8K) | Gemma2-9b-it / Phi-3.5-mini / Mistral-7b | contamination-adjusted | Gemma2-9b 87.0%→79.1% (−7.9 pp); Phi-3.5 88.0%→82.1% (−5.9 pp); Mistral-7b 56.0%→50.0% (−6.0 pp) | https://arxiv.org/abs/2410.05229 | independent academic (GSM-Symbolic, Table 1) | 2024-10-07 |
| R24 | GSM-NoOp (GSM8K + one irrelevant clause) | GPT-4o / o1-mini / Phi-3-mini | long-horizon (robustness) | GPT-4o 94.9%→63.1% (−31.8 pp); o1-mini 94.5%→66.0% (−28.5 pp); Phi-3-mini 80.7%→18.0% (−62.7 pp); up to −65% across models | https://arxiv.org/abs/2410.05229 | independent academic (GSM-Symbolic) | 2024-10-07 |
| R25 | GSM1k (clean human-written mirror of GSM8K) | Several model families (e.g., Mistral/Phi) | contamination-adjusted | Accuracy drops of up to 8% on GSM1k vs GSM8K; gap correlates with likelihood of reproducing GSM8K text (contamination signal) | https://arxiv.org/abs/2405.00332 | independent academic (Scale, GSM1k) | 2024-05-01 |

### Benchmark family 5 — MATH (competition math)

| Row | Benchmark | Model (version) | Metric type | Reported value | Primary source URL | Source type | Date |
|-----|-----------|-----------------|-------------|----------------|--------------------|-------------|------|
| R26 | MATH (original, 5000 test problems) | (benchmark definition / difficulty reference) | public-headline | 5,000 competition problems w/ worked solutions; chosen as the controlled-contamination testbed | https://arxiv.org/abs/2601.04301 | independent academic (contamination study) | 2026-01-07 |
| R27 | MATH (controlled contamination injection) | Decoder transformers up to 344M params | contamination-adjusted | Uncontaminated baseline ≈4% accuracy → near-100% with 1000 test-set replicas injected; sharp jump ~100 replicas | https://arxiv.org/abs/2601.04301 | independent academic (Schaeffer et al.) | 2026-01-07 |
| R28 | MATH (contamination brittleness under sampling) | same | contamination-adjusted | Raising temperature 0→1.0 cuts accuracy by ~2× at low contamination but up to ~40× at high (1000 replicas) — inflated gains collapse under realistic sampling | https://arxiv.org/abs/2601.04301 | independent academic (Schaeffer et al.) | 2026-01-07 |
| R29 | MMLU-Pro (math-heavy reasoning superset, cross-ref) | best models | private-holdout (harder reshuffle) | 16%–33% accuracy drop vs MMLU; applicable to math/reasoning subsets | https://arxiv.org/abs/2406.01574 | independent academic (MMLU-Pro) | 2024-06-03 |

---

## Coverage check against done-criteria

- **≥5 benchmarks with ≥3 rows:** SWE-bench/Verified (R1–R11, 11 rows incl. Pro/EVO variants), GPQA (R12–R15, 4), MMLU (R16–R21, 6), GSM8K (R22–R25, 4), MATH (R26–R29, 4). All five ≥3. ✔
- **Deflationary data point per benchmark:** SWE (R3 contamination-adjusted, R7/R8 private-holdout, R9/R10 long-horizon); GPQA (R14 contamination-adjusted, R15); MMLU (R18/R19/R21 contamination-adjusted, R20 harder reshuffle); GSM8K (R23/R25 contamination-adjusted, R24 robustness); MATH (R27/R28 contamination-adjusted). ✔
- **Every brief "State of the art" claim represented, traced to original source:**
  - Opus 4.1 & GPT-5 drop on private codebases → R6, R7, R8 (arXiv 2509.16941). *Numbers corrected — see Gaps G1.*
  - GPT-5.2 72.8% Verified → SWE-EVO → R4, R9 (arXiv 2512.18470). *SWE-EVO figure corrected to 22.92% — see Gaps G2.*
  - OpenAI stopped reporting SWE-bench Verified, 59.4% flawed → R3 (openai.com).
  - GSM8K contamination cut accuracy up to 13% → R25 (arXiv 2405.00332). *Verified value is 8%, not 13%, and source is GSM1k not 2601.04301 — see Gaps G3.*
  - Leakage 1–45% across QA benchmarks → R21 (arXiv 2310.17589). *Re-sourced from the brief's mis-cite — see Gaps G3.*
  - PR-acceptance 50–60% below SWE-bench → R11 (presenc.ai). *Magnitude differs from brief — see Gaps G4.*

---

## Gaps & contested points

**G1 — SWE-Bench Pro figures in the brief do not match the primary source.** The brief states "Claude Opus 4.1 drops 22.7% → 17.8% and GPT-5 drops 23.1% → 14.9%." The arXiv 2509.16941 paper (read 2026-06-28) reports Claude Opus 4.1 at **17.8% on both the public (N=731) and commercial/held-out (N=276) sets** (≈ flat), and GPT-5 (high) at **41.8% public → 15.7% commercial**. The brief's "22.7%→17.8%" and "23.1%→14.9%" pairings could not be confirmed against the abstract/HTML I read; they may come from a different table partition, model-config row, or paper version. **Rows R6–R8 carry the verified numbers.** The qualitative claim (large public→private drop) holds for GPT-5 (−26.1 pp) but NOT for Opus 4.1 (≈0 pp) — a contested point M2 must handle: the public→private gap is model-dependent, not uniform.

**G2 — SWE-EVO headline figure corrected.** The brief says GPT-5.2 "falls to 22.9% on SWE-EVO." The paper (Table 2) reports GPT-5.2 (SWE-agent) at **22.92%** on SWE-EVO vs **72.80%** on SWE-bench Verified — consistent with the brief (22.9% ≈ 22.92%). Note the *best* model on SWE-EVO is GPT-5.4 at 25.00% (R10); "GPT-5.2" and "GPT-5.4" are distinct rows and should not be conflated downstream.

**G3 — The brief's contamination citation (arXiv 2601.04301) is mis-attributed.** The brief cites 2601.04301 for "removing contaminated items from GSM8K cut accuracy up to 13%" and "leakage of 1-45% across QA benchmarks." On reading 2601.04301 (Schaeffer et al., "Quantifying the Effect of Test Set Contamination on Generative Evaluations," 2026-01-07), that paper studies the **MATH** benchmark with synthetic replica injection on small models — it contains neither the GSM8K-13% figure nor the 1–45% range. I re-sourced both claims to their actual primaries: (a) the GSM8K clean-mirror drop traces to the **GSM1k** paper (arXiv 2405.00332), whose abstract states "accuracy drops of up to **8%**" — not 13%. The "13%" appears in secondary summaries (e.g., applied to Mistral specifically) but I could not confirm 13% in the GSM1k abstract/HTML; **R25 carries 8% (verified); the 13% figure is flagged low-confidence and should not be used in M2 without locating the exact table.** (b) The "1–45%" range traces to **Li, Guerin & Lin, arXiv 2310.17589** ("An Open-Source Data Contamination Report," 2023-10-26) — verified (R21). 2601.04301 is retained correctly as the MATH-contamination primary (R26–R28).

**G4 — Presenc PR-acceptance magnitude differs from the brief.** The brief says "PR-acceptance rates run 50-60% below SWE-bench scores." The Presenc page (read 2026-06-28) reports production PR-acceptance of **35–50%** vs **74–78%** on SWE-bench Verified — a gap of roughly **25–43 percentage points**, or a relative shortfall of ~35–55%. "50–60% below" is not directly stated. R11 carries Presenc's exact figures. Caveat: Presenc is a vendor-adjacent source mixing its own deployment instrumentation with summarized public reports, not a peer-reviewed re-run; treat as a field-proxy lower bound, not an audited number. This is the weakest-provenance row in the dossier.

**G5 — MATH lacks a clean frontier-model contamination delta.** The strongest MATH contamination evidence (R27, R28) is from a *controlled* experiment on small (≤344M-param) models, not a public→clean delta on a named frontier model. There is no verified row of the form "GPT-X scores Y% on MATH but Z% on a decontaminated MATH." M2's MATH contamination fraction will therefore rest on the controlled study plus the cross-benchmark range (R21) and should be marked lower-confidence than GSM8K/MMLU, which have model-specific deltas (R23/R25, R18/R19).

**G6 — GPQA contamination evidence is thin and indirect.** GPQA ships a canary string and Epoch's audit (R15) finds ~90–95% validity, so the dominant deflationary driver is *task difficulty / ceiling* (R13: experts only reach 65–74%) rather than leakage. The only quantified leakage figure (R14) is a ~15 pp drop on a *small contaminated subset* (~3% of questions) via search-time access, not whole-benchmark contamination. GPQA's headline numbers are plausibly *less* inflated by contamination than MMLU/GSM8K — a contested point that pushes against the brief's blanket "all benchmarks overstate" framing and that M2/M3 should treat as a benchmark where the discount may be small.

**G7 — Vendor headline scores partly sourced via independent papers, not vendor pages.** OpenAI/Anthropic launch pages return HTTP 403 to automated fetching, so several vendor-reported headline numbers (e.g., GPT-4o MMLU 88.0%, R17) are sourced from the independent paper that cites them (MMLU-CF) rather than the original vendor post. The number is the vendor-reported value but the URL is the academic re-statement. Two vendor sources *did* resolve and are cited directly: the two OpenAI SWE-bench posts (R1–R3). A future pass with an authenticated/vendor-page-capable fetch should attach original vendor URLs to R16–R17, R22.

**G8 — Model-version heterogeneity across rows.** Rows span GPT-3 (2021) through GPT-5.4 (2025-26) and Claude/Gemini variants; deflationary deltas measured on one model generation may not transfer to another. M2/M3 must not subtract a GSM-Symbolic drop measured on Gemma2-9b (R23) from a GPT-5 headline. Pairing of headline and deflationary rows must be model-family-matched where possible; where it cannot be, the component must be flagged cross-model and low-confidence.

---

## Limitations & counter-evidence

1. **This dossier collects, it does not yet weigh.** Several deflationary deltas are measured on weak/small or older models (R16 GPT-3; R23 9B-class open models; R27 ≤344M-param models). They establish that contamination/horizon gaps *exist* and are large in some regimes, but they are not direct evidence about the frontier models a 2026 federal buyer would actually procure. Counter-evidence: where frontier models were tested directly, some gaps are small (R6/R8: Opus 4.1 ≈ flat public→private; R22→R23: GPT-4o barely moves on GSM-Symbolic numeric perturbation), cutting against a uniform large-overstatement story.
2. **The "field/PR-acceptance" link (R11) is the highest-leverage but lowest-provenance row.** It is the only direct deployment proxy and it comes from a vendor-adjacent source mixing primary instrumentation with public-report aggregation; it should anchor the narrative but not a precise discount until corroborated by an independent re-run.
3. **Vendor headline rows are partially second-hand (G7).** Because vendor pages 403 automated fetches, three headline values are sourced via the academic paper that cites them. The values are standard and consistent with public knowledge, but the provenance is one hop removed.
4. **Brief-vs-source discrepancies are unresolved, not adjudicated (G1, G3, G4).** Three brief numbers (Opus/GPT-5 Pro pairing, GSM8K 13%, PR 50–60%) could not be confirmed at the exact stated value against the cited primary. I kept the verified numbers and flagged the gaps rather than reproduce the brief's figures; if the brief's numbers come from a table I did not reach, M2 should re-open these before computing.
5. **Contamination ≠ overstatement of *deployed* value, necessarily.** A leaked test item inflates a *score*; whether it inflates *deployed* capability depends on whether the deployment task resembles the benchmark. The dossier conflates several distinct deflation mechanisms (leakage, harder reshuffles, longer horizons, robustness perturbations, field acceptance) under one umbrella; M2 must keep them separate, because only some bear directly on procurement validity.
6. **Counter-evidence to the core thesis exists and is recorded.** GPQA (G6) appears comparatively contamination-robust; numeric-only perturbation barely dents frontier models on GSM8K (R22→R23). The honest reading is that overstatement is real and sometimes very large (R3, R9, R24, R18) but is benchmark- and model-dependent, not a flat haircut — which is precisely the nuance the eventual procurement-discount ledger must encode.
