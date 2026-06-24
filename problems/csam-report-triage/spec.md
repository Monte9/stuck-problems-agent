# Spec: CSAM Report Triage — turning 21M CyberTipline reports into a ranked rescue docket

## Objective
"Unstuck" means producing the triage-design package that the under-resourced actors in the child-exploitation reporting pipeline cannot write for themselves: a defensible, citation-grounded set of desk-research artifacts that (1) define what a complete, actionable CyberTipline report contains, (2) quantify the per-sender "noise tax" that buries live-victim cases, (3) specify an implementable prioritization feature schema for ranking a rescue queue with legal-admissibility constraints made explicit, and (4) sort every proposed fix into "NCMEC/platform can do this today" versus "requires statutory change." The end artifact serves policy staff and funders (Congress / appropriators deciding whether to fund NCMEC), NCMEC and platform engineers building triage tooling, and the Internet Crimes Against Children (ICAC) law-enforcement teams who receive the referrals. Every claim must be traceable to a public source so a skeptical regulator or funder can audit it.

## Milestones

### M1: Report-quality rubric grounded in SIO blueprint + 18 U.S.C. 2258A
- **Task:** Build a scoring rubric that defines what a "complete" CyberTipline report contains, derived from the SIO 2024 report's "who/what/where/when" standard and the specific fields named or implied by 18 U.S.C. 2258A; assign weights and a 0–100 completeness score per dimension.
- **Skill:** none — freeform
- **Artifact format:** A markdown document with (1) a rubric table — columns: dimension, description, statutory/SIO basis with citation, weight, and how the dimension is scored (e.g. present/partial/absent); (2) a worked example scoring a hypothetical high-quality report and a hypothetical low-quality "noise" report; (3) a limitations section.
- **Done-criteria:**
  - The rubric has at least 6 distinct scoring dimensions and the weights sum to 100.
  - At least 4 of the rubric's dimensions cite a specific provision of 18 U.S.C. 2258A (subsection-level, e.g. (b)(1), (c)) or a named recommendation from the SIO 2024 report.
  - Two worked examples are scored end-to-end, each producing a numeric 0–100 total that follows from the per-dimension scores shown.
  - A limitations section names at least 3 concrete ways the rubric could mis-score real reports.

### M2: Per-sender noise-cost scorecard ("the noise tax")
- **Task:** Using public platform transparency reports, NCMEC 2024/2025 data, and the Amazon AI Services 1.1M-report episode, build a per-sender scorecard that quantifies report volume against report quality/actionability and estimates the triage burden ("noise tax") imposed on NCMEC and law enforcement. Apply the M1 rubric's logic where sender-level field data is available.
- **Skill:** none — freeform
- **Artifact format:** A ranked table — one row per named sender/platform — with columns: sender, reporting volume (with year and source), an actionability or quality indicator (with source), a noise-tax characterization (qualitative or, where defensible, an estimate with stated assumptions), and a citation per row. Plus a short methods note stating which numbers are reported facts versus estimates, and a limitations section.
- **Done-criteria:**
  - The table contains at least 8 sender/platform rows, including the Amazon AI Services 1.1M no-actionable-information episode as an explicit row.
  - Every quantitative cell (volume, actionability) carries a citation to a public source (transparency report, NCMEC data, SIO, or equivalent), with the URL given.
  - The methods note explicitly distinguishes reported figures from the author's estimates, and every estimate states its assumptions.
  - Senders are ranked by a stated noise-tax criterion, and the ranking logic is described in one sentence a reader can re-apply.
  - A limitations section names at least 3 data-availability gaps (e.g. senders that publish no field-level quality data).

### M3: Prioritization / triage feature schema for ranking the rescue queue
- **Task:** Design a documented feature schema that ranks incoming reports into a rescue-priority queue, covering at minimum imminent-danger signals, novel vs. known-hash status, jurisdiction signals, and sender reliability (consuming the M2 scorecard as the sender-reliability input). Define each feature's data source, value range, and contribution to a priority score.
- **Skill:** none — freeform
- **Artifact format:** A markdown spec with (1) a feature table — columns: feature name, what it captures, data source/where it comes from in a report, value type/range, direction and weight of its effect on priority, and rationale; (2) a stated scoring/ranking function combining the features; (3) at least 3 illustrative reports scored and ranked using the schema.
- **Done-criteria:**
  - The feature table covers all four named signal families (imminent-danger, novel-vs-known-hash, jurisdiction, sender reliability) plus at least 2 additional features, each with a named data source.
  - The sender-reliability feature explicitly references and consumes the M2 scorecard output.
  - A ranking function is stated explicitly enough that two readers given the same three example reports would produce the same ordering.
  - At least 3 example reports are scored and ranked, and the resulting order is consistent with the stated function.
  - Each feature row states whether its value is available at intake or requires enrichment/lookup.

### M4: Legal-admissibility constraints on the triage schema
- **Task:** Document the legal-admissibility and Fourth Amendment / private-search-doctrine constraints that bound how the M3 schema may be built and used (e.g. NCMEC/government-agent status, viewing vs. hash-matching, chain of custody, the private-search doctrine and warrant requirements), and annotate which M3 features or scoring steps are affected by each constraint.
- **Skill:** none — freeform
- **Artifact format:** A markdown document with (1) a constraints table — columns: legal constraint, source (case name/citation or statute), what it restricts, and which M3 feature(s) or processing steps it touches; (2) a per-feature "admissibility note" appended to or cross-referenced against the M3 feature list; (3) a limitations/uncertainty section flagging unsettled or circuit-split areas.
- **Done-criteria:**
  - The constraints table has at least 5 distinct legal constraints, each citing a specific case (with name) or statute provision.
  - At least one constraint addresses the private-search doctrine / Fourth Amendment treatment of platform-flagged content (e.g. Ackerman, Wilson, or equivalent), with a citation.
  - Every M3 feature is explicitly mapped to either "no admissibility constraint identified" or at least one named constraint.
  - The limitations section names at least 2 areas of legal uncertainty or jurisdictional variation (e.g. a circuit split).

### M5: Fix-attribution map — NCMEC/platform action vs. statutory change
- **Task:** Synthesize the proposed fixes surfaced across M1–M4 (quality standards, deduplication, prioritization tooling, sender accountability, admissibility safeguards) into a single map that sorts each fix by who can implement it: NCMEC/platform action alone, versus action requiring statutory or regulatory change. Cite the basis for each attribution.
- **Skill:** none — freeform
- **Artifact format:** A two-axis table or matrix — one row per fix — with columns: fix, which M1–M4 artifact it derives from, actor(s) who must move, "implementable today vs. needs statutory change" classification with one-line justification, and a citation or cross-reference. Plus an executive summary (under 400 words) for a policy/funder audience and a limitations section.
- **Done-criteria:**
  - The map contains at least 10 distinct fixes, each cross-referenced to the M1, M2, M3, or M4 artifact it derives from.
  - Every fix is classified as "implementable today (NCMEC/platform)" or "needs statutory/regulatory change," with a one-line justification each.
  - At least 3 fixes are attributed to statutory change and at least 3 to platform/NCMEC action (i.e. the map is not trivially one-sided).
  - The executive summary is under 400 words and names the single highest-leverage fix in each of the two categories.
  - A limitations section names at least 2 fixes whose actor-attribution is genuinely ambiguous and explains why.
