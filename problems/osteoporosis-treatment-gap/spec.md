# Spec: the post-fracture osteoporosis treatment gap

## Objective
"Unstuck" means the missing dossier exists: a single, sourced, reproducible evidence package that (1) shows where post-fracture treatment rates stand across countries and US systems, (2) inverts the atypical-femoral-fracture scare with explicit benefit-harm arithmetic, (3) quantifies what the gap costs Medicare in deaths and dollars each year, and (4) converts all of that into the two documents the coalitions lack — a CMS rulemaking comment supporting dedicated post-fracture/FLS payment, and an NHS-style business case template for US payers. The end artifact serves the BHOF/ASBMR/Bone Health Policy Institute coalition working the CMS docket and, secondarily, any health-system bone-health champion who needs a ready-made internal pitch. Everything is desk synthesis from published cohorts, registries, IOF SCOPE scorecards, and government dockets — no human action or unpublished data required.

## Milestones

### M1: League table of post-fracture treatment rates
- **Task:** Build a comparative table of post-fragility-fracture osteoporosis treatment rates (pharmacologic treatment initiation within ~12 months of fracture, or the closest definition each source reports) across countries and US health systems/states, from published cohort studies, national registries (e.g., UK FLS-DB, Swedish/Danish registers), IOF SCOPE scorecards, and Medicare claims studies.
- **Skill:** none — freeform
- **Artifact format:** Ranked markdown table with columns: jurisdiction/system, population studied, fracture type(s), treatment definition and time window, treatment rate %, data year(s), source (linked citation). Followed by a "Comparability caveats" section and a "Limitations" section.
- **Done-criteria:**
  - Table contains >= 10 distinct countries AND >= 5 distinct US health systems or states (Kaiser Permanente Healthy Bones must be one row).
  - Every row has >= 1 citation with a working URL to a published study, registry report, or scorecard.
  - Every row states the treatment definition and time window used by its source (no blank cells in those columns).
  - Comparability caveats section names >= 3 specific reasons rates are not directly comparable across rows (e.g., differing time windows, fracture-type mix, claims vs. chart data).
  - At least one row documents the US post-hip-fracture treatment decline with a pre-2010 and a post-2013 data point, each cited.

### M2: Benefit-harm dossier inverting the atypical-fracture scare
- **Task:** Assemble the quantitative benefit-harm case for bisphosphonates after fragility fracture: reproduce the published fractures-prevented-vs-atypical-fractures-caused arithmetic, state NNT/NNH figures, document the post-2010 prescribing collapse, and rebut the major safety counterarguments with cited evidence.
- **Skill:** none — freeform
- **Artifact format:** Structured markdown dossier with sections: (1) headline arithmetic, (2) NNT/NNH table, (3) timeline of the prescribing collapse, (4) counterarguments and rebuttals, (5) limitations and honest residual risks.
- **Done-criteria:**
  - Reproduces the Black et al. NEJM 2020 ratio (hip fractures prevented per atypical femoral fracture caused, at stated follow-up durations) with direct citation, and shows the calculation, not just the headline number.
  - NNT/NNH table gives at least: NNT for hip-fracture prevention and NNT for vertebral-fracture prevention with bisphosphonates, and NNH for atypical femoral fracture and for osteonecrosis of the jaw — each figure cited to a peer-reviewed source.
  - Prescribing-collapse timeline contains >= 3 dated, cited data points (e.g., ~50% use decline post-2010; 15%→3% post-hip-fracture treatment 2004→2013).
  - Counterarguments section addresses >= 3 named concerns (at minimum: atypical femoral fracture, osteonecrosis of the jaw, long-duration use/drug holidays), each with a cited rebuttal or quantified risk.
  - Limitations section concedes >= 2 genuine caveats (e.g., AFF risk rises with duration; data mostly from women) rather than presenting the case as one-sided.

### M3: Medicare cost-of-the-gap model
- **Task:** Rebuild the Royal Osteoporosis Society-style cost model for US Medicare: using the M1 baseline treatment rate and published inputs, estimate annual avoidable refractures, avoidable deaths, and net dollar impact of closing the post-fracture treatment gap via FLS-style care, with all formulas explicit and reproducible.
- **Skill:** none — freeform
- **Artifact format:** Markdown model document with: (1) inputs table (each input sourced), (2) formulas written out, (3) base-case results table, (4) low/base/high sensitivity table, (5) comparison to published FLS cost-effectiveness findings, (6) limitations section.
- **Done-criteria:**
  - Inputs table lists, at minimum: annual fragility fractures in the Medicare population, current post-fracture treatment rate, target achievable rate (with a cited precedent such as an FLS or Kaiser figure), relative refracture-risk reduction from treatment, refracture and hip-fracture costs, post-hip-fracture mortality, and per-patient FLS/intervention cost — each with a citation.
  - Every reported output (avoidable refractures/year, avoidable deaths/year, gross and net dollars/year) can be recomputed from the stated inputs and formulas alone; the document shows at least one fully worked example calculation.
  - Sensitivity section reports low/base/high scenarios varying >= 3 inputs, with the varied values stated.
  - Results are cross-checked against >= 2 published estimates (e.g., the Medicare FLS cost-effectiveness literature, the ROS UK model) with discrepancies explicitly discussed.
  - Limitations section names >= 3 specific model weaknesses (e.g., adherence assumptions, time-to-benefit, claims undercounting).

### M4: CMS docket comment and US FLS business case
- **Task:** Using the M1 table, M2 dossier, and M3 model as inputs, draft (a) a public comment for the next CMS Physician Fee Schedule rulemaking cycle supporting dedicated post-fracture care coordination payment (the G-code ask of the 35-organization coalition), and (b) an NHS-style FLS business case template a US health system or payer could adapt.
- **Skill:** none — freeform
- **Artifact format:** Single markdown artifact in two parts: Part A — docket-ready comment letter (addressee, docket/rule identified, numbered arguments, specific regulatory ask); Part B — business case template (problem statement, intervention, costs, savings, staffing model, KPIs), with bracketed placeholders only for system-specific fields.
- **Done-criteria:**
  - Part A identifies the correct, current CMS rulemaking vehicle (named rule/docket and comment mechanism, verified via web search at generation time) and states one primary regulatory ask in a single sentence.
  - Part A cites the 35-organization coalition letter and >= 5 distinct numeric claims, each traceable to the M1, M2, or M3 artifact (referenced by artifact filename and section) or to a directly cited primary source.
  - Part A pre-empts the cost objection with the M3 net-dollar result and >= 1 peer-reviewed FLS cost-effectiveness citation.
  - Part B includes all six template sections (problem statement, intervention, costs, savings, staffing model, KPIs), with every non-placeholder number sourced from M1–M3 or a cited primary source.
  - Combined artifact contains zero uncited quantitative claims (placeholders in Part B excepted).
