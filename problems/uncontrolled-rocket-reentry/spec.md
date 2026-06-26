# Spec: uncontrolled rocket-body reentries

## Objective
"Unstuck" means producing the attribution document that today does not exist: a public, per-launch-vehicle reentry-compliance and exported-risk ledger covering abandoned rocket bodies of the past decade. It must classify each rocket body as controlled vs. uncontrolled, estimate per-reentry casualty risk, attribute aggregate risk by operator / vehicle family / launching state, overlay ground-track probability against population and airspace to show which countries bear risk they did not create, and rank which vehicle families to target. The end artifact serves regulators and standards bodies (FAA, ICAO, UN COPUOS) and the campaigners pushing the controlled-reentry treaty (Outer Space Institute) — parties who have the published safety threshold and the proven fix but lack the named, priced evidence base to move the standard from recommendation to enforceable rule. Each milestone is pure desk synthesis on open catalogs and published models; nothing requires lab work, human action, or non-public data.

## Milestones

### M1: Methodology and source register
- **Task:** Establish the analytic backbone for the whole ledger: define the study window, the unit of analysis (an abandoned rocket body / upper stage that reentered or remains in orbit), the controlled-vs-uncontrolled classification rule, the casualty-risk model and its inputs, and the canonical open data sources to be used downstream.
- **Skill:** none — freeform
- **Artifact format:** A reference document with: (1) a sourced list of open catalogs and datasets with URLs and what field each provides (e.g. satellite/reentry catalog, dry-mass references, gridded population, airport/airspace data); (2) a written classification rule distinguishing controlled from uncontrolled reentry with the observable signals used to decide each; (3) the casualty-risk formula adopted, written out with every variable defined and a published-paper citation; (4) a stated scope (date window, inclusion/exclusion of payloads vs. stages) and a numbered limitations list.
- **Done-criteria:**
  - Every named data source has a working URL and a one-line statement of which downstream field it supplies.
  - The casualty-risk formula is written explicitly (not just named) with each variable defined and at least one peer-reviewed or agency citation for it.
  - The controlled-vs-uncontrolled classification rule lists the concrete signals used to decide and states how ambiguous/unknown cases are handled.
  - Scope is pinned to an explicit date window and an explicit unit-of-analysis definition; a numbered limitations section lists at least 3 distinct caveats.

### M2: Per-rocket-body classified inventory
- **Task:** Using the M1 register and rules, build the row-level inventory of abandoned rocket bodies in the study window, each labeled controlled or uncontrolled, with the attributes needed for risk estimation (mass, vehicle family, operator, launching state, reentry date/status).
- **Skill:** none — freeform
- **Artifact format:** A table — one row per rocket body — with at minimum: identifier (e.g. NORAD/COSPAR), vehicle family, operator, launching state, dry/reentry mass (with source), launch date, reentry date or "still in orbit," and controlled/uncontrolled label. Plus a coverage note stating how many bodies the window contains, how many are included, and why any are excluded.
- **Done-criteria:**
  - Each row carries a controlled/uncontrolled label assigned by the M1 rule, with a per-row source or basis for mass and for the control label (citation or catalog reference).
  - The classification rule and risk-model inputs cited are the ones defined in M1 (the artifact names M1 as its input and does not introduce a new method silently).
  - The artifact states a total population count for the window and reconciles it against the included rows (included + excluded = total, with exclusion reasons given).
  - At least one independent published statistic is cited as a sanity check on the inventory's scale (e.g. count of uncontrolled reentries or returned mass for a stated year).

### M3: Per-reentry casualty risk and accountability attribution
- **Task:** Apply the M1 casualty-risk model to each uncontrolled body in the M2 inventory to produce a per-reentry risk figure, then aggregate to rank operators, vehicle families, and launching states by total casualty risk and by compliance gap (share exceeding the 1-in-10,000 threshold).
- **Skill:** none — freeform
- **Artifact format:** Two ranked tables: (1) per-rocket-body risk (identifier, vehicle family, launching state, estimated per-reentry casualty risk, above/below 1-in-10,000 flag); (2) aggregate attribution ranked by total risk, with columns for vehicle family / operator / launching state, summed risk, share of fleet-wide risk, and count exceeding threshold. Plus a short reconciliation paragraph comparing the top contributors against published shares.
- **Done-criteria:**
  - Every uncontrolled row from M2 has a numeric per-reentry casualty-risk estimate produced by the M1 formula, with the input values used shown or traceable.
  - Each body is flagged above or below the 1-in-10,000 threshold, and the artifact reports the fleet-wide share exceeding it.
  - Aggregate shares (by vehicle family / operator / launching state) sum to ~100% (within a stated rounding tolerance) and the top contributors are explicitly compared to at least one published attribution figure (e.g. the ~62% Chinese / ~18% Russian-Soviet split) with agreement or divergence noted.
  - The artifact names M2 as its input inventory and M1 as its risk model; no body is risk-scored that is absent from M2.

### M4: Exported-risk overlay by country
- **Task:** Overlay uncontrolled-reentry ground-track probability (governed by orbital inclination determining the latitude band of possible reentry) against gridded population and major-airport/airspace exposure to estimate which countries and population centers absorb risk, and contrast that with which launching states generated it.
- **Skill:** none — freeform
- **Artifact format:** A ranked table of exposed countries/major cities with columns for an exposure metric (e.g. relative reentry-overflight likelihood or population-weighted exposure), the dominant contributing vehicle families/inclinations driving that exposure, and a generated-vs-borne comparison flagging mismatches (risk imported but not exported). Plus a methods note on how ground-track probability was derived from inclination and how exposure was weighted by population/airspace.
- **Done-criteria:**
  - The exposure metric is defined and its derivation from orbital inclination + population (and airspace where used) is written out and traceable to the M3 inventory and M1 sources.
  - The table ranks at least 10 countries or major population centers and identifies, for the top entries, the contributing vehicle families/inclinations from M3.
  - A generated-vs-borne comparison is present that explicitly flags at least one case of a state bearing risk it did not create, consistent with the published Global-South-exposure finding (cited).
  - The artifact names M3 (risk-attributed inventory) as its input and states a limitations note covering ground-track approximation and population-grid resolution.

### M5: Ranked accountability docket
- **Task:** Synthesize M1-M4 into the decision-grade docket: rank vehicle families by how much aggregate casualty risk a controlled-deorbit fix would retire, name the noncompliant top targets, and state which states bear exported risk — framed for FAA/ICAO/UN COPUOS action.
- **Skill:** none — freeform
- **Artifact format:** A standalone briefing document with: (1) a ranked "target list" table of vehicle families/operators with risk-retired-if-fixed and current compliance status; (2) a short exported-risk summary naming the most over-exposed states; (3) an explicit feasibility note that the fix (controlled deorbit) is already routine for at least one named compliant vehicle family; (4) a limitations and "what would change the ranking" section.
- **Done-criteria:**
  - The target-list table ranks vehicle families/operators by aggregate risk retired if fixed, every figure traceable to M3, and labels each as currently compliant or not.
  - At least one named vehicle family is cited as an existing-compliance proof-of-concept (controlled deorbit already routine), with a source.
  - The exported-risk summary names specific over-exposed states drawn from M4 and ties them to specific contributing vehicle families.
  - The document includes a numbered limitations section and at least 2 conditions that would materially change the ranking, and it cites M1-M4 as its inputs (no new uncited numbers introduced).
