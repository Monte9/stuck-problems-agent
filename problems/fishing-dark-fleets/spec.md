# Spec: fishing-dark-fleets

## Objective
"Unstuck" means converting publicly available detection and listing data into named accountability: a consolidated ledger of IUU-listed and dark-fleet vessels, an ownership league table that pierces vessel anonymity where public records allow, a flag-state risk dossier usable by DG MARE for the next carding round and CATCH risk-flagging, and a subsidy-to-operator docket that gives the WTO Fisheries Subsidies Agreement's Article 3 prohibition its first concrete targets. The end artifacts serve three audiences: DG MARE (the only binding market lever), WTO member delegations and the WTO Secretariat's fisheries committee, and the NGO attribution community (GFW Joint Analytical Cell, Financial Transparency Coalition, EJF) who can carry findings into formal channels. Everything is desk attribution over open data — the agent cannot board a vessel, but it can end the anonymity the business model depends on.

## Milestones

### M1: Open-data source inventory and access map
- **Task:** Build a verified inventory of every publicly reachable data source needed for vessel attribution: RFMO IUU vessel lists (and the TMT/IMCS Combined IUU Vessel List), GFW open datasets and APIs, port state control detention databases (Tokyo MOU, Paris MOU, others), corporate/beneficial-ownership registries (OpenCorporates, national registries), sanctions and forced-labor lists (OFAC, CBP WROs), EU carding decisions, and known subsidy disclosures. For each, record what it contains, how to access it without credentials the agent lacks, and confirm it is live as of the run date.
- **Skill:** none — freeform
- **Artifact format:** Table with columns: source name, URL, maintainer, access method (direct download / web page / API / behind login), key fields available (vessel identifiers, ownership, flag, dates), last-updated date as verified during the run, and intended use in M2–M5. Plus a short "gaps" section listing data that is referenced in the literature but not publicly reachable.
- **Done-criteria:**
  - At least 15 distinct sources listed, including at minimum: the Combined IUU Vessel List (or each major RFMO list individually), GFW's SAR vessel-detection dataset page, at least two port state control MOU databases, OpenCorporates, and the EU's IUU carding decision record.
  - Every row has a working URL that was fetched during the run, with the verification date stated.
  - Every row states the access method and whether the agent can actually pull records from it (yes/no/partial) — no source marked usable without a demonstrated fetch.
  - The gaps section names at least 3 known data limitations (e.g., beneficial-ownership coverage, AIS gaps) with a citation each.

### M2: Consolidated dark-fleet vessel ledger
- **Task:** Using the M1 inventory, compile a single deduplicated ledger of vessels currently on RFMO IUU lists or the Combined IUU Vessel List, enriched where possible with identifiers and history (IMO number, MMSI, current and former names, current and former flags, listing RFMO(s), listing date, last known status).
- **Skill:** none — freeform
- **Artifact format:** Markdown table (one row per vessel) with columns: vessel name(s), IMO/MMSI if available, flag (current/former), listing body, listing date, listing reason, source citation. Followed by a methodology section (dedup rules, how conflicts between lists were resolved) and a limitations section.
- **Done-criteria:**
  - At least 100 distinct vessels in the ledger, each carrying at least one hard identifier (IMO number) or, where the vessel has no IMO, name plus flag plus listing body.
  - Every row cites the specific list (with URL) where the vessel appears; at least 90% of rows cite a list that was verified live in M1.
  - Vessels appearing on multiple RFMO lists are merged into one row with all listing bodies shown — spot-checking 5 known cross-listed vessels finds no duplicates.
  - Methodology section states the retrieval date of each source list used and the dedup keys applied.

### M3: Beneficial-owner league table
- **Task:** Attribute owners and operators to the M2 ledger vessels using corporate registries, FTC's "Fishy Networks" findings, TMT/GFW vessel records, court and detention records, and investigative reporting; then rank companies and individuals by number of implicated vessels, replicating and extending the FTC's "ten companies own a quarter of IUU vessels" analysis with current data.
- **Skill:** none — freeform
- **Artifact format:** Ranked table with columns: rank, owner/operator name, jurisdiction of incorporation, number of implicated vessels (with vessel names/IMOs from M2), evidence type (registry record / NGO report / court record / press), confidence label (confirmed / probable / reported-only), citations. Plus a section quantifying the attribution gap (how many M2 vessels remain ownerless and why) and a limitations section.
- **Done-criteria:**
  - At least 10 owners/operators ranked, each linked to at least one specific M2 vessel by name or IMO.
  - Every owner row has at least 2 independent citations, except rows explicitly labeled "reported-only," which must have at least 1 and be visually distinguished.
  - Every attribution carries an explicit confidence label; no row mixes confirmed and reported-only evidence without saying which claim rests on which source.
  - The attribution-gap section states the exact count and percentage of M2 vessels with no identified owner.
  - No owner is named on the strength of a single uncorroborated press article — checkable by inspecting the citations of every "confirmed" row.

### M4: DG MARE carding dossier — flag-state risk ranking
- **Task:** Produce an evidence dossier ranking flag states that export seafood to the EU by dark-fleet activity and forced-labor risk, drawing on the M2 ledger (vessels per flag), the M3 ownership findings, GFW's published dark-activity and forced-labor-risk statistics, EU carding history, and CATCH-relevant trade exposure — structured as the evidence base for the next yellow-card round.
- **Skill:** none — freeform
- **Artifact format:** Ranked table of flag states with columns: state, current EU card status, IUU-listed vessels flagged (from M2), published dark-activity indicators (with source), forced-labor risk indicators (with source), EU import exposure, recommended action (candidate for yellow card / monitor / no action) with one-sentence justification. Plus a methodology section explaining the ranking weights and a section comparing the ranking against the EU's existing carding decisions (where it agrees, where it diverges and why).
- **Done-criteria:**
  - At least 15 flag states ranked; every cell that contains a number or status carries a citation.
  - Each state's current EU card status (green/yellow/red/delisted, with year) is stated and sourced from Commission records.
  - At least 3 states are flagged as yellow-card candidates, each with a justification that cites at least 2 distinct evidence types (e.g., M2 vessel count plus forced-labor indicator).
  - The divergence section explicitly names at least one state where this ranking disagrees with current EU carding status and explains the disagreement.
  - A limitations section addresses at least: EU import-data gaps, the reliability of forced-labor risk models, and flag-hopping.

### M5: WTO Article 3 subsidy-to-operator docket
- **Task:** Trace publicly documented fisheries subsidy programs (EU funds, Chinese fuel/distant-water subsidies, others found in M1 sources) to specific operators or owners appearing in M2/M3, producing a docket of concrete subsidy-to-IUU-operator links that a WTO member or the Secretariat's fisheries committee could act on under Article 3 of the Fisheries Subsidies Agreement.
- **Skill:** none — freeform
- **Artifact format:** Docket with one entry per link: subsidy program (name, granting authority, legal basis, amount if published), recipient operator (cross-referenced to M3 rank and M2 vessels), the IUU determination that triggers Article 3 (which list, which authority, date), evidence chain with citations, and confidence label. Plus a section quoting the relevant Article 3 text and explaining the notification/transparency mechanism (Article 8) a member would use, and a limitations section on temporal mismatch (subsidy date vs. listing date) and evidentiary thresholds.
- **Done-criteria:**
  - At least 3 distinct subsidy-to-operator links documented, each with at least 2 independent sources on the subsidy side and a citation to the operator's IUU listing or M3 entry.
  - Each link states the dates of both the subsidy and the IUU determination, and flags explicitly whether they overlap (Article 3 bites on subsidies to operators engaged in IUU fishing, so timing matters).
  - Article 3's prohibition text is quoted verbatim with a citation to the WTO treaty text, and the docket explains in concrete steps how a member state would raise these cases.
  - Every link carries a confidence label; any link resting on a single investigative report is labeled "reported-only" and excluded from the headline count of 3.
  - A limitations section addresses at least: subsidy opacity in the largest subsidizing states, beneficial-ownership layering between recipient and operator, and what the docket cannot prove from open sources.
