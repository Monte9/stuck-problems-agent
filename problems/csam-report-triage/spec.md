# Spec: CSAM Report Triage — converting 21M CyberTipline reports into a ranked rescue docket

## Objective
"Unstuck" means producing the triage-design document the under-resourced actors (NCMEC, the ICAC Task Forces, and the platforms that file reports) cannot write themselves: a concrete, sourced specification for grading report quality, scoring the senders who generate noise, and ranking the resulting queue toward children in imminent danger — together with a map of which fixes need only NCMEC/platform action versus an act of Congress. The end artifact serves three audiences: a congressional staffer or funder deciding what to appropriate and what to legislate; NCMEC and platform engineers building the triage layer; and the law-enforcement receivers who need a defensible prioritization signal. Every claim is desk forensics on public artifacts (the SIO blueprint, 18 U.S.C. 2258A, published transparency reports, NCMEC's 2025 data, the Amazon-1.1M episode) — no law-enforcement data, no non-public data, no human action.

## Milestones

### M1: Report-quality rubric from the SIO blueprint and statute
- **Task:** Build a scored rubric defining what a "complete" CyberTipline report contains, deriving each criterion from a specific provision of 18 U.S.C. 2258A and/or a specific recommendation in the SIO 2024 report, and assigning each criterion a weight and a near-binary scoring test.
- **Skill:** none — freeform
- **Artifact format:** A rubric table with columns: criterion, what-it-checks, source (statute subsection or SIO page/section), weight, and a binary or short-scale scoring test. Plus a "statutory floor vs. quality ceiling" subsection separating what the statute mandates from what SIO recommends beyond it, and a limitations section.
- **Done-criteria:**
  - The rubric covers, at minimum, the "who, what, where, when" completeness dimensions named in the SIO blueprint, plus a deduplication/novelty dimension and a sender-verification dimension.
  - Every criterion cites a specific source locus: a subsection of 18 U.S.C. 2258A (e.g., 2258A(b) elements) or an identifiable section/page of the SIO 2024 report; no criterion is uncited.
  - Each criterion has a scoring test phrased so two evaluators scoring the same report would agree (binary present/absent or a defined 0-2 scale with anchors), not a subjective adjective.
  - A subsection explicitly distinguishes the statutory minimum (what a platform must include to satisfy the law) from the SIO-recommended quality target.

### M2: Per-sender noise-tax / quality scorecard
- **Task:** Synthesize published platform transparency reports, NCMEC's 2025 CyberTipline data, and the Amazon AI Services 1.1M-report episode into a per-sender scorecard quantifying report volume against report quality / actionability, applying the M1 rubric dimensions where data allows.
- **Skill:** none — freeform
- **Artifact format:** A ranked sender table with columns: sender/platform, reported volume (with year and source), an actionability or quality indicator, the "noise tax" interpretation, and source citation per row. Plus a narrative quantifying the headline GAI noise inversion (1.1M Amazon reports with no actionable info vs. ~200k actionable AI reports buried beneath) and a methodology/limitations section.
- **Done-criteria:**
  - Every numeric figure (report counts, file counts, referral counts, per-sender volumes) carries an inline citation to a named public source (NCMEC 2025 blog, a specific platform transparency report, SIO, Thorn, or IWF) and a year.
  - The scorecard ranks at least 5 distinct senders/platforms, and explicitly includes the Amazon AI Services 1.1M episode as a worked example of the noise tax.
  - The artifact reuses at least three M1 rubric dimensions as the quality axis (rather than inventing a new, uncited quality definition), and names which rubric dimensions cannot be scored from public data and why.
  - A methodology section states, for each quality indicator, whether it is directly reported, derived, or estimated, so a skeptic can see which numbers are inferred.

### M3: Prioritization / ranking feature schema with legal-admissibility constraints
- **Task:** Draft the documented feature set for ranking the report queue toward rescuable children — including imminent-danger keyword signals, novel-vs-known-hash status, jurisdiction signals, and sender reliability (drawn from the M2 scorecard) — with each feature's legal-admissibility and Fourth-Amendment / private-search constraints spelled out.
- **Skill:** none — freeform
- **Artifact format:** A feature-schema table with columns: feature name, signal it captures, data source / where it comes from in a report, ranking direction (raises or lowers priority), and admissibility/legal constraint. Plus a worked scoring example ranking 3-5 hypothetical reports, and a limitations section.
- **Done-criteria:**
  - The schema includes at least the four signal families named in the brief: imminent-danger keywords, novel-vs-known-hash status, jurisdiction signals, and sender reliability — and the sender-reliability feature explicitly references the M2 scorecard as its input.
  - Every feature has an admissibility/legal-constraint cell that names a concrete doctrine or statute (e.g., the private-search doctrine, government-agent question, 2258A reporting-vs-search distinction, NCMEC's legal status), not a generic "may have legal issues."
  - A worked example ranks 3-5 hypothetical reports and shows the per-feature contribution to each rank, so the ranking is reproducible from the schema rather than asserted.
  - The artifact flags which features risk introducing bias or de-prioritizing real victims (e.g., over-trusting hash-known status, language coverage of keyword lists) in a dedicated subsection.

### M4: Fix-ownership map — NCMEC/platform action vs. statute
- **Task:** Map each problem and proposed fix from M1-M3 to the actor who can implement it and the lever required, separating fixes achievable by NCMEC or platform action alone from those requiring an act of Congress (statutory amendment, appropriation).
- **Skill:** none — freeform
- **Artifact format:** A map table with columns: fix (tracing back to an M1/M2/M3 element), owner, lever (operational change / contract / appropriation / statutory amendment), why it is blocked today, and source for the ownership claim. Plus a one-page executive summary aimed at a congressional staffer, and a limitations section.
- **Done-criteria:**
  - Every row traces to a specific element produced in M1, M2, or M3 (named explicitly), so the map is a synthesis of prior artifacts rather than new freeform claims.
  - Each fix is classified into exactly one of: NCMEC-only, platform-only, NCMEC+platform, or requires-Congress — and the requires-Congress rows name the specific statutory provision (18 U.S.C. 2258A subsection) or appropriation that would change.
  - At least one fix is correctly attributed to each of the two top-level categories (achievable without Congress vs. requires Congress), and the SIO "fund and modernize NCMEC" recommendation is placed in the appropriations lever with citation.
  - The executive summary states, in under one page, the noise-tax cost (from M2) and the single highest-leverage fix, with the trade-off named.
