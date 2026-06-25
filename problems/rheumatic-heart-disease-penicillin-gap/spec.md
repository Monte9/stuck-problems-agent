# Spec: Rheumatic heart disease — the penicillin gap

## Objective
"Unstuck" for this problem means producing the named, sourced supply-and-coverage map that does not currently exist at actionable specificity: a desk-research dossier that tells a funder, procurement agency, or health ministry exactly where benzathine penicillin G (BPG) prophylaxis for rheumatic heart disease is failing, why, who makes the molecule, what inaction costs in lives and dollars per country, and how to rebut the safety fear that suppresses use. The end artifact serves three audiences: a funder (CHAI/Gates-style) deciding where a marginal dollar buys the most averted death; a national health ministry deciding whether to keep a prophylaxis register running despite a rare-reaction advisory; and an RHD-advocacy researcher (Reach, World Heart Federation) who needs the gap laid out in one place to lobby from. Every milestone is pure synthesis over published GBD estimates, national register reports, WHO/UNICEF stockout surveys, the GOAL trial, and the AHA advisory — no new data collection, no lab work.

## Milestones

### M1: Country-by-country RHD coverage-and-stockout scorecard
- **Task:** Build a ranked scorecard of the highest-burden RHD countries cross-referencing GBD prevalence/mortality, documented secondary-prophylaxis coverage (from national registers and published surveys), and documented BPG stockout/shortage events, producing a per-country "gap" picture.
- **Skill:** none — freeform
- **Artifact format:** Ranked table, one row per country (>= 15 countries, prioritized by RHD burden), with columns: country; RHD prevalence (count + per-100k, with GBD year); annual RHD deaths; secondary-prophylaxis coverage figure if any (% receiving >=80% scheduled doses, or stated "no register/no data"); most recent documented BPG stockout or shortage (year + one-line description, or "none documented"); citation(s). Plus a methods note stating which GBD release and definitions were used, and a limitations section.
- **Done-criteria:**
  - Table has >= 15 country rows, each ranked or sortable by a stated burden metric.
  - Every prevalence and mortality figure carries an inline citation to GBD or a named published source, with the data year given.
  - Every coverage cell either cites a specific register/survey source or explicitly states "no data / no register," with no blank cells.
  - At least 5 countries have a documented stockout/shortage event with year and source; countries with none say "none documented" rather than being left blank.
  - A limitations section names at least 3 concrete data-quality caveats (e.g. GBD modeling uncertainty, register selection bias, coverage definitions differing across sources).

### M2: BPG supply-chain concentration map
- **Task:** Map the global BPG supply chain end to end — surviving active-pharmaceutical-ingredient (API) makers, finished-dose manufacturers/suppliers, and the chronology of known shortage events — to expose single points of failure.
- **Skill:** none — freeform
- **Artifact format:** A structured brief with (a) a named list/table of currently identifiable BPG API manufacturers and the country each is in; (b) a list/table of major finished-dose (e.g. Bicillin L-A and generic equivalents) suppliers by region; (c) a dated timeline of documented shortage/stockout events (>= 8 entries) with country/region and source; (d) a short "single-point-of-failure" analysis paragraph; plus a limitations/uncertainty section flagging where the count of manufacturers is unverifiable.
- **Done-criteria:**
  - Names >= 3 specific API manufacturers (or states explicitly and with a source that the public count is exactly N and why more cannot be confirmed), each with a citation.
  - Lists >= 5 named finished-dose suppliers or products with regions and citations.
  - Shortage timeline has >= 8 dated entries, each with a year, a place, and a source link.
  - Contains an explicit statement of the global demand-vs-need gap (e.g. CHAI's doses-demanded vs doses-needed figures) with citation.
  - Limitations section flags at least 2 specific points where manufacturer identity or counts could not be independently confirmed.

### M3: Deaths-and-dollars cost-of-inaction model
- **Task:** Using the M1 scorecard as the burden input and the GOAL trial effect size as the efficacy input, compute a transparent per-country estimate of deaths/progression events avertable by closing the prophylaxis gap and the drug cost of doing so.
- **Skill:** none — freeform
- **Artifact format:** A table (one row per country drawn from M1, >= 15 countries) with columns: at-risk/eligible population basis used; current coverage assumption; GOAL-derived relative risk reduction applied; estimated annual progression events or deaths avertable; estimated annual BPG dose count needed; estimated annual drug cost at a stated $/dose. Accompanied by a clearly written "assumptions and formula" box and a sensitivity paragraph showing how the headline number moves under a low/high efficacy or coverage assumption.
- **Done-criteria:**
  - Every computed cell is reproducible from numbers stated in the artifact: the formula, the GOAL effect size (with citation), the $/dose (with citation), and the burden figure (cite M1) are all shown.
  - The GOAL trial figures used (0.8% vs 8.3% progression, ~tenfold reduction) are quoted with their source and the relative risk reduction is derived explicitly, not asserted.
  - Country rows match the country set used in M1 (>= 15), and the artifact names M1 as its burden source.
  - A sensitivity section gives at least a low/base/high range for the headline avertable-deaths and total-cost numbers.
  - An assumptions box lists every simplifying assumption (e.g. extrapolating latent-disease GOAL effect to established RHD, static population, full adherence) — at least 4 assumptions stated.

### M4: Benefit-harm dossier inverting the injection-reaction scare
- **Task:** Draft the ministry-facing benefit-harm dossier that places the rare fatal BPG injection reaction (per the 2022 AHA advisory) against the GOAL/M3 benefit arithmetic, so a program manager can justify continuing prophylaxis.
- **Skill:** none — freeform
- **Artifact format:** A decision-grade memo with: (a) a plain summary of the documented harm — what the AHA 2022 advisory actually reported (reaction type, populations at risk, estimated incidence) with citation; (b) a side-by-side benefit-vs-harm comparison drawing the benefit figure from M3; (c) a short, sourced section of mitigation practices (e.g. supervised administration, contraindications, who is genuinely at higher risk); (d) an explicit number-needed-to-treat vs number-needed-to-harm framing; (e) a limitations section. Written for a non-specialist health official.
- **Done-criteria:**
  - Accurately states what the 2022 AHA presidential advisory reported, including the at-risk population it actually flagged (severe/advanced RHD), with a citation — not a generalized "penicillin is dangerous" claim.
  - Presents a quantified benefit-vs-harm comparison that explicitly cites M3 for the benefit side and a sourced incidence figure for the harm side.
  - Includes at least 3 sourced, concrete mitigation/administration practices.
  - States a number-needed-to-harm-style figure (or explains why it cannot be precisely computed and gives bounds) alongside the benefit, so the asymmetry is legible.
  - Limitations section acknowledges at least 2 caveats (e.g. under-reporting of reactions, applicability of GOAL latent-disease data to symptomatic patients).
