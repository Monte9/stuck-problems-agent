# State: sidelined-immigrant-physicians

status: in_progress
current_milestone: 1
attempt: 0

## Next action

Spec is written (`spec.md`, 4 milestones M1–M4). Decision table row 2 matches next run: the generator executes the current milestone (M1 — dissect the Tennessee defect and define the "strand-the-law" taxonomy) and writes one artifact to `artifacts/`, then `status: awaiting_review`.

## Milestones (from spec.md)
- M1: Anchor case — dissect the Tennessee defect and define the "strand-the-law" taxonomy
- M2: 50-state crosswalk of provisional-licensure rules (coded to M1 taxonomy)
- M3: County HPSA-to-sidelined-IMG match — quantify the unlock
- M4: Model-bill redline + board-rulemaking comment that fixes the defect

## Run log
<!-- newest first, one line per run -->
- 2026-06-25 — planner ran (decision table row 1 — brief present, no `spec.md`). Wrote `spec.md`: 4 milestones building M1 taxonomy → M2 50-state crosswalk → M3 HPSA-to-IMG unlock estimate → M4 model-bill redline + rulemaking comment. All freeform (skills library empty). Set `status: in_progress`, `current_milestone: 1`. Next run generates M1.
- 2026-06-25 — scout ran (decision table row 5 — all prior problems published/dropped, no active problem). Sourced a new stuck problem from the only uncovered roster category, #6 demography (migration, with an aging-demand driver): **sidelined-immigrant-physicians** — "brain waste" in the middle of a US doctor shortage (up to 86,000-physician shortfall by 2036 driven by aging, while ~65,000 fully-trained foreign physicians are barred by rule from practicing; all-occupation immigrant brain waste ~$39B/yr in foregone wages). The fix is proven and cheap (Tennessee's 2023 first-in-nation provisional-license law; ≥9 states enacted, ~30 with bills) but stuck on institutional inertia: the residency-program-sponsor requirement confines eligible jobs to urban teaching hospitals (only ~2% of Medicare-funded residency sits in rural/underserved areas), board rulemaking stalled, and the federal Healthcare Workforce Resilience Act keeps failing to pass. Bottleneck is misaligned incentives + a residency-cartel supply cap, not capability or safety data. Clean desk wedge: a 50-state provisional-licensure crosswalk + county HPSA-to-sidelined-IMG match + model-bill redline — the document that does not yet exist. Scored 9/10, winning a 5-candidate slate (see `[scout]` commit body). Wrote only `problem.md`. Orchestrator created this `state.md` with `status: no_spec`. Next run plans it.
