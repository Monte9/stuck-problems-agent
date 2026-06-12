# State: fishing-dark-fleets

status: awaiting_review
current_milestone: 1
attempt: 0

## Next action

M1 artifact exists at `artifacts/2026-06-12-m1-open-data-source-inventory.md`. The next run matches decision table row 3: the evaluator judges it against the M1 done-criteria and writes a verdict to `verdicts/`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-12 — generator ran on M1: wrote `artifacts/2026-06-12-m1-open-data-source-inventory.md`, a 28-row verified inventory (Combined IUU Vessel List + 7 individual RFMO lists, GFW SAR detections dataset/APIs, Tokyo & Paris MOU PSC databases, ownership registries, OFAC/CBP forced-labor lists, EU carding record, 4 subsidy-disclosure channels), every row fetched live on 2026-06-12 with demonstrated-pull status, plus 7-item gaps section and limitations. Notable: detection data is wide open but attribution-side sources are closing to automation (OpenCorporates hCaptcha, OECD 403, EUR-Lex bot-blocking); NAFO/OFAC downloads were clean and fresh; one IUU Watch PDF link had rotted to an unrelated image. Status set to awaiting_review.
- 2026-06-12 — planner ran: wrote spec.md with 5 milestones (M1 open-data source inventory with demonstrated-fetch requirement; M2 consolidated deduplicated IUU vessel ledger, >=100 vessels with hard identifiers; M3 beneficial-owner league table extending FTC's "ten companies" analysis with confidence labels and a quantified attribution gap; M4 DG MARE carding dossier ranking >=15 flag states with yellow-card candidates; M5 WTO Article 3 subsidy-to-operator docket with dual sourcing and temporal-overlap flags). No skills exist yet, so all milestones are freeform. Status set to in_progress, cursor at M1.
- 2026-06-12 — scout ran: sourced "dark fleets — deaths and forced labor in industrial fishing" (domain: frontier expansion — oceans; 100,000+ fishing deaths/yr and 128,000 in forced labor at sea; detection solved and open via GFW's 2024 Nature SAR mapping, but ownership data exists for only 16% of IUU-implicated vessels, leaving the WTO Fisheries Subsidies Agreement (Sept 2025) and EU CATCH system (Jan 2026) inert against anonymous operators; wedge: owner-attribution league table + DG MARE carding dossier + WTO Article 3 subsidy docket — the methane plumes-to-names playbook at sea). Winner of a 4-candidate slate scored against PREFERENCES.md (runners-up: remittance fees 6/10, hearing loss→dementia 6/10, pig-butchering compounds 5/10 — partially disqualified as actively being solved). Brief written to problem.md; awaiting planner.
