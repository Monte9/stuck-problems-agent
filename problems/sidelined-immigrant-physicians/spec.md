# Spec: the sidelined immigrant physician (brain waste in a doctor shortage)

## Objective
"Unstuck" means producing the synthesis that lets the next ~40 states adopt a provisional-licensure pathway for internationally-trained physicians *without* repeating Tennessee's stranding defect (the teaching-hospital-sponsor tie that confines eligible jobs to urban academic centers). The end artifact is a decision-ready packet: a 50-state crosswalk of provisional-licensure rules that names the specific stranding provisions in each enacted/proposed law; a county-level shortage match that quantifies how many sidelined IMGs a clean statute could unlock and where; and a model-bill redline plus board-rulemaking comment a legislator or medical board could act on within a single legislative session. It serves state legislators and medical boards (who need copyable, defect-free language), advocacy coalitions (Niskanen, Cicero, Upwardly Global, AMA/FSMB) building campaigns, and funders deciding where a dollar of advocacy unlocks the most clinical capacity.

## Milestones

### M1: 50-state provisional-licensure crosswalk
- **Task:** Build a single table covering all 50 states (plus DC) that records, for each state, the current status of an IMG provisional/alternative-pathway licensure law (enacted with year / bill introduced with number / none) and the core requirements (ECFMG certification, USMLE steps required, foreign residency or years-of-practice required, supervision term, sponsor-eligibility clause). Cite a primary or authoritative secondary source per state.
- **Skill:** none — freeform
- **Artifact format:** Wide markdown table, one row per state/DC (51 rows), with columns: State, Status (enacted-YYYY / introduced-billno / none), ECFMG req, USMLE steps req, Foreign-residency-or-practice req, Supervision term, Sponsor-eligibility clause, Source URL. Followed by a "Sources & method" section and a "Limitations / staleness" note.
- **Done-criteria:**
  - All 51 rows present (50 states + DC); no row left entirely blank.
  - Every row with Status other than "none" has at least one source URL in the Source column.
  - At least the nine states the brief cites as having enacted laws are marked enacted, and Tennessee's row explicitly records the residency-program/teaching-hospital sponsor requirement in the Sponsor-eligibility column.
  - A dated "Limitations / staleness" note states when the legislative tracking was current and which states' statuses are uncertain.

### M2: Stranding-defect analysis
- **Task:** Using the M1 crosswalk as input, classify each state's enacted or proposed law by whether it contains one or more "stranding" provisions (teaching-hospital/residency-program sponsor tie, narrow specialty list, sponsor-must-be-academic, excessively long supervision term, or other supply-capping clause) and explain why each named provision limits placement in shortage areas.
- **Skill:** none — freeform
- **Artifact format:** A ranked/grouped markdown table (input: M1 artifact) with columns: State, Stranding provision(s) present, Provision type/tag, Mechanism (one sentence on how it caps supply), Severity (high/medium/low/none), Source. Plus a short prose section defining each provision-type tag and a "clean-statute" reference description (what a defect-free law looks like).
- **Done-criteria:**
  - Every state marked "enacted" or "introduced" in the M1 artifact appears with a stranding-provision classification (including "none found").
  - Each provision-type tag used is defined once in the definitions section.
  - Every claim that a specific state's law contains a stranding provision carries a citation (statute section or secondary source).
  - Tennessee is classified "high" severity with the teaching-hospital/residency-program sponsor tie named as the mechanism.

### M3: County-level shortage / sidelined-IMG match
- **Task:** Combine HPSA / physician-shortage-area data with available estimates of the sidelined-IMG population (national and, where obtainable, by state/metro) to produce a state-by-state estimate of how many additional physicians a clean provisional-licensure statute could plausibly unlock and where the need is greatest. State assumptions explicitly.
- **Skill:** none — freeform
- **Artifact format:** Markdown table, one row per state, with columns: State, HPSA count or shortage-area population, Estimated sidelined IMGs (with basis), Shortage-severity rank, Plausible unlocked-physician estimate, Assumptions/notes, Source(s). Plus a "Methodology & assumptions" section and a "Top-10 highest-leverage states" summary.
- **Done-criteria:**
  - One row per state (50 rows) with a HPSA/shortage figure and a sidelined-IMG estimate (or an explicit "no state-level estimate available; derived from national figure via X" note).
  - Every quantitative estimate is traceable to a cited source or a stated arithmetic assumption shown in the Methodology section (no unsourced/unexplained numbers).
  - A "Top-10 highest-leverage states" list ranks states by combined shortage severity and sidelined-IMG supply, with the ranking rule stated.
  - The Methodology section names every external dataset used (e.g., HRSA HPSA, AAMC, MPI brain-waste) with access date.

### M4: Model-bill redline and board-rulemaking comment
- **Task:** Draft (a) a redline of provisional-licensure statute language that fixes the Tennessee defect — broadening sponsor eligibility beyond residency-operating teaching hospitals — and (b) a board-rulemaking comment a medical board could adopt to implement the pathway without stalling, both grounded in the M2 defect analysis and M3 leverage findings.
- **Skill:** none — freeform
- **Artifact format:** Single markdown document with two parts: Part A, a model-bill redline showing struck/inserted language (clearly marked, e.g., ~~struck~~ / **inserted**) against a baseline (Tennessee or a named clean state) with a per-change rationale; Part B, a board-rulemaking comment letter with specific recommended rule provisions. Plus a one-page "why this matters" framing citing M3's leverage estimate.
- **Done-criteria:**
  - Part A explicitly strikes or rewrites the teaching-hospital/residency-program sponsor tie and shows replacement sponsor-eligibility language, with a rationale referencing the M2 stranding analysis.
  - Every substantive redline change has a one-line rationale.
  - Part B contains at least three concrete, numbered recommended rule provisions addressing implementation (e.g., timelines for board action, supervision definitions, sponsor approval criteria).
  - The framing section cites a specific number from the M3 artifact for unlocked physicians (national or named-state) and names the intended audience (legislator and/or board).
