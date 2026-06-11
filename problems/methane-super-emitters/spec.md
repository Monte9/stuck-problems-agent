# Spec: Methane super-emitters — ending the anonymity that lets leaks persist

## Objective
"Unstuck" means converting open plume detections into named accountability artifacts that someone with leverage can act on without further research: a named-operator super-emitter league table (including who ignores MARS alerts), an EU-importer methane-intensity dossier keyed to the EU Methane Regulation's importer requirements that bind in January 2027, and a country-ranked no-net-cost abatement list that reconciles IEA model numbers with what satellites actually see. The end artifact serves two audiences: regulators (DG ENER implementing the import standard; national regulators receiving MARS notifications) and advocacy/funder organizations (CATF, EDF, Global Methane Hub) who need a citable, source-linked dossier rather than raw plume coordinates. The agent cannot fix a compressor seal; it can produce the attribution-and-ranking synthesis nobody is staffed to do.

## Milestones

### M1: Open-data landscape inventory
- **Task:** Catalog every open dataset and published table usable for plume detection, facility attribution, alert-response tracking, EU import flows, and abatement economics — and record exactly how each is accessed and what fields it exposes.
- **Skill:** none — freeform
- **Artifact format:** Inventory table with columns: dataset name, publisher, URL, access method (download / portal / published report table), temporal coverage, geographic coverage, key fields, attribution granularity (plume / facility / operator / country), update cadence, license/access caveats. Followed by a "gaps and limitations" section and a short "recommended primary sources per downstream milestone (M2–M4)" mapping.
- **Done-criteria:**
  - At least 8 distinct datasets/sources cataloged, including at minimum: UNEP IMEO/MARS public data, Carbon Mapper data portal, a Sentinel-5P-derived super-emitter product (e.g., SRON weekly list), IEA Global Methane Tracker downloadable data, and at least one EU gas-import statistics source (Eurostat, ENTSOG, or equivalent).
  - Every row has a working URL verified during the session (fetched, not assumed) and a stated access method.
  - Each row states attribution granularity explicitly (plume / facility / operator / country).
  - The artifact maps each of M2, M3, and M4 to at least two named primary sources from the table.
  - A limitations section names at least three concrete gaps (e.g., MethaneSAT loss, paywalled GHGSat data, lag in MARS response reporting).

### M2: Named-operator super-emitter league table
- **Task:** Using the sources mapped in M1, build a ranked table of the largest publicly detected oil-and-gas super-emitter events or persistent sources from 2024–2026, attributing each to a named operator and country where public data allows, and flagging MARS notification/response status where published.
- **Skill:** none — freeform
- **Artifact format:** Ranked table with columns: rank, date(s) observed, country, location/basin, facility (if identifiable), operator (named, or "unattributed" with stated reason), estimated emission rate with units, detecting instrument/platform, source citation(s), MARS-notified (yes/no/unknown), response status. Followed by a methodology section (attribution rules, ranking basis) and a limitations section.
- **Done-criteria:**
  - At least 20 rows, all dated 2024-01-01 or later, all from the oil-and-gas sector.
  - Every row cites at least one public detection record or published report with a URL.
  - Every row either names an operator or carries an explicit "unattributed" entry with a one-line reason; at least 10 rows name a specific operator or state-owned company.
  - At least 5 rows carry a sourced statement about MARS notification or operator response status (including documented non-response).
  - Methodology section states the ranking basis (emission rate, persistence, or both) and the attribution evidence standard; limitations section addresses at least: detection bias by satellite coverage, rate-estimate uncertainty, and ownership ambiguity.

### M3: EU-importer methane dossier
- **Task:** Build the dossier DG ENER needs for the importer requirements binding January 2027: EU gas imports (pipeline and LNG) by exporting country and, where public data allows, by supplying company, matched to the best available measured or estimated methane intensity and to each exporter's MRV/reporting status (e.g., OGMP 2.0 membership level).
- **Skill:** none — freeform
- **Artifact format:** Table with columns: exporting country, 2024 and/or 2025 import volume to EU with citation, share of EU imports, main supplying companies (where public), methane intensity estimate with citation and basis (measured vs. inventory vs. modeled), OGMP 2.0 / MRV reporting status, super-emitter events from the M2 artifact attributable to that country. Followed by a section summarizing the EU Methane Regulation importer requirements and timeline, and a limitations section. Names the M2 artifact path as input.
- **Done-criteria:**
  - Country rows collectively cover at least 90% of EU gas import volume for 2024 or 2025, with the coverage percentage computed and stated against a cited total.
  - Every country row has an import-volume citation and either an intensity estimate with citation or an explicit "no public measured estimate" entry.
  - Every country row states OGMP 2.0 (or equivalent MRV) participation status with a citation.
  - At least 5 country rows cross-reference specific events from the M2 league table.
  - The regulation section cites the EU Methane Regulation (Regulation (EU) 2024/1787) directly and states which obligations bind importers in 2027, with at least one citation to the current state of the "simplification" lobbying fight.

### M4: No-net-cost abatement ranking reconciled with observations
- **Task:** Produce a country-ranked list of fossil-methane abatement opportunity using the IEA Methane Abatement Model's open data, and reconcile it against the observational record (M2) — flagging where satellite-observed emissions suggest the model under- or overstates a country's problem.
- **Skill:** none — freeform
- **Artifact format:** Ranked table with columns: country, estimated oil-and-gas methane emissions (Mt, with citation), total abatable volume, no-net-cost abatable volume, headline abatement measures, count and total estimated rate of M2-observed events, divergence note (model vs. observation), citation(s). Followed by a "top 10 highest-leverage country actions" narrative and a limitations section. Names the M2 and M3 artifact paths as inputs.
- **Done-criteria:**
  - At least 15 countries ranked, including all countries that appear in 3 or more M2 rows.
  - Every quantitative cell carries a citation to IEA data or another named public source; no unsourced numbers.
  - Every country row contains an explicit divergence note (even if "consistent" or "no observational coverage").
  - At least 3 countries are flagged where observed super-emitter activity is high but the country has weak or no MRV commitments per M3, each flag supported by both artifacts.
  - Limitations section addresses at least: IEA model vintage and assumptions, satellite coverage bias, and the difference between event-based rates and annualized totals.

### M5: Synthesis brief — "Plumes to names, names to enforcement"
- **Task:** Write the end artifact for regulators and advocates: a policy brief that integrates M2–M4 into a concrete enforcement case — who the worst actors are, which lever reaches each one (EU import standard, MARS escalation, financier pressure), and what DG ENER and advocacy groups should do before January 2027.
- **Skill:** none — freeform
- **Artifact format:** Brief of at most 3,500 words: one-page executive summary; "the league table" section (top findings from M2); "the import lever" section (M3); "the cheapest fixes nobody makes" section (M4); a recommendations section with named addressees; a counterarguments section; full source list. Names the M1–M4 artifact paths as inputs.
- **Done-criteria:**
  - Executive summary fits on one page (under 500 words) and contains at least 3 specific named operators or exporting countries with the lever that reaches each.
  - Every factual claim in the body carries an inline citation to a primary source or to a specific row/section of the M2–M4 artifacts.
  - Recommendations section contains at least 5 recommendations, each naming a specific actor (e.g., DG ENER, UNEP IMEO, a named NGO or funder) and an action checkable in principle within 12 months.
  - Counterarguments section addresses at least: the industry "simplification" push on the EU Methane Regulation, attribution-uncertainty objections to naming operators, and the 2025 US enforcement rollback — each with a sourced response.
  - No claim presents pre-2025 enforcement conditions (e.g., the US waste emissions charge, MethaneSAT) as currently in force.
