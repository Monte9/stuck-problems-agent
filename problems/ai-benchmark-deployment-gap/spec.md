# Spec: the AI-benchmark-to-deployment gap

## Objective
"Unstuck" means a skeptical procurement officer at CAISI/NIST or GSA can open one document and, for each major AI benchmark they are about to wire into the federal eval standard, read off (i) how much of the headline score is contaminated or memorized, (ii) how far the score falls when you move from the public set to a private holdout or a longer-horizon variant, and (iii) a defensible numeric "procurement discount" — the haircut to apply to a vendor's headline number before trusting it — with a falsifiable range and a source URL behind every figure. The end artifact is a reproducible, per-benchmark deployment-validity ledger plus a procurement-facing memo. It serves the named buyer: CAISI/NIST + GSA, who signed a March 2026 MOU to select and interpret procurement benchmarks and have stated this synthesis does not exist. Success is the documented inversion (headline overstates deployment), not a new benchmark or a fix.

## Milestones

### M1: Benchmark inventory and source dossier
- **Task:** Identify the major AI benchmarks used to price/procure frontier models (at minimum SWE-bench / SWE-bench Verified, SWE-bench Pro, SWE-EVO, GPQA, MMLU, GSM8K/math sets, plus contamination-resistant designs like LiveBench, LiveCodeBench, FrontierMath) and assemble a sourced evidence dossier of every relevant data point: vendor headline scores, independent re-runs, contamination/leakage audits, and private-holdout or long-horizon results.
- **Skill:** none — freeform
- **Artifact format:** A table with one row per (benchmark, evidence-item), columns: benchmark, model/model-family, claim type {vendor-headline | independent-rerun | contamination-audit | private-holdout | long-horizon}, reported number(s), source URL, source date, one-line description. Plus a short "benchmarks excluded and why" section.
- **Done-criteria:**
  - At least 8 distinct benchmarks appear as rows.
  - Every evidence-item row carries at least one resolvable source URL and a source date.
  - Every benchmark cited in problem.md (SWE-bench Verified, SWE-bench Pro, SWE-EVO, GSM8K, GPQA, MMLU, LiveBench/LiveCodeBench, FrontierMath) is present or has an explicit excluded-with-reason note.
  - At least 5 rows are contamination/audit or private-holdout/long-horizon evidence (not vendor headlines).

### M2: Contamination / recall fraction per benchmark
- **Task:** Using the M1 dossier, estimate for each benchmark the contamination or recall fraction — the share of the headline score attributable to leaked, memorized, or flawed-test items — as a numeric value or range with its derivation.
- **Skill:** none — freeform
- **Artifact format:** A table keyed by benchmark, columns: benchmark, contamination/recall estimate (point or low–high range), basis {direct audit measurement | flawed-test share | inferred}, the underlying number(s) it is derived from, source URL(s), and a confidence tag {high | medium | low} with one-line justification.
- **Done-criteria:**
  - Every benchmark row from M1's inventory has a contamination/recall cell that is either a number/range or an explicit "no published estimate found" with that stated.
  - Every numeric estimate traces to at least one source URL that also appears in or is consistent with the M1 dossier.
  - At least 4 benchmarks have a quantified estimate grounded in a cited audit (e.g. GSM8K leakage, SWE-bench Verified flawed-test share).
  - Each row carries a confidence tag with a one-line justification.

### M3: Controlled score-drop measurement (public→private, short→long-horizon)
- **Task:** For each model family where paired evidence exists, quantify the controlled score drop from public to private holdout and from short to long-horizon variants of the same benchmark, holding the model constant.
- **Skill:** none — freeform
- **Artifact format:** A table of paired comparisons, columns: model family, benchmark pair (e.g. SWE-bench Verified → SWE-bench Pro; SWE-bench Verified → SWE-EVO), public/short score, private/long score, absolute drop, relative drop (%), source URL(s) for both numbers, and a note on whether the comparison holds the model and scaffold constant.
- **Done-criteria:**
  - At least 6 paired comparisons appear, each with both endpoint scores sourced by URL.
  - The flagship cases from problem.md are present: GPT-5 SWE-bench Pro public→private (≈23.1%→14.9%), Claude Opus 4.1 (≈22.7%→17.8%), GPT-5.2 SWE-bench Verified→SWE-EVO (≈72.8%→22.9%).
  - Every row computes both absolute and relative drop from its two cited numbers, and the arithmetic is internally consistent.
  - Each row states explicitly whether model and scaffold are held constant or notes the confound if not.

### M4: Procurement-discount ledger
- **Task:** Combine M2 (contamination) and M3 (controlled drop) into a per-benchmark procurement discount — the haircut a buyer should apply to a headline score — expressed as a falsifiable range per benchmark (and per model family where data allows), and rank benchmarks by deployment validity.
- **Skill:** none — freeform
- **Artifact format:** A ranked table, columns: benchmark, deployment-validity rank, recommended procurement discount range (e.g. "apply 20–50% haircut"), the M2 + M3 inputs it was derived from, an explicit one-line derivation rule, verdict {survives | use-with-discount | functionally noise}, and source pointers. Plus a "limitations and assumptions" section.
- **Done-criteria:**
  - Every benchmark in the M1 inventory has a discount range (or an explicit "insufficient evidence to quantify" verdict).
  - Each discount range names the specific M2 and/or M3 cells it was derived from, and states the derivation rule used (no unexplained numbers).
  - Benchmarks are ranked, and at least one is labeled "functionally noise" or at least one "survives contamination," matching the verdict logic.
  - A limitations section lists at least 3 named threats to validity (e.g. scaffold variance, small holdout sizes, single-vendor self-reports).

### M5: Procurement-facing memo for CAISI/NIST + GSA
- **Task:** Write a short decision memo addressed to the named buyer that translates the M4 ledger into procurement guidance: which benchmarks to trust, the discount to apply to each, and what to require from vendors.
- **Skill:** none — freeform
- **Artifact format:** A 1–2 page memo with: a one-paragraph bottom line, a compact summary table (benchmark, discount, verdict) drawn from M4, 3–5 concrete procurement recommendations, and a "what would change our conclusion" falsification section. References the M4 ledger as its evidence base.
- **Done-criteria:**
  - The memo names CAISI/NIST and GSA and ties to the March 2026 MOU / federal eval-standard context.
  - The summary table is consistent with M4 (same benchmarks, same discount ranges — no new numbers introduced here).
  - At least 3 actionable, near-binary procurement recommendations are stated (e.g. "require vendors to report a private-holdout score, not only the public set").
  - A falsification section lists at least 2 specific findings that would overturn the memo's conclusion.
