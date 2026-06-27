# Spec: phantom-data-center-load

## Objective
"Unstuck" means producing the first defensible, bottom-up reconciliation of *announced* versus *likely-real* US data-center electric load — a quantified "phantom fraction" (announced/queued load that will never materialize), built from named primary sources, broken out by RTO/ISO where the data allows, and converted into implied generation over-build (GW) and ratepayer cost exposure ($). The end artifact serves FERC and the RTOs writing post-2026 large-load interconnection rules, state PUCs ruling on cost-allocation and IRP-approval dockets now, and the funders/researchers (LBNL, RMI, Brattle, WRI, SELC) who can extend or contest the number. Success is a falsifiable national estimate with an explicit method, sourced inputs, and a stated uncertainty range — something a skeptical regulator could adopt or rebut on the merits rather than on anecdote.

## Milestones

### M1: Evidence base — the phantom signal across sources
- **Task:** Assemble a sourced evidence dossier of every public, quantified data point bearing on the gap between announced/queued data-center load and load that actually materializes — completion/withdrawal rates, duplicate-filing evidence, announced-vs-building gaps, and utility-stated materialization fractions.
- **Skill:** none — freeform
- **Artifact format:** A table of evidence rows (columns: claim/metric, numeric value with units, geography/RTO if any, source organization, publication/document title, year, direct URL) plus a short "what this implies for the phantom fraction" note per cluster of rows; closes with a gaps/limitations section.
- **Done-criteria:**
  - At least 15 distinct quantified data points, each with a specific numeric value and a working source URL (no "various" or unsourced figures).
  - Includes, at minimum: the LBNL *Queued Up: 2025 Edition* historical completion/withdrawal rates, at least one utility-stated materialization fraction (e.g., Exelon ~22%), and at least one announced-vs-building gap figure (e.g., Sightline 12 GW vs 5 GW).
  - At least 3 distinct RTO/ISO or utility territories are represented among the data points (e.g., PJM, ERCOT, a CenterPoint/Exelon territory).
  - Every numeric claim is attributed to a named organization and a dated document; the limitations section names at least 3 specific data gaps or inconsistencies.

### M2: Method — an explicit phantom-fraction estimation framework
- **Task:** Using the M1 dossier, define a transparent, reproducible method for converting raw queued/announced data-center load into an estimate of likely-real load, specifying each discount factor (historical completion rate, duplicate/double-counting, missing site control or offtake) and how they compose.
- **Skill:** none — freeform
- **Artifact format:** A method document: numbered steps, an explicit formula or decision-tree for going from gross queued GW to net expected GW, a parameter table (each discount factor with its assumed value/range and the M1 source justifying it), and a worked numeric example on one RTO.
- **Done-criteria:**
  - Names at least 3 distinct discount/adjustment factors, each with a quantified value or range and a citation to a specific M1 row or source.
  - States the composition rule explicitly (e.g., the formula or sequence by which factors combine) so a third party could reproduce the calculation.
  - Includes one fully worked numeric example: a stated gross queued GW for a named RTO, the factors applied, and the resulting net expected GW.
  - Explicitly addresses double-counting risk (announced vs. under-construction vs. queued) and states how the method avoids counting the same load twice.
  - Lists at least 3 method limitations or assumptions that could bias the estimate, with the direction of bias noted.

### M3: National + by-RTO phantom-fraction estimate
- **Task:** Apply the M2 method to the best available queued/announced data-center load figures to produce a national phantom-fraction range and a per-RTO breakdown wherever the underlying data supports one.
- **Skill:** none — freeform
- **Artifact format:** A ranked/structured table (columns: RTO/ISO or "National", gross announced/queued data-center GW with source, factors applied, net expected GW, implied phantom GW, phantom fraction as a %), with a low/central/high range for the national number and a narrative explaining the spread; plus a limitations section.
- **Done-criteria:**
  - Reports a national phantom-fraction estimate as an explicit low/central/high range (three numbers, in %), each traceable to M2 factors and M1 inputs.
  - Provides a per-RTO or per-territory breakdown for at least 3 named RTOs/ISOs/utilities, each with its gross GW source cited.
  - Every gross GW input figure carries a source URL or document reference; every derived number can be reconstructed from the M2 method.
  - The arithmetic is internally consistent (per-row: net + phantom = gross, within rounding) and at least one row is spot-checkable against its stated factors.
  - Limitations section states which RTOs could not be broken out and why, and flags the single largest source of uncertainty in the national number.

### M4: Ratepayer cost exposure and decision-relevant framing
- **Task:** Translate the M3 phantom GW into implied generation/transmission over-build and an order-of-magnitude ratepayer cost-exposure estimate, then frame the findings against the live FERC/RTO and state-PUC decisions the brief names.
- **Skill:** none — freeform
- **Artifact format:** A briefing document: a cost-exposure table (phantom GW from M3 → assumed $/kW or $/MW-year build cost with source → implied $ exposure, with low/high bounds), a short section mapping each finding to a specific pending decision (FERC 2026 large-load hand-off, named RTO rule processes, state cost-allocation/IRP dockets), and a caveats section.
- **Done-criteria:**
  - Converts at least the central national phantom-GW figure from M3 into a dollar cost-exposure range, with every conversion assumption ($/kW, capacity-auction $, or transmission cost) carrying a cited source.
  - Cost figures are presented as a bounded range (low/high), not a single point, and the calculation chain from phantom GW to dollars is shown.
  - Explicitly cites the M3 artifact as its input and does not introduce a new phantom-fraction number inconsistent with M3.
  - Names at least 2 specific live decisions (e.g., FERC's 2026 RTO hand-off, a named state PUC docket or RTO large-load rule process) and states what the estimate implies for each.
  - Caveats section states at least 3 reasons the cost figure is an order-of-magnitude estimate rather than a precise forecast.
