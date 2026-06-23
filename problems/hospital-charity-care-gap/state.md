# State: hospital-charity-care-gap

status: in_progress
current_milestone: 1
attempt: 0

## Next action

Spec is written (M1–M5). The next run matches decision table row 2: the **generator** executes the current milestone (M1 — Codify the 501(r) scoring rubric from the legal text), writes one artifact to `artifacts/`, and sets `status: awaiting_review`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-23 — planner ran: turned the brief into `spec.md` with 5 milestones, each with near-binary done-criteria. M1: codify the 501(r) scoring rubric from legal text. M2: fix a reproducible named sample of >=15 hospitals/systems + source-inventory (FAP / Plain Language Summary / Schedule H URLs with found/not-found status). M3: score FAP accessibility/compliance per hospital, quoting policy text on load-bearing criteria. M4: layer in Schedule H charity-care spending vs peers (intensity ratio + below-peer flags). M5: assemble the ranked named scorecard with recomputable weighting, "most actionable targets" shortlist, and a standalone limitations section. Milestones build strictly (M1 rubric→M3; M2 inventory→M3,M4; M3+M4→M5). No matching skill exists, so all milestones are freeform; the planner flagged M3 (repeated FAP-text scoring) as a future skill-extraction candidate. Status set to in_progress, current_milestone 1.
- 2026-06-23 — scout ran: sourced "charity care that nonprofit hospitals are legally required to give but mostly don't" (category: economics and inequality — an uncovered roster slot). Human cost: ~$14B/yr wrongly billed for care that should be written off as charity, only ~29% of eligible patients actually receive assistance, against ~$220B in US medical debt. Half-known fix: presumptive eligibility (auto-screen against Medicaid/SNAP/WIC/homelessness instead of application-gating) — Dollar For models full coverage at a 0.7% revenue drop; North Carolina mandated it (Jan 2025 / Jan 2026). Stuck on inverted incentives + near-zero IRC 501(r) enforcement (IRS audited just 35 of ~2,900 hospital orgs in 2024) + deliberate application friction. Desk-research wedge: parse public FAPs + Plain Language Summaries + Form 990 Schedule H into a ranked hospital-by-hospital non-compliance/inaccessibility scorecard that state AGs and IRS TE/GE can act on. Winner of a 4-candidate slate scored against PREFERENCES.md (9/10; runners-up: unclaimed safety-net benefits 7/10 — "actually being solved" by Code for America/BDT; algorithmic gig-wage discrimination 6/10 — fix needs new law not grind; benefits cliffs/EMTRs 4/10 — honest conclusion is a decade of institutional reform). Brief written to problem.md; awaiting planner. Note: after this problem, the only uncovered roster category is Technology and society.
