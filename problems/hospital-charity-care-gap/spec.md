# Spec: Charity care that nonprofit hospitals are legally required to give — and mostly don't

## Objective
"Unstuck" for this problem means producing the missing artifact named in the brief: a comprehensive, hospital-by-hospital, FAP-text-level compliance and inaccessibility scorecard for a defined set of US nonprofit hospitals, built entirely from public text (FAPs, Plain Language Summaries, Form 990 Schedule H, the IRC 501(r) rule). Today only aggregate statistics exist; no one has published a named, sourced, criterion-by-criterion map regulators can act on. The end artifact serves enforcement and advocacy actors — state attorneys general, the IRS TE/GE division, and groups like Dollar For and the Lown Institute — who can act on a named list of specific hospitals but cannot act on a national average. Each milestone moves from codifying the legal standard, to fixing a reproducible sample and source set, to scoring FAP accessibility, to layering in Schedule H spending, to assembling the ranked scorecard with explicit limitations.

## Milestones

### M1: Codify the 501(r) scoring rubric from the legal text
- **Task:** Read the governing legal sources (IRC Section 501(r), the implementing Treasury regulations, and the brief's cited authorities) and translate the financial-assistance requirements into a machine-checkable rubric of scoring criteria, each with an explicit pass/fail or graded definition and a citation to the rule it derives from.
- **Skill:** none — freeform
- **Artifact format:** A criteria table with columns: criterion ID, criterion name, what-to-look-for (the exact textual signal in a FAP/PLS that satisfies it), scoring scale (binary or 0-2 graded with each level defined), and source citation (statute/reg section or named report). Include a short "scope and exclusions" note stating which 501(r) requirements are in scope and which are excluded as not detectable from public text.
- **Done-criteria:**
  - The rubric contains at least 6 distinct criteria, and explicitly includes: (a) whether presumptive eligibility is offered, (b) the free-care income threshold relative to Federal Poverty Level, (c) whether the FAP/summary is publicly posted vs. application-gated, and (d) plain-language accessibility.
  - Every criterion has a citation to a specific legal source (501(r) subsection, a Treasury reg section, or a named report from problem.md), with at least 4 distinct sources cited across the rubric.
  - Every criterion's scoring scale is defined so that two readers applying it to the same FAP text would assign the same score (each scale level has a written definition, no bare adjectives like "good" or "adequate").
  - The scope note names at least 2 specific 501(r) requirements deliberately excluded as not detectable from public text, with a one-line reason for each.

### M2: Fix the hospital sample and locate each hospital's source documents
- **Task:** Define a reproducible sample of named US nonprofit hospitals/systems to score, and for each one locate the URLs of its public FAP, its Plain Language Summary, and its most recent Form 990 Schedule H (or the filing source), recording what was and was not found.
- **Skill:** none — freeform
- **Artifact format:** A sampling-method paragraph (how the list was chosen, stated so it is reproducible — e.g. "the N largest nonprofit systems by revenue per [named source]") followed by a source-inventory table with columns: hospital/system name, state, FAP URL, Plain Language Summary URL, Schedule H / Form 990 source URL, and a found/not-found/paywalled status flag for each of the three document types.
- **Skill input:** uses the scope of detectable signals defined in M1 to confirm the right document types are being collected.
- **Done-criteria:**
  - The sample contains at least 15 distinct named hospitals or hospital systems, each with its state.
  - The sampling method is stated explicitly enough that a reader could reconstruct the same list (a named selection rule and source, not "a selection of hospitals").
  - Every row has a status flag (found / not-found / paywalled) for each of the three document types; no status cells are blank.
  - At least 80% of rows have a working, hospital-specific FAP or Plain Language Summary URL (not a generic hospital homepage), and every listed URL resolves to a document of the type claimed.

### M3: Score FAP accessibility and compliance per hospital
- **Task:** Apply the M1 rubric to each hospital's FAP and Plain Language Summary located in M2, producing a per-hospital score on every criterion with a short text justification and the exact source supporting each non-trivial score.
- **Skill:** none — freeform
- **Artifact format:** A scoring matrix: one row per hospital, one column per M1 criterion, each cell holding the score plus a brief (<= 25 word) justification quoting or paraphrasing the FAP language that drove it; plus a per-hospital total/subscore. Hospitals from M2 whose documents were not found are listed in a separate "could not score" section with the reason.
- **Skill input:** M1 rubric (criteria and scales) and M2 source inventory (which hospitals and which URLs).
- **Done-criteria:**
  - Every hospital from M2 with a found FAP/Plain Language Summary is scored on every M1 criterion; the count of scored hospitals plus the count in "could not score" equals the M2 sample size.
  - Each scored cell cites the specific document (FAP or PLS) the score was read from; for the presumptive-eligibility and income-threshold criteria specifically, the justification quotes or paraphrases the actual policy text, not just a yes/no.
  - Scores use only the scales defined in M1 (no out-of-scale or invented values).
  - At least one criterion shows variation across hospitals (not every hospital identical), demonstrating the rubric discriminates rather than rubber-stamping.

### M4: Layer in Schedule H charity-care spending versus peers
- **Task:** For each scored hospital, extract reported charity-care spending and a revenue/expense denominator from its Form 990 Schedule H (located in M2), compute a charity-care intensity ratio, and flag hospitals spending far below the sample's distribution.
- **Skill:** none — freeform
- **Artifact format:** A table with columns: hospital, charity-care dollars (with Schedule H line reference and fiscal year), denominator used (e.g. total functional expenses or total revenue, named), charity-care-as-percent-of-denominator ratio, and a peer-relative flag (e.g. below the sample 25th percentile). Include a one-paragraph note on the comparability limits of Schedule H figures.
- **Skill input:** M2 source inventory (Schedule H locations) and the M3 hospital list.
- **Done-criteria:**
  - Every hospital with a found Schedule H in M2 has a charity-care dollar figure, a named denominator, a computed ratio, and a fiscal year; hospitals without a found Schedule H are explicitly marked "not available," not silently dropped.
  - Each charity-care dollar figure cites a specific Schedule H part/line and the filing year, so the number is traceable to the source document.
  - The peer-relative flag is defined by a stated rule (e.g. a named percentile or threshold of the sample distribution) and applied consistently to every hospital with data.
  - The comparability note names at least 2 specific reasons Schedule H charity-care figures are imperfectly comparable across hospitals.

### M5: Assemble the ranked non-compliance / inaccessibility scorecard
- **Task:** Combine the M3 accessibility scores and M4 spending flags into a single ranked scorecard naming specific hospitals from best to worst on combined accessibility-and-spending, with a transparent weighting and a standalone limitations section, packaged for a regulator or advocate to act on.
- **Skill:** none — freeform
- **Artifact format:** A ranked master table (one row per hospital, ordered by combined score) with columns surfacing the M3 total, the M4 ratio and flag, and the combined rank; a short methodology box stating exactly how rank was computed and weighted; a "most actionable targets" shortlist of the lowest-scoring named hospitals with a one-line reason each; and a dedicated limitations section.
- **Skill input:** M3 scoring matrix and M4 spending table.
- **Done-criteria:**
  - Every hospital scored in M3 appears exactly once in the ranked table with an explicit rank; no duplicates and no scored hospital omitted.
  - The methodology box states the exact formula/weighting used to combine M3 and M4 into the rank, such that a reader could recompute any hospital's combined score from the M3 and M4 numbers in the table.
  - The "most actionable targets" shortlist names at least 5 specific hospitals and ties each to a concrete weakness (e.g. "no presumptive eligibility AND charity-care ratio below sample 25th percentile").
  - The limitations section states at least 4 specific limitations, including sample-coverage bias, Schedule H comparability, FAP-text-as-of date / staleness risk, and at least one stated reason the scorecard should not be read as a final legal determination of non-compliance.
