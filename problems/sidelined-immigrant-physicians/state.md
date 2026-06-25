# State: sidelined-immigrant-physicians

status: in_progress
current_milestone: 1
attempt: 0

## Next action

Spec is written (`spec.md`, 4 milestones, all freeform). Status is `in_progress` on milestone 1. The next run matches decision table row 2: the generator executes M1 (the 50-state provisional-licensure crosswalk) and writes one artifact to `artifacts/`, then sets `status: awaiting_review`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-25 — planner ran (decision table row 1 — no `spec.md`). Turned the brief into `spec.md` with 4 sequential milestones: M1 50-state provisional-licensure crosswalk (51 rows: status + core requirements + sponsor-eligibility clause, cited per state) → M2 stranding-defect analysis (classify each enacted/proposed law for supply-capping provisions like Tennessee's teaching-hospital sponsor tie) → M3 county-level HPSA shortage / sidelined-IMG match (state-by-state estimate of physicians a clean statute could unlock, plus a top-10 leverage list) → M4 model-bill redline + board-rulemaking comment (fixes the Tennessee defect, legislator/board-actionable). Skills library is empty (README only), so every milestone is freeform. Set `status: in_progress`, `current_milestone: 1`, `attempt: 0`.
- 2026-06-25 — scout ran (decision table row 5 — all prior problems published/dropped, no active problem). Sourced a new stuck problem from the only uncovered roster category, #6 demography (migration, with an aging-demand driver): **sidelined-immigrant-physicians** — "brain waste" in the middle of a US doctor shortage (up to 86,000-physician shortfall by 2036 driven by aging, while ~65,000 fully-trained foreign physicians are barred by rule from practicing; all-occupation immigrant brain waste ~$39B/yr in foregone wages). The fix is proven and cheap (Tennessee's 2023 first-in-nation provisional-license law; ≥9 states enacted, ~30 with bills) but stuck on institutional inertia: the residency-program-sponsor requirement confines eligible jobs to urban teaching hospitals (only ~2% of Medicare-funded residency sits in rural/underserved areas), board rulemaking stalled, and the federal Healthcare Workforce Resilience Act keeps failing to pass. Bottleneck is misaligned incentives + a residency-cartel supply cap, not capability or safety data. Clean desk wedge: a 50-state provisional-licensure crosswalk + county HPSA-to-sidelined-IMG match + model-bill redline — the document that does not yet exist. Scored 9/10, winning a 5-candidate slate (see `[scout]` commit body). Wrote only `problem.md`. Orchestrator created this `state.md` with `status: no_spec`. Next run plans it.
