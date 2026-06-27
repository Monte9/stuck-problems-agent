# Spec: Phantom data-center load

## Objective
"Unstuck" means producing the first defensible bottom-up reconciliation of *announced* versus *real* US data-center electricity demand: a phantom-fraction range by RTO/ISO, an implied over-build figure in GW, and the resulting ratepayer cost exposure in dollars — each number traceable to open, citable sources and bounded with an explicit uncertainty range rather than a false point estimate. The headline forecasts driving gas plant builds, transmission, and double-digit retail price hikes sum un-deduplicated interconnection queues; nobody has published a falsifiable national de-duplicated number. The end artifact serves FERC (writing per-RTO large-load interconnection rules in 2026), the RTOs themselves (PJM, ERCOT), and state PUCs ruling on integrated resource plans (IRPs) and cost-allocation right now. It must be defensible enough that a hostile utility analyst can check every step, and conservative enough that its phantom-fraction range survives that scrutiny. The work is pure desk synthesis on open data; no milestone requires non-public data, lab work, or human action.

## Milestones

### M1: Evidence base and method scaffold
- **Task:** Assemble a sourced inventory of the open datasets and reports needed to estimate phantom data-center load (LBNL *Queued Up: 2025 Edition*, RTO/ISO large-load interconnection reports and queues for at least PJM and ERCOT, relevant state PUC/IRP dockets, and developer/tracker announcements such as Sightline), and define the reconciliation method — i.e., the explicit categories of "phantom" (duplicate filings across territories, projects lacking site control or signed offtake, capacity double-counted between "announced" and "under construction") and how each will be estimated from those sources.
- **Skill:** none — freeform
- **Artifact format:** A source inventory table (columns: source name, publisher, date, URL, geographic/RTO coverage, what variable it supplies, access status verified-reachable yes/no) followed by a "Method" section defining each phantom category, the data signal used to detect it, and the formula linking inputs to the phantom fraction.
- **Done-criteria:**
  - Source inventory lists >= 8 distinct sources, each with a working public URL and a one-line note of what data it supplies; at least PJM and ERCOT are each represented by >= 1 RTO-specific source.
  - LBNL *Queued Up: 2025 Edition* is cited with its specific completion/withdrawal statistics (e.g., the ~13% reached-operation / 77% withdrawn figures) quoted with numbers, not paraphrased loosely.
  - The Method section defines >= 3 distinct phantom categories, and for each names the specific source-derived signal used to detect it and a formula or decision rule (not prose alone) linking inputs to an estimate.
  - Every quantitative claim carries an inline citation to a source in the inventory; no number appears without a source.

### M2: Announced load baseline by RTO
- **Task:** Using the M1 inventory, build the gross "announced" data-center load figure (GW of interconnection requests / large-load queue) for each covered RTO, before any de-duplication, with a clear as-of date and horizon for each number.
- **Skill:** none — freeform
- **Artifact format:** A table with one row per RTO (columns: RTO, announced data-center load GW, as-of date, horizon year, source citation, notes on scope/definition) plus a short reconciliation paragraph explaining definitional differences between RTOs (e.g., large-load queue vs. interconnection request vs. forecast).
- **Done-criteria:**
  - Covers >= 4 RTOs/ISOs including PJM and ERCOT; each row has an announced-load GW figure, an as-of date, and a horizon year.
  - Every announced-load figure cites a source from the M1 inventory (or a clearly-added new source with URL); no figure is unsourced.
  - The reconciliation paragraph explicitly flags at least 2 definitional inconsistencies across RTOs that would otherwise cause double-counting or apples-to-oranges comparison.
  - A clearly-labeled national total (sum of rows) is given, with an explicit statement of what coverage fraction of US load it represents.

### M3: Phantom-fraction estimation by RTO
- **Task:** Apply the M1 method to the M2 announced baselines to estimate, per RTO, a phantom fraction as a low–central–high range, decomposed by phantom category (duplication, no site control/offtake, announced-vs-building double count), anchoring each haircut to a cited benchmark (e.g., LBNL withdrawal rates, Exelon's 22%-materialize statement, CenterPoint 1->25 GW, Sightline 12 GW announced vs 5 GW building).
- **Skill:** none — freeform
- **Artifact format:** A table with one row per RTO (columns: RTO, announced GW from M2, phantom fraction low/central/high, real-load GW low/central/high) plus a per-category breakdown table showing the haircut applied for each phantom category with its anchoring citation, and a "Limitations" subsection.
- **Done-criteria:**
  - Every RTO row gives phantom fraction as an explicit low/central/high range (three numbers), not a single point estimate.
  - Each phantom-category haircut is tied to >= 1 named, cited empirical benchmark; no haircut is asserted without a source anchor.
  - The resulting real-load GW range is arithmetically consistent with the announced GW and the stated fraction (evaluator can recompute from the row's own numbers and reproduce them).
  - The Limitations subsection names >= 3 specific sources of error (e.g., parcel-matching is inferential, queue snapshots are stale, offtake status is often confidential) and states the direction each likely biases the estimate.

### M4: Over-build and ratepayer cost exposure
- **Task:** Translate the M3 real-load ranges into implied generation/transmission over-build (GW built or planned against load that the central/high phantom estimate says will not appear) and into a ratepayer cost-exposure range in dollars, using cited cost anchors (e.g., PJM capacity-auction clearing values, per-kW capacity costs, observed retail-rate increases).
- **Skill:** none — freeform
- **Artifact format:** A table (columns: RTO, implied over-build GW range, cost-exposure $ range, cost basis/citation) plus a transparent worked calculation for at least one RTO showing every input, multiplier, and source, and a "Limitations" subsection.
- **Done-criteria:**
  - Provides an implied over-build GW range and a ratepayer cost-exposure dollar range for >= 3 RTOs including PJM, each as a low/high (or central with range), not a point estimate.
  - At least one RTO has a fully worked calculation where every multiplier and input is shown and individually cited, such that a skeptical evaluator can reproduce the dollar figure by hand from the stated inputs.
  - Cost anchors (e.g., the PJM capacity-auction jump from $2.2B to $16.4B, retail-rate increases, $/kW capacity cost) are quoted with numbers and cited, not paraphrased.
  - The Limitations subsection states >= 2 reasons the cost figure could be over- or under-stated and the direction of each bias.

### M5: Decision-maker briefing and falsifiability
- **Task:** Synthesize M2–M4 into a concise briefing aimed at FERC, RTOs, and state PUCs that states the national phantom-fraction range, the headline over-build and cost-exposure figures, the single most load-bearing assumption, and an explicit "how to falsify this" section telling a critic exactly which numbers to attack and what new data would move the estimate.
- **Skill:** none — freeform
- **Artifact format:** A 1–2 page briefing: an executive summary box with the headline national numbers (phantom fraction range, over-build GW, cost exposure $), a "key findings" list, a "what would change our answer" / falsifiability section, and a one-line takeaway for each audience (FERC, RTO, state PUC).
- **Done-criteria:**
  - States a national phantom-fraction range and national over-build GW and cost-exposure $ figures, each consistent with (recomputable from) the M3/M4 tables.
  - Identifies explicitly the single most load-bearing assumption and quantifies how the headline number moves if that assumption is wrong.
  - The falsifiability section names >= 3 specific, checkable challenges (which number, which source, what new evidence would change it) — phrased so a critic could act on each.
  - Includes a distinct one-line, actionable takeaway addressed to each of FERC, an RTO (PJM or ERCOT), and a state PUC.
  - Every headline number in the executive summary traces back to a cited figure in an earlier milestone artifact; no new unsourced number is introduced.
