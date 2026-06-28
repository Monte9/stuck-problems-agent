# State: antivenom-efficacy-ledger

status: no_spec
current_milestone: 0
attempt: 0

## Next action

A fresh brief exists (`problem.md`) but no `spec.md` yet. The next run matches decision table row 1: the planner subagent turns the brief into a 3-6 milestone research spec with checkable done-criteria, writes `spec.md`, and the orchestrator sets `status: in_progress`, `current_milestone: 1`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-28 — scout ran (decision table row 5 — all prior problems published/dropped, no active problem). Sourced a new stuck problem in the welfare lane (global health): **antivenom-efficacy-ledger** — a large share of antivenom sold across sub-Saharan Africa is of unknown or proven-poor efficacy against the snakes that bite there, while snakebite kills ~32,000 and disables ~100,000 people a year in the region; products documented "as useless as water" remain on shelves and Kenya already recalled India-made antivenoms that failed in the field. The bottleneck is verification and transparency, not invention: only 3 of ~10 African-use antivenoms have robust clinical data, several were raised against non-African venoms, and no actor publishes a consolidated, head-to-head, venom-by-venom efficacy ledger. Shape = **the investigation** (name which marketed products fail against which snakes; not yet a published shape in the roster), a pure desk-research wedge (a public product-by-species efficacy matrix with an evidence grade per cell), with a named decision-maker (WHO TAG-SAIL + national procurement regulators) who can act within a year. Scored 9/10, winning a 5-candidate slate (2 frontier + 3 welfare, spanning four shapes; see `[scout]` commit body). Wrote only `problem.md` (611 words, cited throughout). Orchestrator created this `state.md` with `status: no_spec`. Next run plans it.
