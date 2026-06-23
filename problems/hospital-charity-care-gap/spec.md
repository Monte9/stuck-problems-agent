# Spec: Charity care that nonprofit hospitals are legally required to give — and mostly don't

## Objective
"Unstuck" looks like a named, hospital-by-hospital scorecard that turns the diffuse, well-documented aggregate failure (71% of eligible patients billed, ~$14B/yr in care that should be charity) into a checkable list of specific institutions whose Financial Assistance Policies (FAPs), Plain Language Summaries (PLS), and Schedule H charity-care spending fall short of IRC Section 501(r) intent. The end artifact serves regulators who can act on names rather than statistics: the IRS TE/GE division (audit targeting), state Attorneys General (consumer-protection and nonprofit-oversight authority), and advocacy groups like Dollar For and the Lown Institute (campaign and navigation targeting). The chain builds a defensible scoring rubric, applies it to a fixed sample of hospitals using only public text, cross-references charity-care spending against revenue, and produces the ranked scorecard plus a method-and-limitations writeup that survives a hostile read by a hospital's general counsel.

## Milestones

### M1: Build the scoring rubric and fix the hospital sample
- **Task:** Define a transparent, machine-checkable scoring rubric for FAP/PLS accessibility and 501(r) compliance (drawing on the actual 501(r) regulatory requirements and Dollar For / Lown / CFPB criteria), and select a fixed, reproducible sample of nonprofit hospitals to score in later milestones.
- **Skill:** none — freeform
- **Artifact format:** A markdown document with (a) a rubric table: each scoring dimension as a row with columns Dimension, What it measures, How scored (point values / thresholds), Public source it is read from, and the 501(r) or advocacy basis; (b) a named, numbered list of the sample hospitals (target 20-40) with city/state, parent system, and the URL or filing where their FAP/PLS/Schedule H will be found; (c) a short sampling-rationale section.
- **Done-criteria:**
  - The rubric contains at least 6 distinct scoring dimensions, each citing a specific 501(r) provision (e.g. 501(r)(4) FAP requirements, widely-available-policy rules) or a named external source (Dollar For, Lown, CFPB) for why it matters.
  - Each rubric dimension states an explicit, near-binary or numeric scoring rule (e.g. "income eligibility threshold >=200% FPL = full points; 138-199% = partial; <138% or unstated = zero"), not a subjective adjective.
  - The sample lists at least 20 named, real US nonprofit hospitals, each with a working URL or EIN/filing reference where its FAP or PLS can be located.
  - The sampling rationale states how hospitals were chosen (e.g. geography, system size, mix of states including NC) and acknowledges what the sample is and is not representative of.

### M2: Extract and score FAP / Plain Language Summary text for the sample
- **Task:** For each hospital in the M1 sample, retrieve its FAP and Plain Language Summary from public sources and apply the M1 rubric, recording the evidence (quoted text or specific location) behind every score.
- **Skill:** none — freeform
- **Artifact format:** A per-hospital scoring table (one row per hospital) with one column per M1 rubric dimension holding the assigned score, plus an evidence column or linked appendix giving a short verbatim quote or precise location (page/section/URL) supporting each non-trivial score, and a total accessibility/compliance score per hospital.
- **Done-criteria:**
  - Every hospital from the M1 sample appears as a row; hospitals whose FAP/PLS could not be located are explicitly marked "not found" with the search attempted, not silently dropped.
  - Every dimension score for every located hospital is backed by a verbatim quote or a precise source location (URL plus section/page), so an evaluator can re-check it.
  - Scores are computed using the exact rubric rules from M1 (same dimensions, same point values); any deviation is flagged and justified.
  - A per-hospital total score is present and its arithmetic matches the component scores.

### M3: Cross-reference Schedule H charity-care spending against revenue
- **Task:** For the same sample hospitals (or the subset with available filings), pull Form 990 Schedule H figures for charity care / financial assistance and total functional expenses or patient revenue, and compute a charity-care-as-share-of-expense (or revenue) ratio to flag systems spending far below peers.
- **Skill:** none — freeform
- **Artifact format:** A table with columns: hospital, EIN, filing year, charity care at cost ($), total expenses or net patient revenue ($), charity-care ratio (%), and a peer-relative flag (e.g. quartile or below-median marker), plus a short note on which Schedule H line items were used.
- **Done-criteria:**
  - Each row cites the specific Form 990 Schedule H filing (year and source, e.g. ProPublica Nonprofit Explorer or IRS, with the exact line items used) so the dollar figures are traceable.
  - The charity-care ratio is computed consistently for every hospital using the same numerator and denominator definition, stated once in the note.
  - Hospitals missing a usable filing are listed as "filing unavailable" with the source checked, not omitted.
  - At least one peer-relative comparison (median, quartile, or ranking) is present so low spenders are identifiable, not just listed in isolation.

### M4: Assemble the ranked non-compliance / inaccessibility scorecard
- **Task:** Combine the M2 accessibility/compliance scores and M3 charity-care ratios into a single ranked scorecard naming the hospitals most likely to be under-serving eligible patients, with a transparent combination method and an explicit limitations section.
- **Skill:** none — freeform
- **Artifact format:** A ranked table (worst first) with columns: rank, hospital, state, M2 accessibility/compliance score, M3 charity-care ratio and peer flag, a combined concern score or tier, and the single most actionable issue per hospital; followed by a method section (how the two inputs were weighted/combined) and a limitations section.
- **Done-criteria:**
  - Every hospital scored in both M2 and M3 appears in the ranking; hospitals scored in only one are either included with the gap noted or explicitly listed as excluded with the reason.
  - The combination method is stated explicitly (weights or tiering rules) and the final rank order is consistent with applying that stated method to the M2 and M3 inputs.
  - Each ranked row names one concrete, citable issue traceable back to an M2 quote or M3 figure (e.g. "application-only, no presumptive eligibility; charity care 0.4% of expenses, bottom quartile").
  - The limitations section names at least three specific threats to validity (e.g. sample size/selection, filing-year mismatches, FAP text not reflecting actual screening practice, "not found" hospitals) and states which regulator each tier of the scorecard is most actionable for.
