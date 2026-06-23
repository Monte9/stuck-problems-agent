# Spec: Charity care that nonprofit hospitals are legally required to give — and mostly don't

## Objective
"Unstuck" means producing a concrete, hospital-by-hospital non-compliance / inaccessibility scorecard that turns the aggregate "$14 billion under-billed, only 29% of eligible patients helped" statistic into a named list a regulator can act on. The end artifact serves three audiences who can each act on named hospitals but not on aggregates: state Attorneys General (consumer-protection and charitable-trust enforcement), the IRS Tax-Exempt/Government Entities division (Section 501(r) compliance and the rare revocation lever), and advocacy groups like Dollar For and the Lown Institute (campaign targeting). Every milestone accumulates toward that scorecard: first we fix the rubric and the sample frame, then we collect and score the public FAP / Plain Language Summary text, then we layer in Schedule H spending ratios, then we fuse it into a ranked, fully-sourced scorecard with a methodology and limitations section honest enough to survive hostile scrutiny.

## Milestones

### M1: Build the scoring rubric and the hospital sample frame
- **Task:** Define a machine-checkable rubric for FAP / Plain Language Summary (PLS) compliance and accessibility (the criteria the brief names: presumptive eligibility offered y/n, income eligibility threshold vs. 200% FPL, application-gated vs. application-free, PLS readability, FAP findable online), grounding each criterion in the specific IRC 501(r) / Treasury Reg. 1.501(r) requirement or named best practice it tests; and assemble a fixed, reproducible sample frame of 25-40 named US nonprofit hospitals/systems to evaluate.
- **Skill:** none — freeform
- **Artifact format:** Two sections. (1) A rubric table with columns: criterion name, what it measures, scoring scale (e.g. 0/1 or 0-2 with each level defined), legal/best-practice basis with source URL. (2) A sample-frame table with columns: hospital/system name, city, state, why included (selection rationale, e.g. largest by revenue / known prior coverage / geographic spread), and the URL of its FAP or hospital web page.
- **Done-criteria:**
  - Rubric contains at least 5 distinct criteria, each with a defined 0/1 or graded scoring scale stated in the table (no criterion left as prose only).
  - Every rubric criterion cites at least one source URL anchoring it to a 501(r) requirement or a named best-practice source (e.g. Treasury Reg, IRS guidance, Dollar For, Lown).
  - Sample frame lists between 25 and 40 distinct named hospitals or hospital systems, each with city, state, and a working URL.
  - Sample frame includes hospitals from at least 8 different US states (to avoid single-jurisdiction bias) and at least one North Carolina hospital (the presumptive-eligibility mandate jurisdiction, for contrast).
  - A selection-rationale sentence accompanies the frame explaining how the sample was chosen and what it is and is not representative of.

### M2: Collect and score each hospital's FAP and Plain Language Summary against the rubric
- **Task:** For every hospital in the M1 sample frame, locate the public FAP and Plain Language Summary, and apply the M1 rubric to score each criterion, recording the verbatim quote or specific page location that justifies each score.
- **Skill:** none — freeform
- **Artifact format:** One row per hospital. Columns: hospital/system name, FAP URL, PLS URL, one column per M1 rubric criterion holding the score, and an "evidence" column per scored criterion (or a linked evidence sub-table) holding the verbatim policy quote or page reference supporting the score. A short "documents not found" subsection lists any hospital whose FAP or PLS could not be located, with the searches attempted.
- **Done-criteria:**
  - Every hospital in the M1 sample frame appears exactly once (either scored, or explicitly listed under "documents not found" with the URLs/searches attempted).
  - Every applied score uses the exact scale defined in the M1 rubric (no scores outside the defined range).
  - Each non-null criterion score is backed by a verbatim quote from the FAP/PLS or a specific page/section reference, not a paraphrase.
  - Every FAP URL and PLS URL cell either holds a working source URL or is explicitly marked "not found".
  - The "income threshold vs. 200% FPL" and "presumptive eligibility offered" criteria are scored for every hospital that has a located FAP (these two are the brief's headline criteria and may not be left blank when the document exists).

### M3: Layer in Form 990 Schedule H charity-care spending ratios
- **Task:** For each hospital in the M1 frame (matched to its filing organization), pull the most recent available Form 990 Schedule H and compute the charity-care-as-share-of-revenue (or share-of-expense) ratio, then flag hospitals spending far below the peer set.
- **Skill:** none — freeform
- **Artifact format:** One row per hospital. Columns: hospital/system name, EIN (if found), filing year, Schedule H charity-care figure used (Part I financial assistance at cost), denominator used (total revenue or total functional expenses, stated consistently), computed ratio, source URL or filing locator, and a flag (below / at / above sample median). Include a short note stating which denominator was chosen and why, and how peers were compared.
- **Done-criteria:**
  - Every hospital from M1 appears exactly once, either with a computed ratio or explicitly marked "Schedule H not located" with the search attempted.
  - Every numeric charity-care figure cites the source filing via URL or a named locator (e.g. ProPublica Nonprofit Explorer page, IRS index) sufficient for a third party to retrieve it.
  - The same denominator definition is applied to every row (the artifact states which denominator and flags any row forced to deviate).
  - A sample median (or comparable peer benchmark) is computed and stated as a number, and each row's below/at/above flag is consistent with that benchmark.
  - The filing year is recorded for every row so no figure is presented without its vintage.

### M4: Fuse into the ranked non-compliance / inaccessibility scorecard
- **Task:** Combine the M2 accessibility scores and the M3 spending ratios into a single composite scorecard that ranks the named hospitals from most to least concerning, with a transparent weighting and a clear statement of what each rank means for a regulator.
- **Skill:** none — freeform
- **Artifact format:** A ranked master table (one row per hospital, ordered worst-to-best) with columns: rank, hospital/system name, state, composite concern score, key red flags (e.g. "application-gated; threshold below 200% FPL; charity spend below median"), and links back to the M2 and M3 evidence rows. Followed by a "Methodology" section stating the exact composite formula/weights, and a "Limitations" section.
- **Done-criteria:**
  - Every hospital that was successfully scored in M2 and M3 appears in the ranked table with a numeric composite score and an explicit rank.
  - The Methodology section states the exact formula and weights used to combine M2 and M3 inputs into the composite score, such that an evaluator could recompute any single row's score by hand from the underlying M2/M3 values.
  - Every row's "key red flags" entry is traceable to a specific score or ratio in the M2 or M3 artifacts (no flag without an underlying datum).
  - The ranking order is internally consistent with the composite scores (higher concern ranked worse).
  - The Limitations section names at least 4 concrete threats to validity (e.g. small sample, denominator-choice sensitivity, FAP text vs. actual practice gap, filing-year staleness, hospitals excluded for missing documents) and states explicitly that low scores reflect public-document deficiencies, not proven failure to deliver care.
  - The artifact names its three intended audiences (state AGs, IRS TE/GE, advocacy groups) and states, in one or two sentences each, what action the scorecard enables for them.
