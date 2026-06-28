# Spec: the AI-benchmark-to-deployment gap

## Objective
"Unstuck" means CAISI/NIST and GSA — the buyers actively writing the federal AI-procurement evaluation standard in 2026 — can open a single reproducible **deployment-validity ledger** that, for each major public benchmark (SWE-bench/Verified, GPQA, MMLU, and the headline math sets such as GSM8K/MATH), states with sourced evidence how much a headline score overstates real deployed performance: the contamination/recall fraction, the controlled public-to-private and short-to-long-horizon score drops, and a defensible **procurement discount** — the haircut a buyer should subtract from a vendor's reported number before trusting it. The end artifact serves that named buyer (CAISI/NIST + GSA) as a drop-in input to their benchmark-selection methodology. It is a teardown: the contribution is the documented, falsifiable inversion of inflated numbers, assembled from fragments that already exist but have never been put in one table — not a new benchmark and not a fix.

## Milestones

### M1: Evidence dossier — collect the raw fragments
- **Task:** For each target benchmark (SWE-bench / SWE-bench Verified, GPQA, MMLU, and at least two math sets including GSM8K), gather every reachable published data point bearing on deployment validity: vendor-reported headline scores, independent re-runs, contamination/leakage audits, private-holdout or "Pro" variants, and long-horizon variants. Record each as a row with the exact number and its primary source.
- **Skill:** none — freeform
- **Artifact format:** A source-keyed evidence table with columns: `benchmark | model (and version) | metric type {public-headline | private-holdout | long-horizon | contamination-adjusted | field/PR-acceptance} | reported value | primary source URL | source type {vendor | independent academic | leaderboard} | date`. Followed by a "gaps & contested points" section listing benchmarks where evidence is thin or sources conflict.
- **Done-criteria:**
  - At least 5 distinct benchmarks each have >=3 evidence rows.
  - Every row has a working primary-source URL and a publication date; no row cites a blog summarizing an unnamed study.
  - Each benchmark has at least one row tagged `contamination-adjusted` OR one tagged `private-holdout`/`long-horizon` (i.e., at least one deflationary data point per benchmark), or is explicitly flagged in the gaps section as lacking one.
  - Every quantitative claim that appears in the problem brief's "State of the art" paragraph is represented by at least one row, each traced to its original arXiv/vendor source rather than to the brief.

### M2: Quantify the three gap components per benchmark
- **Task:** Using the M1 dossier as input, compute for each benchmark three numbers with stated ranges: (i) contamination/recall fraction (share of headline score attributable to leaked/flawed items), (ii) public-to-private score drop, and (iii) short-to-long-horizon score drop. Show the arithmetic from named M1 rows; where a component cannot be computed, mark it "insufficient evidence" rather than guessing.
- **Skill:** none — freeform
- **Artifact format:** A per-benchmark computation table: `benchmark | contamination fraction [low–high] | public→private drop (pp) [low–high] | short→long-horizon drop (pp) [low–high] | M1 rows used (IDs) | derivation note`. Each cell either a range or the literal token "insufficient evidence". A methods preamble states the formula used for each component.
- **Done-criteria:**
  - Every numeric cell either is a low–high range traceable to specific M1 rows (cited by ID/source) or reads exactly "insufficient evidence".
  - Each component's formula is stated once in the preamble and applied identically across benchmarks (an evaluator can re-derive one cell from the cited M1 rows and reproduce the range).
  - No component value is computed from a single data point without the artifact flagging it as low-confidence (n=1).
  - At least 4 of the 5+ benchmarks have at least two of the three components populated with a range (not "insufficient evidence").

### M3: Derive the per-benchmark procurement discount
- **Task:** Convert the M2 components into a single falsifiable **procurement discount range** per benchmark per model family — the percentage-point haircut a buyer should subtract from a vendor's headline score — and classify each benchmark as "survives contamination / usable", "usable with large discount", or "functionally noise". The combination rule from M2 components to discount must be explicit and uniform.
- **Skill:** none — freeform
- **Artifact format:** A ranked table (most-trustworthy benchmark first): `benchmark | model family | implied procurement discount [low–high pp or %] | classification {usable | discount-heavily | noise} | dominant driver {contamination | private-gap | horizon-gap} | confidence {high|med|low} | components used`. Preceded by a stated combination rule and followed by a worked example for one benchmark.
- **Done-criteria:**
  - The rule mapping M2 components to the discount is written explicitly and is reproducible (the evaluator can apply it to one benchmark's M2 row and get the table's number).
  - Every benchmark in the table carries a discount range, a classification, and a confidence label; ranking order matches a stated, monotonic criterion (e.g., ascending discount or descending confidence).
  - At least one benchmark is classified "noise" or "discount-heavily" AND at least one "usable", and each classification cites the M2 components that drove it.
  - The worked example shows the full arithmetic from M1 rows → M2 components → final discount for one named benchmark.

### M4: Buyer-facing brief, limitations, and falsification tests
- **Task:** Package M3 into a one-page decision aid addressed to CAISI/NIST + GSA: how to apply the discounts when interpreting a vendor's reported benchmark score in procurement, plus an explicit limitations section and a list of tests that would falsify or update each discount.
- **Skill:** none — freeform
- **Artifact format:** A short brief with: (1) a "how to use this" paragraph naming the buyer and the procurement decision it informs; (2) the M3 ranked discount table reproduced or referenced; (3) a numbered limitations section; (4) a "what would change these numbers" section listing concrete, checkable falsification tests per benchmark or per discount.
- **Done-criteria:**
  - The brief names CAISI/NIST and GSA and states, in one sentence, the procurement action the discounts feed (interpreting/selecting benchmarks for federal AI procurement).
  - The limitations section lists at least 5 distinct, specific threats to validity (e.g., model-version drift, scaffold variance, small-n components, vendor-vs-independent source asymmetry), each tied to where in M1–M3 it bites.
  - The falsification section lists at least one concrete test per benchmark whose outcome would move that benchmark's discount, phrased so a reader could in principle run it (e.g., "re-score on holdout X; if drop < Y pp, lower the discount").
  - No discount or classification appears in the brief that is not backed by an M3 row; the brief introduces no new numbers absent from M1–M3.
