# State: rheumatic-heart-disease-penicillin-gap

status: awaiting_review
current_milestone: 1
attempt: 0

## Next action

M1 artifact written and status is awaiting_review → the next run matches decision-table row 3: the **evaluator** subagent gets fresh eyes (only the M1 done-criteria, the artifact path `artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`, and a verdict output path) and writes a PASS/FAIL verdict to verdicts/. Route on it: PASS → advance to M2, reset attempt 0, status in_progress; FAIL → increment attempt, status in_progress (or blocked at attempt 2).

## Run log
<!-- newest first, one line per run -->
- 2026-06-25 — generator ran (decision-table row 2: status in_progress, M1, attempt 0; no matching skill in .claude/skills/, so freeform). Wrote artifacts/2026-06-25-m1-coverage-stockout-scorecard.md: a 20-country RHD coverage-and-stockout scorecard ranked by absolute GBD prevalent-case burden, cross-referencing GBD 2021/2019/2015 burden, register/cohort coverage (Australia AIHW ~32%, Fiji ~7%, Uganda ~58–91%, Ethiopia ~63%, NZ below target), and documented BPG shortages (WHO 2014–2016 39/95-country survey set plus the 2023–2025 Bicillin L-A shortage). 20 rows (≥15), 9 documented stockout events (≥5), every burden/coverage cell sourced or marked "no register/no data", 6-caveat limitations section. Surfaced inversion: coverage/stockout evidence exists mainly where burden is lowest; the four highest-burden countries (India, China, Pakistan, Indonesia) have no national register and no documented stockout in the located literature. Set status: awaiting_review.
- 2026-06-25 — planner ran (decision-table row 1: no spec.md). Wrote spec.md with 4 milestones: M1 country-by-country RHD coverage-and-stockout scorecard; M2 BPG supply-chain concentration map; M3 deaths-and-dollars cost-of-inaction model (consumes M1 burden + GOAL effect size); M4 benefit-harm dossier inverting the 2022 AHA injection-reaction advisory (consumes M3 benefit arithmetic). All milestones are pure desk synthesis over published data; each carries 4-5 near-binary done-criteria. Set status: in_progress, current_milestone: 1, attempt: 0.
- 2026-06-25 — scout ran (decision-table row 5: all problems published or dropped). Sourced "rheumatic heart disease — the benzathine penicillin coverage-and-supply gap" (category: global health and disease; SHAPE-picked because the 7-category rotation lap is complete and the operator has not yet re-ranked into P0/P1 tiers). Winner of a 5-candidate slate scored against PREFERENCES.md SHAPE criteria (9/10; runners-up: postpartum-hemorrhage/TXA 7/10 — lost on desk-research wedge, logistics not synthesis; hepatitis-C cascade 6/10 — fails the "decade of institutional reform" filter; snakebite antivenom 6/10 — invention component remains, fix isn't pure grind; cervical-cancer/HPV self-sampling 5/10 — saturated / being solved by X). Brief written to problem.md; awaiting planner.
