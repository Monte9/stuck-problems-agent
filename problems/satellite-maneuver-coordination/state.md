# State: satellite-maneuver-coordination

status: no_spec
current_milestone: 0
attempt: 0

## Next action

A fresh problem brief exists (`problem.md`) but there is no `spec.md` yet. The next run matches decision-table row 1: the **planner** subagent turns the brief into a research spec with 3–6 milestones, each with explicit checkable done-criteria, then sets `status: in_progress`, `current_milestone: 1`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-27 — scout ran (decision-table row 5: all problems published or dropped). Sourced "Satellite maneuver coordination — the missing right-of-way rulebook for on-orbit collision avoidance" (payoff: frontier progress / space; shape: the measurement-forecast — a costed comparison of candidate deconfliction rules, deliberately NOT the over-represented overdue-fix dossier). Winner (score 9.0) of a 5-candidate slate scored against PREFERENCES.md, spanning both lanes (4 frontier + 1 welfare-adjacent) and four shapes. Runners-up/cuts: AI bio-uplift evals teardown 7.0 (evidence genuinely contested + crowded — risk of "one more opinion"); cislunar SSA tracking-gap forecast 6.5 (already being built — Oracle 2027/Astrobotic — contribution drifts to commentary); LEO debris / Kessler-tipping-point measurement 6.0 (strong numbers but overlaps covered uncontrolled-rocket-reentry; the coordination-rule cut is sharper); sodium-ion grid-battery forecast 5.5 (fails skepticism filter — actively solved at scale by CATL/BYD in 2026). Deciding preference: all four anchor invariants met cleanly — quantified stakes (Starlink ~300k avoidance maneuvers in 2025, +50% YoY, ~1M projected by 2027; 144,404 maneuvers Dec 2024–May 2025), a desk-research wedge (simulate four proposed right-of-way rules against published conjunction data and produce the missing costed rulebook, not a recommendation to study it), a named decision-maker who can act within a year (Office of Space Commerce / TraCSS, whose operator-to-operator deconfliction layer is on the roadmap but unbuilt and whose rule is undecided), and a sharp earned inversion (uncoordinated dual maneuvers can *raise* post-maneuver collision probability — both satellites swerve the same way). Brief (569 words) written to problem.md; awaiting planner.
