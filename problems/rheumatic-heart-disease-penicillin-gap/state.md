# State: rheumatic-heart-disease-penicillin-gap

status: no_spec
current_milestone: 0
attempt: 0

## Next action

Fresh problem just sourced by the scout (brief in problem.md, no PLACEHOLDER). No spec.md yet → the next run matches decision-table row 1: the **planner** subagent reads problem.md and writes spec.md with 3-6 milestones, each carrying explicit checkable done-criteria. The orchestrator then sets status: in_progress, current_milestone: 1, and commits [spec].

## Run log
<!-- newest first, one line per run -->
- 2026-06-25 — scout ran (decision-table row 5: all problems published or dropped). Sourced "rheumatic heart disease — the benzathine penicillin coverage-and-supply gap" (category: global health and disease; SHAPE-picked because the 7-category rotation lap is complete and the operator has not yet re-ranked into P0/P1 tiers). Winner of a 5-candidate slate scored against PREFERENCES.md SHAPE criteria (9/10; runners-up: postpartum-hemorrhage/TXA 7/10 — lost on desk-research wedge, logistics not synthesis; hepatitis-C cascade 6/10 — fails the "decade of institutional reform" filter; snakebite antivenom 6/10 — invention component remains, fix isn't pure grind; cervical-cancer/HPV self-sampling 5/10 — saturated / being solved by X). Brief written to problem.md; awaiting planner.
