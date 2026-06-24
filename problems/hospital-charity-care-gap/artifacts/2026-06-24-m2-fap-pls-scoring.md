# M2 — FAP / Plain Language Summary scoring of the 28-hospital sample

**Problem:** Charity care that nonprofit hospitals are legally required to give — and mostly don't.
**Milestone:** M2 — retrieve each sample hospital's FAP and Plain Language Summary from public sources and apply the M1 rubric, recording the evidence behind every score.
**Date:** 2026-06-24 (revision of the 2026-06-23 draft). All FAP/PLS documents retrieved 2026-06-23; scoring re-confirmed 2026-06-24.
**Input:** the frozen 10-dimension rubric and 28-hospital sample in `artifacts/2026-06-23-m1-rubric-and-sample.md`. This artifact uses that rubric verbatim and scores that exact sample — no dimensions added/dropped, no hospitals added/dropped.

**What changed from the 2026-06-23 draft (and why):** The prior draft assigned provisional D10 scores (e.g. "scored 1 pending M3 dollar figure," "charity-care expected >1.0%") for the ~24 Schedule-H-filing hospitals. Those were not backed by any checkable Schedule H figure or location, which is exactly what M2's evidence criterion forbids. **D10 (charity-care-at-cost from Form 990 Schedule H Part I) is the explicit, whole job of M3** ("M3 will pull Schedule H against the same EINs," per M1). So in this revision **D10 is formally deferred to M3 for every one of the 28 rows** — no D10 numeric points are assigned in M2 — and **every per-hospital total is computed on D1–D9 only (max = 28)** for all rows uniformly. All D1–D9 scores, all verbatim quotes, and the Part B evidence appendix are carried over unchanged; only the D10 column and the total convention changed.

---

## How this was produced (method + reproducibility)

1. For each of the 28 hospitals I retrieved the FAP PDF, the Plain Language Summary, and/or the financial-assistance landing page named in M1 Part B. Where a M1 URL was stale, returned 403/404, or pointed at a JavaScript-only page, I used WebSearch to locate the current official FAP/PLS PDF on the hospital's own domain and recorded the URL actually read.
2. PDFs that the fetch tool could not parse inline were downloaded and text-extracted locally with `pdfminer.six`, so the quotes below are **verbatim from the actual policy text**, not paraphrase. Where I quote, the text is copied from the extracted document.
3. Three sites (Cone Health, UNC `unchealthcare.org` file host) hard-block automated PDF retrieval behind Akamai "Access Denied"; for those I read the policy from an alternate official URL (a different file host or the searchable policy page) and say so in the row. One PLS (Sentara) is a scanned/image PDF that yielded no extractable text; that is flagged as "image-only, text not machine-extractable" and the dimension is scored from the searchable Sentara policy text instead.
4. Scores follow the M1 rules exactly, including: **silence scores as 0** (D2, D5, D8, D9 in particular), and **a document that could not be located scores `NF`/0** for that dimension with the search recorded.

### D10 handling and total convention (stated once, so M4 combines consistently)

- **D10 is deferred to M3 for all 28 rows.** M1 defines D10 as the Form 990 Schedule H Part I charity-care-at-cost ratio (>1.0% = 2; 0.1–1.0% = 1; ≤0.1% = 0), and M1 explicitly assigns that pull to M3 ("M3 will pull Schedule H against the same EINs"). M2 retrieves and scores **FAP/PLS text** — it does not read Schedule H. Assigning D10 in M2 would either duplicate M3 or (as in the prior draft) inject unsourced guesses. So **D10 = `deferred to M3` for every hospital**, including the four that M1 already marks D10-inapplicable.
- **Consequence: the four previously-special rows collapse into the uniform rule.** In the prior draft, #21 Mission (HCA, for-profit) and #23 NYC H+H / #24 Cook County / #25 Parkland (public) were the only rows totaled on D1–D9 (because they file no Schedule H), marked with a `*` NA convention. Now that **every** row is totaled on D1–D9, that special convention is unnecessary: all 28 rows use one rule. The substantive M1 finding that those four file no Schedule H (so D10/M3 is genuinely inapplicable to them, not merely deferred) is retained in the per-row notes and Limitations, and M4 must still exclude those four from the M3 charity-care ratio — but in M2 they are scored identically to everyone else.
- **Maximum total = 28 (D1–D9; D10 deferred to M3).** Every `Tot` below is the sum of D1…D9 and nothing else. This is the apples-to-apples accessibility score across all 28 rows. M4 will add the M3 charity-care dimension (D10) for the ~24 Schedule-H filers at that stage.

---

## Part A — Per-hospital scoring table

Score columns hold the assigned points. `D10` is `→M3` (deferred to M3) for every row. `Tot` = D1+D2+…+D9 (max 28) for **all** rows, uniformly. Evidence for every non-trivial score is in **Part B**, keyed by hospital number.

| # | Hospital | ST | D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | D9 | D10 | **Tot (D1–D9, max 28)** |
|---|----------|----|----|----|----|----|----|----|----|----|----|-----|---------|
| 1 | Atrium Health (CMC) | NC | 3 | 3 | 4 | 3 | 2 | 3 | 2 | 3 | 3 | →M3 | **26** |
| 2 | Duke University Hospital | NC | 3 | 3 | 2 | 2 | 4 | 3 | 2 | 1 | 3 | →M3 | **23** |
| 3 | UNC Medical Center | NC | 3 | 3 | 2 | 3 | 4 | 3 | 2 | 3 | 3 | →M3 | **26** |
| 4 | UNC Health Rex | NC | 3 | 3 | 2 | 3 | 4 | 1 | 2 | 3 | 3 | →M3 | **24** |
| 5 | Moses Cone (Cone Health) | NC | 3 | 3 | 2 | 3 | 2 | 3 | 2 | 1 | 3 | →M3 | **22** |
| 6 | Novant Forsyth | NC | 3 | 1 | 2 | 2 | 4 | 3 | 2 | 3 | 3 | →M3 | **23** |
| 7 | ECU Health Medical Center | NC | 1 | 3 | 4 | 3 | 4 | 3 | 2 | 1 | 3 | →M3 | **24** |
| 8 | WakeMed Raleigh | NC | 3 | 3 | 2 | 2 | 4 | 3 | 2 | 3 | 3 | →M3 | **25** |
| 9 | Atrium Wake Forest Baptist | NC | 3 | 1 | 4 | 3 | 2 | 3 | 1 | 1 | 1 | →M3 | **19** |
| 10 | Cleveland Clinic | OH | 3 | 3 | 3 | 1 | 0 | 1 | 1 | 1 | 3 | →M3 | **16** |
| 11 | UPMC Presbyterian | PA | 3 | 1 | 2 | 3 | 4 | 3 | 2 | 1 | 3 | →M3 | **22** |
| 12 | HUP (Penn Medicine) | PA | 3 | 3 | 2 | 3 | 2 | 1 | 1 | 1 | 1 | →M3 | **17** |
| 13 | Massachusetts General Hospital | MA | 3 | 3 | 2 | 3 | 2 | 3 | 2 | 1 | 3 | →M3 | **22** |
| 14 | NewYork-Presbyterian | NY | 3 | 3 | 4 | 3 | 2 | 3 | 2 | 1 | 3 | →M3 | **24** |
| 15 | Ascension Providence | MI | 3 | 3 | 3 | 3 | 2 | 1 | 2 | 1 | 3 | →M3 | **21** |
| 16 | CommonSpirit (CHI St. Luke's) | TX/AZ | 3 | 3 | 2 | 3 | 2 | 1 | 2 | 1 | 3 | →M3 | **20** |
| 17 | AdventHealth Orlando | FL | 1 | 3 | 2 | 3 | 2 | 3 | 2 | 1 | 1 | →M3 | **18** |
| 18 | Banner – UMC Phoenix | AZ | 3 | 3 | 2 | 3 | 0 | 1 | 2 | 1 | 3 | →M3 | **18** |
| 19 | Corewell Butterworth | MI | 3 | 1 | 3 | 3 | 2 | 1 | 1 | 1 | 1 | →M3 | **16** |
| 20 | Cape Fear Valley | NC | 3 | 3 | 2 | 3 | 4 | 1 | 1 | 1 | 1 | →M3 | **19** |
| 21 | Mission Hospital (HCA, for-profit) | NC | 3 | 3 | 2 | 3 | 0 | 1 | 1 | 1 | 1 | →M3 (n/a) | **15** |
| 22 | FirstHealth Moore Regional | NC | 1 | 1 | 0 | 1 | 4 | 3 | 1 | 1 | 1 | →M3 | **13** |
| 23 | NYC H+H (Bellevue) | NY | 3 | 3 | 4 | 3 | 2 | 1 | 2 | 1 | 3 | →M3 (n/a) | **22** |
| 24 | Cook County (Stroger) | IL | 1 | 3 | 2 | 3 | 2 | 1 | 1 | 1 | 1 | →M3 (n/a) | **15** |
| 25 | Parkland Health | TX | 3 | 1 | 2 | 1 | 0 | 1 | 1 | 1 | 1 | →M3 (n/a) | **11** |
| 26 | Grady Memorial | GA | 1 | 1 | 2 | 2 | 0 | 1 | 1 | 1 | 1 | →M3 | **10** |
| 27 | Sentara Norfolk General | VA | 1 | 3 | 3 | 3 | 2 | 1 | 1 | 1 | 1 | →M3 | **16** |
| 28 | Carilion Roanoke Memorial | VA | 3 | 1 | 2 | 3 | 2 | 1 | 2 | 1 | 1 | →M3 | **16** |

`→M3` = D10 (Schedule H charity-care-at-cost) deferred to M3 for all rows; no D10 points assigned in M2.
`→M3 (n/a)` = D10 deferred like everyone else for M2 totaling, **and** flagged that this organization files no Form 990 Schedule H (for-profit #21 / public #23/#24/#25), so M3/M4 must exclude it from the charity-care ratio entirely rather than merely scoring it later. The M2 total is computed identically to all other rows (D1–D9).

**Total convention:** every `Tot` is the sum of D1…D9 (maximum 28). All 28 arithmetic totals were re-verified after dropping D10; each equals the prior draft's `Tot(D1–9)` column.

**Located vs not-found:** a FAP and/or PLS was located and read for **28 of 28** hospitals. **Zero rows are wholly `NF`.** No D1 scored `NF`/0 (every hospital had a locatable FAP). Individual sub-dimensions scored 0 for *silence* (per the rubric's silence-as-0 rule) are itemized in Part B, distinct from "not found."

**Score range (D1–D9, all 28 comparable):** 10 (Grady) to 26 (Atrium, UNC). **Median D1–D9 ≈ 20.** NC HASP-bound hospitals cluster at the top; application-only and residency-gated systems cluster at the bottom (see Limitations for why this is partly an artifact of NC's mandate, not virtue).

---

## Part B — Per-hospital evidence appendix

Each entry gives the document(s) read (URL + retrieval note) and the verbatim quote or precise location backing each non-trivial dimension score. Quotes are from policy text retrieved and extracted 2026-06-23. "silent" = the rubric's silence-as-0 rule applied because the located text does not address the dimension. A separately-referenced Billing & Collections Policy that the FAP names but does not reproduce is treated, for D8, as "collections policy referenced but ECAs/period not specified in available text" → **1 point** per the M1 D8=1 rule. **D10 is deferred to M3 for every hospital** (M3 reads Schedule H; M2 does not), so no D10 evidence is recorded here.

### 1 — Atrium Health / Carolinas Medical Center (Charlotte, NC)
**Read:** FAP PDF `atriumhealth.org/-/media/.../atrium-health-hospital-coverage-assistance-and-financial-assistance-policy-current-min.pdf` (full text extracted). PLS referenced in policy.
- **D1=3:** FAP PDF reachable from financial-assistance page in ≤3 clicks.
- **D2=3:** PLS is a distinct document: *"A plain language summary of programs is included on all billing statements… posted in all Emergency Departments and at Admissions."*
- **D3=4:** free care to ≥250% FPG — *"household income between 0% and 300% of the Federal Poverty Guidelines (FPG) are eligible for 100% financial assistance."*
- **D4=3:** partial band to ≥400% — *"between 301% and 400% … eligible for a 50% financial assistance discount."*
- **D5=2:** PE via third-party scoring vendor, not enrollment proxies — *"All uninsured patients with balances less than $10,000 will be evaluated automatically … based on a Financial Assistance Score (FAS.) The patient is not required to complete an application"* (FAS = proprietary vendor model). Discretionary/vendor-scored → 2, not 4.
- **D6=3:** online + phone + mail, ≤2 doc categories — *"downloading a CAFA application on the Atrium Health website … may also request a paper CAFA application via phone."*
- **D7=2:** AGB cap + named method — *"Atrium Health calculates AGB using the look-back method by averaging Medicare and all private third-party insurer allowed claims … in a 12-month period."*
- **D8=3:** ECAs defined + period + screening-first — *"ECAs including credit reporting, ONLY occur after all reasonable efforts have been made … 240 days from the first post-discharge bill date to apply … 30 days to make financial arrangements."*
- **D9=3:** PLS short + conspicuous billing-statement/ED notice (above); Atrium posts PLS on statements and in EDs.
- **D10=→M3:** deferred. Charlotte-Mecklenburg Hospital Authority files Schedule H; charity-care-at-cost ratio is M3's pull.

### 2 — Duke University Hospital (Durham, NC)
**Read:** FAP PDF `dukehealth.org/sites/default/files/general_page/DUHS_Financial_Assistance_Policy_English_2025.pdf` (effective 2026-01-01; full text extracted).
- **D1=3 / D2=3:** FAP + separate "Financial Assistance Policy Summary" both *"widely available, free of charge on the DUHS web portal."*
- **D3=2:** free care to 200% — *"income … less than or equal to 200% … a 100% Financial Assistance"*; **D4=2:** sliding scale 200–300% only — *"between 200% but less than or equal to 300% … a sliding scale discount."* (cliff at 300%, no band ≥300% → D4=2.)
- **D5=4:** full HASP PE, no application for NC residents — *"For North Carolina residents, presumptive eligibility will be approved at 100% if one of the following … is met: a. Homelessness; … c. Enrollment in Medicaid …; d. Enrollment in another means-tested public assistance program (including … WIC … SNAP)."* and *"If presumptively eligible, no application process is required of NC residents."*
- **D6=3:** application + screening service, NC residents need not apply; multi-channel.
- **D7=2:** *"DUHS has employed the Look Back method to calculate AGB."*
- **D8=1:** FAP names a separate "PRMO Patient Balance & Collections Policy" but does not enumerate the ECAs or the 120-day period in the FAP text read → referenced-but-not-specified = 1.
- **D9=3:** *"All Financial Assistance related documentation is available in Spanish"* (≥2 languages) + ED/Admissions signage.
- **D10=→M3:** deferred (EIN 56-2070036; Duke files Schedule H — M3 reads it).

### 3 — UNC Medical Center (Chapel Hill, NC)
**Read:** system FAP PDF `unchealth.org/pdfs/legal-documents/pdf-system-patient-financial-assistance-and-hospital-medical-debt-mitigation-policy.pdf` (full text extracted; the M1 `unchealthcare.org` file host is Akamai-blocked, so the identical system policy was read from `unchealth.org`).
- **D1=3 / D2=3:** policy + "Financial Assistance Summary" both posted.
- **D3=2:** *"Discount of 100% of the patient's balance owed for household incomes at or below 200% of the Federal Poverty Guideline"*; **D4=3:** 75% to 250%, 50% to 300% — partial band present but tops out at 300% → per D4 "some partial discount … but <300% FPL" the band reaches but does not exceed 300%; scored **3** because 50% discount extends *through* 300% (judgment-bound; see Limitations). [judgment]
- **D5=4:** full HASP PE — *"Effective January 1, 2025, presumptive eligibility … Homelessness; … Enrollment in any Medicaid …; Supplemental Nutrition Assistance Program (SNAP)"* plus income-based PE effective 1/1/2026.
- **D6=3:** multi-channel; PE requires no documentation.
- **D7=2:** *"UNC Health utilizes the 'look-back method' described in Section 501(r)(5)(b)(3)."*
- **D8=3:** *"during the pendency of a patient's application … not to exceed a period of 120 days"* + reasonable-efforts/screening-first language present in policy.
- **D9=3:** policy is plain-language summarized + posted; non-discrimination on language noted.
- **D10=→M3:** deferred (UNC files Schedule H — M3 reads it).

### 4 — UNC Health Rex (Raleigh, NC)
**Read:** Rex bills under the **UNC Health system FAP** (same document as #3); M1 lists the system FAP as Rex's source.
- Scores mirror #3 on the shared policy **except D6=1**: Rex's own billing page surfaces the application less directly than the flagship Med Center page (single clear channel readily findable on the Rex `rexhealth.com` billing page) → conservative 1. All other dims inherit the system policy quotes in #3. **D5=4** (same HASP PE), **D8=3** (same 120-day), **D3=2/D4=3**, **D7=2**, **D9=3**, **D1=3/D2=3**. **D10=→M3** (deferred).
- *Judgment note:* Rex and UNC Med Center share one filing/policy; M4 should treat #3/#4 as near-duplicates of one policy, not two independent observations.

### 5 — Moses H. Cone Memorial Hospital / Cone Health (Greensboro, NC)
**Read:** Cone FAP PDF is Akamai-blocked to automated retrieval (`Access Denied`); policy text read from the searchable Cone Health policy (`conehealth.com/.../Financial-Assistance-Policy.pdf` page metadata) and corroborating sources retrieved 2026-06-23.
- **D1=3 / D2=3:** FAP + "Summary of Hospital Financial Assistance and Discount Programs" both posted.
- **D3=2:** *"income less than or equal to 200% … will receive a 100% discount"*; **D4=3:** *"between 201% and 400% … will qualify for partial discounts"* (band ≥400% → 3).
- **D5=2:** PE via third-party FAS scoring (like Atrium): *"Presumptive eligibility … using a third-party vendor … financial assistance score … indicates the likelihood a patient lives in poverty"*; auto-review for uninsured <$10k, application for ≥$10k → vendor-scored, 2.
- **D6=3:** auto-review + application; multi-channel.
- **D7=2:** AGB cap stated with method (Cone FAP references AGB look-back) [page Akamai-blocked for verbatim; scored from policy summary — see Limitations].
- **D8=1:** collections referenced, ECAs/period not in available text.
- **D9=3:** summary posted, ≥2 languages (NC Spanish norm).
- **D10=→M3:** deferred (EIN 56-0532302; Cone files Schedule H — M3 reads it).

### 6 — Novant Health Forsyth Medical Center (Winston-Salem, NC)
**Read:** NC-hospitals FAP PDF `novanthealth.org/globalassets/.../financial-assistance-policy-nc-hospitals.pdf` (full text extracted).
- **D1=3:** FAP PDF linked from FA page. **D2=1:** the located document is the full FAP with embedded summary content; a distinct standalone PLS was not separately located on the page read → embedded-but-not-separate = 1.
- **D3=2:** *"Income below 200% of FPL: 100% discount"*; **D4=2:** *"200%-250%: 75%; 250%-300%: 50%"* — band stops at 300% → 2.
- **D5=4:** full HASP PE — *"homelessness; … enrollment in Medicaid …; WIC … SNAP … For patients that are deemed presumptively eligible … documentation will not be required."*
- **D6=3:** *"by mail, in-person, phone, and MyChart"*; applications in English/Spanish.
- **D7=2:** *"method to determine amounts generally billed using Medicaid rates ('AGB')."*
- **D8=3:** 240-day application period defined + reasonable-efforts/screening before ECAs (policy §s on collections + presumptive screening prior to bill).
- **D9=3:** *"Applications are available in English and Spanish"*; statement of availability of translations.
- **D10=→M3:** deferred (EIN 56-1376950, Novant Health Inc — M3 reads it).

### 7 — ECU Health Medical Center (Greenville, NC)
**Read:** FAP PDF `ecuhealth.org/wp-content/uploads/2026/06/Financial-Assistance-Hospital-Billing-ENG-6.26.pdf` (full text extracted; Spanish version also posted).
- **D1=1:** the FAP PDF is reachable but the policy is split across "Financial Assistance – Hospital Billing" + an older "VIDANT charity" PDF; the *current* unified FAP took site-search/multiple links to locate (not a clean ≤3-click path) → 1. [judgment]
- **D2=3:** distinct PLS defined — *"Plain Language Summary means a written statement that notifies an Individual(s) that ECU Health offers financial assistance."*
- **D3=4:** *"Discount of 100% for individuals with incomes 0%-300% FPL"* (≥250%).
- **D4=3:** *"50% for 301%-350%; 25% for 351%-400% FPL"* (≥400%).
- **D5=4:** full HASP PE — *"presumptively eligible … Homelessness; … Enrollment in Medicaid …; WIC … SNAP … documentation will not be required."*
- **D6=3:** MyChart + phone + mail; multi-channel.
- **D7=2:** *"uses a look back method based on claims allowed by Medicare fee-for-service and all private health insurers."*
- **D8=1:** collections referenced; ECA enumeration/period not in the FAP text read.
- **D9=3:** English + Spanish FAP both posted.
- **D10=→M3:** deferred (EIN 56-2141073, UHSEC — M3 reads it).

### 8 — WakeMed Raleigh Campus (Raleigh, NC)
**Read:** FAP PDF `wakemed.org/sites/default/files/pdf/Regulatory/FA Policy_English.pdf` (full text extracted; English + Spanish + summary posted).
- **D1=3 / D2=3:** "Charity Care Policy" + "Charity Care Policy Summary" (English + Spanish) all posted.
- **D3=2:** free care to ~300% via charity sliding scale (income guidelines to 300% FPL); 100% off gross charges for eligible — scored 2 (threshold at/below 300% but 100%-free ceiling is ≤200–250% band on the attached sliding scale). [judgment — sliding-scale exhibit attached, not fully in text]
- **D4=2:** sliding scale to 300%; **D5=4:** full PE — *"Enrollment in Medicaid of patient or a child …; SNAP (formerly known as Food Stamps) … therefore presumptively"* + non-income PE.
- **D6=3:** application online/mail; English + Spanish.
- **D7=2:** *"WakeMed will use the 'Look-Back Method,' as defined in IRS regulations."*
- **D8=3:** *"WakeMed will not engage in ECAs during the one hundred twenty (120) day period after the first post-discharge"* + enumerated ECAs (adverse credit report, requiring payment before non-emergent care) + reasonable-efforts/presumptive-screening-first.
- **D9=3:** English + Spanish policy and applications.
- **D10=→M3:** deferred (WakeMed files Schedule H — M3 reads it).

### 9 — Atrium Health Wake Forest Baptist Medical Center (Winston-Salem, NC)
**Read:** FA landing page `wakehealth.edu/.../financial-assistance` (HTML extracted); operates under Atrium CAFA framework.
- **D1=3:** FA page reachable. **D2=1:** page references documents but a standalone PLS PDF was **not directly linked** on the page read; summary content is on the page → embedded = 1.
- **D3=4:** *"100% Financial Assistance (≤300% Federal Poverty Guidelines)"* (page table). **D4=3:** *"Partial Assistance (301-400% FPG)."*
- **D5=2:** inherits Atrium FAS vendor-scoring PE (not enrollment proxies on the page read) → 2.
- **D6=3:** *"apply online through the application portal or by downloading an application and mailing it."*
- **D7=1:** AGB cap implied by Atrium framework but **not stated with method on the page read** → 1. [judgment]
- **D8=1:** collections referenced, not specified on page read.
- **D9=1:** page is English; footer language list present but no separately-posted plain-language summary located → English-only + summary-on-page only = 1.
- **D10=→M3:** deferred (Wake Forest Baptist files Schedule H — M3 reads it).

### 10 — Cleveland Clinic (Cleveland, OH)
**Read:** FA page `my.clevelandclinic.org/patients/billing-finance/financial-assistance` (HTML extracted) + linked FAP/AGB PDFs.
- **D1=3 / D2=3:** FAP policy PDF + "Financial Assistance Program Summary" both linked.
- **D3=3:** *"Free Care Level: Up to 400% of Federal Poverty Level"* → ≥250% but the **full-free** ceiling is presented as up-to-400% qualifying for assistance with a 100% tier — scored 3 (200–249% would be 3; the 400% figure is the outer eligibility, the 100%-free tier sits below) [judgment — exact 100% cutoff in the FAP PDF not extracted; conservative 3].
- **D4=1:** discount structure above the free tier exists but the band/max FPL was **not explicitly stated** in the content read → some partial discount, <300% certainty → 1. [judgment]
- **D5=0:** **application-only** — *"to be considered for financial assistance … you are required to cooperate with our Medicaid screening process"*; no PE/enrollment-proxy language located → silence-as-0.
- **D6=1:** application + multiple vendor phone lines; single primary channel emphasized, Medicaid-screening precondition → 1.
- **D7=1:** AGB doc exists (*"Basis for Calculating Amounts Charged to Patients"*) but cap/method figure not in the page text read → 1.
- **D8=1:** collections not detailed on page read.
- **D9=3:** *"English, Spanish, Arabic, Russian, Ukrainian, Nepali, Creole"* — translations actually posted (≥2 languages).
- **D10=→M3:** deferred (EIN 34-0714585, Cleveland Clinic Foundation — M3 reads it).

### 11 — UPMC Presbyterian (Pittsburgh, PA)
**Read:** FAP process-policy PDF `upmc.com/-/media/upmc/.../financial-assistance-process-policy.pdf` (full text extracted).
- **D1=3:** FAP PDF linked from "Apply" page. **D2=1:** the located document is the full systemwide policy; a separate standalone PLS was not located alongside it → embedded = 1.
- **D3=2:** *"Indigence: Income falls below 300% of the Federal Poverty Guidelines"* → 100% at ≤300% but scored 2 conservatively because the discrete 100%-free FPL cutoff vs sliding portion was judgment-bound. [judgment — see Limitations]
- **D4=3:** *"Discounted Care … greater than 300% and less than or equal to 400%"* (band to 400%).
- **D5=4:** strong PE — *"Presumptive eligibility may be granted … 1. homelessness …; 2. participation in WIC; 3. receiving SNAP … typically a 100% discount."*
- **D6=3:** application + predictive-model fallback; multi-channel.
- **D7=2:** *"UPMC will use the Look-Back method to determine AGB. The lowest amount currently calculated is 10% resulting in a discount of 90%."*
- **D8=1:** *"Refer to UPMC Billing and Collections Policy HS-RE0724 for the actions"* — ECAs in separate policy, not enumerated in FAP read → 1.
- **D9=3:** *"communicated to patients in … the most prevalent languages spoken in applicable hospital service area communities."*
- **D10=→M3:** deferred (EIN 25-1423657, UPMC — M3 reads it).

### 12 — Hospital of the University of Pennsylvania / Penn Medicine (Philadelphia, PA)
**Read:** Penn FA policy page + plain-language summary page (`pennmedicine.org/patient-resources/policies/financial-assistance/...`); the direct FAP PDF guess 404'd, so scored from the official policy + PLS pages and search-corroborated text retrieved 2026-06-23.
- **D1=3 / D2=3:** "Financial assistance policy" page + distinct "Financial Assistance Summary (plain language)" page both exist.
- **D3=2:** *"below 300% … will qualify for a full coverage discount"* → 100% at ≤300% (scored 2; the 100%-free FPL ceiling vs sliding split judgment-bound). **D4=3:** *"301% and 400% will qualify for a discounted coverage rate."*
- **D5=2:** the PLS describes income/size review and 5-business-day contact but **no enrollment-proxy PE** (Medicaid/SNAP/WIC) language was located on the pages read → discretionary/none-stated; scored 2 conservatively as some presumptive review may occur [judgment — could be 0 if strictly silence-as-0; see Limitations].
- **D6=1:** *"in-person … or by mail by calling a financial counselor"* — application largely phone/in-person/mail; online application not prominent on pages read → 1.
- **D7=1:** AGB cap not stated with method on pages read → 1.
- **D8=1:** collections not detailed on pages read.
- **D9=1:** pages English; no separately-posted multi-language PLS located → 1.
- **D10=→M3:** deferred (Penn-area filing entity 23-2810852 files Schedule H — M3 reads it).

### 13 — Massachusetts General Hospital / Mass General Brigham (Boston, MA)
**Read:** MGB FAP PDF `massgeneralbrigham.org/content/dam/.../financial-assistance-policy-english.pdf` + summary PDF (full FAP text extracted).
- **D1=3 / D2=3:** FAP PDF + separate "Financial Assistance Policy (Summary)" PDF both posted.
- **D3=2:** *"less than or equal to 300% of the Federal Poverty Guidelines (FPG)"* free tier; **D4=3:** *"more than 300% but less than or equal to 600%"* (band well past 400%).
- **D5=2:** PE via MA Health Safety Net / MassHealth — *"patients with full HSN are presumptively eligible for this discount"* — but this is a state-program proxy applied via HSN enrollment, application otherwise required → 2.
- **D6=3:** application + Patient Gateway + phone; multi-channel.
- **D7=2:** §"Amounts Generally Billed" present — AGB tied to Commercial payers, method stated.
- **D8=1:** separate "Credit and Collection Policy" referenced (May 2025), ECAs not enumerated in FAP read → 1.
- **D9=3:** MGB posts the FAP/summary/application in multiple languages (MA prevalent-language requirement) — translated docs available.
- **D10=→M3:** deferred (MGB Inc 22-2658209 files Schedule H — M3 reads it).

### 14 — NewYork-Presbyterian Hospital (New York, NY)
**Read:** Charity Care/Financial Aid Policy PDF `nyp.org/pdf/financial-aid/English-FinancialAid-Policy.pdf` + summary PDF (full text extracted).
- **D1=3 / D2=3:** full policy PDF + *"plain language"* summary, *"in English and other languages,"* both posted.
- **D3=4:** policy covers to *"below 600% of the federal poverty level"* with a sliding fee scale; free-care tier well above 250% → 4 (free care at low-FPL bands per attached sliding fee scale exhibit). [the 100% cell is in the attached "Sliding Fee Scale" exhibit; scored 4 on the policy's broad reach — see Limitations]
- **D4=3:** sliding fee scale to 600% FPL (band ≥400%).
- **D5=2:** PE only via **credit-agency scoring after non-payment** — *"obtain reports from third parties such as credit agencies … to determine whether they may be presumptively eligible"* under limited post-discharge conditions; not enrollment proxies → 2.
- **D6=3:** application any time during billing/collection; documentation pay stub/1040; *"Assets may not be taken into account."*
- **D7=2:** *"an eligible individual may not be charged more than amounts generally billed … Hospital will apply a sliding scale discounting methodology to the AGB."*
- **D8=1:** *"collection practices … are outlined in a separate Collection Policy"* — referenced, ECAs not enumerated in FAP read → 1.
- **D9=3:** materials *"available, upon request and without charge, from Admitting and Emergency … in [other] languages"* + conspicuous-posting clause.
- **D10=→M3:** deferred (NYP files Schedule H — M3 reads it).

### 15 — Ascension Providence Hospital (Southfield/Novi, MI)
**Read:** Ascension national FAP template (e.g. Saint Agnes / Via Christi 2025 FAPs on `healthcare.ascension.org`) read 2026-06-23; the MI-specific Providence page was not separately reachable, so scored from the Ascension standard FAP (250% FPL, presumptive scoring) which is the uniform national policy — flagged in Limitations.
- **D1=3 / D2=3:** Ascension posts FAP + "Summary of Financial Assistance Policy" (Exhibit C PLS) per market.
- **D3=3:** *"incomes less than or equal to 250% of the Federal Poverty Level (FPL) are eligible for 100% charity care"* (≥250% → would be 4; scored 3 because 250% is the boundary, not above it). [judgment]
- **D4=3:** discount tiers above 250% (AGB-based) extend the band (to 500% in some Ascension markets) → 3.
- **D5=2:** *"eligible pursuant to presumptive scoring"* — vendor presumptive scoring, application otherwise → 2.
- **D6=1:** application + 240-day window; channels not richly specified in template read → 1. [judgment]
- **D7=2:** AGB cap + method stated in Ascension FAP.
- **D8=1:** separate billing/collections policy referenced.
- **D9=3:** Ascension posts FAP/PLS in multiple languages (the search surfaced Arabic, Spanish versions).
- **D10=→M3:** deferred (Ascension Providence Hospital entity 38-1358212 files Schedule H — M3 reads it).

### 16 — CommonSpirit Health / CHI St. Luke's facility (Phoenix/Houston)
**Read:** CommonSpirit "Summary of Financial Assistance Policy" PDF `commonspirit.org/content/dam/.../stlukes-health-all-locations-financial-assistance-summary-en.pdf` (full text extracted).
- **D1=3 / D2=3:** FAP + this Summary (PLS) both posted, English + Spanish.
- **D3=2:** *"family income of up to 200% of the Federal Poverty Level … 100% discount."* **D4=3:** *"between 201-400% … reduced to the Amount Generally Billed (AGB)"* (band to 400%).
- **D5=2:** *"In some cases, patients may be awarded financial assistance without a formal application"* — discretionary PE, application is the default → 2.
- **D6=1:** *"Completed a Financial Assistance Application and provided supporting documentation"* — application-led, single submission path emphasized → 1.
- **D7=2:** *"you will not be required to pay more than the Amount Generally Billed … reflects the amount … paid … by private health insurers and Medicare."*
- **D8=1:** collections in separate FAP/policy, not in summary read → 1.
- **D9=3:** *"available … in both English and Spanish"* + translation-on-request clause.
- **D10=→M3:** deferred (CommonSpirit 47-0617373 / facility entity files Schedule H — M3 reads it).

### 17 — AdventHealth Orlando (Orlando, FL)
**Read:** AdventHealth FA legal page + regional FAP PDFs (`adventhealth.com/legal/financial-assistance`); the AdventHealth-Orlando packet PDF returned 403, so scored from AdventHealth's posted policy text + corroborating FAP search results retrieved 2026-06-23 (flagged).
- **D1=1:** FAP exists but is **fragmented across many facility/region PDFs**; the Orlando-specific FAP packet 403'd and the unified policy took site-search to locate → 1. [judgment]
- **D2=3:** distinct PLS/brochure ("Financial Assistance Brochure") posted.
- **D3=2:** *"charity care … at or below 200% of the Federal Poverty Level"* (some facilities 250%) → 2.
- **D4=3:** *"greater than 200% but less than 400% … significant discount"* (band to 400%).
- **D5=2:** *"When a patient is presumptively determined to be eligible …"* — PE referenced but as a discretionary determination with notify-and-apply-for-more language; not enrollment-proxy auto-grant → 2.
- **D6=3:** application accepted *"for up to 240 days following the first billing statement"*; brochure + application + phone.
- **D7=2:** AGB cap stated with look-back basis in AdventHealth FAP.
- **D8=1:** collections in separate policy; 240-day app window noted but ECA enumeration not in text read → 1.
- **D9=1:** Orlando FAP located only in English on pages read; no separately-posted translation confirmed → 1. [judgment]
- **D10=→M3:** deferred (AdventHealth files Schedule H — M3 reads it).

### 18 — Banner – University Medical Center Phoenix (Phoenix, AZ)
**Read:** Banner "Summary of Financial Assistance Programs" PDF `bannerhealth.com/-/media/.../9999-0061-BH-Summary-Of-Financial-Assistance-Programs-And-Application.pdf` (full text extracted).
- **D1=3 / D2=3:** FAP + this Summary-and-Application (PLS) posted.
- **D3=2:** charity care at ≤200% FPL (free); *"income … equal to or less than 200% of the Federal Poverty Level"* → 2. **D4=3:** *"equal to or less than 400% … BH Financial Assistance"* discount band to 400%.
- **D5=0:** **application-only** in the PLS read — *"you will qualify for BH Financial Assistance (1) if … 400% … and, (2) if requested … you apply for Medicaid/AHCCCS, fully cooperate"*; **no PE/enrollment-proxy language** in the summary → silence-as-0. (Full FAP may add PE; the public-facing PLS does not — scored on located text per silence rule.)
- **D6=1:** application required + advance-deposit for non-emergent services; single application path → 1.
- **D7=2:** *"you will in no case be charged more than Amounts Generally Billed … average of the amounts … paid … by private health insurers and Medicare."*
- **D8=1:** *"billing and collections policy … available on the Banner Health website"* — referenced, not enumerated → 1.
- **D9=3:** *"Spanish translation of this Summary, the Hospital's financial assistance and billing policies, and the application forms are available"* (multi-language Arabic version also located).
- **D10=→M3:** deferred (Banner UMC Phoenix files Schedule H — M3 reads it).

### 19 — Corewell Health Butterworth Hospital (Grand Rapids, MI)
**Read:** Corewell FA page `corewellhealth.org/billing/financial-assistance` + FA eligibility policy PDF (search-corroborated; `assets.contentstack.io/.../financialassistancepolicyenglish.pdf`), retrieved 2026-06-23.
- **D1=3:** FA page + policy PDF reachable. **D2=1:** standalone PLS not separately located on page read; summary content embedded → 1. [judgment]
- **D3=3:** *"100% free care for patients with household income at or below 250% FPL"* (≥250% boundary → 3). **D4=3:** *"sliding-scale discounts up to 400% FPL."*
- **D5=2:** Michigan systems commonly apply presumptive scoring; Corewell policy references presumptive determination but enrollment-proxy auto-grant not confirmed in text read → 2. [judgment]
- **D6=1:** *"apply within 240 days of your first post-discharge billing statement"* — application-led; channels not richly enumerated on page read → 1.
- **D7=1:** AGB cap referenced but method/figure not in text read → 1.
- **D8=1:** collections referenced; ECAs/period not in text read → 1.
- **D9=1:** page English; no separately-posted multi-language PLS confirmed → 1. [judgment]
- **D10=→M3:** deferred (Corewell/Butterworth files Schedule H — M3 reads it).

### 20 — Cape Fear Valley Medical Center (Fayetteville, NC)
**Read:** "Debt Mitigation and Presumptive Financial Assistance" PDF + FAP PDF (`capefearvalley.com/sites/default/files/2025-09/...`), retrieved 2026-06-23.
- **D1=3 / D2=3:** FAP + dedicated presumptive/debt-mitigation page both posted.
- **D3=2:** sliding-scale 100% tier at low FPL; **D4=3:** *"sliding scale … household income is between 201% and 500% … discounts between 25% and 75%"* (band to 500%).
- **D5=4:** full HASP PE — *"Criteria for presumptive eligibility include homelessness, enrollment in Medicaid, participation in WIC, or SNAP"* (no application required).
- **D6=1:** *"complete a financial assistance application and provide documentation … mailed to PO Box 2000"* — application + mail emphasized; documentation-heavy → 1.
- **D7=1:** AGB cap not stated with method in text read → 1.
- **D8=1:** collections/debt-mitigation referenced; ECA period not enumerated in text read → 1.
- **D9=1:** English document located; no separately-posted translation confirmed → 1. [judgment]
- **D10=→M3:** deferred (Cape Fear Valley files Schedule H — M3 reads it).

### 21 — Mission Hospital / HCA (Asheville, NC) — FOR-PROFIT (files no Schedule H)
**Read:** Mission/HCA "Charity Financial Assistance (Medical Debt Mitigation) Policy" page + uninsured-discount text (`missionhealth.org/patient-resources/.../financial-assistance`), retrieved 2026-06-23.
- **D1=3 / D2=3:** policy page + uninsured-patient summary document.
- **D3=2:** *"free hospital care … whose income is less than 200 percent of the federal poverty level"* → 2. **D4=3:** *"between 201 and 400 percent … expanded financial assistance"* + *"PLP … 400 and 1,000% FPL"* (band ≥400%).
- **D5=0:** **application-only** — *"To qualify for free care, you must complete a financial assistance application and provide … documents"*; no PE/enrollment-proxy language located → silence-as-0. (Notably, as a for-profit, Mission is **not bound by NC HASP's presumptive-eligibility mandate** the way the NC nonprofits are — a substantive finding, not just a documentation gap.)
- **D6=1:** application + documentation required; single path → 1.
- **D7=1:** uninsured-discount stated; AGB method not given → 1.
- **D8=1:** collections referenced; not enumerated → 1.
- **D9=1:** English; no separately-posted translation confirmed → 1. [judgment]
- **D10=→M3 (n/a):** as a for-profit, HCA's Mission files **no Form 990 Schedule H**, so D10/M3 is genuinely inapplicable (not merely deferred) — M3/M4 must exclude it from the charity-care ratio. For M2 it is totaled on D1–D9 like every other row. **Tot (D1–D9) = 15.**

### 22 — FirstHealth Moore Regional Hospital (Pinehurst, NC)
**Read:** FirstHealth FA page + Credit-and-Collection / Medical Debt Mitigation Procedure PDF (`firsthealth.org/app/files/public/.../Credit and Collection-Medical Debt Mitigation Procedure Revised 03072025.pdf`), retrieved 2026-06-23.
- **D1=1:** FA content is housed inside the Credit-and-Collection/MDMP procedure rather than a clearly-labeled standalone FAP; took site-search to locate → 1. [judgment]
- **D2=1:** no distinct PLS PDF located; summary content embedded → 1.
- **D3=0:** *"Patients at or below 100% of poverty qualify for assistance"* — the **stated income floor for the income-based tier is only 100% FPL**, which is *<138% FPL* per the D3 rule (and far below the 250% Dollar For benchmark); separate PE screening exists but the *income* free-care threshold as written is 100% → **0** under the rubric. (This is a genuine red flag, see Limitations — third-party data say effective free-care reaches ~204% FPL in practice, but the *policy text* states 100%.)
- **D4=1:** *"families under 322% will qualify for discounted care"* (per third-party read of FirstHealth practice) but the policy's own discounted band above the free tier is thinly specified → 1. [judgment]
- **D5=4:** full HASP PE — *"Beginning January 1, 2025, FirstHealth will perform a non-income based presumptive eligibility screening on all guarantors … according to North Carolina Medicaid Debt Mitigation program guidelines"* + income-based screening 1/1/2026; *"not required to provide documentation."*
- **D6=3:** screening at registration (no application needed for PE) + mail application; low burden via auto-screening → 3.
- **D7=1:** AGB not stated with method in text read → 1.
- **D8=1:** collections/MDMP procedure is the document but ECA enumeration/120-day not cleanly in text read → 1.
- **D9=1:** English; no separately-posted translation confirmed → 1. [judgment]
- **D10=→M3:** deferred (FirstHealth files Schedule H — M3 reads it).

### 23 — NYC Health + Hospitals / Bellevue (New York, NY) — PUBLIC (files no Schedule H)
**Read:** NYC H+H Financial Assistance + sliding-fee-scale table PDF (`nychealthandhospitals.org/financial-assistance/`, `hhinternet.blob.core.windows.net/.../sliding-fee-scale-table.pdf`), retrieved 2026-06-23.
- **D1=3 / D2=3:** FA program page + downloadable sliding-fee-scale table + "Options" summary.
- **D3=4:** *"0% – 200% FPL: $0 copay"* and free care; the H+H scale provides nominal/$0 charges across low-FPL bands and assistance up to high FPL → 4. **D4=3:** sliding scale extends well above 400% (Options covers higher bands).
- **D5=2:** financial assistance via application + presumptive sliding placement; no enrollment-proxy auto-grant documented → 2.
- **D6=1:** *"go into one of the … sites to meet with a Financial Counselor"* / in-person-oriented application → 1. (Mitigated by immigration-protected, no-data-sharing design, but channel is in-person/application.)
- **D7=2:** charges capped at Medicaid-rate equivalents on the scale (*"100% of Medicaid rate"* tiers) — effectively an AGB-equivalent cap stated → 2.
- **D8=1:** collections governed by NY state law + separate policy; not enumerated in text read → 1.
- **D9=3:** materials posted, immigration-protected, multi-language NYC norm; conspicuous all-comers notice → 3.
- **D10=→M3 (n/a):** public benefit corporation; files **no Form 990 Schedule H**, so D10/M3 is inapplicable (not merely deferred). Totaled on D1–D9 like every other row. **Tot (D1–D9) = 22.**

### 24 — Cook County Health / Stroger Hospital (Chicago, IL) — PUBLIC (files no Schedule H)
**Read:** CareLink page + FAP PDF (`cookcountyhealth.org/wp-content/uploads/Financial-Assistance-Policy-_English.pdf`, `/carelink/`), retrieved 2026-06-23.
- **D1=1:** FAP exists but assistance is routed through the CareLink program page; standalone FAP PDF took search to locate → 1. [judgment]
- **D2=3:** CareLink summary + application + FAP all posted.
- **D3=2:** *"uninsured individuals with an annual income equal to or less than 250% of the Federal Poverty guidelines … eligible for a 100% discount"* — 100% free at ≤250% → 2 (boundary). [judgment — could be 4 at exactly 250%; scored 2 conservatively]
- **D4=3:** *"30% discount 50% discount or 100% discount"* sliding to *"600% of federal poverty guidelines"* (band ≥400%).
- **D5=2:** sliding placement + presumptive elements, but enrollment-proxy auto-grant not documented; **residency-gated to Cook County** → 2.
- **D6=1:** *"go into one of the Cook County Health sites to meet with a Financial Counselor"* — in-person application → 1.
- **D7=1:** charge cap not stated with AGB method in text read → 1.
- **D8=1:** collections not enumerated in text read → 1.
- **D9=1:** application materials English (and Spanish in practice) but a separately-posted plain-language multi-language PLS not confirmed in text read → 1. [judgment]
- **D10=→M3 (n/a):** public system; files **no Schedule H**, so D10/M3 inapplicable (not merely deferred). Totaled on D1–D9. **Tot (D1–D9) = 15.**

### 25 — Parkland Health / Parkland Memorial Hospital (Dallas, TX) — PUBLIC (files no Schedule H)
**Read:** Parkland Financial Assistance page (`parklandhealth.org/parkland-financial-assistance`, `/for-patients/financial-assistance`), retrieved 2026-06-23.
- **D1=3:** PFA program page reachable. **D2=1:** standalone PLS PDF not located; summary on page → 1. [judgment]
- **D3=2:** *"Dallas County residents with household income at or below 200% of the Federal Poverty Level qualify for complete free care"* → 2.
- **D4=1:** *"between 201% and 250% FPL qualify for discounted care on a sliding scale"* — partial band but tops at 250% (<300%) → 1.
- **D5=0:** application + **Dallas County residency proof required**; no PE/enrollment-proxy auto-grant documented → silence-as-0. (Residency gate is itself an access barrier beyond what the rubric captures — noted for M4.)
- **D6=1:** *"requires proof of Dallas County residency"* + application + financial-counselor calculation → documentation-heavy, single path → 1.
- **D7=1:** charge cap/AGB method not stated in text read → 1.
- **D8=1:** collections not enumerated in text read → 1.
- **D9=1:** English page; multi-language PLS not confirmed → 1. [judgment]
- **D10=→M3 (n/a):** public hospital district; files **no Schedule H**, so D10/M3 inapplicable (not merely deferred). Totaled on D1–D9. **Tot (D1–D9) = 11.**

### 26 — Grady Memorial Hospital / Grady Health System (Atlanta, GA)
**Read:** Grady "Financial Assistance Program Policy" PDF (`gradyhealth.org/wp-content/uploads/Financial-Assistance-Program-Policy-1.pdf`) + FA page, retrieved 2026-06-23.
- **D1=1:** FAP PDF exists but the FA program page routes to phone scheduling; PDF took search to locate → 1. [judgment]
- **D2=1:** standalone PLS not separately located; copays/summary doc embedded → 1.
- **D3=2:** *"Fulton and DeKalb County residents with household income at or below 200% … qualify for complete charity care"* → 2.
- **D4=2:** *"between 201% and 300% FPL qualify for discounted care on a sliding scale"* (band to 300%) → 2.
- **D5=0:** *"call … to schedule a time to meet with a Financial Counselor"* + **county-residency-gated**; no PE/enrollment-proxy auto-grant documented → silence-as-0.
- **D6=1:** application within 240 days + in-person financial counselor; documentation required → 1.
- **D7=1:** AGB method not stated in text read → 1.
- **D8=1:** collections not enumerated in text read → 1.
- **D9=1:** English; multi-language PLS not confirmed → 1. [judgment]
- **D10=→M3:** deferred (Grady Health System, nonprofit corp, files Schedule H — M3 reads it).

### 27 — Sentara Norfolk General Hospital (Norfolk, VA)
**Read:** Sentara FAP policy + Plain Language Summary PDFs (`shc-p-001.sitecorecontenthub.cloud/...`); **the PLS PDF is image-only and yielded no extractable text** — scored from the Sentara FAP policy text and `sentara.com/billing/financial-assistance` search-corroborated content retrieved 2026-06-23 (flagged).
- **D1=1:** FAP/PLS hosted on a content-hub CDN linked from facility billing pages; the policy took several hops to reach and the PLS PDF was image-only → 1. [judgment]
- **D2=3:** a distinct "Financial Assistance Policy Plain Language Summary" PDF exists (located, though image-only) → PLS present = 3.
- **D3=3:** *"income is 300% or below the … federal poverty level … free care"* (Hampton Roads facilities) → ≥250% → 3.
- **D4=3:** *"between 300% and 400% … 80% discount"* (band to 400%).
- **D5=2:** *"presumptive financial assistance … if the patient is deemed eligible for or has Medicaid coverage, homeless, deceased … SNAP … FQHC"* — strong PE criteria, but applied as a write-off determination rather than a no-application auto-grant for all NC-style proxies, and VA has no HASP mandate → 2. (Arguably 4; scored 2 because the PLS confirming no-application auto-grant was image-only/unreadable — judgment-bound, see Limitations.)
- **D6=1:** application + asset test (*"less than $50,000 in available assets"*); documentation-heavy → 1.
- **D7=1:** AGB method not confirmed in readable text → 1.
- **D8=1:** collections not enumerated in readable text → 1.
- **D9=1:** PLS exists but image-only (not machine-readable, an accessibility concern); multi-language posting not confirmed → 1. [judgment]
- **D10=→M3:** deferred (Sentara files Schedule H — M3 reads it).

### 28 — Carilion Roanoke Memorial Hospital (Roanoke, VA)
**Read:** Carilion "Financial Assistance Policy" PDF `carilionclinic.org/financial_assistance_policy_english.pdf` (full text extracted) + application PDF.
- **D1=3 / D2=1:** FAP PDF + application posted; a distinct standalone PLS was not separately located (summary content within FAP) → D2=1.
- **D3=2:** *"100% Financial Assistance is provided to patients with available assets of less than $25,000 and family income less than 300% of FPG"* — free care to <300% but asset-gated → 2 (judgment; the 100% tier reaches near 300% but is asset-conditioned).
- **D4=3:** *"total gross family income less than 500% of the FPG … eligible for financial assistance"* (band to 500%).
- **D5=2:** *"Uninsured patients will be screened for presumptive eligibility for 100% discount … through qualification through: Free clinic … FQHCs … other state or local assistance programs"* — PE via program/clinic enrollment proxies, screened (no application for those) → 2 (not full HASP, no Medicaid/SNAP/WIC enumerated as auto-grant; VA has no mandate).
- **D6=1:** *"must complete a FAA, provide required documentation, and … validation with external agencies"* — documentation + external validation, asset test → 1.
- **D7=2:** *"Amounts Generally Billed (AGB) … calculated using the look back method as prescribed by Internal Revenue Code Section 501(r)."*
- **D8=1:** *"actions … in the event of nonpayment are described in a separate Billing and Collection Policy"* — referenced, not enumerated in FAP read → 1.
- **D9=1:** English FAP located; no separately-posted translation confirmed in text read → 1. [judgment]
- **D10=→M3:** deferred (Carilion Clinic files Schedule H — M3 reads it).

---

## Cross-cutting observations (for M4, not new scoring)

- **The NC HASP mandate is visible in the text.** All five NC academic/large-system nonprofits with extractable full FAPs (Duke #2, UNC #3/#4, Novant #6, ECU #7, WakeMed #8) carry **near-identical D5=4 presumptive-eligibility language** (homelessness / Medicaid / SNAP / WIC, no application, with a 1/1/2025 non-income and 1/1/2026 income-based effective date). This is the HASP mandate working as written. Cape Fear Valley (#20) and FirstHealth (#22) carry the same language. **Atrium (#1) and Cone (#5) instead use third-party FAS vendor scoring (D5=2)** rather than enumerated enrollment proxies — a defensible but weaker form that an NC AG could question against the HASP "auto-qualify Medicaid/SNAP/WIC" wording.
- **The for-profit contrast lands.** Mission/HCA (#21, D5=0, application-only) is the only NC hospital in the sample with **no presumptive-eligibility pathway in its public text** — consistent with HASP binding nonprofits but not HCA's for-profit Mission.
- **Out-of-state and residency-gated public systems score lowest on D5/D6.** Cleveland Clinic (#10), Banner (#18), Parkland (#25), Grady (#26) are application-led with Medicaid-screening preconditions and (for the public systems) county-residency gates — the application-friction the Dollar For report names as the dominant driver of the 71% gap.
- **D8 is systematically depressed by document architecture, not necessarily by non-compliance.** Most FAPs satisfy 501(r)(6) by *referencing* a separate Billing & Collections Policy rather than enumerating ECAs and the 120-day period inside the FAP. Per the M1 D8 rule this scores 1 ("referenced but not specified in available text"). Only Atrium (#1), UNC (#3/#4), Novant (#6), and WakeMed (#8) put the ECA list + period inside the FAP text I read (D8=3). This is a real, defensible-as-written distinction but M4 should flag it as partly a drafting-style artifact (the separate policy may fully comply).
- **D10 is intentionally absent from these M2 numbers.** The charity-care-at-cost dimension is M3's measurement; it will be added for the ~24 Schedule-H filers at that stage, and the four non-filers (#21/#23/#24/#25) will be ranked on D1–D9 accessibility only. M4 must therefore not treat the 28-point M2 totals as final compliance scores — they are the accessibility half.

---

## Limitations & counter-evidence

- **Pages I could not reach / read in full.** (a) **Cone Health (#5)** FAP PDF and the **UNC `unchealthcare.org` file host** are behind Akamai "Access Denied" to automated retrieval; I read UNC from the identical system policy on `unchealth.org` (verbatim) and Cone from its searchable policy text + corroborating sources (not the raw PDF) — so Cone's D7 in particular is scored from summary text, not the PDF clause. (b) **Sentara (#27)** PLS PDF is **image-only and produced zero extractable text**; its D2/D5/D9 are scored from the FAP policy text and search-corroborated content, and the image-only PLS is itself counted against D9 accessibility. (c) **AdventHealth-Orlando (#17)** packet PDF and the **Cleveland Clinic / CommonSpirit / Banner** internal FAP clauses for D4/D7 were read from posted summaries and pages rather than the full underlying FAP in some cases; where a clause was not in the text I actually retrieved I applied the silence/conservative rule and marked the dimension `[judgment]`. (d) **Ascension Providence MI (#15)** was scored from Ascension's uniform national FAP template (250% FPL, presumptive scoring) because the MI-Providence-specific page was not separately reachable; if the MI facility deviates from the template my D3/D5 could be off by 1.
- **FAP text ≠ actual screening practice — in both directions, and the FirstHealth case shows it.** FirstHealth (#22) scores D3=0 because its *policy text* states free care only "at or below 100% of poverty," yet third-party data say its *effective* free-care reach is ~204% FPL. So a low D3 here may understate real generosity — and conversely, the NC hospitals' model D5=4 language does not prove their billing offices actually auto-grant. This rubric measures **disclosed policy accessibility**, which is what a regulator can cite; M3's Schedule H dollars are the partial corrective.
- **Silence-scored-as-0 is contestable and I applied it literally.** D5=0 for Cleveland Clinic (#10), Banner (#18), Mission (#21), Parkland (#25), Grady (#26) means "no presumptive-eligibility language was findable in the public text I read," not "this hospital never grants assistance without an application." Banner's full FAP (vs the PLS I read) may contain PE language; a hospital's counsel would argue exactly that. Each 0 is defensible only as "not findable by a diligent public reader on the document retrieved 2026-06-23," and the specific document read is named per row so the claim is re-checkable.
- **Dimensions where my reading was judgment-bound** (flagged `[judgment]` inline): D3/D4 boundary calls where the 100%-free FPL cutoff sits in an *attached sliding-scale exhibit* I could not always extract (NYP #14, WakeMed #8, MGB #13, UPMC #11, Penn #12, Ascension #15, Cook County #24); D1 "clicks-to-FAP" accessibility calls (ECU #7, AdventHealth #17, FirstHealth #22, Sentara #27, Grady #26, Cook County #24); D9 "translation actually posted" calls where I could confirm English but not a separately-posted translation (many regionals). A second scorer could move several of these ±1; the point values are transparent so M4 can re-derive. In particular, **UPMC #11 and Penn #12 D3 are scored 2 conservatively** where a generous reading (free care to 300%) could justify 4 — I chose the lower score wherever the discrete 100%-free FPL ceiling vs. the sliding portion was ambiguous in the text retrieved.
- **D10 is formally deferred to M3, not scored in M2.** This revision assigns **no** D10 points and computes every total on D1–D9 only (max 28). M1 defines D10 as the Form 990 Schedule H Part I charity-care-at-cost ratio and explicitly assigns the Schedule H pull to M3; M2 reads FAP/PLS text, not tax filings. The prior draft's provisional D10 guesses ("scored 1 pending M3 dollar figure," "expected >1.0%") were removed precisely because they were not backed by a checkable Schedule H figure. **Consequence and caveat for M4:** the 28-point M2 totals are an *accessibility* score, not a full compliance score — they understate nothing and overstate nothing about actual charity-care spending, which arrives in M3. The four non-filers (#21 for-profit Mission/HCA; #23 NYC H+H; #24 Cook County; #25 Parkland) file no Schedule H at all, so for them D10/M3 is inapplicable rather than merely deferred; M4 must rank those four on D1–D9 accessibility only and never on the charity-care ratio.
- **Sample bias compounds the score spread.** The high-scoring cluster is dominated by **NC HASP-bound hospitals**, which are *legally required* to have the PE language that earns D5=4 — so the NC subset scoring well is partly a mandate artifact, not evidence NC hospitals are intrinsically more generous. The sample over-represents large web-publishing systems (M1's stated bias), so even the low scorers here are likely **more** accessible than the absent small/rural hospitals. M4 must frame results as "among prominent web-publishing systems, these score worst," not "worst in America."
- **Single-source aggregate framing.** The motivating "71% billed / $14B" figures trace to one advocacy source (Dollar For, *Bridging the Chasm*, 2024); this scorecard does not depend on those aggregates being exactly right (it scores each hospital on its own retrieved text), but the problem's framing does, and a hostile reader will note the source's campaign interest.

---

### Sources (documents actually retrieved 2026-06-23)

Per-hospital FAP/PLS URLs are named inline in Part B. Rubric and sample: `artifacts/2026-06-23-m1-rubric-and-sample.md`. 501(r) basis for each dimension: IRS [501(r)(4)](https://www.irs.gov/charities-non-profits/financial-assistance-policy-and-emergency-medical-care-policy-section-501r4), [501(r)(5)](https://www.irs.gov/charities-non-profits/limitation-on-charges-section-501r5), [501(r)(6)](https://www.irs.gov/charities-non-profits/billing-and-collections-section-501r6); [26 CFR 1.501(r)-4](https://www.law.cornell.edu/cfr/text/26/1.501(r)-4). NC HASP benchmark: [NC Health News, 2024](https://www.northcarolinahealthnews.org/2024/08/13/nc-medical-debt-relief-plan-11-hospital-must-dos-for-hospitals/). Application-friction basis: [Dollar For, *Bridging the Chasm*, 2024](https://dollarfor.org/wp-content/uploads/2024/04/Dollar_For.Bridging_the_Chasm.pdf). Verbatim policy quotes above were copied from each hospital's FAP/PLS PDF or page text extracted locally (pdfminer.six) on 2026-06-23; where a page was Akamai-blocked or image-only the row says so and names the alternate source read. Schedule H charity-care figures (D10) are deferred to M3 and will be pulled from ProPublica [Nonprofit Explorer](https://projects.propublica.org/nonprofits/) against the EINs in M1.
