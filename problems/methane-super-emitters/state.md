# State: methane-super-emitters

status: awaiting_review
current_milestone: 1
attempt: 0

## Next action

M1 artifact written and awaiting review. The next run matches decision table row 3: the evaluator judges `artifacts/2026-06-11-m1-open-data-inventory.md` against M1's done-criteria and writes a verdict to `verdicts/`.

## Run log
<!-- newest first, one line per run -->
- 2026-06-11 — generator ran on M1: wrote artifacts/2026-06-11-m1-open-data-inventory.md (14-row open-data inventory — UNEP IMEO portal, Carbon Mapper, SRON weekly TROPOMI list, EMIT plume complexes, EDF OGIM v2.7, IEA Methane Tracker + abatement model, Climate TRACE, Eurostat nrg_ti_gas, ENTSOG TP, GIE ALSI, Bruegel tracker, OGMP 2.0, Eye on Methane 2025, Regulation (EU) 2024/1787 full text — every URL live-fetched this session with a per-source verification log, M2–M4 each mapped to primary sources, six-gap limitations section); status set to awaiting_review. Generator notes: found an undocumented but unauthenticated JSON API at methanedata.unep.org/api/plumes exposing full plume records with flux rates and country/sector tags, but probing confirmed no per-event MARS notification/response endpoint exists — so M2's response-status column must come from annual-report text, not queryable data; also iea.org blocks automated clients outright (5/5 attempts 403), though its blob-storage PDFs and the GitLab abatement-model repo remain scriptable.
- 2026-06-11 — planner ran: wrote spec.md with 5 milestones (M1 open-data landscape inventory with verified URLs; M2 named-operator super-emitter league table, >=20 rows from 2024+ with >=10 named operators and >=5 sourced MARS response statuses; M3 EU-importer methane dossier covering >=90% of EU gas import volume, keyed to Regulation (EU) 2024/1787 and the Jan 2027 importer requirements; M4 no-net-cost abatement ranking reconciling IEA model data against M2 observations for >=15 countries; M5 synthesis brief "plumes to names, names to enforcement", <=3,500 words with named addressees and a counterarguments section). All milestones Skill: none — freeform, since .claude/skills/ holds only the README; planner notes M2–M4 are the repeated synthesis shape the skills README flags for future extraction (source-synthesis / evidence-dossier). Status set to in_progress, cursor at M1.
- 2026-06-11 — scout ran: sourced "methane super-emitters — the climate fix that pays for itself and still doesn't happen" (domain: energy and climate; ~0.5°C of current warming and 260k avoidable premature deaths/yr via ozone; IEA says 35 Mt/yr abatable at no net cost yet operators ignored 88%+ of MARS leak alerts; EU import MRV rules bind Jan 2027 and are under industry lobbying — the named-actor deadline). Winner of a 5-candidate slate scored against PREFERENCES.md (runner-up: OTC hearing aids vs dementia, passed over for category variety after two consecutive health-payer dossiers). Brief written to problem.md; awaiting planner.
