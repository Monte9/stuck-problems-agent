# Triaging the CyberTipline: which fixes for the child-exploitation reporting pipeline need a statute, and which need only NCMEC and platforms

## Abstract

In 2025 the US CyberTipline received 21.3 million child-sexual-abuse reports and referred 18.8 million to law enforcement, but officers say they receive far more than they can investigate and cannot reliably rank them (NCMEC 2026; SIO 2024). This is a triage problem, not a detection problem. Through five desk-research stages, this work built the triage-design package the under-resourced actors cannot write for themselves: a report-completeness rubric, a per-sender noise scorecard, a rescue-priority scoring schema, its legal constraints, and a map of who can fix what. Three findings stand out. A single sender, Amazon AI Services, filed 1.1 million reports in 2025 that contained no actionable information, so the "AI CSAM surge" is mostly noise. A model-quality report can score 95 out of 100 on completeness yet rank near the bottom on rescue priority. Of 13 fixes, 8 are buildable today by NCMEC and platforms with no statute. The recommendation: fund the metadata-only triage layer now (no legislative dependency); pursue the field-mandate statute on a slower track.

## Background

US law (18 U.S.C. 2258A) compels a platform that finds apparent CSAM to report it to NCMEC's CyberTipline, which triages and refers reports to law enforcement. In 2025 the CyberTipline received 21.3 million reports covering 61.8 million files and referred 18.8 million to law enforcement (NCMEC 2026). The classifiers that find this content are in production: Thorn's Safer processed over 318 million lines of text and flagged 1.3 million potential lines for 86 companies in 2025 (problem brief). The bottleneck is downstream. A Stanford Internet Observatory (SIO) study based on interviews with more than 60 officers found law-enforcement teams "receive far more reports than they can investigate" and "are constrained in their ability to accurately prioritize" them (SIO 2024). SIO's 2024 report is the blueprint: standardize report quality around "who, what, where, when," modernize NCMEC's tooling, improve deduplication, and give law enforcement better triage signals (SIO 2024). The proof the problem is fixable sits inside the same data. Snap recalibrated its reporting in 2024 after admitting many of its CyberTips "lack sufficient context for law enforcement to take action," producing "a significant drop in our overall reporting volume to NCMEC and a similar decline in escalations" (Snap 2024). One sender chose to stop sending noise, at no cost to anyone.

## Method

Five stages, each one artifact, each evaluated by an independent reviewer who quoted the milestone's done-criteria, spot-checked citations against primary sources, and wrote a verdict before the next stage ran. M1 built an 8-dimension report-completeness rubric (weights summing to 100, scoring a report 0 to 100 on investigability), anchoring six dimensions to subsection-level provisions of 18 U.S.C. 2258A. M2 built a 14-row per-sender noise scorecard from NCMEC's published per-ESP volumes and its named-deficiency list. M3 built an 8-feature rescue-priority schema with the scoring function `PRIORITY = 15·F1 + 15·F2 + 10·F3 + 8·F4 + SENDER(F5) + 5·F6 + 4·F7 − 9·F8` (range −30 to +105), consuming the M2 scorecard as its sender-reliability input. M4 documented 8 legal constraints (Fourth Amendment, private-search doctrine, statute) and mapped each to the features it touches. M5 sorted every fix into "implementable today" versus "needs statutory change." All five verdicts passed on the first attempt. Artifacts and verdicts are linked in the references and live in the problem directory.

## Findings

### 1. The headline "AI CSAM surge" is mostly one sender's noise.

Of 1.5 million generative-AI-related reports in 2025, 1.1 million came from Amazon AI Services and contained no actionable information (NCMEC 2026). That is roughly 73% of the GAI-nexus total from a single source. The same sender filed only 30,759 reports in 2024 (NCMEC 2024 per-ESP data), so this is a 2025 surge of empty volume that buries the roughly 200,000 actionable AI reports underneath it. Volume and actionability are orthogonal: NCMEC's own classification labels roughly half of all reports "informational" rather than "referral" (SIO 2024, from NCMEC data: ~37% in 2021, ~51% in 2022, ~50% in 2023).

| Sender | Volume (year) | Quality signal | Noise tier |
|---|---|---|---|
| Amazon AI Services | 1,100,000 (2025) | "no actionable information" (NCMEC) | Severe |
| Grindr | 78,886 (2024) | NCMEC-named; >80% of cohort lacked location | High |
| Facebook | 8,590,357 (2024) | human review, files, bundling | Good-faith |
| Instagram | 3,320,008 (2024) | same Meta program | Good-faith |
| WhatsApp | 1,851,086 (2024) | E2EE, no published rate | Moderate/opaque |

The largest reporter by volume, Facebook at 8.59 million, ranks near the bottom on noise tax because it runs human review, attaches files, and bundles duplicates (NCMEC 2024 per-ESP data; M2). High volume from a good-faith sender is the statute working, not a problem.

### 2. NCMEC already names its worst senders, and almost nobody uses the list.

In its 2023 report (p. 9) NCMEC names 13 companies whose reports "consistently lack substantive information," including Grindr, Lightspeed Systems, Megapersonals, Truth Social (TMTG), Redgifs, and Internet Archive, and states that more than 80% of the 100+-report members of that list filed reports lacking enough data to determine a location (NCMEC 2023; M2). This is a ready-made sender-reliability prior. The M3 schema consumes it directly (feature F5), mapping each named sender to a priority penalty.

### 3. A complete report is not a high-priority report.

The schema separates completeness from rescue priority, the exact distinction SIO named as unsolved. A Facebook report that scores 95 out of 100 on completeness, with file, account ID, upload IP, and timestamp, scores 6 on rescue priority once the schema sees it is a known-hash viral duplicate with no imminence and no novel victim (M3, Report B). A live-sextortion report from Grindr, a high-noise sender, scores 87, because imminence and a novel victim image dominate the sender penalty (M3, Report A). An automated Amazon-style GAI dump hits the floor at −30 (M3, Report C). The viral-duplicate penalty sinks complete-but-stale reports; imminence and novelty raise thin-but-live ones.

### 4. The cheapest fix is not the highest-leverage one, and they sit on opposite sides of the statutory line.

| Fix | Actor | Class |
|---|---|---|
| Set "File Viewed by Company" flag accurately | Platforms | Today |
| Recalibrate over-reporting (Snap model) | Platforms | Today |
| Deduplicate/bundle before review | Platforms + NCMEC | Today |
| Build the rescue-priority triage layer | NCMEC | Today |
| Operationalize the sender-reliability prior | NCMEC | Today |
| Mandate the quality fields | Congress | Statute |
| Mandate ICAC outcome reporting | Congress/DOJ | Statute |
| Codify NCMEC's status / triage safe-harbor | Congress | Statute |

Of 13 fixes, 8 are implementable today by NCMEC and platforms, 3 need statutory change, and 2 are mixed (M5). The root cause is the (a)-mandatory / (b)-discretionary split in 18 U.S.C. 2258A: the law compels the volume of reporting but makes every quality field "optional at the sole discretion of the provider" (18 U.S.C. 2258A(b); M1). NCMEC cannot close that gap itself. If it issued binding quality standards, courts could treat platforms as government agents and suppress millions of reports under the private-search doctrine (United States v. Ackerman; M4). So the highest-leverage fix (mandate the fields) needs Congress, while the most shippable fix (the triage layer) needs no one's permission.

## Recommendations

| Item | Executor | Cost | Anchor |
|---|---|---|---|
| Build the metadata-only rescue-priority triage layer | NCMEC + platforms | No statute required | M3 schema; M5 Fix 7 |
| Operationalize the sender-reliability prior from NCMEC's named list | NCMEC | No statute required | M2 §2; M5 Fix 9 |
| Design the schema to be Fourth-Amendment-agnostic (never open a never-viewed file) | NCMEC + platforms | No statute required | M4 §3; M5 Fix 11 |
| Scale deduplication/bundling and over-reporting recalibration | Platforms + NCMEC | No statute required | M5 Fixes 5, 6 |
| Mandate the quality fields in 18 U.S.C. 2258A(b) | Congress | Authorization | M1 §1; M5 Fix 1 |
| Mandate ICAC outcome reporting | Congress / DOJ-OJJDP | Authorization | M5 Fix 12 |

Sequence the today-fixes first. The triage layer (Fixes 7, 9, 11) converts NCMEC's existing manual urgent escalation, 63,892 reports in 2023 (NCMEC 2023), into a documented, auditable docket using only signals already in reports, and M4 confirms it is lawful today if built on hash and field metadata rather than file-opening. Deduplication and recalibration deliver value in parallel. The statutory asks are real but slower, and they are coupled to the today-work: the triage layer's weights cannot be empirically tuned until ICAC outcome data exists, which needs a reporting mandate. Fund the layer; pursue the mandate.

## Limitations

1. The M1 and M3 weights are an analyst allocation, not a validated model. Only the ordering (imminence > novelty > jurisdiction > sender, with a large viral penalty) is sourced to SIO and NCMEC emphasis; the exact coefficients are tagged `[speculative]` in the artifacts. SIO notes ICAC Task Forces lack outcome transparency, so there is no arrest or rescue ground truth to fit weights against (SIO 2024).
2. Almost no sender publishes field-level quality data. For 10 of the 14 scorecard rows there is no public per-sender actionability rate, so opacity, not measured noise, is the central data gap (M2 §4).
3. The scorecard mixes years: Amazon's 1.1 million is 2025; the other per-sender volumes are 2024, the most recent verifiable per-ESP breakdown (NCMEC's 2025 company-level table did not parse). Each cell states its year.
4. The strongest sender signal, NCMEC's named-deficiency list, is from the 2023 report and is binary, not graded; the >80%-location figure is a cohort statistic, not a per-company rate, and the list may have changed since (M2 §4).
5. The triage schema is a reconstruction of NCMEC-style triage from public signals, not NCMEC's actual model, which is not public, in part for Fourth-Amendment reasons (M3 §4).
6. The "today vs. statute" line is partly a matter of legal risk appetite. Some today-fixes are implementable only on the conservative, voluntariness-preserving path; a more aggressive reading could manufacture the agent-of-government exposure the classification exists to avoid (M5).
7. A poorly drafted field mandate could itself convert platforms into government agents and reduce admissibility, so "needs a statute" does not guarantee the statute would be net-positive (M5, tagged `[speculative]`).

## References

1. NCMEC, "The Work Never Stops: First Look at NCMEC's 2025 Data" (2026). https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data
2. Stanford Internet Observatory, "The CyberTipline Report" / "How to Fix Online Child Exploitation Reporting" (2024). https://cyber.fsi.stanford.edu/publication/how-fix-online-child-exploitation-reporting-system ; underlying PDF: https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf
3. 18 U.S.C. 2258A (Cornell LII). https://www.law.cornell.edu/uscode/text/18/2258A
4. NCMEC, "2024 CyberTipline Reports by Electronic Service Providers." https://ncmec.org/content/dam/missingkids/pdfs/cybertiplinedata2024/2024-reports-by-esp.pdf
5. NCMEC, 2023 CyberTipline Report. https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf
6. Snap, "Recalibration of Our Reporting." https://values.snap.com/news/recalibration-reporting
7. NBC News, "Child exploitation watchdog says Meta encryption led to sharp decrease." https://www.nbcnews.com/tech/security/child-exploitation-watchdog-says-meta-encryption-led-sharp-decrease-ti-rcna205548
8. United States v. Ackerman, 831 F.3d 1292 (10th Cir. 2016). https://law.justia.com/cases/federal/appellate-courts/ca10/14-3265/14-3265-2016-08-05.html
9. United States v. Wilson, 13 F.4th 961 (9th Cir. 2021). https://cdn.ca9.uscourts.gov/datastore/opinions/2021/09/21/18-50440.pdf
10. United States v. Reddick, 900 F.3d 636 (5th Cir. 2018). https://law.justia.com/cases/federal/appellate-courts/ca5/17-41116/17-41116-2018-08-17.html
11. United States v. Jacobsen, 466 U.S. 109 (1984). https://supreme.justia.com/cases/federal/us/466/109/

## Provenance

This report was produced by an autonomous research loop that runs one phase per scheduled wake: plan, generate, evaluate, publish. Each of the five artifacts was checked by an independent evaluator that quoted the done-criteria and spot-checked citations against primary sources before the next stage ran; all five passed on the first attempt. The five artifacts and their verdicts live in `problems/csam-report-triage/artifacts/` and `problems/csam-report-triage/verdicts/`.
