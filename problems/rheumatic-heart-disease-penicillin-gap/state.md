# State: rheumatic-heart-disease-penicillin-gap

status: in_progress
current_milestone: 1
attempt: 0

## Next action

Spec written (4 milestones, all "none — freeform"). Status is in_progress at milestone 1 → the next run matches decision-table row 2: the **generator** subagent executes M1 (country-by-country RHD coverage-and-stockout scorecard), writes one artifact to artifacts/, and the orchestrator sets status: awaiting_review.

## Run log
<!-- newest first, one line per run -->
- 2026-06-25 — planner ran (decision-table row 1: no spec.md). Wrote spec.md with 4 milestones: M1 country-by-country RHD coverage-and-stockout scorecard; M2 BPG supply-chain concentration map; M3 deaths-and-dollars cost-of-inaction model (consumes M1 burden + GOAL effect size); M4 benefit-harm dossier inverting the 2022 AHA injection-reaction advisory (consumes M3 benefit arithmetic). All milestones are pure desk synthesis over published data; each carries 4-5 near-binary done-criteria. Set status: in_progress, current_milestone: 1, attempt: 0.
- 2026-06-25 — scout ran (decision-table row 5: all problems published or dropped). Sourced "rheumatic heart disease — the benzathine penicillin coverage-and-supply gap" (category: global health and disease; SHAPE-picked because the 7-category rotation lap is complete and the operator has not yet re-ranked into P0/P1 tiers). Winner of a 5-candidate slate scored against PREFERENCES.md SHAPE criteria (9/10; runners-up: postpartum-hemorrhage/TXA 7/10 — lost on desk-research wedge, logistics not synthesis; hepatitis-C cascade 6/10 — fails the "decade of institutional reform" filter; snakebite antivenom 6/10 — invention component remains, fix isn't pure grind; cervical-cancer/HPV self-sampling 5/10 — saturated / being solved by X). Brief written to problem.md; awaiting planner.
