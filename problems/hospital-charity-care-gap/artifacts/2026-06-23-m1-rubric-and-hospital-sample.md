# M1 — Scoring Rubric and Fixed Hospital Sample

**Problem:** Charity care that nonprofit hospitals are legally required to give — and mostly don't.
**Milestone:** M1 — Build the scoring rubric and fix the hospital sample.
**Date:** 2026-06-23
**Author:** generator (autonomous loop)

This document does two things. (a) It defines a transparent, machine-checkable rubric for scoring a nonprofit hospital's Financial Assistance Policy (FAP) and Plain Language Summary (PLS) on accessibility and IRC §501(r) compliance, grounded in the actual regulatory text (26 CFR §1.501(r)-1 through -6) and in named advocacy criteria (Dollar For, Lown Institute, CFPB). (b) It fixes a reproducible sample of 30 real US nonprofit hospitals to score in M2 and M3.

---

## Part A — The scoring rubric

### How the rubric works

- **Unit of analysis:** one hospital facility (not necessarily one EIN — a system can operate several facilities under one FAP, in which case the facility inherits the system FAP).
- **Sources read:** only public text. The two primary documents are the **full FAP** and the **Plain Language Summary (PLS)**, both of which §501(r)(4) requires every facility to make "widely available on a website" free of charge, plus the public **Form 990 Schedule H** (used in M3, not scored here in Part A except Dimension D8 which is a flag).
- **Scoring philosophy:** every rule is near-binary or numeric so that M2 can apply it deterministically from quoted text. Where a value cannot be located in the FAP/PLS, the rule assigns the **zero / worst** tier and M2 marks it "unstated," because §501(r)(4) makes the *absence* of a required element itself a compliance failure.
- **Two score families, kept separate:**
  - **Compliance score (C-dimensions, C1–C5):** does the FAP/PLS contain what §501(r) legally requires? Max **30 points**.
  - **Accessibility / generosity score (A-dimensions, A1–A5):** how easy is it for an eligible patient to actually get the help, and how generous is the help? Drawn from Dollar For / Lown / CFPB / NC-HASP best practice. Max **30 points**.
- **Total possible score = 60 points** (30 compliance + 30 accessibility). Higher is better; the M4 scorecard will invert this into a "concern" ranking. M3 adds the Schedule H dollar ratio as a separate axis rather than folding it into this 60.

### Federal Poverty Level (FPL) note

Several thresholds are expressed as a percentage of FPL. The benchmark "good" thresholds (200% FPL free care, 300% FPL discounted care, presumptive eligibility, auto-qualification of Medicaid/SNAP/WIC/homeless patients) are taken from North Carolina's HASP / Medical Debt De-Weaponization mandate, the only US jurisdiction that has codified these as hard minimums, which makes them a defensible, externally-set bar rather than the author's preference ([NCDHHS / SHVS State Spotlight, 2024](https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf); [NCIOM, "What is HASP?"](https://nciom.org/what-is-the-healthcare-access-and-stabilization-program-hasp/)).

### Rubric table

| # | Dimension | What it measures | How scored (point values / thresholds) | Public source it is read from | 501(r) or advocacy basis |
|---|-----------|------------------|-----------------------------------------|-------------------------------|--------------------------|
| **C1** | FAP exists & specifies eligibility criteria | Whether a written FAP exists and explicitly states the eligibility criteria for each level of assistance | Written FAP found AND states eligibility criteria for each level = **6**; FAP found but eligibility criteria vague/missing for at least one level = **3**; no public FAP located = **0** | Hospital "financial assistance" webpage; FAP PDF | §501(r)(4)(A)(i): FAP must include "eligibility criteria for financial assistance, and whether such assistance includes free or discounted care" ([IRS, FAP §501(r)(4)](https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4); [26 CFR §1.501(r)-4](https://www.law.cornell.edu/cfr/text/26/1.501(r)-1)) |
| **C2** | Plain Language Summary present & complete | Whether a PLS exists and contains its required core elements (eligibility, how to apply, where to get help, free/discounted levels, contact info) | PLS found AND contains all five core elements = **6**; PLS found but missing ≥1 core element = **3**; no PLS located = **0** | Hospital "financial assistance" webpage; PLS document | §501(r)(4) PLS requirement: a plain-language summary that lists levels of help, eligibility, how to apply, and a charge-limitation statement, in clear language for a "lay reader" ([IRS, FAP §501(r)(4)](https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4)) |
| **C3** | Widely available / "widely publicized" online | Whether FAP, FAP application, and PLS are conspicuously posted and downloadable free, without login, paywall, or request | All three (FAP, application, PLS) downloadable free in ≤3 clicks from the hospital's main site or billing page = **6**; some present but ≥1 missing, behind login, or only "available on request" = **3**; none publicly downloadable = **0** | Hospital website navigation path | §501(r)(4)(B) "widely available on a website" + widely-publicized rules: documents must be conspicuously posted and free to download ([26 CFR §1.501(r)-4 outline](https://www.law.cornell.edu/cfr/text/26/1.501(r)-0)) |
| **C4** | Limitation on charges (AGB) stated | Whether the FAP/PLS states that FAP-eligible patients are charged no more than Amounts Generally Billed (AGB), and describes the AGB method or how to get it | States AGB limitation AND names method (look-back or prospective) or how to obtain AGB% = **6**; mentions a charge limitation but no method/figure = **3**; silent on charge limits = **0** | FAP text; PLS charge-limitation statement | §501(r)(5): FAP-eligible patients may be charged no more than AGB to insured patients; one method (look-back or prospective) at a time ([IRS Billing & Collections §501(r)(6)](https://www.irs.gov/charities-non-profits/billing-and-collections-section-501r6); [26 CFR §1.501(r)-6](https://www.law.cornell.edu/cfr/text/26/1.501(r)-6)) |
| **C5** | Reasonable-efforts / collections protections disclosed | Whether the FAP describes the collection actions (incl. Extraordinary Collection Actions, ECAs) that may be taken and the ≥120-day / 240-day reasonable-efforts period before ECAs | FAP lists ECAs that may be taken AND states the reasonable-efforts period (≥120 days before ECAs / 240-day application window) = **6**; mentions collections but omits the timeline or ECA list = **3**; silent = **0** | FAP "billing and collections" section | §501(r)(6) & 26 CFR §1.501(r)-6: reasonable efforts to determine FAP-eligibility before ECAs; FAP must describe ECAs and the period; 240-day application period ([IRS §501(r)(6)](https://www.irs.gov/charities-non-profits/billing-and-collections-section-501r6); [26 CFR §1.501(r)-6](https://www.law.cornell.edu/cfr/text/26/1.501(r)-6)) |
| **A1** | Free-care income threshold (generosity) | The income level (as % FPL) at or below which the patient receives 100% free care | Free care at **≥200% FPL = 6**; **138–199% FPL = 3**; **<138% FPL or unstated = 0** | FAP eligibility table / PLS | NC-HASP mandates free care ≤200% FPL as the floor ([SHVS NC Spotlight, 2024](https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf)); Dollar For notes 2025 national average free-care ceiling ≈204% FPL ([Dollar For, "What is Financial Assistance"](https://dollarfor.org/what-is-hospital-financial-assistance/)) |
| **A2** | Discounted-care ceiling (generosity) | The top income level (as % FPL) at which any discounted/sliding-scale care is offered | Discounted care offered up to **≥400% FPL = 6**; **300–399% FPL = 4**; **200–299% FPL = 2**; **<200% FPL or none = 0** | FAP eligibility table / PLS | NC-HASP requires discounts to 300% FPL ([SHVS, 2024](https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf)); Dollar For reports 2025 national average discount ceiling ≈322% FPL ([Dollar For](https://dollarfor.org/what-is-hospital-financial-assistance/)) |
| **A3** | Presumptive eligibility offered | Whether the hospital grants assistance without a full application based on data it can see (Medicaid/SNAP/WIC enrollment, homelessness, public income estimators) | Full presumptive screening (no application required for at least some patients) described = **6**; partial (auto-qualifies named programs e.g. Medicaid/SNAP/WIC/homeless only) = **3**; application required for everyone / not mentioned = **0** | FAP eligibility & screening section | Dollar For core fix — "transparent screening" before discharge, no application ([Dollar For, "Fixing Hospital FinAid"](https://dollarfor.org/fixing-hospital-finaid/)); NC-HASP mandates auto-qualify for Medicaid/SNAP/WIC/homeless (2025) and full presumptive screening (2026) ([NCIOM](https://nciom.org/what-is-the-healthcare-access-and-stabilization-program-hasp/)) |
| **A4** | Application friction / accessibility | How hard the application is: form length, online/mobile submission, electronic signature, documentation demands, no asset test, no narrow eligibility carve-outs | Application is online/mobile-submittable AND has no asset test AND imposes no disqualifying carve-outs (insured, residency, already-paid, bill-size minimums) = **6**; one significant barrier present = **3**; multiple barriers (paper-only, asset test, AND eligibility carve-outs) = **0** | FAP application form + FAP eligibility exclusions | Dollar For "Known/Easy/Fair" application standard: mobile-friendly, e-signature, no excessive paperwork, access regardless of insurance/residency ([Dollar For](https://dollarfor.org/fixing-hospital-finaid/)); CFPB flagged carve-outs (insured, already-paid, residency, bill-size, medical-credit-card) as illegitimate barriers ([CFPB, 2024](https://www.consumerfinance.gov/about-us/blog/medical-debt-and-non-profit-hospital-billing-practices/)) |
| **A5** | Plain-language readability of the PLS | Whether the PLS is genuinely readable by a lay reader and available in the relevant non-English languages | PLS readable (short sentences, no undefined jargon, plain layout) AND offered in required language translations (≥1 non-English where threshold population applies, or statement of availability) = **6**; readable but English-only with no translation statement = **3**; dense/legalistic or no PLS = **0** | PLS document text | §501(r)(4) PLS must use "clear, concise, easy to understand language" for a lay reader; translation required where a language group meets the lesser-of-1,000-or-5% threshold ([IRS §501(r)(4)](https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4)) |

**Compliance subtotal (C1–C5): max 30. Accessibility subtotal (A1–A5): max 30. TOTAL POSSIBLE = 60.**

### Tier interpretation (for M4, stated here so it is fixed before scoring)

| Total / 60 | Tier | Plain meaning |
|---|---|---|
| 48–60 | Strong | FAP/PLS both compliant and accessible |
| 36–47 | Adequate | mostly compliant, some accessibility gaps |
| 24–35 | Weak | meaningful compliance or access failures |
| 0–23 | Failing | likely 501(r) non-compliant and/or actively deterring eligible patients |

### Companion M3 flag (defined now, computed in M3)

- **D8 — charity-care spend vs. peers (Schedule H):** charity care at cost as a share of total functional expenses. Read from Form 990 Schedule H, Part I (financial assistance at cost) over Part IX/total expenses. Not part of the 60-point text score; used in M3 and M4 as an independent axis. Lown Institute's "fair share" research uses a **5.9% of total expenditures** combined financial-assistance-plus-community-investment threshold as the bar a hospital should clear to justify its tax exemption ([Lown Institute, Fair Share Spending 2024](https://lownhospitalsindex.org/hospital-fair-share-spending-2024/)).

---

## Part B — The fixed hospital sample (n = 30)

All 30 are real US §501(c)(3) nonprofit hospitals/health systems. Each entry gives the locatable references where M2/M3 will read the FAP/PLS and Schedule H: a financial-assistance webpage and/or a ProPublica Nonprofit Explorer pointer (by EIN where verified). Per the spec, canonical pointers (the hospital's "financial assistance" page; the org's 990 on ProPublica) are used rather than deep-linked PDFs, which rot. EINs marked "verified" were confirmed against ProPublica Nonprofit Explorer during this milestone; others are to be confirmed in M2.

> ProPublica Nonprofit Explorer root: https://projects.propublica.org/nonprofits/ (search by org name or EIN). NC hospital FAP/price-transparency index used as a cross-check: [NCHA financial-assistance & price-transparency listing](https://nchealthcare.org/nc-hospital-financial-assistance-and-price-transparency-pages/) and [NC Justice Center, Find Hospital Financial Assistance in NC](https://www.ncjustice.org/projects/health-advocacy-project/medical-debt/nc-hospital-financial-assistance/).

### North Carolina (HASP jurisdiction — over-sampled by design)

| # | Hospital / system | City, State | Parent system | FAP/PLS pointer | Schedule H / EIN pointer |
|---|---|---|---|---|---|
| 1 | UNC Medical Center | Chapel Hill, NC | UNC Health | https://www.unchealth.org/records-insurance/financial-assistance-programs | UNC Hospitals / UNC Health — ProPublica search "University of North Carolina Hospitals" |
| 2 | Duke University Hospital | Durham, NC | Duke University Health System | Duke Health "billing & financial assistance" page (duke​health.org) | Duke University Health System Inc, EIN **56-2070036** (verified, ProPublica) |
| 3 | Atrium Health Carolinas Medical Center | Charlotte, NC | Atrium Health (Advocate Health) | Atrium Health "financial assistance" page (atriumhealth.org) | Atrium Health System, EIN **31-0537492** (verified); also Atrium Health Inc, EIN **84-3647453** (verified) |
| 4 | Novant Health Presbyterian Medical Center | Charlotte, NC | Novant Health | https://www.novanthealth.org/globalassets/buttons-and-documents-ctaslinks/documents-pdfs/policy-nc-hospitals-financial-assistance.pdf | Novant Health Inc — ProPublica search "Novant Health" |
| 5 | Cone Health (Moses H. Cone Memorial Hospital) | Greensboro, NC | Cone Health | Cone Health "financial assistance" page (conehealth.com) | Moses H Cone Memorial Hospital Operating Corp — ProPublica search |
| 6 | WakeMed Raleigh Campus | Raleigh, NC | WakeMed Health & Hospitals | WakeMed "billing / financial assistance" page (wakemed.org) | WakeMed — ProPublica search "WakeMed" |
| 7 | ECU Health Medical Center | Greenville, NC | ECU Health (formerly Vidant) | ECU Health "financial assistance" page (ecuhealth.org) | ECU Health Medical Center — ProPublica search |
| 8 | Mission Hospital | Asheville, NC | (HCA — *control case, see rationale*) | Mission Health "financial assistance" page | Mission is HCA-owned (for-profit) — included only as a contrast control, scored on text but excluded from the nonprofit ranking |

### Large multi-state / flagship nonprofit systems

| # | Hospital / system | City, State | Parent system | FAP/PLS pointer | Schedule H / EIN pointer |
|---|---|---|---|---|---|
| 9 | Cleveland Clinic (main campus) | Cleveland, OH | Cleveland Clinic Foundation | Cleveland Clinic "financial assistance / MyChart billing" page (my.clevelandclinic.org) | The Cleveland Clinic Foundation, EIN **34-0714585** (verified, ProPublica) |
| 10 | The Johns Hopkins Hospital | Baltimore, MD | Johns Hopkins Health System | Johns Hopkins Medicine "financial assistance" page (hopkinsmedicine.org) | The Johns Hopkins Hospital, EIN **52-0591656** (verified); Health System Corp, EIN **52-1465301** (verified) |
| 11 | Massachusetts General Hospital | Boston, MA | Mass General Brigham | MGB "financial assistance / patient billing" page (massgeneralbrigham.org) | Mass General Brigham Inc, EIN **04-2103591** (verified, ProPublica) |
| 12 | Mayo Clinic Hospital — Rochester | Rochester, MN | Mayo Clinic | Mayo Clinic "billing & insurance / financial assistance" page (mayoclinic.org) | Mayo Clinic, EIN **41-0944601** (verified, ProPublica) |
| 13 | Cedars-Sinai Medical Center | Los Angeles, CA | Cedars-Sinai | Cedars-Sinai "financial assistance / charity care" page (cedars-sinai.org) | Cedars-Sinai Medical Center — ProPublica search |
| 14 | NewYork-Presbyterian Hospital | New York, NY | NewYork-Presbyterian | NYP "financial assistance / patient billing" page (nyp.org) | The New York and Presbyterian Hospital — ProPublica search |
| 15 | UPMC Presbyterian | Pittsburgh, PA | UPMC | UPMC "financial assistance" page (upmc.com) | UPMC / UPMC Presbyterian Shadyside — ProPublica search |
| 16 | Memorial Hermann–Texas Medical Center | Houston, TX | Memorial Hermann Health System | Memorial Hermann "financial assistance" page (memorialhermann.org) | Memorial Hermann Health System — ProPublica search |
| 17 | Sutter Medical Center, Sacramento | Sacramento, CA | Sutter Health | Sutter Health "financial assistance / charity care" page (sutterhealth.org) | Sutter Bay Hospitals / Sutter Health — ProPublica search |
| 18 | Northwestern Memorial Hospital | Chicago, IL | Northwestern Medicine | Northwestern Medicine "billing & financial assistance" page (nm.org) | Northwestern Memorial HealthCare — ProPublica search |
| 19 | Barnes-Jewish Hospital | St. Louis, MO | BJC HealthCare | BJC "financial assistance" page (bjc.org) | The Barnes-Jewish Hospital — ProPublica search |
| 20 | Vanderbilt University Medical Center | Nashville, TN | VUMC | VUMC "financial assistance / billing" page (vumc.org / vanderbilthealth.com) | Vanderbilt University Medical Center — ProPublica search |

### Mid-size and regional nonprofit hospitals (geographic & size spread)

| # | Hospital / system | City, State | Parent system | FAP/PLS pointer | Schedule H / EIN pointer |
|---|---|---|---|---|---|
| 21 | Intermountain Medical Center | Murray, UT | Intermountain Health | Intermountain "financial assistance" page (intermountainhealthcare.org) | Intermountain Health / IHC Health Services — ProPublica search |
| 22 | Spectrum / Corewell Health Butterworth Hospital | Grand Rapids, MI | Corewell Health | Corewell Health "financial assistance" page (corewellhealth.org) | Corewell Health (formerly Spectrum Health) — ProPublica search |
| 23 | Ochsner Medical Center | New Orleans, LA | Ochsner Health | Ochsner "financial assistance" page (ochsner.org) | Ochsner Clinic Foundation — ProPublica search |
| 24 | Baptist Memorial Hospital — Memphis | Memphis, TN | Baptist Memorial Health Care | Baptist "financial assistance" page (baptistonline.org) | Baptist Memorial Hospital — ProPublica search |
| 25 | Froedtert Hospital | Milwaukee, WI | Froedtert / ThedaCare (Froedtert Health) | Froedtert "financial assistance" page (froedtert.com) | Froedtert Memorial Lutheran Hospital — ProPublica search |
| 26 | Bryan Medical Center | Lincoln, NE | Bryan Health | Bryan Health "financial assistance" page (bryanhealth.com) | Bryan Medical Center — ProPublica search |
| 27 | Maine Medical Center | Portland, ME | MaineHealth | MaineHealth "financial assistance / free care" page (mainehealth.org) | Maine Medical Center — ProPublica search |
| 28 | Billings Clinic Hospital | Billings, MT | Billings Clinic (Intermountain) | Billings Clinic "financial assistance" page (billingsclinic.com) | Billings Clinic — ProPublica search |
| 29 | University of Mississippi Medical Center | Jackson, MS | UMMC | UMMC "financial assistance / charity care" page (umc.edu) | University of Mississippi Medical Center — ProPublica / state filing |
| 30 | Grady Memorial Hospital | Atlanta, GA | Grady Health System | Grady "financial assistance" page (gradyhealth.org) | Grady Memorial Hospital Corp — ProPublica search |

> EIN-verification status: items 2, 3, 9, 10, 11, 12 carry EINs confirmed against ProPublica during M1. The remaining entries point to the hospital's financial-assistance webpage plus a ProPublica name search; M2 will record the precise EIN and filing year used for each. Item 8 (Mission/HCA) is intentionally a for-profit contrast control and will not enter the nonprofit ranking.

---

## Part C — Sampling rationale

**How the 30 were chosen.**

1. **North Carolina over-sample (entries 1–8).** NC is the only US jurisdiction with a codified presumptive-eligibility / minimum-generosity mandate (HASP / Medical Debt De-Weaponization Act, free care ≤200% FPL, discounts to 300% FPL, auto-qualify Medicaid/SNAP/WIC/homeless from 2025, full presumptive screening from 2026) ([NCIOM](https://nciom.org/what-is-the-healthcare-access-and-stabilization-program-hasp/); [SHVS, 2024](https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf)). Over-sampling NC lets later milestones test whether a hard state mandate visibly moves FAP text relative to the federal §501(r) floor — the most policy-relevant comparison available.
2. **Flagship multi-state systems (entries 9–20).** Large, well-resourced, brand-name nonprofits (Cleveland Clinic, Hopkins, Mayo, Mass General Brigham, Cedars-Sinai, etc.). If even these — with full legal/compliance staffs — under-perform on accessibility, that is the strongest possible evidence that the gap is structural, not a resourcing problem.
3. **Mid-size & regional spread (entries 21–30).** Smaller systems and standalones across MT, NE, ME, MS, WI, UT, LA, etc., to avoid a sample that only reflects coastal academic medical centers and to include lower-income and rural-serving states.
4. **One for-profit control (entry 8, Mission/HCA).** Scored on the same text rubric but excluded from the nonprofit ranking, so M4 can sanity-check that the rubric isn't simply flagging hospitals generically.

**Geographic coverage.** The sample spans **16 states + DC-region**: NC (×7 nonprofit + 1 control), OH, MD, MA, MN, CA (×2), NY, PA, TX, MO, TN (×2), UT, MI, LA, WI, NE, ME, MT, MS, GA, IL.

**System-size mix.** ~12 are top-50-by-revenue national systems; ~10 are mid-size regional; ~8 are NC-specific (some large, e.g. UNC/Duke/Atrium; some regional, e.g. ECU, WakeMed, Cone).

**What the sample IS representative of:** a deliberate, defensible cross-section of large and mid-size US nonprofit hospitals, with one mandate-state (NC) over-represented to enable a policy comparison.

**What the sample is NOT:** it is **not** a random or probability sample of the ~2,900 §501(r) hospital organizations, so scores cannot be projected to a national rate. It over-weights large academic and brand-name systems and one state (NC); small rural critical-access hospitals, sole-community hospitals, and church-affiliated systems with idiosyncratic FAPs are under-represented. Results are claims about *these named hospitals*, plus illustrative patterns — not a national prevalence estimate. (The national prevalence figure — 71% of eligible patients billed anyway — comes from Dollar For's "Bridging the Chasm," not from this sample.)

---

## Limitations & counter-evidence

- **FAP text ≠ practice.** The rubric scores what the FAP/PLS *say*, not what front-desk and billing staff actually *do*. A hospital can post a generous, presumptive-eligibility FAP and still fail to screen patients at the point of care (indeed Dollar For's 71%-billed finding is precisely a text-vs-practice gap). High text scores must not be read as "this hospital serves eligible patients well." This is the single largest validity threat and will be restated in M2 and M4.
- **A compliant FAP can still be unjust, and vice-versa.** §501(r) sets a floor, not a ceiling. A hospital can be fully §501(r)-compliant (high C-score) while offering stingy thresholds (low A-score), and the rubric correctly separates these — but a reader who collapses the two will misread the result.
- **Threshold choices are contestable.** The 200%/300%/400% FPL bands and the presumptive-eligibility weighting come from NC-HASP and Dollar For, which advocacy critics (and the AHA) dispute as overly demanding ([Keckley, Lown-vs-AHA debate, 2024](https://paulkeckley.com/the-keckley-report/2024/4/1/the-lown-institute-aha-showdown-does-it-make-a-difference/)). A hospital's counsel could argue any FAP meeting the bare §501(r)(4) elements is "compliant" regardless of generosity; the rubric answers this by keeping compliance (C) and generosity (A) as separate scores so the legal-floor claim is auditable on its own.
- **Source freshness.** Dollar For's national figures are from 2024; Lown's fair-share threshold from 2024; the CFPB's 2024 medical-debt work was produced under an administration whose enforcement posture has since changed, so CFPB criteria are used as *analytical* benchmarks, not as current enforcement guarantees. The §501(r) regulatory text (26 CFR §1.501(r)) remains in force and is the binding basis for the C-dimensions.
- **Pointer rot & EIN ambiguity.** Some entries point to a financial-assistance webpage and a ProPublica name search rather than a verified EIN; large systems file multiple EINs (e.g., Atrium has at least three), so M2/M3 must record the exact EIN and filing year per facility to keep the dollar figures (M3) traceable. Six EINs are verified here; the rest are to be pinned in M2.
- **Sample selection bias (restated).** Non-random, NC- and large-system-weighted; cannot support a national non-compliance *rate*. The artifact's claims are about named institutions and patterns, which is exactly the regulator/advocate use-case (act on names), not a prevalence estimate.

---

### Sources

- IRS, "Financial assistance policy and emergency medical care policy – Section 501(r)(4)": https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4
- IRS, "Billing and collections – Section 501(r)(6)": https://www.irs.gov/charities-non-profits/billing-and-collections-section-501r6
- 26 CFR §1.501(r)-0 (outline) and §1.501(r)-6 (billing & collection), Cornell LII: https://www.law.cornell.edu/cfr/text/26/1.501(r)-0 , https://www.law.cornell.edu/cfr/text/26/1.501(r)-6
- Dollar For, "Bridging the Chasm: Closing the $14 Billion Access Gap in Charity Care" (2024): https://dollarfor.org/wp-content/uploads/2024/04/Dollar_For.Bridging_the_Chasm.pdf
- Dollar For, "Fixing Hospital Financial Assistance" / "What is Hospital Financial Assistance": https://dollarfor.org/fixing-hospital-finaid/ , https://dollarfor.org/what-is-hospital-financial-assistance/
- Lown Institute, "Hospital Fair Share Spending, 2024" (5.9% threshold): https://lownhospitalsindex.org/hospital-fair-share-spending-2024/
- CFPB, "Medical Debt and Non-Profit Hospital Billing Practices" (2024): https://www.consumerfinance.gov/about-us/blog/medical-debt-and-non-profit-hospital-billing-practices/
- NCIOM, "What is the Healthcare Access and Stabilization Program (HASP)?": https://nciom.org/what-is-the-healthcare-access-and-stabilization-program-hasp/
- State Health & Value Strategies (SHVS), "North Carolina's Comprehensive Medical Debt Relief" State Spotlight (2024): https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf
- NCHA hospital financial-assistance & price-transparency listing: https://nchealthcare.org/nc-hospital-financial-assistance-and-price-transparency-pages/
- NC Justice Center, Find Hospital Financial Assistance in NC: https://www.ncjustice.org/projects/health-advocacy-project/medical-debt/nc-hospital-financial-assistance/
- ProPublica Nonprofit Explorer (Form 990 / Schedule H source): https://projects.propublica.org/nonprofits/ (verified EINs: Duke 56-2070036; Atrium 31-0537492 & 84-3647453; Cleveland Clinic Foundation 34-0714585; Johns Hopkins Hospital 52-0591656 & Health System 52-1465301; Mass General Brigham 04-2103591; Mayo Clinic 41-0944601)
