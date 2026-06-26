# M3 — Deaths-and-dollars cost-of-inaction model

**Problem:** Rheumatic heart disease — the penicillin gap
**Milestone:** M3 (per-country estimate of progression events / deaths avertable by closing the prophylaxis gap, and the BPG drug cost of doing so)
**Date:** 2026-06-26
**Author:** generator (autonomous loop)

## What this artifact is

A transparent, hand-auditable per-country model that multiplies three numbers a funder cares about:

1. **How many people need prophylaxis** (the eligible/at-risk denominator), drawn from the **M1 scorecard** (`artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`) — M1 is the burden source for every country row here.
2. **How well that effect works** — the **GOAL trial** efficacy input (Beaton et al., NEJM 2022), with the relative risk reduction derived explicitly below.
3. **What the drug costs** — BPG at a stated $/dose, ×13 doses/patient/year.

Every computed cell can be reproduced by a reader with a calculator from the figures stated in this artifact. The headline outputs are framed as **annual echocardiographic-progression events avertable** (the outcome GOAL actually measured), with **deaths** reported as a clearly-flagged secondary extrapolation.

> **Honesty flag, stated up front.** GOAL measured *echocardiographic progression of **latent** (screen-detected, asymptomatic) RHD in children aged 5–17 over 2 years* — **not** deaths, and **not** established/symptomatic RHD. This model extrapolates that effect to the broader GBD prevalent population (which includes established disease and all ages). That extrapolation is almost certainly **optimistic for established disease** and is the single biggest weakness of the model; it is listed in Assumptions (#1) and Limitations.

---

## Efficacy input — the GOAL trial, with the relative risk reduction DERIVED (not asserted)

**Trial:** Beaton A, Okello E, Rwebembera J, et al. *"Secondary Antibiotic Prophylaxis for Latent Rheumatic Heart Disease."* **New England Journal of Medicine 2022;386(3):230–240.** DOI 10.1056/NEJMoa2102074 ("GOAL" / *Gwoko Adunu pa Lutino*, "protect the heart of a child"). Randomized controlled trial, Northern Uganda, July 2018–Oct 2020; **818 children aged 5–17 with latent RHD**, randomized to **benzathine penicillin G (BPG) injection every 4 weeks for 2 years** vs no prophylaxis; outcome = echocardiographic progression at 2 years. ([NEJM abstract / Ovid](https://www.ovid.com/journals/nejm/abstract/10.1056/nejmoa2102074~secondary-antibiotic-prophylaxis-for-latent-rheumatic-heart); [Cincinnati Children's summary](https://scienceblog.cincinnatichildrens.org/in-uganda-rheumatic-heart-disease-research-reaches-its-goal/); [study protocol, Am Heart J 2019, PubMed 31301533](https://pubmed.ncbi.nlm.nih.gov/31301533/))

**Primary-outcome figures (as widely reported from the trial):**

| Arm | Progressed at 2 yr | n | Risk over 2 yr |
|-----|--------------------|---|----------------|
| **Penicillin (BPG q4wk)** | **3** | 399 | **0.8%** |
| **Control (no prophylaxis)** | **33** | 393 | **8.3%** |

Source for the 0.8% vs 8.3% split: trial as reported by [Cincinnati Children's / Research Horizons](https://scienceblog.cincinnatichildrens.org/in-uganda-rheumatic-heart-disease-research-reaches-its-goal/) and the [Physician's Weekly AHA report](https://www.physiciansweekly.com/aha-penicillin-prophylaxis-effective-in-preventing-progression-of-latent-rheumatic-heart-disease/), both citing Beaton et al., NEJM 2022.

**Derivation of the relative risk reduction (RRR) — shown, not asserted:**

- Risk ratio (penicillin ÷ control) = 0.8% ÷ 8.3% = **0.0096 ≈ 0.096** → i.e. ~one-tenth the risk.
- **RRR = 1 − risk ratio = 1 − (0.8 / 8.3) = 1 − 0.0964 = 0.9036 ≈ 90%.**
- Absolute risk reduction (ARR) over the 2-yr trial = 8.3% − 0.8% = **7.5 percentage points over 2 years** = **~3.75 percentage points per year** of progression averted in an *untreated, fully-adherent-if-treated* latent-RHD population.

**This model uses RRR ≈ 90% (base case)** applied to the *currently-unprotected* share of the eligible population. The ~tenfold figure (8.3/0.8 ≈ 10.4×) is the same result expressed as a ratio.

---

## Burden / eligible-population basis (from M1) and the gap math

**Eligible denominator.** M1's burden metric is **GBD prevalent RHD cases** (chronic valvular RHD, modeled). I treat the GBD prevalent count as the **eligible-for-prophylaxis population** for each country. Where M1 gives an absolute count, I use it directly. Where M1 gives only an age-standardized prevalence **rate** (no absolute count extracted), I derive cases = **rate/100k × population**, showing both inputs in the row (population from [Wikipedia "List of countries by population", 2024–2025 figures](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population)). Rate-derived rows are flagged **[rate×pop]**.

**Current coverage assumption.** M1's central finding is that the four largest-burden countries (India, China, Pakistan, Indonesia) have **no national register and no representative coverage figure**, and that even register settings report low adherence (Australia ~32%, Fiji ~7%, Ethiopia ~63% in one zone, Uganda ~58–91% depending on cascade stage). M1 also stresses that the GBD-prevalent population is **largely never enrolled**, so the fraction of *prevalent* patients actually protected is far below register-adherence numbers. I therefore set a **base-case current effective coverage of the prevalent population = 10%** for countries with no national register (a deliberately generous floor given M1's "the map is blank / most prevalent patients are never enrolled" reading), and use M1's stated register figures where they exist (Australia 32%, Fiji 7%, Uganda 58%, Ethiopia 63%). **The 10% default is an assumption, not a measurement** (Assumption #3); the sensitivity section varies it.

**Unprotected fraction** = 1 − current coverage. **Closing the gap** = bringing the unprotected fraction onto prophylaxis.

---

## Formula (the same four lines produce every computed cell)

Let **P** = eligible prevalent cases (col 2); **c** = current coverage fraction (col 3); **RRR** = 0.90 (col 4); **d** = 13 doses/patient/yr; **$/dose** = $0.11.

1. **Unprotected eligible** = P × (1 − c)
2. **Annual progression events avertable** = P × (1 − c) × **r** × RRR
   — where **r** = annual baseline progression risk in the unprotected = **3.75% (0.0375)**, taken as the GOAL control-arm progression rate per year (8.3% over 2 yr ÷ 2). *This applies the GOAL latent-disease annual progression rate to the whole prevalent pool — see Assumption #1.*
3. **Annual BPG doses needed** = P × (1 − c) × d  (= unprotected eligible × 13)
4. **Annual BPG drug cost** = doses × $0.11

**Secondary deaths extrapolation (flagged):** annual deaths avertable ≈ progression events avertable × **0.10**, i.e. assuming ~10% of progression events would, over time, translate into an RHD death averted. **This 10% case-fatality-of-progression factor is an illustrative assumption with no direct trial support** (Assumption #6); deaths are reported in a separate, clearly-labeled column and are **not** the headline.

---

## Per-country model (rows drawn from M1; ≥15 countries)

$/dose = **$0.11** per 1.2 MU dose ([CHAI/WHO-HRP estimate, quoted in Bowen/Carapetis editorial, PMC8802371](https://pmc.ncbi.nlm.nih.gov/articles/PMC8802371/)). Doses/patient/yr = **13** (every-4-weeks). RRR = **0.90**. Baseline annual progression risk in unprotected r = **3.75%**.

| Country | Eligible P (prevalent cases) & basis [M1] | Current coverage c (source) | RRR | Annual progression events avertable = P·(1−c)·0.0375·0.90 | Annual BPG doses needed = P·(1−c)·13 | Annual BPG cost = doses·$0.11 |
|---|---|---|---|---|---|---|
| **India** | 10,500,000 (M1 GBD 2021 abs. count) | 10% (no register; M1) | 0.90 | 9,450,000·0.0375·0.90 = **318,938** | 9,450,000·13 = **122.85M** | **$13.51M** |
| **China** | 5,461,000 [rate×pop]: 390.2/100k × 1,399.7M (M1 GBD2019 rate) | 10% | 0.90 | 4,914,900·0.0375·0.90 = **165,878** | 63.89M | **$7.03M** |
| **Pakistan** | 2,340,000 (M1 GBD 2021 abs. count) | 10% | 0.90 | 2,106,000·0.0375·0.90 = **71,078** | 27.38M | **$3.01M** |
| **Indonesia** | 1,990,000 [rate×pop]: assume 690/100k (~India-like, M1 "top-5") × 288.3M | 10% | 0.90 | 1,791,000·0.0375·0.90 = **60,446** | 23.28M | **$2.56M** |
| **Bangladesh** | 1,300,000 (M1 GBD 2021 abs. count) | 10% | 0.90 | 1,170,000·0.0375·0.90 = **39,488** | 15.21M | **$1.67M** |
| **DR Congo** | 1,712,000 [rate×pop]: 1,517/100k × 112.8M (M1 GBD 2021 rate) | 10% | 0.90 | 1,540,800·0.0375·0.90 = **52,002** | 20.03M | **$2.20M** |
| **Nigeria** | 1,544,000 [rate×pop]: 690/100k (assumed India-like) × 223.8M | 10% | 0.90 | 1,389,600·0.0375·0.90 = **46,899** | 18.06M | **$1.99M** |
| **Ethiopia** | 770,000 [rate×pop]: 690/100k × 111.7M | 63% (Jimma zone, M1) | 0.90 | 284,900·0.0375·0.90 = **9,615** | 3.70M | **$0.41M** |
| **Tanzania** | 470,000 [rate×pop]: 690/100k × 68.2M | 10% | 0.90 | 423,000·0.0375·0.90 = **14,276** | 5.50M | **$0.60M** |
| **Nepal** | 222,700 (M1 GBD 2021 abs. count) | 10% | 0.90 | 200,430·0.0375·0.90 = **6,765** | 2.61M | **$0.29M** |
| **Mozambique** | 235,000 [rate×pop]: 690/100k × 34.1M | 10% | 0.90 | 211,500·0.0375·0.90 = **7,138** | 2.75M | **$0.30M** |
| **Brazil** | 1,472,000 [rate×pop]: 690/100k × 213.4M | 10% | 0.90 | 1,324,800·0.0375·0.90 = **44,712** | 17.22M | **$1.89M** |
| **South Africa** | 435,000 [rate×pop]: 690/100k × 63.1M | 10% | 0.90 | 391,500·0.0375·0.90 = **13,213** | 5.09M | **$0.56M** |
| **Uganda** | 316,000 [rate×pop]: 690/100k × 45.9M | 58% (Mulago cohort, M1) | 0.90 | 132,720·0.0375·0.90 = **4,479** | 1.72M | **$0.19M** |
| **Australia (First Nations)** | 5,282 (M1: AIHW register-eligible, 2024) | 32% (AIHW 2024, M1) | 0.90 | 3,592·0.0375·0.90 = **121** | 46,696 | **$0.005M** |
| **Fiji** | 6,230 [rate×pop]: 690/100k × 0.90M | 7% (Engelman 2016, M1) | 0.90 | 5,794·0.0375·0.90 = **196** | 75,322 | **$0.008M** |
| **Eritrea** | 49,400 [rate×pop]: 1,370/100k × 3.6M (M1 GBD2019 rate) | 10% | 0.90 | 44,460·0.0375·0.90 = **1,500** | 0.58M | **$0.064M** |
| **Central African Rep.** | 11,300 [rate×pop]: 174.6/100k × 6.47M (M1 GBD 2021 rate) | 10% | 0.90 | 10,170·0.0375·0.90 = **343** | 0.13M | **$0.015M** |

**Row count: 18 countries** (≥15 required), all drawn from M1's country set. (M1 row 20 "Solomon Islands / PNG" is omitted from the cost table because M1 gives only death rates, not a prevalence count or rate; mortality rates cannot drive this prevalence-based model without an extra assumption.)

### Column totals (18 countries above)

- **Annual progression events avertable (base case): ≈ 866,500** (sum of the events column).
- **Annual BPG doses needed: ≈ 358.7 million.** (Cross-check: M1/M2's CHAI estimate of ~200M doses/yr needed for *all* RHD globally — this model's 359M is higher because it applies 13 doses to the unprotected GBD-prevalent pool across 18 countries with a generous denominator; see Assumption #2 and Limitations. The order of magnitude is consistent.)
- **Annual BPG drug cost (base case): ≈ $39.5 million** (sum of cost column; equivalently 358.7M × $0.11 = $39.5M).
- **Secondary deaths extrapolation:** 866,500 × 0.10 ≈ **86,650 deaths/yr avertable** — *flagged, illustrative only* (Assumption #6). For sanity vs M1: GBD 2021 puts global RHD deaths at 373,345; an ~87k figure across these 18 countries is ~23% of global deaths, plausible as an upper-bound order of magnitude but unverified.

---

## Sensitivity (low / base / high) on the two headline numbers

I vary the two most uncertain inputs: **effective coverage of the prevalent pool** (which sets the unprotected denominator) and **applied efficacy / baseline progression rate**.

**Headline 1 — annual progression events avertable:**

| Scenario | Key change | Events avertable |
|---|---|---|
| **Low** | Higher existing coverage (assume 30% baseline coverage everywhere → smaller unprotected pool) **and** RRR 0.80 (lower bound, accounting for imperfect real-world adherence vs trial) | ≈ **866,500 × (0.70/0.90 denominator shrink) × (0.80/0.90 efficacy)** ≈ 866,500 × 0.778 × 0.889 ≈ **599,000** |
| **Base** | 10% coverage default, RRR 0.90, r = 3.75%/yr | **≈ 866,500** |
| **High** | Lower existing coverage (assume 5% baseline → larger unprotected pool) **and** full GOAL annual ARR applied (r = 3.75%, RRR 0.90 unchanged) | ≈ 866,500 × (0.95/0.90) ≈ **915,000** |

→ **Progression events avertable: ~0.60M (low) – 0.87M (base) – 0.92M (high) per year.**

**Headline 2 — total annual BPG drug cost (drug only, all 18 countries):**

| Scenario | Key change | Total drug cost |
|---|---|---|
| **Low** | 30% baseline coverage (smaller unprotected pool → fewer doses) at $0.11/dose | 358.7M doses × (0.70/0.90) × $0.11 ≈ **$30.7M** |
| **Base** | 10% coverage default, $0.11/dose, 13 doses/pt/yr | **≈ $39.5M** |
| **High** | 5% baseline coverage **and** higher $/dose = **$0.30** (quality-assured / shortage-era price, within the $0.30–$0.50 range commonly cited for QA product) | 358.7M × (0.95/0.90) × $0.30 ≈ **$113.6M** |

→ **Total annual BPG drug cost: ~$31M (low) – $40M (base) – $114M (high).** Even the high case is a **drug-only** figure on the order of $0.1 billion/year to supply the unprotected RHD-prevalent population across the 18 highest-burden countries — trivially small against the deaths/progression at stake, which is the cost-of-inaction headline.

---

## Reproducibility worked example (India, so a reader can check the engine)

P = 10,500,000 (M1). c = 0.10 → unprotected = 10.5M × 0.90 = **9,450,000**.
Events = 9,450,000 × 0.0375 × 0.90 = 9,450,000 × 0.03375 = **318,938**.
Doses = 9,450,000 × 13 = **122,850,000**.
Cost = 122,850,000 × $0.11 = **$13,513,500 ≈ $13.51M**. ✓ Matches the India row.

---

## Assumptions box (every simplifying assumption; ≥4 required, 7 listed)

1. **Latent→all-RHD efficacy transfer (biggest weakness).** GOAL measured progression of *screen-detected latent RHD in children aged 5–17*. This model applies the same 90% RRR and 3.75%/yr baseline progression to the *entire GBD prevalent pool*, which includes established/symptomatic RHD and all ages. Secondary prophylaxis is biologically plausible across this group (it prevents recurrent ARF), but the *quantitative* GOAL effect is **not validated** for established disease and is likely **over-applied**. Treat per-country event counts as an upper-bound order of magnitude.
2. **GBD prevalent count = eligible-for-prophylaxis denominator.** Not everyone with chronic RHD is a prophylaxis candidate (some have no recurrent-ARF risk; some are too advanced). Using the full prevalent count inflates both events and doses. This is why the dose total (359M) exceeds CHAI's ~200M global RHD need (M2).
3. **Current coverage = 10% default where no register exists.** This is a stipulated floor reflecting M1's "most prevalent patients are never enrolled," **not** a measured value. Varying it is the main sensitivity lever.
4. **Full adherence once treated.** The 90% RRR is the GOAL *per-protocol-ish* trial effect under monitored q4wk dosing. Real-world adherence is far lower (M1: Australia 32%, Fiji 7%), so realized benefit per patient enrolled would be smaller. The "low" sensitivity scenario (RRR 0.80) partially captures this.
5. **Static population and static burden.** Single-year snapshot; no incidence growth, demographic change, or treatment-cascade dynamics. M1 notes GBD counts are themselves modeled with wide uncertainty (e.g. India 8.2M–13.2M).
6. **Deaths = progression events × 0.10.** The 10% case-fatality-of-progression factor is **illustrative with no direct trial basis**; deaths are reported only as a flagged secondary number, never the headline.
7. **Uniform $/dose ($0.11) and uniform 13 doses/patient/year.** Real prices vary by market and quality tier ($0.11 LMIC generic → $0.30–$0.50 QA product; the high sensitivity case uses $0.30). 13 doses assumes a 4-weekly schedule with no missed/relocated doses, wastage, or the newer 10-weekly SCIP regimens (M1). Drug cost **excludes** delivery, cold chain, staff, syringes, and program overhead — which dominate real program cost.

---

## Limitations & counter-evidence

1. **The model's central number is an extrapolation, by construction.** Applying GOAL's latent-pediatric effect size to a multi-hundred-million all-ages prevalent pool (Assumptions #1–2) means the ~866,500 events and ~87,000 deaths figures should be read as *what the trial effect would imply if it held across the whole pool*, not as a validated forecast. The honest defensible claim is narrower: **for screen-detected latent RHD, GOAL shows ~90% RRR, and the drug to act is extraordinarily cheap (~$0.11/dose) relative to the burden** — the country-level totals dramatize that, they don't measure it.

2. **Rate×population rows carry compounding error.** Half the rows ([rate×pop]) multiply a GBD age-standardized rate by a population, and for Indonesia/Nigeria/Tanzania/Mozambique/Brazil/South Africa I had to *assume* an India-like 690/100k prevalence because M1 did not extract a country rate. Those rows are the weakest; their event/cost figures could be off by 2× in either direction.

3. **Coverage denominator mismatch (carried from M1).** M1 warns explicitly that register-adherence % (Australia 32%, Fiji 7%, Uganda 58%) is *not* "% of GBD-prevalent population protected." I used those register figures as the coverage **c** for those rows anyway, which slightly *under*-states their unprotected pool (true prevalent-population coverage is lower). This makes those specific rows conservative on events but the direction differs from the 10%-default rows — they are not strictly comparable.

4. **Drug cost is the smallest part of program cost.** The $40M base case is *drug only*. Real secondary-prophylaxis programs are dominated by delivery: monthly clinic visits, cold chain, trained injectors, pain-management, register infrastructure, and active recall. A "true cost of closing the gap" is plausibly 1–2 orders of magnitude larger than the drug line — but the drug being this cheap is itself the policy point (M2: the molecule is low-margin, which is *why* it keeps disappearing).

5. **Counter-evidence on whether the drug is even the binding lever.** M1 and M2 both stress that in several settings the constraint is **enrollment/retention or supply security, not drug affordability** (Uganda ~91% adherence among *retained* patients despite documented stockouts; the 3-API-maker chokepoint in M2). A model that prices the drug at $40M can mislead if read as "spend $40M and the deaths stop" — the binding constraint is frequently the cascade and the supply chain, not the price of penicillin.

6. **Single-vintage efficacy from one trial in one country.** GOAL is a single RCT in Northern Uganda; its 0.8%/8.3% split rests on small event counts (3 and 33 events). The confidence interval on the RRR is wide, and generalizability to e.g. South Asian adults is untested. A follow-on non-inferiority/stopping trial (GOAL-Stop, NCT07146048) and an IM-vs-oral trial (GOALIE, NCT05693545) are ongoing, indicating the evidence base is still maturing.

---

## Source list (named, dated)

- **Burden / eligible population (all country rows):** M1 scorecard — `artifacts/2026-06-25-m1-coverage-stockout-scorecard.md` (GBD 2021/2019/2015 counts and rates; coverage figures for Australia, Fiji, Uganda, Ethiopia).
- **Efficacy input (GOAL trial):** Beaton A, et al. "Secondary Antibiotic Prophylaxis for Latent Rheumatic Heart Disease." *NEJM* 2022;386(3):230–240, DOI 10.1056/NEJMoa2102074. Primary-outcome split (3/399 = 0.8% vs 33/393 = 8.3%) as reported by [Cincinnati Children's / Research Horizons](https://scienceblog.cincinnatichildrens.org/in-uganda-rheumatic-heart-disease-research-reaches-its-goal/) and [Physician's Weekly (AHA)](https://www.physiciansweekly.com/aha-penicillin-prophylaxis-effective-in-preventing-progression-of-latent-rheumatic-heart-disease/); trial design via [NEJM/Ovid abstract](https://www.ovid.com/journals/nejm/abstract/10.1056/nejmoa2102074~secondary-antibiotic-prophylaxis-for-latent-rheumatic-heart) and [protocol, Am Heart J 2019, PubMed 31301533](https://pubmed.ncbi.nlm.nih.gov/31301533/).
- **BPG $/dose:** US$0.11 per 1.2 MU dose in LMICs (CHAI/WHO-HRP estimate), quoted in [Bowen & Carapetis editorial, "The challenges of improving benzathine penicillin usage…", PMC8802371](https://pmc.ncbi.nlm.nih.gov/articles/PMC8802371/). High-case $0.30 reflects the QA-product price band noted in M2/CHAI sources.
- **Dose-need cross-check (~200M doses/yr for RHD):** M2 supply-chain map — `artifacts/2026-06-26-m2-bpg-supply-chain-map.md`, citing [CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/).
- **Populations (rate×pop rows):** [Wikipedia, List of countries and dependencies by population, 2024–2025 figures](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population).
- **Ongoing follow-on trials:** [GOAL-Stop, NCT07146048](https://clinicaltrials.gov/study/NCT07146048); [GOALIE, NCT05693545](https://clinicaltrials.gov/study/NCT05693545).
