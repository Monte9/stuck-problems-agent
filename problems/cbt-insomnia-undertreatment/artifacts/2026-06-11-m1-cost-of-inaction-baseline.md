# M1 — Cost-of-inaction baseline: chronic insomnia treated with pills instead of CBT-I

**Problem:** cbt-insomnia-undertreatment · **Milestone:** 1 · **Date:** 2026-06-11
**Bottom line:** Continuing the status quo — hypnotic prescribing instead of guideline-recommended CBT-I — costs an estimated **$92 million per 100,000 US adults per year** (sensitivity range **$17M–$146M**), dominated by productivity loss, plus measurable excess healthcare spending and hypnotic-attributable hip fractures in adults 65+.

---

## 1. Summary table of key quantities

| # | Quantity | Value | Year (data / pub) | Population | Source |
|---|----------|-------|-------------------|------------|--------|
| 1 | Chronic insomnia prevalence (used as central input) | ~8% of adults ("one in 12") | 2023 | Adults in US + 8 other high-income countries (RAND survey) | [RAND RRA2166-1 press release, 2023](https://www.rand.org/news/press/2023/03/17.html); [report PDF](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2100/RRA2166-1/RAND_RRA2166-1.pdf) |
| 2 | Chronic insomnia disorder prevalence (high input) | ~10% of adults meet diagnostic criteria (30%–20%–10% rule: 30% symptoms, 15–20% report symptoms, ~10% meet criteria) | 2022 (review) | US/general adult | Morin & Jarrin, *Sleep Medicine Clinics* 2022, [PMID 35659072](https://pubmed.ncbi.nlm.nih.gov/35659072/); AASM-aligned estimate also in [JCSM](https://jcsm.aasm.org/doi/pdf/10.5664/jcsm.26391) |
| 3 | Global clinically relevant insomnia prevalence (context, not used in model) | 16.2% | 2025 | Global adults, systematic literature review | *Sleep Medicine Reviews* 2025, [PMC12676268](https://pmc.ncbi.nlm.nih.gov/articles/PMC12676268/) |
| 4 | US adults ever using CBT-I | 3.5% lifetime; 2.6% past year; only 15.1% recognized CBT-I at all | 2025 survey (pub. 2026) | 3,080 US adults, nationally representative | *Behavioral Sleep Medicine*, [DOI 10.1080/15402002.2025.2610674](https://doi.org/10.1080/15402002.2025.2610674) / [PMC12797138](https://pmc.ncbi.nlm.nih.gov/articles/PMC12797138/) |
| 5 | Insomnia patients referred to CBT-I | <10% of patients with likely insomnia diagnosis | 2018 (narrative review) | US patients at academic medical centers | Koffel et al., *J Gen Intern Med* 2018, [PMC5975165](https://pmc.ncbi.nlm.nih.gov/articles/PMC5975165/) |
| 6 | Zolpidem prescriptions dispensed, US | >11 million (rank #54 of all drugs); 10.8M in 2021, declining since 2013 | 2023; 2021 | US outpatient | [ClinCalc DrugStats: Zolpidem](https://clincalc.com/DrugStats/Drugs/Zolpidem) (2023); [Statista, 2021](https://www.statista.com/statistics/1373894/total-prescriptions-of-zolpidem-in-the-united-states/) |
| 7 | Benzodiazepine prescriptions dispensed, US | 92 million (alprazolam 38%, clonazepam 24%, lorazepam 20%) | 2019 (FDA DSC pub. 2020) | US outpatient retail + mail-order pharmacies | [FDA Drug Safety Communication, Sept 2020](https://www.fda.gov/media/142368/download?attachment=) |
| 8 | Duration of benzodiazepine use | ~50% of patients dispensed oral benzodiazepines received them for ≥2 months | 2018 (FDA DSC pub. 2020) | US outpatients | [FDA Drug Safety Communication, Sept 2020](https://www.fda.gov/media/142368/download?attachment=) |
| 9 | Benzodiazepine use, adults 65–80 | 8.7% used in one year; long-term use (≥120 days/yr) rises with age to nearly one-third of older users | 2008 data (pub. 2015) | US adults 65–80, LifeLink LRx national prescription database | Olfson et al., *JAMA Psychiatry* 2015, [DOI 10.1001/jamapsychiatry.2014.1763](https://jamanetwork.com/journals/jamapsychiatry/fullarticle/2019955); summarized in [PMC5173408](https://pmc.ncbi.nlm.nih.gov/articles/PMC5173408/) |
| 10 | Harm: Z-drugs → fractures, older adults | OR 1.63 (95% CI 1.42–1.87) for fractures; zolpidem risk modified by age — >300% increase in users over 85; falls OR elevated but not statistically significant | 2018 meta-analysis | Older adults, 14 studies | Treves et al., *Age and Ageing* 2018, [DOI 10.1093/ageing/afx167](https://academic.oup.com/ageing/article/47/2/201/4564456) |
| 11 | Harm: Z-drugs in dementia | Higher-dose z-drugs: any fracture HR 1.67, hip fracture HR 1.96, stroke HR 1.88 vs. untreated sleep-disturbed comparators | 2020 cohort | People living with dementia, England (population-based) | Richardson et al., *BMC Medicine* 2020, [DOI 10.1186/s12916-020-01821-5](https://doi.org/10.1186/s12916-020-01821-5) |
| 12 | Harm: benzodiazepines → Alzheimer's disease | Ever-use adjusted OR 1.51 (95% CI 1.36–1.69); >180 prescribed daily doses OR 1.84 (1.62–2.08), dose-response | 2000–2009 data (pub. 2014) | 1,796 AD cases / 7,184 controls, age >66, Quebec | Billioti de Gage et al., *BMJ* 2014, [DOI 10.1136/bmj.g5205](https://doi.org/10.1136/bmj.g5205) / [PMC4159609](https://pmc.ncbi.nlm.nih.gov/articles/PMC4159609/) |
| 13 | Trained CBT-I/BSM provider supply | 659 behavioral sleep medicine providers in the US (88% of 752 worldwide); 58% concentrated in 12 states; 4 states (NH, HI, SD, WY) had zero | 2016 | US credentialed BSM providers | Thomas et al., *J Clin Sleep Med* 2016, [PubMed 27159249](https://pubmed.ncbi.nlm.nih.gov/27159249/) / [PMC5070478](https://pmc.ncbi.nlm.nih.gov/articles/PMC5070478/) |
| 14 | Productivity cost of insomnia, US (central input) | $207.5 billion/year (lost productivity / GDP output); 44–54 working days lost per affected worker/year | 2023 | US working-age adults | [RAND RRA2166-1, 2023](https://www.rand.org/news/press/2023/03/17.html); [DOI 10.7249/RRA2166-1](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2100/RRA2166-1/RAND_RRA2166-1.pdf) |
| 15 | Productivity cost, comorbidity-adjusted (low input) | $63.2 billion/year net of 26 comorbid conditions; $2,280/worker with insomnia (presenteeism-dominated) | 2008–2009 data (pub. 2011, 2011 USD) | 7,428 employed US health-plan subscribers (America Insomnia Survey) | Kessler et al., *Sleep* 2011, [DOI 10.5665/SLEEP.1230](https://academic.oup.com/sleep/article/34/9/1161/2454605) / [PMC3157657](https://pmc.ncbi.nlm.nih.gov/articles/PMC3157657/) |
| 16 | Healthcare savings from digital CBT-I (modifiable-cost anchor) | $2,083/patient first-year savings (−42% total cost); pharmacy −$1,745 (−46%); n=21,797 (11,027 users, 10,770 matched controls) | 2025 | US insured patients prescribed SleepioRx | *J Health Econ Outcomes Res* 2025, [DOI 10.36469/001c.146434](https://doi.org/10.36469/001c.146434) / [PMC12619666](https://pmc.ncbi.nlm.nih.gov/articles/PMC12619666/) |
| 17 | Incremental healthcare expenditure, diagnosed sleep disorders (high-bound input) | $6,975/person/year (any G47.x sleep-disorder diagnosis; insomnia not separable) | 2018 MEPS data (pub. 2021) | US adults, ~13.6M with diagnosed sleep disorder | Huyett & Bhattacharyya, *J Clin Sleep Med* 2021, [DOI 10.5664/jcsm.9392](https://doi.org/10.5664/jcsm.9392) / [PMC8494101](https://pmc.ncbi.nlm.nih.gov/articles/PMC8494101/) |
| 18 | All-cause cost difference, Medicare insomnia patients (context only — NOT used; see Limitations) | +$63,607/year vs. matched controls, driven by inpatient care | 2006–2013 data (pub. 2019) | 151,668 Medicare beneficiaries with insomnia vs. 333,038 controls | Wickwire et al., *Sleep* 2019, [DOI 10.1093/sleep/zsz007](https://academic.oup.com/sleep/article/42/4/zsz007/5288676) |
| 19 | Hip fracture hospitalizations, US 65+ | ~319,000/year; 88% of hip-fracture hospitalizations caused by falls | accessed 2026 (CDC facts page; underlying data 2019–2021) | US adults 65+ | [CDC Older Adult Fall Prevention — Facts](https://www.cdc.gov/falls/data-research/facts-stats/index.html) |
| 20 | First-year direct medical cost per hip fracture | $50,508/patient (Medicare claims); alternative matched-cohort estimate $39,497 | 2019 publication | US Medicare hip/intertrochanteric fracture patients | Adeyemi & Delhougne, *JBJS Open Access* 2019, [PMC6510469](https://pmc.ncbi.nlm.nih.gov/articles/PMC6510469/); matched-cohort alternative [PMC3557373](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3557373/) |
| 21 | US adult population (normalization denominator) | 258.3 million adults 18+; 55.8 million aged 65+ (21.6% of adults) | 2020 Census | US | [US Census Bureau, adult population 2020](https://www.census.gov/library/stories/2021/08/united-states-adult-population-grew-faster-than-nations-total-population-from-2010-to-2020.html); [US Census Bureau, 65+ population 2020](https://www.census.gov/library/stories/2023/05/2020-census-united-states-older-population-grew.html) |

---

## 2. Worked cost-of-inaction model (per 100,000 US adults, annual)

**Definition.** "Cost of inaction" = the annual economic burden attributable to chronic insomnia that remains *untreated by CBT-I* under the status quo, in a representative population of 100,000 US adults, expressed in three additive components: (A) productivity loss, (B) excess healthcare spending demonstrably modifiable by digital CBT-I, and (C) direct medical costs of hypnotic-attributable hip fractures in adults 65+.

### Central-case inputs

| Symbol | Input | Value | Source row |
|--------|-------|-------|------------|
| P | Chronic insomnia prevalence | 8% | Row 1 |
| U | Share of insomnia sufferers untreated by CBT-I | 95% (assumption: 5% treated, bracketed by 3.5% lifetime population use and <10% patient referral) | Rows 4–5 |
| Prod | National productivity loss | $207.5B/yr | Row 14 |
| A_pop | US adults | 258.3M | Row 21 |
| S | First-year modifiable healthcare spend per untreated patient | $2,083 | Row 16 |
| E_share | Adults 65+ as share of adults | 21.6% (55.8M / 258.3M) | Row 21 |
| B_use | Benzodiazepine use among 65+ | 8.7% | Row 9 |
| HF_base | Baseline hip-fracture hospitalization rate, 65+ | 319,000 / 55.8M = 0.572%/yr | Rows 19, 21 |
| OR | Hypnotic fracture odds ratio (≈RR; rare outcome) | 1.63 | Row 10 |
| C_HF | First-year direct cost per hip fracture | $50,508 | Row 20 |

### Component A — productivity loss among untreated chronic insomnia sufferers

```
A1. National productivity loss per adult  = $207.5B ÷ 258.3M adults      = $803.33 per adult per year
A2. Per 100,000 adults                    = $803.33 × 100,000            = $80,332,946
A3. Attributable to UNTREATED sufferers   = $80,332,946 × 0.95           = $76,316,299
Component A ≈ $76.32M
```
(The RAND total already embeds its ~8% prevalence, so A scales by total adults, not by the insomnia subgroup; the 95% untreated share isolates the inaction-attributable portion.)

### Component B — excess healthcare spending modifiable by CBT-I

```
B1. Chronic insomnia sufferers            = 100,000 × 0.08               = 8,000
B2. Untreated by CBT-I                    = 8,000 × 0.95                 = 7,600
B3. Modifiable spend per untreated person = $2,083 (demonstrated first-year dCBT-I savings, Row 16)
B4. Component B                           = 7,600 × $2,083               = $15,830,800
Component B ≈ $15.83M
```

### Component C — hypnotic-attributable hip fractures, adults 65+

```
C1. Adults 65+ per 100,000 adults         = 100,000 × 0.216              = 21,600
C2. Benzodiazepine users (one-year)       = 21,600 × 0.087               = 1,879
C3. Baseline hip-fracture rate, 65+       = 319,000 ÷ 55,800,000         = 0.00572 /person-yr
C4. Excess rate among exposed             = 0.00572 × (1.63 − 1)         = 0.00360 /person-yr
C5. Excess hip fractures per year         = 1,879 × 0.00360              = 6.77
C6. Component C                           = 6.77 × $50,508               = $341,939
Component C ≈ $0.34M
```
(Conservative: counts benzodiazepine users only — z-drug-only users excluded to avoid overlap guessing; counts hip fractures only, not other fractures, falls without fracture, strokes, MVAs, or dementia costs.)

### Central total

```
Total = A + B + C = $76.32M + $15.83M + $0.34M = $92.49M  ≈  $92M per 100,000 adults per year
```

## 3. Sensitivity analysis (low / central / high)

| Input varied | Low scenario | Central | High scenario |
|---|---|---|---|
| Prevalence P | 6% (Row 2 range floor) | 8% | 10% (Row 2) |
| Untreated share U | 90% | 95% | 97% |
| Productivity basis | Kessler comorbidity-adjusted $63.2B (2011 USD, Row 15), and only 50% counted as remediable by treatment | RAND $207.5B × U | RAND $207.5B × U |
| Healthcare basis | $2,083 × 50% realistic engagement | $2,083 | $6,975 (MEPS incremental, Row 17 — overattribution flagged) |
| Older-adult exposure | Long-term users only (31.4% of users); $39,497/fracture | 8.7% users; $50,508 | 12% total sedative-hypnotic exposure (benzo + z-drug, assumption [speculative]); $50,508 |

**Low scenario arithmetic:**
```
A_low = ($63.2B ÷ 258.3M) × 100,000 × 0.90 × 0.50 = $244.68 × 100,000 × 0.45 = $11.01M
B_low = 100,000 × 0.06 × 0.90 × $2,083 × 0.50      = 5,400 × $1,041.50      = $5.62M
C_low = (1,879 × 0.314) × 0.00360 × $39,497         = 590 × 0.00360 × $39,497 = $0.08M
Total_low ≈ $16.7M
```

**High scenario arithmetic:**
```
A_high = $80,332,946 × 0.97                          = $77.92M
B_high = 100,000 × 0.10 × 0.97 × $6,975              = 9,700 × $6,975        = $67.66M
C_high = (21,600 × 0.12) × 0.00360 × $50,508         = 2,592 × 0.00360 × $50,508 = $0.47M
Total_high ≈ $146.1M
```

**Result: cost of inaction ≈ $92M per 100,000 adults per year (range $17M–$146M).** Even the low scenario — comorbidity-adjusted productivity in 14-year-old dollars, halved for engagement realism, harms restricted to long-term older users — exceeds $16M per 100,000 adults annually.

### Scale reference
Per 100,000 adults, the central case implies ~7,600 untreated chronic insomnia sufferers served by roughly **0.26 trained BSM providers** (659 US providers ÷ 258.3M adults × 100,000 — Rows 13, 21), i.e., ~29,800 untreated patients per trained provider. This is the supply-side case for digital CBT-I, taken up in M2.

---

## 4. Limitations & counter-evidence

1. **Productivity dominates and is the softest number.** Component A is 83% of the central estimate. RAND's $207.5B is a top-down, survey-based estimate including self-reported presenteeism and does not fully isolate insomnia from comorbid depression, pain, and apnea. Kessler's comorbidity-adjusted figure is 3.3× lower ($63.2B), and it is in 2011 dollars — the low and central scenarios therefore mix price vintages (no inflation adjustment applied), which biases the *low* bound further down rather than making the range artificially tight. A payer who only credits medical spend should look at B + C alone: ~$5.7M–$68.1M per 100,000 adults.
2. **Treatment counterfactual is optimistic.** The model implicitly assumes untreated patients could be treated and would benefit at the rates observed in studies. Real-world digital CBT-I uptake and completion are well below 100% (the SleepioRx cohort consists of patients who were prescribed and engaged — a selection-biased group likely healthier and more motivated than average). The 50% engagement haircut in the low scenario is a judgment call, not an empirical parameter [speculative].
3. **Observational harm estimates risk confounding by indication and reverse causation.** People prescribed hypnotics differ systematically from those who are not (sicker, more comorbid, more sleep-disturbed — and insomnia itself raises fall risk). The benzodiazepine–Alzheimer's association (Row 12) may partly reflect prodromal dementia symptoms being treated with benzodiazepines rather than causation; this is a live debate in the literature. Component C treats OR≈RR (acceptable for a ~0.6%/yr outcome) and assumes the fracture OR from mixed-hypnotic studies applies to the benzodiazepine-using population.
4. **Data vintage is uneven.** Older-adult benzodiazepine prevalence is from 2008 data (Row 9); provider counts are from 2016 (Row 13) and predate the post-COVID telehealth expansion and digital therapeutics era; benzodiazepine dispensing is from 2019. Zolpidem prescriptions have *declined* since 2013 (Row 6) — counter-evidence that part of the problem is already shrinking without intervention, though 92M annual benzodiazepine prescriptions and ~11M zolpidem prescriptions remain large absolute exposures.
5. **Possible double counting between components.** Component B (modifiable healthcare spend of untreated insomnia patients) and Component C (fracture costs among older hypnotic users) draw from overlapping populations; a 65+ insomnia patient who fractures a hip could contribute to both. Because C is only 0.4% of the central total, the overstatement is bounded at well under 1%, but it is not zero.
6. **US-only and uniform-population assumptions.** All inputs are US; the per-100,000 figure assumes national age structure (21.6% of adults 65+) and prevalence apply uniformly. A Medicare Advantage population would have far higher C and B (cf. Row 18's +$63,607 all-cause Medicare cost difference — deliberately *excluded* from the model because it is an all-cause difference, not an attributable cost, and using it would inflate the estimate roughly 30-fold); a young commercial population would have near-zero C.

---

## 5. Self-check against done-criteria

- Every summary-table row carries value, year, population, and a URL/DOI to a peer-reviewed, governmental, or primary source — done (Rows 1–21).
- Model arithmetic shown line by line; final figure reproducible from stated inputs — done (Sections 2–3).
- Sensitivity check with explicit low/high arithmetic producing a stated range ($17M–$146M) — done (Section 3).
- Limitations section with six named weaknesses, including data vintage, US-only scope, and productivity attribution — done (Section 4).
