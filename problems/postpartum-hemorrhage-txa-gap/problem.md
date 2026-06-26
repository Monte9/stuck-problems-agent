# Postpartum hemorrhage: a pennies-cost drug, proven to cut deaths, still given too late or not at all

> Intake brief from the scout routine, 2026-06-26. Category: global health and disease (shape pick; rotation lap complete, so shape decides — not category).
> Bottleneck type: adoption grind plus misaligned supply incentives. The drug and the protocol are both proven and on the WHO essential-medicines list; nobody is staffed to map, country by country, where they are missing from the kit, the guideline, and the shelf.

## (a) The problem, in plain language

Postpartum hemorrhage (PPH) — bleeding after childbirth — is the world's single leading cause of maternal death. It kills roughly **70,000 women a year** and accounts for **over 20% of all maternal deaths**, almost all of them in low- and middle-income countries (LMICs) ([WHO, 2023](https://www.who.int/news/item/11-10-2023-who-issues-global-plan-to-tackle-leading-cause-of-death-in-childbirth); [BJOG/PMC, 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC12678032/)). About 14 million women experience PPH each year. These are not deaths from an exotic, hard-to-treat condition: most are healthy women who bleed out in the hours after a normal delivery, in facilities, because the response is too slow.

## (b) The half-known solution

Two cheap, proven fixes already exist:

1. **Tranexamic acid (TXA).** The WOMAN trial (2017, ~20,000 women) showed TXA given within 3 hours of bleeding onset cuts PPH death by **31%**, with thromboembolic events no higher than placebo. Crucially, **every 15-minute delay erases ~10% of the survival benefit** ([Lancet/WOMAN; PMC review, 2025](https://pmc.ncbi.nlm.nih.gov/articles/PMC12244439/)). TXA costs roughly a dollar a dose and is on the WHO Essential Medicines List.
2. **The E-MOTIVE bundle.** A 2023 cluster-randomized trial across **80 hospitals in Kenya, Nigeria, South Africa, and Tanzania** paired a cheap calibrated blood-collection drape (objective early detection) with the WHO first-response bundle (massage, oxytocic, TXA, IV fluids, escalation). It cut severe PPH outcomes by **60%** (1.6% vs 4.3%; RR 0.40) ([NEJM, 2023](https://www.nejm.org/doi/full/10.1056/NEJMoa2303966)). WHO folded it into guidelines almost immediately.

The science is settled. The gap is between "WHO recommends it" and "the woman bleeding in a district hospital actually gets it, on time."

## (c) Why it is stuck

In the E-MOTIVE countries, audits found TXA was administered **late and mostly as a last resort** before surgery — not as first-line treatment ([scoping review, PMC](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9223501/)). The blockers are unglamorous and country-specific: TXA absent from national delivery kits and PPH protocols; frequent **stockouts** of PPH commodities; provider unawareness; and task-shifting rules that bar the nurse or midwife present at the bleed from giving the drug ([WHO PPH Roadmap, 2023](https://cdn.who.int/media/docs/default-source/reproductive-health/maternal-health/pph-roadmap.pdf); [Nigeria awareness survey, medRxiv 2023](https://www.medrxiv.org/content/10.1101/2023.06.02.23290525.full.pdf)). This is a classic overdue-diffusion pattern (scurvy, Semmelweis): the cure is known and cheap, but no single actor owns closing the last mile, and "collecting and distributing a $1 drug" attracts no commercial pull.

## (d) The AI-agent wedge

A model running unsupervised can build the artifact that currently does not exist: a **structured, country-by-country PPH treatment-gap matrix** for high-burden LMICs. For each country, synthesize from public sources: (i) is TXA on the national Essential Medicines List and standard treatment guideline; (ii) is it in the national delivery/PPH kit and at what level of care; (iii) published stockout/availability and administration-timing evidence; (iv) whether scope-of-practice rules let the front-line birth attendant administer it; (v) E-MOTIVE/drape adoption status. The deliverable is a ranked shortlist of "cheapest next fixes" — e.g., "Country X has TXA on its EML but not in its delivery kit; a kit-line edit is a one-meeting decision" — handed to a named actor. This is desk synthesis the agent produces itself, not a research recommendation.

## (e) Who is closest today

The **WHO PPH Roadmap (2023–2030)**, funded by **MSD for Mothers** and the **Gates Foundation**, coordinated with **FIGO, ICM, UNFPA, and UNICEF** ([FIGO, 2023](https://www.figo.org/news/new-who-postpartum-haemorrhage-roadmap-essential-tool-reduce-maternal-mortality-between-2023)). The **University of Birmingham E-MOTIVE team** runs the trial and scale-up. These bodies have the mandate and the money; what they lack is a maintained, granular gap map to direct the next dollar. WHO's "global call for data on PPH" signals they know the data is fragmented — the wedge meets a stated need.
