# M2 — Benefit-harm dossier: inverting the atypical-femoral-fracture scare

**Problem:** the post-fracture osteoporosis treatment gap
**Milestone:** M2 | **Date:** 2026-06-12 | **Status:** draft for evaluation
**Inputs used:** M1 league table (`artifacts/2026-06-12-m1-treatment-rate-league-table.md`), for the prescribing-collapse and decline figures.

## How to read this dossier

The central clinical fact this package establishes: **for the patient population that matters here — older adults who have already had a fragility fracture — the fractures bisphosphonates prevent outnumber the atypical femoral fractures (AFFs) they cause by roughly two orders of magnitude.** The AFF scare that drove the post-2008 US prescribing collapse (documented in M1) inverted a benefit-harm ratio that the best data show running ~75:1 to 270:1 in favor of treatment in White women, and still strongly favorable (~11:1 to ~40:1) in the highest-risk subgroup (Asian women at the longest durations). This dossier reproduces that arithmetic from the primary source, gives NNT/NNH figures, dates the prescribing collapse, rebuts the named safety concerns, and concedes the genuine residual risks.

All AFF/hip-fracture-prevented figures are **per 10,000 women treated** unless stated. Every quantitative claim is sourced inline.

---

## 1. Headline arithmetic — the Black et al. NEJM 2020 ratio

**Source:** Black DM, Geiger EJ, Eastell R, et al. "Atypical Femur Fracture Risk versus Fragility Fracture Prevention with Bisphosphonates." *N Engl J Med* 2020;383:743-753. [NEJM](https://www.nejm.org/doi/full/10.1056/NEJMoa1916525) · [PMC9632334 full text](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/). Cohort: 196,129 women in Kaiser Permanente Southern California; 277 AFFs observed (1.74 per 10,000 patient-years overall).

The paper models, **per 10,000 women treated**, the number of hip fractures and total clinical fractures *prevented* against the number of AFFs *caused*, stratified by race and by treatment duration. The defensible figures (from Table 3 / Figure 3 of the paper, as extracted from the PMC full text):

| Population | Duration | Hip fx prevented | Total clinical fx prevented | AFFs caused | Hip-only ratio | All-clinical ratio |
|---|---|---|---|---|---|---|
| **White women** | 3 years | 149 | 541 | 2 | **~75 : 1** | **~270 : 1** |
| **White women** | 5 years | 286 | 859 | 8 | **~36 : 1** | **~107 : 1** |
| **Asian women** | 3 years | 91 | 330 | 8 | **~11 : 1** | **~41 : 1** |
| **Asian women** | 5 years | 174 | 524 | 38 | **~4.6 : 1** | **~14 : 1** |

### The calculation shown (not just the headline)

The ratio is simply *(fractures prevented) ÷ (AFFs caused)*, both expressed per 10,000 women over the same horizon:

- **White women, 3 years, hip-only:** 149 hip fractures prevented ÷ 2 AFFs caused = **74.5 ≈ 75 prevented hip fractures per AFF.**
- **White women, 3 years, all clinical fractures:** 541 ÷ 2 = **270.5 ≈ 271 prevented clinical fractures per AFF.**
- **White women, 5 years, hip-only:** 286 ÷ 8 = **35.75 ≈ 36 hip fractures per AFF.** The ratio *worsens* with duration because AFF count rises faster (2→8) than hip-fractures-prevented (149→286) — this is the kernel of truth inside the scare, and the basis for drug holidays (Section 4).
- **Asian women, 5 years, hip-only:** 174 ÷ 38 = **4.6 hip fractures per AFF** — the least favorable cell in the entire analysis, and still net-positive once all clinical fractures (524 ÷ 38 = 13.8) are counted.

The authors' own conclusion: decreases in osteoporotic and hip-fracture risk during 1–10 years of bisphosphonate use "far outweighed the increased risk of atypical fracture among Whites but less so among Asians" ([Black 2020, NEJM abstract](https://pubmed.ncbi.nlm.nih.gov/32813950/)).

**Why this is the right anchor for the treatment-gap argument:** the patients in the M1 league table — post-hip-fracture, post-fragility-fracture older adults — are *secondary-prevention* patients at far higher baseline fracture risk than the average woman in this prevalent-user cohort. Higher baseline risk means more fractures prevented per 10,000 treated, which pushes the benefit-harm ratio further in favor of treatment than the figures above (which include lower-risk prevalent users).

---

## 2. NNT / NNH table

NNT = number needed to treat to prevent one fracture; NNH = number needed to (harm) treat to cause one adverse event. Lower NNT and higher NNH both favor treatment.

| Metric | Figure | Population / duration | Source |
|---|---|---|---|
| **NNT — hip fracture** | **100** | Postmenopausal women, *secondary* prevention (existing osteoporosis/prior fracture), alendronate, ~1–4 yr | [AAFP review of alendronate, AFP 2008](https://www.aafp.org/pubs/afp/issues/2008/0901/p579.html) |
| **NNT — vertebral fracture** | **16** | Same secondary-prevention population, alendronate | [AAFP, AFP 2008](https://www.aafp.org/pubs/afp/issues/2008/0901/p579.html) |
| NNT — hip (cross-drug, 3 yr) | 48 (strontium) – 91 (bisphosphonates) | Network meta-analysis, 3-yr horizon | [Freemantle et al., Rheumatol Int 2010](https://link.springer.com/article/10.1007/s00296-009-1311-y) ([PubMed](https://pubmed.ncbi.nlm.nih.gov/20035331/)) |
| NNT — vertebral (cross-drug, 3 yr) | 9 (strontium) – 21 (ibandronate) | Same | [Freemantle et al., 2010](https://pubmed.ncbi.nlm.nih.gov/20035331/) |
| **NNH — atypical femoral fracture** | **~5,750** (≈1.74 AFFs per 10,000 pt-yr) overall; duration-dependent (see below) | KPSC prevalent users, all durations | [Black 2020, PMC9632334](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/) |
| NNH — AFF, 3–5 yr use | ~3,940 (2.54 per 10,000 pt-yr) | KPSC, 3–5 yr exposure | [Black 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/) |
| NNH — AFF, 8+ yr use | ~760 (13.10 per 10,000 pt-yr) | KPSC, ≥8 yr exposure | [Black 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/) |
| **NNH — osteonecrosis of the jaw (ONJ)** | **~10,000 to ~100,000+** (1 case per 10,000 to <1 per 100,000 patient-treatment-years); prevalence 0.07–0.10% | Oral bisphosphonate osteoporosis dosing | [AAFP, AFP 2012](https://www.aafp.org/pubs/afp/issues/2012/0615/p1134.html); [Khan et al. / BJMP review](https://www.bjmp.org/content/oral-bisphosphonates-and-risk-osteonecrosis-jaw) |

**Reading the table:** treating ~100 high-risk women for a few years prevents a hip fracture; you must treat somewhere between ~760 (8+ years) and ~5,750 (average) women for a *year* to cause one AFF, and ~10,000–100,000 to cause one ONJ. The harm denominators are 1–3 orders of magnitude larger than the benefit denominator. AFF NNH is computed as 10,000 ÷ (rate per 10,000 patient-years): e.g., 10,000 ÷ 1.74 = 5,747.

---

## 3. Timeline of the prescribing collapse

Six dated, cited data points. The first three are the prescribing/use decline; the next three are the post-fracture-treatment-rate decline carried forward from M1 (with the corrected, defensible figures flagged in the M1 brief).

| Year(s) | Event / data point | Figure | Source |
|---|---|---|---|
| ~1995–2006 | Oral bisphosphonate use rises for over a decade after alendronate launch | (rising) | [Jha et al., JBMR 2015](https://pubmed.ncbi.nlm.nih.gov/26018247/) |
| 2006 | Use **plateaus** as media safety reports (AFF, ONJ) emerge; FDA/ASBMR did *not* recommend use restrictions | peak | [Jha et al., JBMR 2015](https://pubmed.ncbi.nlm.nih.gov/26018247/) |
| **2008 → 2012** | Oral bisphosphonate use **declines >50%** in the US | **>50% drop** | [Jha et al., JBMR 2015 (PubMed)](https://pubmed.ncbi.nlm.nih.gov/26018247/); [Wiley full text](https://onlinelibrary.wiley.com/doi/pdf/10.1002/jbmr.2565) |
| 2002 → 2011 | Post-hip-fracture treatment within 12 mo (commercial + Medicare-suppl. claims): **40.2% → 20.5%** | halved | [Solomon et al., JBMR 2014 (PMC4258070)](https://pmc.ncbi.nlm.nih.gov/articles/PMC4258070/) (M1 row 10) |
| **2004 → 2015** | Post-hip-fracture initiation within 180 days (Truven MarketScan): **9.8% → 3.3%** | two-thirds drop | [Desai et al., JAMA Netw Open 2018 (PMC6324295)](https://pmc.ncbi.nlm.nih.gov/articles/PMC6324295/) (M1 row 19) |
| 2011 → 2012 | Subtrochanteric/diaphyseal (AFF-type) fracture incidence peaks at 30.5/100,000 then falls to 26.7/100,000 — but **intertrochanteric (typical) hip fractures continued to decline through 2006 and again 2008–2012**, i.e., the scare cut typical-fracture prevention without a commensurate AFF benefit | 30.5 → 26.7 /100k | [Jha et al., JBMR 2015](https://pubmed.ncbi.nlm.nih.gov/26018247/) |

**Note on the "15% → 3%" soundbite (per M1 finding):** the widely repeated advocacy figure "post-hip-fracture treatment fell from ~15% to ~3% (2004→2013)" does *not* match the underlying peer-reviewed series. The defensible figures are Desai's **9.8% (2004) → 3.3% (2015)** at 180 days and Solomon's **40.2% (2002) → 20.5% (2011)** at 12 months. This dossier uses those. The direction and magnitude of the collapse are robust; the exact "15%" starting point is not.

**Ecological caution (Jha's own framing):** Jha et al. is an *ecological* analysis. It establishes temporal coincidence of safety-media → use decline → plateau/uptick in some fracture trends, not causation. It is strong enough to date the collapse and tie it to the safety scare, not strong enough to claim the scare *caused* a measured rise in typical hip fractures.

---

## 4. Counterarguments and rebuttals

### 4.1 "Bisphosphonates cause atypical femoral fractures"
**True, but quantified and dwarfed by benefit.** AFFs are real and dose/duration-dependent. Risk vs. <3 months of use: HR **8.86** (95% CI 2.79–28.20) at 3–5 years, **19.88** (6.32–62.49) at 5–8 years, **43.51** (13.70–138.15) at ≥8 years ([Black 2020, PMC9632334](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/)). But absolute rates stay low (1.74 per 10,000 patient-years overall; 13.10 even at 8+ years), and the fractures-prevented-to-AFF ratio remains 36:1 to 271:1 in White women and net-positive even in Asian women at 5 years (Section 1). The rational response to the duration effect is a **drug holiday**, not non-treatment — and crucially, AFF risk *reverses* fast on stopping: HR **0.52** (0.37–0.72) within 3–15 months of discontinuation, and a ~74–79% reduction beyond 15 months ([Black 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/)). Hip-fracture protection persists longer than AFF risk after stopping, which is exactly why the drug-holiday strategy works.

### 4.2 "Bisphosphonates cause osteonecrosis of the jaw"
**Rare at osteoporosis doses; concentrated in cancer/IV dosing.** For oral bisphosphonates at osteoporosis doses, ONJ incidence is on the order of **1 per 10,000 to <1 per 100,000 patient-treatment-years**, prevalence 0.07–0.10% ([AAFP, AFP 2012](https://www.aafp.org/pubs/afp/issues/2012/0615/p1134.html); [BJMP review](https://www.bjmp.org/content/oral-bisphosphonates-and-risk-osteonecrosis-jaw)). The high ONJ rates that drive public fear come from **high-dose IV bisphosphonates in oncology**, not osteoporosis therapy. Modifiable: risk concentrates around invasive dental procedures, so completing dental work before/around initiation mitigates most of it. NNH (Section 2) is 1–2 orders of magnitude larger than the hip-fracture NNT.

### 4.3 "Long-duration use is dangerous — patients shouldn't stay on these drugs"
**Correct in part, and already solved by guideline drug holidays — which argue for *starting*, not avoiding, treatment.** The AFF duration gradient (Section 4.1) is real. The guideline answer is to treat for ~3–5 years, reassess, and consider a holiday in lower-risk patients while continuing high-risk patients ([Adler et al., ASBMR Task Force, JBMR 2016](https://pubmed.ncbi.nlm.nih.gov/26350171/)). The duration concern is an argument about *when to pause*, not a reason to leave a post-fracture patient untreated — yet M1 shows the scare produced the latter, the opposite of the evidence-based response. A patient who never starts gets none of the front-loaded benefit and faces the full untreated refracture risk.

### 4.4 (Bonus) "The fractures they prevent are mostly vertebral/asymptomatic anyway"
**No — hip-fracture prevention is real and the highest-stakes endpoint.** NNT for hip fracture is ~100 in secondary prevention (Section 2), and post-hip-fracture mortality runs ~20–30% at one year (to be quantified in M3). The Black analysis counts *hip* fractures prevented (149–286 per 10,000) specifically, not just vertebral.

---

## 5. Limitations and honest residual risks

This is a benefit-harm case, not a sales sheet. Genuine caveats:

1. **AFF risk genuinely rises steeply with duration.** The HR reaches 43.5 at ≥8 years ([Black 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/)). The favorable headline ratio (75:1) is a 3-year, White-women figure; it degrades to ~4.6:1 (hip-only) for Asian women at 5 years. The case for *time-limited* treatment with reassessment is strong; the case for indefinite treatment without holiday is not.

2. **The data are overwhelmingly from women.** Black 2020 is women-only; the AAFP NNT figures are postmenopausal women; M1 shows men are treated at roughly half the rate and are far less studied. The benefit-harm ratio in men is plausibly similar but is *not* directly established by these sources. [speculative] Extending these ratios to men assumes comparable baseline fracture risk and AFF susceptibility.

3. **Race/ethnicity modifies the ratio substantially.** Asian women carry markedly higher AFF risk (38 vs 8 AFFs at 5 years per 10,000) ([Black 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC9632334/)). Black women had too few AFFs to estimate a ratio at all. A blanket "270:1" claim is White-women-specific; honest advocacy must present the range.

4. **Jha 2015 is ecological and ends in 2012.** It cannot prove the safety scare *caused* excess typical fractures, and it does not capture the 2013–2025 period. The prescribing-collapse claim past 2012 rests on the separate claims series (Desai to 2015, Solomon to 2011), which themselves end before 2016.

5. **NNT figures are duration-heterogeneous.** The AAFP secondary-prevention NNTs (hip 100, vertebral 16) span 1–4 year follow-ups, not a single standardized horizon ([AAFP 2008](https://www.aafp.org/pubs/afp/issues/2008/0901/p579.html)); the network-meta-analysis NNTs are 3-year ([Freemantle 2010](https://pubmed.ncbi.nlm.nih.gov/20035331/)). They are not perfectly comparable to the Black per-10,000 model, which is a prevalent-user simulation, not a trial-based NNT.

6. **ONJ incidence estimates span an order of magnitude** (1 per 10,000 to <1 per 100,000) across studies with different ascertainment ([BJMP review](https://www.bjmp.org/content/oral-bisphosphonates-and-risk-osteonecrosis-jaw)); one long-term alendronate cohort reported 262 per 100,000 person-years, far above the modal estimate. The NNH is real but imprecise.

7. **Counter-evidence acknowledged:** the AFF scare was not pure irrationality — AFFs are a genuine iatrogenic harm, were under-recognized before ~2008, and the duration gradient validates *some* of the caution. The error was the policy response (stop treating fracture patients) being the opposite of the evidence-based one (treat time-limited, take holidays). This dossier inverts the *scare*, not the underlying safety signal.

---

## Forward pointer to M3 (not a finding)

M3's cost model should use: NNT-hip ≈ 100 (secondary prevention) or, better, a relative refracture-risk reduction derived from trial data; post-hip-fracture one-year mortality (~20–30%, to be sourced); and the M1 baseline (21.1% Traditional Medicare) vs. target (35.4% UK FLS to 68–80% flagship) treatment-rate band. The benefit-harm ratios here justify the model's assumption that closing the gap is net-beneficial at the population level.
