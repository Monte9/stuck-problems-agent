# M3 — Schedule H charity-care spending cross-referenced against expenses

**Problem:** Charity care that nonprofit hospitals are legally required to give — and mostly don't.
**Milestone:** M3 — pull Form 990 Schedule H financial-assistance-at-cost figures for the frozen 28-hospital sample and compute a charity-care-as-share-of-expense ratio that flags systems spending far below peers; supply the D10 score deferred from M2.
**Date:** 2026-06-24. All Form 990 figures extracted from IRS Modernized e-File XML retrieved 2026-06-24 (see Method).
**Inputs:** the frozen sample and D10 rule in `artifacts/2026-06-23-m1-rubric-and-sample.md`; the D1–D9 scores in `artifacts/2026-06-24-m2-fap-pls-scoring.md` (which deferred D10 to this milestone). The sample is frozen: all 28 rows are present below; none added or dropped.

---

## Numerator and denominator definition (stated ONCE, applied to every hospital)

- **Numerator = Form 990 Schedule H, Part I, Line 7a, column (e): "Financial Assistance at cost — Net community benefit expense."** This is charity care / financial assistance valued *at cost* (gross cost less any direct offsetting revenue such as Medicaid charity payments). In the IRS e-file XML this is the element `IRS990ScheduleH/FinancialAssistanceAtCostGrp/NetCommunityBenefitExpnsAmt` (older schema tag `FinancialAssistanceAtCostTyp`). It is the M1/D10 figure ("Schedule H Part I charity-care-at-cost").
- **Denominator = total functional expenses** = Form 990, Part IX, Line 25, column (A) = e-file element `CYTotalExpensesAmt` for the same filing/period. Using one organization's own total expense as denominator keeps numerator and denominator on the same filing and the same accounting basis.
- **Ratio = Numerator ÷ Denominator × 100.** I verified this self-computed ratio reproduces the IRS-printed Schedule H Part I Line 7a column (f) "Percent of total expense" (`TotalExpensePct`) to within rounding on spot checks (Duke 3.45% vs IRS 3.45%; Banner 1.63% vs 1.63%; Sentara 1.67% vs 1.65%). I report **my own consistently-computed ratio** for every row so the denominator is identical across the sample.
- **D10 score** (per the M1 rule, applied to the ratio above): **2** = ratio > 1.0%; **1** = 0.1%–1.0%; **0** = ≤ 0.1% or Schedule H not filed/located.
- **Peer flag** is computed over the **17 cleanly-attributable 501(c)(3) hospital/operating filers** (the rows with a verified facility-or-operating-entity figure; the MGB group-return aggregate, the for-profit, the public hospitals, and the unavailable rows are excluded from the quartile math and flagged separately). Across those 17: **median = 1.35%, lower quartile (Q1) = 0.88%, upper quartile (Q3) = 2.79%.** "Bottom quartile" = ratio ≤ 0.88%; "top quartile" = ratio ≥ 2.79%.

---

## Core table (all 28 sample rows)

Ratios are for filing year **FY2023** (the most recent year present in the IRS e-file XML extract for these entities as of 2026-06-24); fiscal-period-end is shown per row because hospitals use different fiscal years. "EIN used" is the entity actually filing Schedule H, which **differs from the M1 EIN in several cases** (see EIN-reconciliation note); dollar figures trace to that entity's filing.

| # | Hospital | EIN used | Period end | Charity care at cost (Line 7a-e, $) | Total expenses (Part IX-25A, $) | Ratio % | Peer flag | D10 |
|---|----------|----------|-----------|------------------------------:|------------------------------:|------:|-----------|:--:|
| 8 | WakeMed Raleigh | 56-6017737 | 2023-09-30 | 116,034,706 | 2,092,838,776 | **5.54** | top quartile | 2 |
| 5 | Moses Cone (Cone Health oper. corp) | 58-1588823 | 2023-09-30 | 63,479,590 | 1,745,593,096 | **3.64** | top quartile | 2 |
| 2 | Duke University Hospital | 56-2070036 | 2023-06-30 | 159,367,231 | 4,623,216,546 | **3.45** | top quartile | 2 |
| 6 | Novant Health (Forsyth) | 56-1376950 | 2023-12-31 | 111,584,803 | 3,902,611,082 | **2.86** | top quartile | 2 |
| 7 | ECU Health Med Ctr (Pitt County Mem.) | 56-0585243 | 2023-09-30 | 44,910,860 | 1,643,233,968 | **2.73** | above median | 2 |
| 4 | UNC Health Rex | 56-1509260 | 2023-06-30 | 30,925,578 | 1,623,015,427 | **1.91** | above median | 2 |
| 27 | Sentara Norfolk General (Sentara Hospitals) | 54-1547408 | 2023-12-31 | 58,370,130 | 3,500,319,133 | **1.67** | above median | 2 |
| 18 | Banner – UMC Phoenix (Banner Health) | 45-0233470 | 2023-12-31 | 141,369,990 | 8,672,348,619 | **1.63** | above median | 2 |
| 16 | CommonSpirit (St. Joseph's Phoenix → Dignity Health) | 94-1196203 | 2023-06-30 | 136,855,373 | 10,126,687,245 | **1.35** | at median | 2 |
| 22 | FirstHealth Moore Regional | 56-1936354 | 2023-09-30 | 14,012,239 | 1,096,646,867 | **1.28** | below median | 2 |
| 10 | Cleveland Clinic | 34-0714585 | 2023-12-31 | 92,419,889 | 8,518,490,199 | **1.08** | below median | 2 |
| 9 | Atrium Wake Forest Baptist (NC Baptist Hosp.) | 56-0552787 | 2023-12-31 | 26,495,754 | 2,929,347,846 | **0.90** | below median | 1 |
| 28 | Carilion Roanoke (Carilion Medical Center) | 54-0506332 | 2023-09-30 | 15,701,863 | 1,769,567,616 | **0.89** | below median | 1 |
| 14 | NewYork-Presbyterian | 13-3957095 | 2023-12-31 | 84,771,020 | 9,755,790,336 | **0.87** | bottom quartile | 1 |
| 12 | HUP / Penn (Presby. Med. Ctr of Univ. of PA) | 23-2810852 | 2023-06-30 | 4,592,398 | 1,175,954,738 | **0.39** | bottom quartile | 1 |
| 15 | Ascension Providence MI → Henry Ford Providence | 38-1358212 | 2023-06-30 | 2,705,882 | 904,524,555 | **0.30** | bottom quartile | 1 |
| 26 | Grady Memorial | 26-2037695 | 2023-12-31 | 0 | 2,185,617,947 | **0.00** | bottom quartile | 0 |
| 13 | Mass General / MGB *(system group-return aggregate, not MGH alone)* | 90-0656139 | 2023-09-30 | 110,886,113 | 21,584,405,066 | **0.51** | bottom-quartile-equivalent | 1 |
| 1 | Atrium Health / Carolinas Medical Center | — (33-… group) | — | filing unavailable | filing unavailable | — | — | 0\* |
| 3 | UNC Medical Center | 56-1118388 | — | filing inapplicable (governmental) | — | — | — | n/a |
| 11 | UPMC Presbyterian | — | — | filing unavailable | filing unavailable | — | — | 0\* |
| 17 | AdventHealth Orlando | — | — | filing unavailable | filing unavailable | — | — | 0\* |
| 19 | Corewell Butterworth (Corewell Health West) | 38-2715520 | 2023-12-31 | filing unavailable (no Sched H in e-file XML) | 5,399,882,862 | — | — | 0\* |
| 20 | Cape Fear Valley | — | — | filing unavailable | filing unavailable | — | — | 0\* |
| 21 | Mission Hospital (HCA, for-profit) | — | — | filing inapplicable (for-profit) | — | — | — | n/a |
| 23 | NYC Health + Hospitals / Bellevue | — | — | filing inapplicable (public benefit corp) | — | — | — | n/a |
| 24 | Cook County Health / Stroger | — | — | filing inapplicable (public) | — | — | — | n/a |
| 25 | Parkland Health | — | — | filing inapplicable (public district) | — | — | — | n/a |

**D10 conventions in the last column.** `2`/`1`/`0` are scored from the computed ratio per the M1 D10 rule. `n/a` = the organization files **no** Form 990 Schedule H by governance type (for-profit #21; state-governmental #3 UNC and #23/#24/#25 public) — D10 is genuinely inapplicable, not a zero. `0\*` = **"filing unavailable" → D10 = 0 under the M1 rule** ("≤0.1% *or Schedule H not filed/located* = 0"); the asterisk flags that this 0 means "no usable facility-level Schedule H located," **not** a confirmed near-zero spend. M4 must treat `0\*` rows as a data gap, not as evidence of stinginess, and must exclude #3/#21/#23/#24/#25 from the charity-care ratio entirely.

---

## Peer comparison (low spenders are identifiable, not just listed)

Across the **17 cleanly-attributable 501(c)(3) hospital/operating filers** (FY2023, financial-assistance-at-cost ÷ total functional expenses):

- **Median = 1.35%.** **Q1 (lower quartile) = 0.88%; Q3 (upper quartile) = 2.79%.** Range 0.00%–5.54%.
- **Top quartile (≥ 2.79%) — most generous:** WakeMed 5.54%, Moses Cone 3.64%, Duke 3.45%, Novant 2.86%. **All four are North Carolina nonprofits** — consistent with NC's HASP regime pushing charity-care delivery, not just disclosure.
- **Bottom quartile (≤ 0.88%) — flagged low spenders:** Grady 0.00%, Henry Ford Providence (the M1 "Ascension Providence" facility, now Henry Ford) 0.30%, Penn/HUP 0.39%, NewYork-Presbyterian 0.87%. **The MGB system group-return aggregate (0.51%) falls in this band too**, with the caveat below.
- **The spread is ~18× from bottom to top of the computable set** (0.30% Penn vs 5.54% WakeMed; Grady's 0.00% is a special case, below). Two very large, well-resourced academic systems — **Penn/HUP (0.39%) and NewYork-Presbyterian (0.87%)** — sit in the bottom quartile despite multi-billion-dollar expense bases, making them the most defensible "spends far below peers" flags in this sample. NYP's $84.8M of charity care is large in dollars but only 0.87% of its $9.76B expense base; Penn/HUP's $4.6M is low in both dollars and ratio.
- **Grady Memorial (0.00%) is a true zero on Line 7a but must be read carefully.** Grady's filing reports $142.9M of gross financial-assistance cost **fully offset by direct offsetting revenue** (Georgia DSH / Fulton-DeKalb indigent-care funding), so *net* Line 7a = $0; separately it books $49.5M (2.65%) of unreimbursed Medicaid on Line 7b. Grady is a safety-net hospital funded by county appropriations rather than by absorbing charity cost itself — a structural feature, not necessarily under-service. Flagged for M4 as "ratio 0.00% but driven by offsetting public funding, not absence of charity care."

---

## EIN reconciliation (M1 EINs corrected to the actual Schedule H filer)

M1 flagged that "several systems file Schedule H under a parent/group EIN, not per facility." That proved decisive: **the M1 EIN was the wrong (non-Schedule-H-filing) entity for six rows**, and I substituted the operating-hospital EIN that actually files Schedule H, verified in the IRS e-file index and XML:

| # | M1 EIN (parent/holding) | M1 entity filed Schedule H? | EIN used here (operating hospital) | Note |
|---|----|----|----|----|
| 5 | 56-0532302 (Moses H Cone Memorial Hospital — *strategic-oversight parent*) | No (Sched H absent) | **58-1588823** The Moses H. Cone Memorial Hospital **Operating** Corporation | Correct operating filer; 3.64% |
| 7 | 56-2141073 (Univ. Health Systems of Eastern Carolina — *support parent*) | No | **56-0585243** Pitt County Memorial Hospital Inc (= ECU Health / fmr Vidant Med Ctr) | Operating hospital; 2.73% |
| 11 | 25-1423657 (UPMC — *parent holding co*) | No | UPMC Presbyterian Shadyside 25-0965480 **not in e-file XML index** | → filing unavailable |
| 12 | 23-2810852 | **Yes** (Presbyterian Med Ctr of Univ. of PA Health) | 23-2810852 (unchanged) | 0.39% |
| 13 | 22-2658209 (Mass General Brigham Inc — *small mgmt entity, $129M*) | No | **90-0656139** MGB **& Affiliates Group Return** (system aggregate) | MGH not isolable; 0.51% system-wide |
| 15 | 38-1358212 | **Yes**; entity is now **Henry Ford Providence Hospital** (post-2024 Ascension→Henry Ford transfer) | 38-1358212 (unchanged) | 0.30%; name changed |
| 16 | 47-0617373 (CommonSpirit Health — *national parent*) | No | **94-1196203** Dignity Health (CommonSpirit AZ facility filer, incl. St. Joseph's Phoenix) | 1.35% (Dignity-wide AZ/CA aggregate) |

Confirmed-as-correct M1 EINs (Schedule H present and parsed): Duke 56-2070036, Novant 56-1376950, Cleveland Clinic 34-0714585, NewYork-Presbyterian 13-3957095, Banner 45-0233470, Sentara 54-1547408, Carilion (Med Center) 54-0506332, Grady 26-2037695, FirstHealth 56-1936354, NC Baptist/Atrium Wake Forest 56-0552787, UNC Rex 56-1509260.

---

## Why the "filing unavailable" / "filing inapplicable" rows are what they are (source checked)

- **#3 UNC Medical Center — filing inapplicable (governmental).** University of North Carolina Hospitals (EIN 56-1118388) is a state-owned component of UNC Health and **files no Form 990 at all** — ProPublica Nonprofit Explorer returns *zero* filings (with-data and without-data both 0) for that EIN, and IRS records show no subsection/ruling. As a governmental entity it is not a 501(c)(3) Schedule H filer. (Its sister entity **Rex Hospital Inc, 56-1509260, is a separate private 501(c)(3) that does file** — row #4, 1.91%.) Source: [ProPublica Nonprofit Explorer EIN 56-1118388](https://projects.propublica.org/nonprofits/organizations/561118388).
- **#21 Mission/HCA, #23 NYC H+H, #24 Cook County, #25 Parkland — filing inapplicable.** Per M1, the for-profit (HCA) and the three public hospitals do not file Form 990 Schedule H; D10/M3 is inapplicable and they are retained for FAP/PLS comparison only.
- **#1 Atrium / Carolinas Medical Center — filing unavailable.** Atrium operates as "The Charlotte-Mecklenburg Hospital Authority," whose Form 990 group filings appear as **990EZ group returns** ("Atrium Health Inc" 84-3647453 and "Atrium Health System" 31-0537492 both file 990**EZ**, not a facility Schedule H). No CMC-facility-level Schedule H is separately e-filed as parseable XML. Source checked: [ProPublica EIN 84-3647453](https://projects.propublica.org/nonprofits/organizations/843647453) (990EZ group return), IRS e-file index 2021–2024.
- **#11 UPMC Presbyterian — filing unavailable.** The M1 parent EIN 25-1423657 files no Schedule H (its 990 mission is "support of subsidiary…"); the operating UPMC Presbyterian Shadyside (25-0965480) has **no recent filing with data on ProPublica and is absent from the IRS e-file XML index 2021–2024**, so no traceable facility figure could be pulled. Source checked: [ProPublica EIN 25-0965480](https://projects.propublica.org/nonprofits/organizations/250965480); IRS index.
- **#17 AdventHealth Orlando — filing unavailable.** The Orlando hospital files within the AdventHealth/"Adventist Health System Sunbelt" consolidated structure; EIN 59-0724459 (the Orlando entity) has no recent with-data filing on ProPublica and is **not in the IRS e-file XML index**, and the management-corporation EIN 59-2170012 files a FY2022 990 with **no Schedule H**. No facility-isolable figure available. Source checked: [ProPublica EIN 59-0724459](https://projects.propublica.org/nonprofits/organizations/590724459); IRS index.
- **#19 Corewell Butterworth — filing unavailable.** Corewell Health West (38-2715520, the operating entity for Butterworth, $5.40B FY2023 total expenses, marked `HospitalInd=true`) filed a FY2023 e-file 990 that **contains Schedules D, J, O, R but no IRS990ScheduleH block** in the e-file XML retrieved — so no Line 7a charity-care figure is present to read. (This is itself notable: a $5.4B hospital operator with no parseable Schedule H in its e-file.) Total expenses are shown for context only; the ratio is not computable. Source: IRS e-file XML object 202403129349300230, retrieved 2026-06-24.
- **#20 Cape Fear Valley — filing unavailable.** The Cape Fear / Cumberland County Hospital System filing entity could not be unambiguously resolved to a Schedule-H-bearing e-file in the index within this milestone's search; marked unavailable rather than guessed. (Candidate: Cumberland County Hospital System Inc 56-0845796 — to confirm in M4 if needed.)

---

## Method + reproducibility

1. **Source of truth = IRS Modernized e-File (MeF) 990 XML**, the authoritative filing, not a summary. I downloaded the IRS annual index CSVs (`index_2021.csv … index_2024.csv`) from `https://apps.irs.gov/pub/epostcard/990/xml/<year>/index_<year>.csv`, mapped each hospital EIN → `OBJECT_ID` for its most recent **`990`** (not 990T/990EZ) return, then located and extracted that `<OBJECT_ID>_public.xml` from the IRS monthly bulk ZIPs at `https://apps.irs.gov/pub/epostcard/990/xml/2024/2024_TEOS_XML_<MM>A.zip` (the 2024 folder holds FY2023 returns). The deprecated `s3.amazonaws.com/irs-form-990` per-object bucket now 404s, and ProPublica's `download-xml` endpoint is Cloudflare-blocked to automated agents — the IRS bulk ZIPs are the reliable path.
2. From each XML I read three elements: `TaxPeriodEndDt`, `CYTotalExpensesAmt` (denominator), and `FinancialAssistanceAtCostTyp/NetCommunityBenefitExpnsAmt` (numerator, Schedule H Part I Line 7a col e). For Grady I additionally read `UnreimbursedMedicaidGrp` and `DirectOffsettingRevenueAmt` to explain the 0.00%.
3. Entity resolution used ProPublica Nonprofit Explorer's search and organization API (`projects.propublica.org/nonprofits/api/v2/…`) to find the correct operating-hospital EIN when the M1 parent EIN filed no Schedule H. Every dollar figure in the table traces to a single named EIN + e-file `OBJECT_ID` (FY2023). Each `OBJECT_ID` can be re-pulled from the same IRS bulk ZIP, or viewed on ProPublica at `projects.propublica.org/nonprofits/organizations/<EIN>` (Schedule H is in the linked full filing).

XML object IDs used (FY2023): Duke 202401369349301020 · Rex 202401299349304320 · Moses Cone Oper. 202412279349300946 · Novant 202433199349311768 · ECU/Pitt 202401919349300920 · WakeMed 202412289349304056 · NC Baptist 202443209349312174 · Cleveland Clinic 202423199349303332 · Penn 202401349349304080 · NYP 202413189349304986 · Henry Ford Providence 202411319349304866 · Dignity 202401329349300010 · Banner 202413209349312811 · FirstHealth 202412279349301761 · Grady 202423199349302397 · Sentara 202403139349301645 · Carilion 202412289349303876 · MGB group 202402269349300855 · Corewell West 202403129349300230 (no Sched H).

---

## Limitations & counter-evidence

- **At-cost net-of-offset accounting makes the numerator slippery, and Grady proves it.** Line 7a is charity care valued at cost *net of direct offsetting revenue* (Medicaid charity payments, DSH, indigent-care grants). A safety-net hospital whose charity cost is reimbursed by a county or state DSH program will show a low or zero *net* ratio (Grady = 0.00%, with $142.9M gross fully offset) while actually delivering large volumes of free care. The ratio measures **uncompensated cost the hospital itself absorbs**, which is what bears on the 501(r) "is it pulling its weight" question — but it is not a clean proxy for "amount of free care delivered." Low-ratio safety-net and public-funded hospitals (Grady; arguably NYP's Medicaid-heavy mix) must not be ranked as "stingy" without this caveat.
- **System / group aggregates are not the named facility.** Three reported ratios are aggregates, not the M1-named hospital: **#13 MGB 0.51%** is the entire 17-hospital MGB system group return ($21.6B), not Mass General alone — MGH (The General Hospital Corporation, 04-2697983) is not separately in the e-file XML index, so I could not isolate it; **#16 Dignity 1.35%** spans Dignity Health's multi-state hospitals, not St. Joseph's Phoenix alone; **#6 Novant** and **#18 Banner** are system-wide filers covering the named facility plus siblings. M4 must label these as system, not facility, observations. A facility with a generous local FAP can be buried inside a lower system average and vice versa.
- **Seven of 28 rows have no usable Schedule H figure (six "unavailable", one truly inapplicable governmental), plus four governance-inapplicable.** That is a real coverage gap: the computable peer set is **17 of the ~24 nominal 501(c)(3) filers**. The "unavailable" rows (Atrium CMC, UPMC, AdventHealth Orlando, Corewell, Cape Fear Valley) are **not** low spenders — they are entities that file a 990EZ group return, file under a parent with no Schedule H, are absent from the e-file XML extract, or whose facility EIN I could not resolve within this milestone. Scoring them D10 = 0 is the M1 rule mechanically applied ("not located = 0"), but M4 must read those zeros as **missing data, not measured non-compliance**, or it will libel five hospitals. That Corewell's $5.4B operating entity has *no Schedule H block in its e-file XML at all* is a genuine and surprising finding worth a second look, not yet a finding of non-compliance.
- **Single filing year; no multi-year smoothing.** Every ratio is FY2023 only (the most recent year uniformly available in the e-file extract). Charity care swings year to year with Medicaid policy, disaster relief, and one-time write-offs; a single year can mis-rank a hospital that had an atypical year. M4 should treat the bottom-quartile flags as "worth auditing," not "proven under-spenders," and ideally pull a 3-year average before publishing names. Fiscal-year-ends also differ (Jun/Sep/Dec), so FY2023 spans different real-world periods across rows.
- **The denominator choice changes the headline.** I use total functional expenses (the IRS Schedule H Line 7a col f basis). Lown Institute's "fair share" methodology instead compares community-benefit spending to the *value of the hospital's tax exemption*, which produces very different rankings ([Lown Institute Hospitals Index methodology](https://lownhospitalsindex.org/methodology/)). A hospital can clear my 1.0% bar yet still spend less than its tax break is worth. My ratio answers "how much of its spending is charity care," not "is it earning its exemption." Both are defensible; M4 should state which question it is answering.
- **Schedule H is self-reported and not line-item audited.** Hospitals exercise discretion in what they classify as financial assistance vs bad debt vs Medicaid shortfall, and the IRS rarely audits the at-cost computation. Cross-hospital comparisons assume consistent classification that is not guaranteed. The figures are the best public, traceable evidence available — but they are the hospital's own numbers.
- **EIN-substitution risk.** For the six corrected rows I matched the operating entity by name/location and confirmed `HospitalInd`/Schedule H presence, but a wrong-entity substitution would silently corrupt a ratio. Each substitution is documented in the EIN-reconciliation table with the e-file OBJECT_ID so it is re-checkable; if M4 finds a mismatch, that row should drop to "unavailable."

---

### Sources

- **Primary:** IRS Modernized e-File 990 XML, retrieved 2026-06-24 from the IRS bulk ZIPs at `https://apps.irs.gov/pub/epostcard/990/xml/2024/` (FY2023 returns) and the IRS annual index CSVs `https://apps.irs.gov/pub/epostcard/990/xml/<year>/index_<year>.csv`. Per-filing OBJECT_IDs listed in Method; each is re-pullable and is also linked from each org's [ProPublica Nonprofit Explorer](https://projects.propublica.org/nonprofits/) page (full filing → Schedule H).
- Schedule H Part I line definitions: IRS, [About Schedule H (Form 990)](https://www.irs.gov/forms-pubs/about-schedule-h-form-990) and [2025 Instructions for Schedule H](https://www.irs.gov/instructions/i990sh). XML element naming corroborated via the IRS990ScheduleH Part I metadata ([irsx.info skedh_part_i](http://www.irsx.info/metadata/parts/skedh_part_i.html)).
- Entity resolution: ProPublica Nonprofit Explorer search + organization API (`https://projects.propublica.org/nonprofits/api/`), accessed 2026-06-24.
- Peer-relative / fair-share framing and its alternative-denominator caveat: [Lown Institute Hospitals Index methodology](https://lownhospitalsindex.org/methodology/).
- Frozen sample, D10 rule, EIN list: `artifacts/2026-06-23-m1-rubric-and-sample.md`. D1–D9 scores this builds on: `artifacts/2026-06-24-m2-fap-pls-scoring.md`.
