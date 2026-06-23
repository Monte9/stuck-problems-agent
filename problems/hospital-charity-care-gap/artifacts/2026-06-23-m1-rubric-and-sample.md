# M1 — FAP/PLS Accessibility & 501(r) Compliance Scoring Rubric + Fixed Hospital Sample

> Generated 2026-06-23. Milestone 1 of the hospital-charity-care-gap chain.
> Purpose: define a transparent, machine-checkable rubric for scoring nonprofit-hospital
> Financial Assistance Policies (FAPs), Plain Language Summaries (PLS), and Schedule H
> charity-care spending against IRC Section 501(r), and fix a reproducible sample of
> hospitals to score in M2–M4.

This document is the *measurement contract*. M2 reads FAP/PLS text against dimensions
D1–D8; M3 reads Schedule H against D9–D10; M4 combines them. Every score below resolves
to a number with no subjective adjective. Where a dimension rests on a statute, the
governing text is 26 CFR § 1.501(r)-4 (the final Treasury/IRS regulations implementing
IRC § 501(r), effective for tax years beginning after 29 Dec 2015). Where it rests on
advocacy benchmarks, the source is Dollar For, the Lown Institute, or the CFPB.

---

## (a) Scoring rubric

**Max possible score = 100 points**, split into two blocks:

- **Accessibility & 501(r) text compliance (D1–D8): 70 points** — read from the FAP and PLS text. Scored in M2.
- **Charity-care generosity (D9–D10): 30 points** — read from Form 990 Schedule H. Scored in M3.

Each dimension's max is shown in the "How scored" column; the column maxes sum to 100.

| # | Dimension | What it measures | How scored (point values / thresholds) | Public source it is read from | 501(r) provision or advocacy basis |
|---|-----------|------------------|------------------------------------------|-------------------------------|-------------------------------------|
| **D1** | FAP is publicly posted & retrievable | Whether the full written FAP document can be located on the hospital website by a non-expert in ≤3 clicks from a "billing/financial assistance/patient resources" entry point, without login or payment. | **10** = full FAP PDF/page found ≤3 clicks from a top-level billing/patients menu; **5** = found only via site-search or >3 clicks; **0** = not locatable from the hospital site (only a phone number, or 404/dead link). | Hospital website (FAP page) | 26 CFR § 1.501(r)-4(b)(5) "widely publicizing" requires the FAP be "widely available on a website." |
| **D2** | Plain Language Summary exists & is genuinely plain | Whether a distinct PLS document exists and meets the regulation's "clear, concise, and easy to understand" standard, proxied by a readability test. | **10** = distinct PLS document exists **and** Flesch–Kincaid grade level ≤8 (or equivalently Flesch Reading Ease ≥60); **5** = PLS exists but grade level 9–12; **0** = no distinct PLS, or grade level >12, or only the full legalese FAP is offered as the "summary." | Hospital website (PLS document); readability computed with a fixed tool (e.g. `textstat`) | 26 CFR § 1.501(r)-4(c) requires a PLS "written … in a manner reasonably calculated to be understood." Plain-language proxy aligns with CFPB's emphasis on consumer comprehensibility. |
| **D3** | Income eligibility threshold for **free** care | Generosity of the cutoff at or below which care is 100% free. | **10** = free care to **≥250% FPL**; **8** = **200–249% FPL**; **5** = **138–199% FPL**; **2** = **100–137% FPL**; **0** = below 100% FPL **or** threshold not stated in the FAP. | FAP eligibility section | 26 CFR § 1.501(r)-4(b)(1)(i) requires eligibility criteria be stated. Threshold tiers benchmarked to Dollar For (recommends ≥200% FPL free) and NC HASP minimum (free ≤200% FPL). |
| **D4** | Discounted-care (sliding scale) ceiling | Upper income bound for any partial/discounted assistance. | **8** = discounts extend to **≥400% FPL**; **5** = **300–399% FPL**; **3** = **201–299% FPL**; **0** = no discount tier above the free-care cutoff, or unstated. | FAP eligibility / discount schedule | 26 CFR § 1.501(r)-4(b)(1)(i)–(ii). Benchmark: NC HASP requires 50–75% discounts up to 300% FPL; Dollar For flags absence of a discount tier as a barrier. |
| **D5** | Presumptive eligibility offered | Whether the FAP grants assistance **without a full application** based on data the hospital can already see (Medicaid/SNAP/WIC enrollment, homelessness, prior FAP grant, or a third-party income estimator). | **12** = FAP explicitly grants **automatic/presumptive** eligibility from enrollment in ≥1 named means-tested program **or** an income estimator, with no application required; **6** = presumptive determination mentioned but discretionary, vendor-scored only, or limited to one narrow category; **0** = application is required in all cases, or presumptive eligibility is not mentioned. | FAP "presumptive eligibility" / "other sources of information" section | 26 CFR § 1.501(r)-4(b)(1)(iii) & (b)(4) permit determining eligibility from third-party info. Core fix per Dollar For "Bridging the Chasm" (2024); mandated in NC effective 1 Jan 2025 (auto-qualify) / 1 Jan 2026 (full screening). |
| **D6** | Application friction | How hard it is to apply when an application *is* required. | **8** = application downloadable online **and** accepts proof by mail/email/portal **and** does not require notarization or in-person submission; **4** = online form exists but requires in-person drop-off **or** lists ≥4 mandatory document types; **0** = no downloadable application (phone/office only) **or** application not findable. | FAP application form + "how to apply" section | 26 CFR § 1.501(r)-4(b)(2) requires the FAP describe the application method and 1.501(r)-4(b)(5)(ii) requires the application form be online. Friction-as-deterrent is the central CFPB / Dollar For critique. |
| **D7** | AGB (limitation on charges) disclosure | Whether the FAP states that FAP-eligible patients are not charged more than Amounts Generally Billed to insured patients, and states the AGB method. | **6** = FAP states the AGB cap **and** names the method (look-back or prospective) **and** gives the AGB percentage or how to obtain it; **3** = AGB cap stated but method/percentage absent; **0** = no AGB statement. | FAP "limitation on charges" section / PLS | 26 CFR § 1.501(r)-4(b)(1)(ii) and § 1.501(r)-5 (limitation on charges). PLS must state the AGB protection per 1.501(r)-4(c)(2). |
| **D8** | Billing & collections / ECA safeguards | Whether the FAP describes the actions taken for nonpayment, the 240-day application period, and the "reasonable efforts" made before Extraordinary Collection Actions (ECAs). | **6** = FAP describes nonpayment actions **and** states the ≥240-day FAP-application period **and** commits to a reasonable-efforts/notification step before ECAs; **3** = nonpayment actions described but ECA safeguards or 240-day window omitted; **0** = no billing/collections section. | FAP "billing and collections" section | 26 CFR § 1.501(r)-4(b)(4) (actions for nonpayment) and § 1.501(r)-6 (240-day notification period; reasonable efforts before ECAs). CFPB 2024 flagged collections on FAP-eligible patients. |
| **D9** | Charity care as share of expense (Schedule H) | Charity care **at cost** as a percent of total functional expenses — the most direct generosity signal. | **18** = ratio **≥4.0%**; **13** = **2.0–3.99%**; **8** = **1.0–1.99%**; **3** = **0.1–0.99%**; **0** = **<0.1%** or not reported. | Form 990 Schedule H, Part I line 7a (financial assistance at cost) ÷ Form 990 Part IX total functional expenses (denominator definition fixed in M3). | IRS Form 990 Schedule H is the 501(r)-linked community-benefit return. Threshold framing draws on Lown Institute "Fair Share" (5.9% of expenses on financial assistance + community investment combined as the full-fair-share bar). |
| **D10** | Peer-relative charity-care position | Where the hospital's D9 ratio sits relative to the rest of the sample, so chronic low spenders are flagged even if their absolute ratio looks non-trivial. | **12** = **top quartile** of the sample's D9 ratio; **8** = **2nd quartile (above median)**; **4** = **3rd quartile**; **0** = **bottom quartile**. Quartiles computed across all sample hospitals with a usable filing in M3. | Form 990 Schedule H, same line items as D9, ranked within the M1 sample | Lown Institute "Fair Share Spending" peer-relative method; Dollar For "Bottom Line" peer comparisons. Relative scoring guards against grading everyone against an arbitrary absolute bar. |

**Internal-consistency check (column maxes):** D1 10 + D2 10 + D3 10 + D4 8 + D5 12 + D6 8 + D7 6 + D8 6 = **70** (accessibility block). D9 18 + D10 12 = **30** (generosity block). Total = **100**. A higher total = more accessible / more compliant / more generous; the M4 scorecard inverts this into a "concern" ranking (low score = high concern).

**Handling of "not found":** If a FAP/PLS cannot be located in M2, D1–D8 are not silently zeroed by fiat — the hospital is marked **"FAP not found"** with the search trail recorded, and treated as D1=0 with the remaining text dimensions flagged "unscored — document not located" so the failure mode (no public document) is visible and distinct from a located-but-weak policy. Likewise a missing Schedule H in M3 is "filing unavailable," not a zero.

---

## (b) Sample of nonprofit hospitals / hospital organizations (28)

All EINs and ProPublica Nonprofit Explorer organization pages below were located via ProPublica
Nonprofit Explorer (`projects.propublica.org/nonprofits/organizations/<EIN>`), which hosts the
Form 990 + Schedule H filings M3 will read. FAP/PLS pages will be retrieved in M2 from each
system's public "financial assistance" web page; the URL stems below are the entry points M2
will start from (M2 records the exact final URL and quote). EINs are written without dashes to
match the ProPublica URL slug.

| # | Hospital / organization | City, State | Parent system | EIN (ProPublica org page) | FAP/PLS web entry point (for M2) |
|---|--------------------------|-------------|----------------|----------------------------|-----------------------------------|
| 1 | Charlotte-Mecklenburg Hospital Authority (Atrium Health) | Charlotte, **NC** | Advocate Health / Atrium Health | 561376950 *(see note)* / Atrium Health Inc 843647453 | atriumhealth.org → Patients & Visitors → Financial Assistance |
| 2 | Moses H. Cone Memorial Hospital | Greensboro, **NC** | Cone Health (Risant/Kaiser) | 560532302 | conehealth.com → Patients & Visitors → Billing & Financial Assistance |
| 3 | WakeMed | Raleigh, **NC** | WakeMed Health & Hospitals (independent) | 566017737 | wakemed.org → Patients & Visitors → Billing → Financial Assistance |
| 4 | East Carolina Health (ECU Health Medical Center) | Greenville, **NC** | ECU Health | 911997979 | ecuhealth.org → Patients & Visitors → Financial Assistance |
| 5 | Duke University Health System Inc | Durham, **NC** | Duke Health | 562070036 | dukehealth.org → Patients → Billing → Financial Assistance |
| 6 | Novant Health Inc | Winston-Salem, **NC** | Novant Health | 561376950 *(see note)* | novanthealth.org → Patients → Billing → Financial Assistance |
| 7 | The Cleveland Clinic Foundation | Cleveland, OH | Cleveland Clinic | 340714585 (filing entity) | clevelandclinic.org → Patients → Billing & Insurance → Financial Assistance |
| 8 | Mayo Clinic (Rochester) | Rochester, MN | Mayo Clinic | 416011702 | mayoclinic.org → Patient & Visitor Guide → Billing → Financial Assistance |
| 9 | Cedars-Sinai Medical Center | Los Angeles, CA | Cedars-Sinai | 951644600 | cedars-sinai.org → Patients & Visitors → Billing → Financial Assistance |
| 10 | NYU Langone Hospitals | New York, NY | NYU Langone Health | 133971298 | nyulangone.org → Insurance & Billing → Financial Assistance |
| 11 | Sutter Health | Sacramento, CA | Sutter Health | 942788907 | sutterhealth.org → For Patients → Billing → Financial Assistance |
| 12 | Banner Health | Phoenix, AZ | Banner Health | 450233470 | bannerhealth.com → Patients & Visitors → Financial Assistance |
| 13 | Intermountain Health Care Inc | Salt Lake City, UT | Intermountain Health | 870269232 | intermountainhealthcare.org → Billing → Financial Assistance |
| 14 | Baylor Scott & White Health | Dallas, TX | Baylor Scott & White | 463131350 | bswhealth.com → Patient Tools → Billing → Financial Assistance |
| 15 | Trinity Health Corporation | Livonia, MI | Trinity Health (Catholic) | 351443425 | trinity-health.org / local-site → Financial Assistance |
| 16 | UPMC | Pittsburgh, PA | UPMC | 251778658 | upmc.com → Patients & Visitors → Billing → Financial Assistance |
| 17 | Geisinger Medical Center | Danville, PA | Geisinger | 240795959 | geisinger.org → Patient Care → Billing → Financial Assistance |
| 18 | Corewell Health (formerly Spectrum/Beaumont) | Grand Rapids, MI | Corewell Health | 611740292 | corewellhealth.org → Patients & Visitors → Billing → Financial Assistance |
| 19 | Icahn School of Medicine / Mount Sinai Hospital | New York, NY | Mount Sinai Health System | 136171197 (Icahn) / Mount Sinai Hospital files separately | mountsinai.org → Patient Care → Billing → Financial Assistance |
| 20 | Johns Hopkins Health System–affiliated (Johns Hopkins University filing) | Baltimore, MD | Johns Hopkins Medicine | 520595110 (university filer) | hopkinsmedicine.org → Patient Care → Billing → Financial Assistance |
| 21 | Mayo Clinic Health System (regional) | Eau Claire, WI | Mayo Clinic | 390813418 | mayoclinichealthsystem.org → Billing → Financial Assistance |
| 22 | Baylor Scott & White Medical Center – Centennial | Frisco, TX | Baylor Scott & White | 824052186 | bswhealth.com (facility page) → Financial Assistance |
| 23 | Atrium Medical Center | Middletown, OH | Premier Health | 311079309 | premierhealth.com → Patients → Billing → Financial Assistance |
| 24 | NYU Langone Health System | New York, NY | NYU Langone Health | 472613531 | nyulangone.org → Insurance & Billing → Financial Assistance |
| 25 | Geisinger System Services | Danville, PA | Geisinger | 232164794 | geisinger.org → Billing → Financial Assistance |
| 26 | Cedars-Sinai Medical Care Foundation | Beverly Hills, CA | Cedars-Sinai | 954457756 | cedars-sinai.org → Billing → Financial Assistance |
| 27 | Intermountain Healthcare Foundation Inc | Salt Lake City, UT | Intermountain Health | 800225150 | intermountainhealthcare.org → Financial Assistance |
| 28 | The Moses H. Cone Memorial Hospital Operating Corporation | Greensboro, **NC** | Cone Health | 581588823 | conehealth.com → Billing & Financial Assistance |

**Notes & caveats on the EINs (to be resolved, not assumed, in M2/M3):**

- **EIN 561376950 appears for both Atrium (Charlotte-Mecklenburg Hospital Authority) and Novant Health Inc in different ProPublica search results.** This is an unresolved ambiguity from the desk search. M3 must open the ProPublica org page for 561376950, read the legal name on the filing, and assign it to whichever entity it actually belongs to (almost certainly Novant Health Inc; Atrium's primary recent filer entity is **Atrium Health Inc, EIN 843647453**). Until verified, rows 1 and 6 are flagged as **EIN-ambiguous** and M3 will confirm both before using any dollar figures.
- **Cleveland Clinic** appears under multiple EINs in ProPublica (340714585 as the historical filing entity; 912153073 also surfaced). M3 will use whichever entity carries the operating-hospital Schedule H; both are recorded here.
- Several large systems file **system-level group returns** rather than per-hospital returns; the Schedule H read in M3 is therefore at the filing-entity level stated in the EIN column, and the FAP read in M2 is at the system level unless a named facility (rows 22, 23) has its own policy. This system-vs-facility level mismatch is an explicit limitation (below).
- The **web entry points are navigation stems, not deep links** — they describe the click path M2 will follow. M2 records the exact resolved URL and a verbatim quote for every score, and marks any hospital whose FAP/PLS cannot be reached as "FAP not found."

---

## (c) Sampling rationale

**How the 28 were chosen.** This is a *purposive*, not random, sample built to exercise the
rubric across the axes the rubric cares about, while keeping every entity verifiable in
ProPublica Nonprofit Explorer:

1. **North Carolina over-weighting (6 of 28: rows 1–6, 28).** NC is the only state mandating
   presumptive eligibility — auto-qualification of Medicaid/SNAP/WIC/homeless patients from
   1 Jan 2025 and full presumptive screening with no application from 1 Jan 2026
   ([NC Health News, 2024](https://www.northcarolinahealthnews.org/2024/08/13/nc-medical-debt-relief-plan-11-hospitalmust-dos-for-hospitals/);
   [SHVS State Spotlight, 2024](https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf)).
   All 99 NC acute-care hospitals opted into HASP, so NC FAPs *should* score at the top of
   D3, D5 and D6 — they are the built-in "what good looks like" control group. Atrium, Duke,
   Novant, Cone, ECU and WakeMed cover the state's largest systems plus one independent.
2. **Geographic spread (≥12 states).** NC, OH, MN, CA, NY, AZ, UT, TX, MI, PA, MD, WI — to
   avoid reading one state's regulatory regime as if it were national.
3. **System-size mix.** National giants (Mayo, Cleveland Clinic, Trinity, Banner, Baylor
   Scott & White, UPMC, Intermountain), large regional systems (Sutter, Corewell, Geisinger,
   NYU Langone, Mount Sinai, Cedars-Sinai), and at least one smaller/community facility
   (Atrium Medical Center–Middletown OH; BSW–Centennial). Trinity Health is included as a
   large **Catholic** system, whose Ethical & Religious Directives can change FAP framing.
4. **Locatability first.** Every row resolves to a ProPublica org page (EIN confirmed via
   ProPublica search) and a public hospital website with a financial-assistance section, so
   M2 and M3 can actually find the documents. Entities where the desk search returned an
   ambiguous or multi-entity EIN are flagged rather than dropped.

**What this sample is and is NOT representative of.**

- It is **not a probability sample** and yields **no national prevalence estimate.** It cannot
  support claims like "X% of US nonprofit hospitals fail D5." It supports *comparative* and
  *existence* claims: which named hospitals score worst, and that weak/strong policies exist.
- It is **biased toward large, well-resourced, name-brand systems** because those have the
  most easily locatable EINs and web FAPs. Large academic systems may have *better* web
  posting (helping D1) but are also the systems most criticized for low charity-care ratios
  (D9) — so the bias does not run cleanly in one direction. **Small rural and critical-access
  hospitals, public/government hospitals, and systems with hard-to-find websites are
  under-represented**, and those are plausibly where FAP accessibility is worst; this sample
  will therefore tend to *understate* the inaccessibility problem nationally.
- **NC is deliberately over-represented** (a single state is ~21% of the sample), which makes
  the sample skew toward the strongest-regulation environment — again biasing the overall
  picture *optimistically* relative to the median US hospital.
- Several rows are **system/group-return filers, not single hospitals**, so D9–D10 ratios are
  system-wide and not comparable to a single-facility ratio; M3 states the filing level per row.
- The sample is **frozen as of 2026-06-23.** Systems merge and rename (Cone→Risant, Spectrum→Corewell,
  Atrium→Advocate Health); M2/M3 use the entity named here and note any post-freeze change.

---

## Limitations & counter-evidence

- **FAP text ≠ practice.** The entire D1–D8 block scores *what the policy document says*, not
  what front-desk and billing staff actually do. A hospital can publish a model FAP and still
  fail to screen patients (the core Dollar For finding: ~71% of eligible patients are billed
  despite policies existing — [Dollar For "Bridging the Chasm," 2024](https://dollarfor.org/wp-content/uploads/2024/04/Dollar_For.Bridging_the_Chasm.pdf)).
  A high accessibility score is necessary, not sufficient, for actual access. This rubric
  cannot detect a "good policy, bad practice" hospital; it can only flag "bad policy" ones.
- **Counter-evidence on absolute charity-care thresholds (D9).** The Lown 5.9% "fair share"
  bar combines financial assistance *and* community investment and has been contested by the
  American Hospital Association as methodologically biased for excluding IRS-recognized
  community-benefit categories such as Medicaid shortfall and research
  ([AHA, 2024](https://www.aha.org/news/blog/2024-03-25-there-nothing-fair-about-lown-institutes-fair-share-report)).
  This rubric therefore uses charity-care-at-cost alone for D9 (a narrower, more defensible
  number than Lown's combined metric) and leans on the *peer-relative* D10 so the score does
  not depend on defending one absolute cutoff. A hospital serving a wealthy, well-insured
  catchment may legitimately have low charity care; D10 partly but not fully controls for this.
- **Readability proxy for D2 is imperfect.** Flesch–Kincaid penalizes long medical/legal terms
  that may be unavoidable and rewards short sentences that can still be confusing. It is a
  reproducible proxy for "plain language," not a definitive test of comprehensibility; M2 will
  state the exact tool and version used and quote the scored passage.
- **EIN/entity ambiguity is real and unresolved here.** At least one EIN (561376950) maps to two
  named systems in the desk search, and several systems file group returns; dollar figures in M3
  are only as good as the entity resolution done there. These are flagged, not hidden.
- **Sample selection bias runs optimistic.** As noted in the rationale, over-weighting NC and
  large name-brand systems likely makes the sample *kinder* than a random national draw would be.
  Findings should be read as "even among large, visible, mostly well-resourced systems, here is
  the spread," and explicitly not as a national compliance rate.
- **501(r) regulatory text is stable but enforcement context is shifting.** The CFPB medical-debt
  rule (2024) was subsequently **vacated by a federal court** in 2025
  ([Brownstein, 2025](https://www.bhfs.com/insight/federal-court-vacates-cfpbs-medical-debt-rule-finds-fcra-preempts-state-laws/)),
  so CFPB criteria are used here as *analytic benchmarks for what matters to patients*, not as
  currently-binding rules. The binding law for D1–D8 remains 26 CFR § 1.501(r)-4/-5/-6.

---

### Sources

- 26 CFR § 1.501(r)-4 — Financial assistance policy and emergency medical care policy: <https://www.law.cornell.edu/cfr/text/26/1.501(r)-4>
- IRS — FAP & emergency care policy, Section 501(r)(4): <https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4>
- IRS — Financial Assistance Policies (FAPs) overview: <https://www.irs.gov/charities-non-profits/financial-assistance-policies-faps>
- Dollar For, "Bridging the Chasm" (2024): <https://dollarfor.org/wp-content/uploads/2024/04/Dollar_For.Bridging_the_Chasm.pdf>
- Dollar For — "Bottom Line" report: <https://dollarfor.org/press/bottom-line-report-press-release/>
- Lown Institute — Hospital Fair Share Spending 2024: <https://lownhospitalsindex.org/hospital-fair-share-spending-2024/>
- Lown Institute — Fair Share Spending project: <https://lowninstitute.org/projects/hospital-fair-share-spending/>
- AHA rebuttal to Lown (2024): <https://www.aha.org/news/blog/2024-03-25-there-nothing-fair-about-lown-institutes-fair-share-report>
- CFPB — Fair Debt Collection 2024 annual report (medical-debt complaints): <https://files.consumerfinance.gov/f/documents/cfpb_fdcpa-2024-annual-report_2024-09.pdf>
- Brownstein — federal court vacates CFPB medical-debt rule (2025): <https://www.bhfs.com/insight/federal-court-vacates-cfpbs-medical-debt-rule-finds-fcra-preempts-state-laws/>
- NC Health News — NC medical-debt relief plan, 11 must-dos (2024): <https://www.northcarolinahealthnews.org/2024/08/13/nc-medical-debt-relief-plan-11-hospitalmust-dos-for-hospitals/>
- State Health & Value Strategies — North Carolina spotlight (2024): <https://www.shvs.org/wp-content/uploads/2024/11/SHVS_State-Spotlight_North-Carolina_Final.pdf>
- ProPublica Nonprofit Explorer (EIN/Schedule H source): <https://projects.propublica.org/nonprofits/>
