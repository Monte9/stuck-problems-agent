# M4 — CMS docket comment and US FLS business case

**Problem:** the post-fracture osteoporosis treatment gap
**Milestone:** M4 | **Date:** 2026-06-23 | **Status:** draft for evaluation
**Inputs used (by filename):**
- M1 league table — `artifacts/2026-06-12-m1-treatment-rate-league-table.md`
- M2 benefit-harm dossier — `artifacts/2026-06-12-m2-benefit-harm-dossier.md`
- M3 Medicare cost-of-the-gap model — `artifacts/2026-06-13-m3-medicare-cost-of-the-gap-model.md` (the passing 2026-06-13 revision)

This artifact has two parts. **Part A** is a docket-ready public comment for the next CMS Physician Fee Schedule rulemaking cycle. **Part B** is an NHS-style Fracture Liaison Service (FLS) business-case template a US health system or payer can adapt. Every quantitative claim is traced to M1/M2/M3 (by filename + section) or to a directly cited primary source. Part B carries bracketed placeholders **only** for system-specific fields.

---

## Rulemaking-vehicle verification (done at generation time, 2026-06-23)

The correct, current vehicle and its status as of today:

- **The last completed cycle** is the **CY 2026 Medicare Physician Fee Schedule final rule, CMS-1832-F**, released by CMS on **October 31, 2025** ([CMS fact sheet, CMS-1832-F](https://www.cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-final-rule-cms-1832-f); [Federal Register, published Nov. 5, 2025, 2025-19787](https://www.federalregister.gov/documents/2025/11/05/2025-19787/medicare-and-medicaid-programs-cy-2026-payment-policies-under-the-physician-fee-schedule-and-other)). Its proposed-rule predecessor was **CMS-1832-P** (docket **CMS-2025-0304**), with a 60-day comment window that closed **September 12, 2025** ([CMS-1832-P fact sheet](https://www.cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-pfs-proposed-rule-cms-1832-p); [regulations.gov docket CMS-2025-0304](https://www.regulations.gov/docket/CMS-2025-0304)).
- **The next cycle — the CY 2027 PFS proposed rule — has NOT yet been published as of 2026-06-23.** On the standard CMS calendar the PFS proposed rule appears in **early-to-mid July** each year with a **60-day comment period** (the CY 2026 proposed rule was issued July 14–16, 2025; the CY 2025 proposed rule July 10, 2024) ([CMS-1832-P fact sheet](https://www.cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-pfs-proposed-rule-cms-1832-p)). The CY 2027 proposed rule is therefore expected **~July 2026**, i.e. within weeks of this artifact's date.

**Implication for the commenter.** Because the CY 2027 proposed rule is not yet on the street, this comment is drafted as a **template keyed to the CY 2027 PFS proposed rule**, with the rule's file code and docket number left as the only two bracketed fields in Part A — they will read approximately **`CMS-18[xx]-P`** / **`CMS-2026-0[xxx]`** and must be filled from the Federal Register notice on the day of filing. Everything else (addressee, comment mechanism, arguments, the single regulatory ask) is fixed and correct now.

**Comment mechanism (verified).** CMS PFS rules take comment exclusively through the formal notice-and-comment process: electronically at **[regulations.gov](https://www.regulations.gov/)** ("Submit a comment," referring to the rule's file code), or by mail to the CMS address printed in the rule's ADDRESSES section (for the CY 2026 cycle: Centers for Medicare & Medicaid Services, Dept. of HHS, Attention: [file code], P.O. Box 8016, Baltimore, MD 21244-8016) ([CMS-1832-P fact sheet / Federal Register ADDRESSES section](https://www.cms.gov/newsroom/fact-sheets/calendar-year-cy-2026-medicare-physician-fee-schedule-pfs-proposed-rule-cms-1832-p)). There is no other route; comments emailed to CMS staff or sent outside the docket are not part of the record.

**What CMS has already done — the wedge this comment builds on.** In the **CY 2025** PFS proposed rule, CMS for the first time proposed coding to support post-fracture management — a global post-operative add-on construct (referred to in commentary as **"GPOC1"**) and the broader **Advanced Primary Care Management (APCM)** codes — and issued a Request for Information on how often evidence-based post-fracture care fails to be delivered ([BHOF, "Medicare's Proposed 2025 PFS Rule Takes Critical First Steps," July 2024](https://www.bonehealthandosteoporosis.org/news/medicares-proposed-2025-pfs-rule-takes-critical-first-steps-to-improve-post-fracture-care-for-osteoporosis-patients-in-the-us/)). The coalition's stated objection is that APCM codes "would have minimal impact in closing the care gap" because most post-fracture programs sit in **orthopedics, rheumatology, and endocrinology — not primary care** ([Bone Health Policy Institute, "35 National Health Organizations Call on Medicare…," Sept. 9, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)). The CY 2027 ask below is the next step: a **dedicated, specialty-agnostic post-fracture care-coordination payment**.

---

# PART A — Docket-ready public comment

> **[Bracketed fields in Part A are limited to the two rule identifiers that do not yet exist on 2026-06-23; fill from the Federal Register notice on filing day.]**

**Submitted electronically via [regulations.gov](https://www.regulations.gov/)**
**Re: File Code [CMS-18xx-P], Docket [CMS-2026-0xxx] — Medicare and Medicaid Programs; CY 2027 Payment Policies Under the Physician Fee Schedule**

**To:** The Honorable Administrator, Centers for Medicare & Medicaid Services
Department of Health and Human Services
Attention: [CMS-18xx-P]

**Date:** [date of filing, within the 60-day comment window]

**From:** [Commenting organization / clinician / coalition — system-specific]

## 1. The single regulatory ask (one sentence)

**CMS should finalize, in the CY 2027 Physician Fee Schedule, a dedicated, specialty-agnostic Post-Fracture Care Coordination (PFCC) payment — a stand-alone HCPCS G-code, billable by orthopedics, rheumatology, endocrinology, geriatrics, or primary care — that reimburses the coordinator-based identification, risk assessment, treatment initiation, and follow-up of Medicare beneficiaries who have sustained a fragility fracture, at a rate that covers the documented ~$182-per-patient cost of fracture-liaison-service (FLS) care coordination.**

(The $182 per-patient FLS coordination cost is input I14 in `artifacts/2026-06-13-m3-medicare-cost-of-the-gap-model.md`, §1, sourced to [*Osteoporos Int* 2021, PMC9291535](https://pmc.ncbi.nlm.nih.gov/articles/PMC9291535/); the comparable Solomon base-case figure is $105/patient.)

## 2. Why this matters: the treatment gap is real, large, and getting worse

The United States has a documented and worsening post-fracture treatment gap. The following figures are each traceable to the cited artifact and underlying primary source:

1. **Only 21.1% of Traditional Medicare beneficiaries who suffer a fragility fracture are started on anti-osteoporosis therapy** (2017–2019). Source: M1 row 12 (`artifacts/2026-06-12-m1-treatment-rate-league-table.md`), from [Azad et al., *Osteoporos Int* 2025, PubMed 39570337](https://pubmed.ncbi.nlm.nih.gov/39570337/).
2. **For hip-fracture patients specifically, US initiation fell from 9.8% (2004) to 3.3% (2015)** in a consistent commercial/Medicare-supplemental claims series — a two-thirds decline. Source: M1 row 19, from [Desai et al., *JAMA Netw Open* 2018, PMC6324295](https://pmc.ncbi.nlm.nih.gov/articles/PMC6324295/).
3. **US oral bisphosphonate use fell more than 50% from 2008 to 2012**, the prescribing collapse that followed the atypical-femoral-fracture (AFF) safety scare. Source: M2 §3, from [Jha et al., *JBMR* 2015, PubMed 26018247](https://pubmed.ncbi.nlm.nih.gov/26018247/).
4. **Organized FLS-type systems reach far higher rates: 68% at Kaiser Permanente Southern California's Healthy Bones program, 72–80% at Geisinger's HiROC**, versus 14–32% in matched usual-care patients in the same system. Source: M1 rows 1–2, from [Dell, *Osteoporos Int* 2011](https://link.springer.com/article/10.1007/s00198-011-1712-0) and [Geisinger HiROC, *Osteoporos Int* 2017](https://link.springer.com/article/10.1007/s00198-017-4270-2). The gap between organized and unselected care is the entire policy opportunity.
5. **The coalition's own framing: roughly 80% of fracture patients are never offered osteoporosis screening or treatment**, against ~95% of heart-attack patients who receive secondary-prevention therapy. Source: [Bone Health Policy Institute, Sept. 9, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones); the 20%-of-hip-fracture-patients-treated comparison appears in [BHOF, July 2024](https://www.bonehealthandosteoporosis.org/news/medicares-proposed-2025-pfs-rule-takes-critical-first-steps-to-improve-post-fracture-care-for-osteoporosis-patients-in-the-us/).

## 3. The clinical case is settled, and the safety objection that drove the collapse is quantitatively wrong

The post-2008 prescribing collapse was driven by fear of atypical femoral fractures. The arithmetic inverts that fear:

- **In White women, bisphosphonates prevent roughly 75 hip fractures (and ~270 total clinical fractures) for every 1 atypical femoral fracture they cause at 3 years.** Source: M2 §1, reproducing [Black et al., *NEJM* 2020;383:743-753, PMC9632334](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/): 149 hip fractures prevented ÷ 2 AFFs caused per 10,000 women = 74.5.
- **The number needed to treat to prevent one hip fracture is ~100 in secondary prevention; the number needed to harm for one AFF ranges from ~5,750 (average exposure) to ~760 (8+ years).** Source: M2 §2, from [AAFP/AFP 2008](https://www.aafp.org/pubs/afp/issues/2008/0901/p579.html) and Black 2020. The harm denominator is one to two orders of magnitude larger than the benefit denominator.
- The post-fracture Medicare population is a **higher-baseline-risk secondary-prevention population**, which pushes the benefit-harm ratio further toward treatment than the prevalent-user figures above (M2 §1).

CMS does not need to adjudicate this science: it is the consensus of ASBMR, BHOF, and the 35-organization coalition. CMS needs only to **pay for the coordination labor that turns this evidence into treated patients.**

## 4. Pre-empting the cost objection: this is cost-effective, and the "does it pay for itself" question is precisely the payment-design question before CMS

A predictable objection is budget impact. The honest, sourced answer:

- **Closing the gap to a realistic 42% prevents ~3,600 Medicare refractures and ~900 associated deaths per year** in the FFS population; even the conservative floor (target 35.4%, the UK national FLS audit rate) prevents ~1,600 refractures and ~400 deaths/yr. Source: M3 §3–§4 (`artifacts/2026-06-13-m3-medicare-cost-of-the-gap-model.md`).
- **The gross annual medical offset is ~$73M (blended) to ~$89M (hip-weighted upper bound).** Source: M3 §3.
- **Whether the program nets positive depends entirely on how the coordination labor is paid — which is exactly what this rulemaking decides.** Under whole-population FLS staffing charged to every fractured beneficiary, M3's base case is a **net cost of ~$136M/yr**; under a **targeted-outreach** cost basis (charging coordination only on the incremental patients actually moved to treatment) the same scenario flips to **net +$185M/yr in savings**. Source: M3 §3–§4 and the M3 forward-pointer. **The requested PFCC G-code is the mechanism that makes targeted, efficient coordination billable — i.e., it is the design choice that determines the sign of the budget impact.**
- **The peer-reviewed US cost-effectiveness literature finds FLS cost-saving over a lifetime horizon.** A US health-system Markov model found an FLS produces **153 fewer fractures, 37.4 more QALYs, and saves $66,879 per 10,000 post-hip-fracture patients** versus usual care, with an ICER of **$22,993/QALY even when FLS cost is doubled** ([Solomon et al., *Osteoporos Int* 2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766/); also M3 §5 cross-check 2). A systematic review of FLS economic evaluations concluded FLS is **cost-effective versus usual care regardless of program intensity or country**, with US cost/QALY of $14,513–$112,877 ([Wu et al., *Osteoporos Int* 2018, PubMed 29460102 / DOI 10.1007/s00198-018-4411-2](https://pubmed.ncbi.nlm.nih.gov/29460102/)).
- **International corroboration:** the Royal Osteoporosis Society estimates universal FLS coverage in England prevents 74,000 fractures (incl. 31,000 hip) over 5 years and returns **£3.28 per £1 invested** ([ROS/APPG inquiry, 2021–2023](https://theros.org.uk/latest-news/parliamentary-group-publishes-the-findings-of-its-inquiry-into-the-postcode-lottery-faced-by-the-3-5m-people-with-osteoporosis/); also M3 §5 cross-check 3).

**The defensible claim CMS should hear:** a modest, cost-effective coordination payment unlocks a large death-and-disability reduction. We do **not** claim first-year budget neutrality under whole-population costing; we claim that the requested code is the lever that makes the intervention both clinically effective and fiscally efficient.

## 5. Why the existing CY 2025/2026 codes are insufficient

CMS's first-step APCM and global post-operative add-on codes are welcome but inadequate, for the reason the 35-organization coalition stated: **most post-fracture programs operate in orthopedics, rheumatology, and endocrinology — not primary care — so primary-care-anchored APCM codes "would have minimal impact in closing the care gap"** ([Bone Health Policy Institute, Sept. 9, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)). A dedicated, **specialty-agnostic** PFCC G-code reaches the clinicians who actually run FLS programs.

## 6. The 35-organization coalition

This comment aligns with the **letter of September 9, 2024, in which 35 national patient and health-professional organizations, led by the Bone Health & Osteoporosis Foundation (BHOF) and the American Society for Bone and Mineral Research (ASBMR), called on CMS to include in its Medicare PFS regulation a payment mechanism that adequately covers the cost of proven post-fracture care coordination (fracture liaison services)** ([Bone Health Policy Institute, Sept. 9, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)). That coalition cited **10 million Americans with osteoporosis, over 2 million fragility fractures per year, more hospitalizations than heart attacks/strokes/breast cancer combined, and projected national costs exceeding $95 billion by 2040 absent reform** (same source). The CY 2027 PFCC G-code is the concrete realization of that ask.

## 7. Numbered summary of the asks

1. **Finalize a stand-alone, specialty-agnostic Post-Fracture Care Coordination (PFCC) G-code** in the CY 2027 PFS, billable across orthopedics, rheumatology, endocrinology, geriatrics, and primary care.
2. **Set the work and practice-expense RVUs so reimbursement covers the documented ~$105–$182 per-patient FLS coordination cost** (M3 I14).
3. **Do not require the billing clinician to be in primary care**, the explicit failure mode of the APCM approach (§5).
4. **Adopt a quality measure tied to the code** — e.g., the share of fragility-fracture beneficiaries assessed and, where indicated, started on therapy within 12 months — benchmarked against the 21.1% national baseline (M1 row 12) and the 35.4% UK-FLS / 68% Kaiser targets (M1 rows 6, 2).

Respectfully submitted,
[Name, credentials, organization — system-specific]

---

# PART B — NHS-style FLS business-case template (for a US health system or payer)

> Adapt by replacing every **[bracketed placeholder]** with your own system-specific value. All **non-placeholder** numbers are sourced from M1–M3 or a cited primary source. Where a national benchmark is given, use it until your own data replace it.

## B.1 Problem statement

- **[Health system / payer name]** treats approximately **[N fragility fractures per year]** in beneficiaries aged 50+. Of these, **[X%]** are currently started on anti-osteoporosis therapy within 12 months — versus a US Traditional Medicare benchmark of **21.1%** (M1 row 12; [Azad et al. 2025](https://pubmed.ncbi.nlm.nih.gov/39570337/)) and a hip-fracture-specific low of **3.3%** (M1 row 19; [Desai et al. 2018](https://pmc.ncbi.nlm.nih.gov/articles/PMC6324295/)).
- **About 14% of fractured Medicare beneficiaries suffer a subsequent fracture within 12 months** (M3 input I3; [Milliman 2021](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf)). One-year mortality is **~20% after any fragility fracture and ~30% after a hip fracture** (M3 inputs I11–I12; Milliman 2021).
- **Roughly 80% of fracture patients are never offered screening or treatment**, versus ~95% of heart-attack patients receiving secondary prevention ([Bone Health Policy Institute, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)).

## B.2 Intervention

A coordinator-based **Fracture Liaison Service (FLS)**: systematic identification of every fragility-fracture patient, fracture-risk assessment (including DXA), initiation of guideline anti-osteoporosis therapy, and structured follow-up — the model that lifts treatment rates to **68% (Kaiser Healthy Bones)** and **72–80% (Geisinger HiROC)** versus 14–32% usual care in the same systems (M1 rows 1–2). The clinical justification — that bisphosphonates prevent ~75 hip fractures per AFF caused, NNT-hip ≈100 — is documented in M2 §1–§2.

- **Recommended target treatment rate:** set a realistic **42%** (the Solomon FLS base case; M3 input I6) as the program goal, with **35.4%** (UK national FLS audit; M1 row 6) as the conservative floor and **68%** (Kaiser) as the stretch goal.

## B.3 Costs

| Item | Value | Source |
|---|---|---|
| FLS care-coordination cost per patient | **$105–$182** | M3 input I14 ([*Osteoporos Int* 2021, PMC9291535](https://pmc.ncbi.nlm.nih.gov/articles/PMC9291535/); Solomon base $105, [PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766/)) |
| Annual coordination cost (whole-population screening) | **[N patients] × $182 = [$ ]** | formula M3 eq. (6) |
| Annual coordination cost (targeted outreach only) | **(target rate − current rate) × [N] × $182 = [$ ]** | formula M3 eq. (6t) |
| Coordinator staffing (FTE) | **[# FLS coordinator FTEs]** (see B.5) | system-specific |
| DXA / assessment capacity | **[system-specific]** | system-specific |
| **Excluded:** drug acquisition, dental clearance, infusion administration | not in coordination cost | M3 §6 limitation 5 |

## B.4 Savings

- **Incremental medical offset per avoided subsequent fracture:** **$20,140** (blended, 180-day, Parts A&B) and **>$37,000** for the index-hip-fracture subset (M3 inputs I9, I16; [Milliman 2021](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf)).
- **Projected avoidable events (scale to your volume using M3 eq. 1–5):** at the Medicare-FFS scale (≈1.15M fractured beneficiaries with Parts A&B), closing the gap to 42% prevents **~3,600 refractures and ~900 deaths/yr**, gross offset **~$73M (blended) to ~$89M (hip-weighted)** (M3 §3). For **[your system]**, multiply by **[your N ÷ 1,148,000]**.
- **Lifetime-horizon cost-effectiveness:** an FLS saves **$66,879 per 10,000 post-hip-fracture patients** with an ICER of **$22,993/QALY** even at doubled FLS cost ([Solomon et al. 2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766/)); FLS is cost-effective across settings, US cost/QALY $14,513–$112,877 ([Wu et al. 2018, PubMed 29460102](https://pubmed.ncbi.nlm.nih.gov/29460102/)).
- **ROI benchmark:** universal FLS in England returns **£3.28 per £1 invested** ([ROS/APPG 2021–2023](https://theros.org.uk/latest-news/parliamentary-group-publishes-the-findings-of-its-inquiry-into-the-postcode-lottery-faced-by-the-3-5m-people-with-osteoporosis/)); the targeted-outreach Medicare scenario is comparable (~$4.3 saved per $1 of outreach; M3 §5 cross-check 3).
- **Honest framing:** under whole-population costing the first-year offset does **not** cover the program (net ~−$136M at Medicare scale; M3 §3). Build the case on **cost-effectiveness and targeted-outreach net savings (~+$185M/yr)**, not first-year budget neutrality (M3 §6 limitation 6).

## B.5 Staffing model

- **Core role: FLS coordinator** (nurse practitioner, PA, or RN) — performs identification, assessment, treatment initiation, and follow-up. Per-patient coordination cost of $105–$182 (M3 I14) corresponds to roughly an NP visit + DXA.
- **Suggested ratio:** **[# coordinator FTEs]** sized to **[N annual fragility fractures]**; published FLS programs run on coordinator-led, physician-supervised models ([Kaiser Healthy Bones 10-step protocol; Dell 2011](https://link.springer.com/article/10.1007/s00198-011-1712-0)).
- **Physician champion:** **[named orthopedist / rheumatologist / endocrinologist]** — note the program need not be primary-care-based; specialty placement is the norm ([Bone Health Policy Institute 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)).
- **Supporting:** DXA technologist capacity, IT identification feed from ED/ortho/admission records (the Geisinger/Kaiser "identify–test–treat" backbone; M1 rows 1–2).
- **[Reporting line / governance — system-specific]**

## B.6 KPIs

| KPI | Definition | Benchmark / target | Source |
|---|---|---|---|
| Post-fracture treatment rate | % of fragility-fracture patients started on anti-osteoporosis therapy within 12 mo | Baseline **21.1%** → target **42%** → stretch **68%** | M1 rows 12, 2; M3 I6 |
| FLS capture rate | % of eligible fracture patients identified by the FLS | **[target %]** | system-specific |
| Refractures avoided / yr | from M3 eq. (1)–(2) applied to your volume | scales to ~3,600/yr at Medicare-FFS scale | M3 §3 |
| Deaths avoided / yr (associated) | from M3 eq. (4); read as "associated," not certain lives saved | ~900/yr at Medicare scale | M3 §3, §6 limitation 1 |
| Medication persistence at 1 yr | % still on therapy at 12 mo | **58%** modeled; aim higher | M3 input I8 ([Solomon 2014](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766/)) |
| Net financial result | gross offset − program cost, by cost basis | targeted-outreach can net **+$185M/yr** at Medicare scale | M3 §4 |
| DXA completion rate | % of identified patients receiving BMD assessment | **[target %]** | system-specific |

---

## Limitations & counter-evidence

1. **The rulemaking vehicle is not yet published.** The CY 2027 PFS proposed rule was not on the Federal Register as of 2026-06-23 (verified above). Part A's two bracketed identifiers (file code, docket number) and the exact comment deadline cannot be finalized until CMS issues the rule, expected ~July 2026. If CMS's calendar slips, the commenter must re-confirm the vehicle. The mechanism (regulations.gov, file-code reference) and the substantive arguments do not change.
2. **The headline target rates (Kaiser 68%, Geisinger 72–80%) are the weakest-sourced numbers carried forward.** Kaiser's 68% is a 2012 conference figure reported by a trade outlet, now 14 years old and not independently audited (M1 Limitations). The business case should treat **35.4% (UK national FLS audit)** as the defensible target a real rollout achieves, with 68% as aspirational — consistent with M1's own caution.
3. **The net-dollar argument is sign-sensitive to a modeling convention, not a clinical fact.** M3's base case is a net *cost* (~−$136M/yr) under whole-population costing and net *savings* (~+$185M/yr) only under targeted outreach (M3 §3–§4, §6 limitation 6). Part A is careful to claim cost-*effectiveness*, not first-year budget neutrality; an evaluator or CMS reader who wants "it pays for itself in year one" will not find it supported, and should not.
4. **Avoidable-deaths figures are upper-bound-leaning.** Preventing a refracture does not avert the full post-fracture mortality, because much of that mortality reflects underlying frailty and competing causes (M3 §6 limitation 1). "~900 deaths/yr" is "deaths associated with prevented refractures," not certain lives saved.
5. **All dollar inputs are 2016-USD (Milliman) or 2014/2021 CEA vintages; none is 2026.** Inflation since 2016 means the offsets are lower bounds (M3 §6 limitation 8). The comment does not adjust for inflation, which is conservative for the savings case but means absolute dollars understate current magnitude.
6. **The evidence base is overwhelmingly from women.** Black 2020 (the benefit-harm anchor) and the AAFP NNTs are women-only; men are treated at roughly half the rate and are far less studied (M2 §5 limitation 2). The business case applies population-level figures to mixed-sex populations; the male-specific benefit-harm ratio is plausibly similar but not directly established `[speculative]`.
7. **Counter-evidence on the "collapse" narrative:** several systems are *improving* (UK FLS-DB 30.0%→35.4%; ANZHFR 20%→37%; M1 Limitations), and the US "3.3%" figure is a narrow 180-day oral-claims commercial figure, not the whole story — the same country shows 21–29% in broader Medicare definitions (M1 Limitations). Honest advocacy quotes the range with definitions, which Part A does (21.1% headline, 3.3% as the hip-specific low).
8. **The requested code does not yet exist and CMS may decline or restructure it.** APCM/global-post-op codes already proposed (CY 2025) are CMS's actual current posture; the coalition's view that they are insufficient is an advocacy position, not a CMS finding. CMS could reasonably argue existing codes suffice — the comment's job is to rebut that, not to assume it away.

---

## Self-verification against M4 done-criteria

- **Correct, current rulemaking vehicle, web-verified at generation time:** CY 2027 PFS proposed rule (not yet published as of 2026-06-23; CY 2026 final rule CMS-1832-F released Oct 31, 2025 was the last completed cycle). Comment mechanism = regulations.gov with file-code reference. ✔ (verification section + Part A)
- **One primary regulatory ask in a single sentence:** Part A §1. ✔
- **Cites the 35-organization coalition letter:** Part A §6 and §1, §5 ([Bone Health Policy Institute, Sept. 9, 2024](https://www.bonehealthpolicyinstitute.org/newsroom/35-national-health-organizations-call-on-medicare-to-use-2025-payment-rule-to-improve-patient-care-and-prevent-osteoporosis-related-broken-bones)). ✔
- **≥5 distinct numeric claims traceable to M1/M2/M3 (by filename + section) or primary source:** Part A §2 lists 5 (21.1% M1 r12; 9.8%→3.3% M1 r19; >50% decline M2 §3; 68%/72–80% M1 r1–2; 80%/95% coalition), plus §3 (75:1, NNT 100, NNH 5,750–760) and §4 (3,600 refx/900 deaths, $73–89M, ±$136M/+$185M). ✔
- **Pre-empts cost objection with M3 net-dollar result + ≥1 peer-reviewed FLS cost-effectiveness citation:** Part A §4 uses M3's ±$136M / +$185M result plus Solomon 2014 (PMC4176766) AND Wu 2018 (PubMed 29460102), both peer-reviewed. ✔
- **Part B includes all six template sections with placeholders only for system-specific fields:** B.1 problem, B.2 intervention, B.3 costs, B.4 savings, B.5 staffing, B.6 KPIs — present; brackets confined to system-specific fields. ✔
- **Zero uncited quantitative claims (Part B placeholders excepted):** every number carries an M1/M2/M3 reference or a primary citation; one `[speculative]` flag retained (male ratio). ✔
