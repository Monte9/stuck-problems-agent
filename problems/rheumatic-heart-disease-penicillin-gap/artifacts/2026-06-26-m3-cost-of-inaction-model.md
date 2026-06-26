# M3 — Deaths-and-dollars cost-of-inaction model

**Problem:** Rheumatic heart disease — the penicillin gap
**Milestone:** M3 (per-country deaths/progression avertable + drug cost of closing the prophylaxis gap)
**Date:** 2026-06-26
**Author:** generator (autonomous loop)

## What this artifact is

A transparent, fully reproducible per-country estimate of (a) how many RHD deaths/progression events are avertable per year if the secondary-prophylaxis gap were closed, and (b) what the benzathine penicillin G (BPG) drug bill of doing so would be. Two inputs feed it:

- **Burden input:** the M1 scorecard (`artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`). Every prevalence and death figure below is lifted from M1's cells, which in turn cite GBD 2021 / GBD 2015 (see M1 for the per-cell vintage). **M1 is the named burden source for this milestone.**
- **Efficacy input:** the GOAL trial effect size (NEJM 2021), derived explicitly below.

This is a back-of-envelope decision model, not an epidemiological microsimulation. Its purpose is to give a funder/ministry an order-of-magnitude "deaths-per-dollar" frame, with every cell traceable to a stated number and formula. Read the assumptions box and limitations before quoting any figure — the central extrapolation (GOAL's *latent-disease progression* effect onto *established-RHD mortality*) is an assumption, not a measured fact, and is flagged throughout.

---

## The efficacy input: deriving the GOAL relative risk reduction

The 2021 NEJM **GOAL trial** (Gulu, Uganda; Beaton et al., "Secondary Antibiotic Prophylaxis for Latent Rheumatic Heart Disease," *NEJM* 2021;385(24):2211–2221, [NEJM/NCT03346525](https://www.nejm.org/doi/full/10.1056/NEJMoa2102074)) randomized children/adolescents with **latent (echo-screen-detected, subclinical) RHD** to intramuscular BPG every 4 weeks vs no prophylaxis, over **2 years**.

Quoted result (modified intention-to-treat, 818 children with paired echocardiograms; ~409 per arm):

> "Just three participants (0.8%) who received penicillin experienced latent rheumatic heart disease progression after two years, compared to 33 (8.3%) who didn't receive the treatment" — a **tenfold** difference. ([Cincinnati Children's Science Blog summary of GOAL](https://scienceblog.cincinnatichildrens.org/in-uganda-rheumatic-heart-disease-research-reaches-its-goal/); primary publication [NEJM 2021](https://www.nejm.org/doi/full/10.1056/NEJMoa2102074))

**Relative risk reduction (RRR), derived explicitly — not asserted:**

```
Progression, penicillin arm  = 0.8%  = 0.008
Progression, control arm     = 8.3%  = 0.083

Relative risk (RR) = 0.008 / 0.083 = 0.0964   (penicillin patients had ~9.6% of control's risk)
RRR = (control − penicillin) / control
    = (0.083 − 0.008) / 0.083
    = 0.075 / 0.083
    = 0.9036  ≈ 90.4%

Fold reduction = 0.083 / 0.008 = 10.4  ("~tenfold", consistent with the quote)
```

So the **GOAL-derived RRR is ≈ 90% (0.904)**. This is the efficacy figure applied in the model's base case. The "~tenfold" language in the problem brief corresponds to the RR of 0.096; the 90.4% RRR is its complement. Both come from the same two percentages above.

**Critical honesty flag (carried into the assumptions box and limitations):** GOAL measured **echocardiographic progression of *latent* (subclinical) disease over 2 years**, *not* mortality, and *not* in patients with established symptomatic RHD. Applying a 90% RRR to *established-RHD annual deaths* is an **extrapolation across both the outcome (progression → death) and the population (latent → established)**. There is no trial that measured BPG's effect on established-RHD mortality. This model therefore presents a *biologically-motivated upper-plausible* benefit, and the sensitivity section halves the efficacy to show how soft the headline is.

## The cost input: $/dose

- **Base $/dose = US$0.30** per 1.2-million-unit (1.2 MU) dose — a deliberately conservative midpoint above the lowest LMIC procurement price.
- **Low $/dose = US$0.11** — CHAI's reported LMIC average procurement price for a 1.2 MU BPG dose ([CHAI, as reported via WHO/PAHO 2017 shortage briefing](https://www.paho.org/en/news/27-12-2017-shortages-benzathine-penicillin-how-big-problem-and-why-it-matters); the problem brief frames the dose as costing "on the order of cents").
- **High $/dose = US$1.00** — the upper bound of CHAI's stated LMIC range: "Prices for BPG in these markets are low, typically **less than US$1 per dose**" ([CHAI/Oxford, *International Health* 2024;16(3):279, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). (Note: US Bicillin L-A list prices are an order of magnitude higher — tens of dollars/dose per [GoodRx](https://www.goodrx.com/bicillin-l-a) — but the burden, and thus the model, is overwhelmingly LMIC, where the cents-to-$1 range governs. This is itself the M2 "too cheap to make" story.)

## Dosing & population basis

- **Doses per patient-year = 13** — secondary prophylaxis is one IM BPG injection every 3–4 weeks; the standard adequacy schedule is 13 doses on a 4-weekly cycle (the ≥80% threshold = 11 of 13, per M1's coverage definition, [NZ adherence review, PMC8048926](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8048926/)).
- **At-risk/eligible population basis = GBD prevalent chronic-RHD cases** (from M1). This is the population that *should* be on prophylaxis. It is **not** the same denominator as M1's register-coverage %, which counts only enrolled patients (M1's central caveat — do not conflate them).

---

## Formula box

For each country (base case):

```
(1) Deaths avertable / yr  =  AnnualRHDdeaths × UnprotectedFraction × RRR
       where UnprotectedFraction = 0.90 (base assumption: ~90% of prevalent
       patients are not on adequate prophylaxis — see assumption A5), RRR = 0.904

(2) Annual BPG doses needed to close the gap  =  PrevalentCases × UnprotectedFraction × 13

(3) Annual drug cost  =  DosesNeeded × $/dose   (base $0.30)
```

Cells are computed **only where M1 supplied an extractable absolute count**. Where M1 marked a count "not extracted," the cell here is **"NA — basis missing in M1"** rather than an invented number. This is honest about the same gap M1 flagged: coverage/burden data are blank exactly where burden is highest outside South Asia.

---

## Per-country model (rows = M1 country set, ≥15)

Deaths-avertable uses M1 annual-death counts; doses/cost use M1 prevalent-case counts. "NA" = M1 did not provide an extractable absolute figure for that cell (handled honestly, not imputed).

| # | Country | At-risk/eligible basis (M1) | Current coverage assumption | GOAL RRR applied | Deaths avertable/yr (base) | Annual doses needed | Annual drug cost @ $0.30/dose |
|---|---------|------------------------------|------------------------------|------------------|-----------------------------|----------------------|-------------------------------|
| 1 | **India** | 10.5M prevalent (GBD 2021); 166,000 deaths/yr (GBD 2021) | ~0% effective (no national register, M1) → 90% unprotected | 0.904 | **135,058** = 166,000×0.90×0.904 | **122,850,000** = 10.5M×0.90×13 | **$36,855,000** |
| 2 | **China** | 72,600 deaths/yr (GBD 2015); prevalence not extracted in M1 | ~0% effective (no register, M1) → 90% unprotected | 0.904 | **59,067** = 72,600×0.90×0.904 | NA — prevalence missing in M1 | NA |
| 3 | **Pakistan** | 2.34M prevalent (GBD 2021); 24,200 deaths/yr (GBD 2021) | ~0% effective (no register, M1) → 90% unprotected | 0.904 | **19,689** = 24,200×0.90×0.904 | **27,378,000** = 2.34M×0.90×13 | **$8,213,400** |
| 4 | **Indonesia** | Top-5 global case-holder; absolute count NOT extracted in M1 | ~0% effective (no register, M1) | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 5 | **Bangladesh** | 1.30M prevalent (GBD 2021); 20,900 deaths/yr (GBD 2021) | ~0% effective (no register, M1) → 90% unprotected | 0.904 | **17,004** = 20,900×0.90×0.904 | **15,210,000** = 1.30M×0.90×13 | **$4,563,000** |
| 6 | **DR Congo / Congo** | Among top-5 case-holders; very high rate; absolute NOT extracted in M1 | ~0% effective (no register, M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 7 | **Nigeria** | High absolute burden; count NOT extracted in M1 | ~0% effective (no register, M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 8 | **Ethiopia** | High burden; count NOT extracted in M1 | ~63% adherent in one clinic zone (Jimma), no national figure (M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 9 | **Tanzania** | E. sub-Saharan hotspot; count NOT extracted in M1 | ~0% effective (no register, M1) | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 10 | **Nepal** | 222,700 prevalent (GBD 2021); 3,800 deaths/yr (GBD 2021) | ~0% effective (no register, M1) → 90% unprotected | 0.904 | **3,092** = 3,800×0.90×0.904 | **2,605,590** = 222,700×0.90×13 | **$781,677** |
| 11 | **Mozambique** | E. sub-Saharan hotspot; count NOT extracted in M1 | ~0% effective (no register, M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 12 | **Uganda** | Register >3,500; high burden; absolute NOT extracted in M1 | ~91% adherent among *retained*, but retention is the binding constraint (M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 13 | **Brazil** | Largest LatAm burden; count NOT extracted in M1 | No national register (M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 14 | **South Africa** | High burden; count NOT extracted in M1 | No register (M1); documented stockout | 0.904 | NA — deaths missing in M1 | NA — prevalence missing in M1 | NA |
| 15 | **Australia (First Nations)** | ~5,282 First Nations register-eligible (AIHW 2024, M1) | **~32% receive ≥80% doses (AIHW 2024, M1)** → 68% unprotected | 0.904 | NA — death count not extracted in M1 (low national); benefit dominated by morbidity not mortality | **46,693** = 5,282×0.68×13 | **$14,008** @ $0.30 (≈ **$1.4M** at US Bicillin ~$30/dose) |
| 16 | **Fiji** | High per-capita; screen-detected cohort; absolute count NOT extracted in M1 | **~7% adequate adherence (Engelman 2016, M1)** → ~93% unprotected | 0.904 | NA — deaths missing in M1 (small absolute) | NA — prevalence count missing in M1 | NA |

**Rows: 16 countries** (≥15 required), matching the M1 country set 1:1 (M1's row 17 New Zealand, row 18 Eritrea, row 19 CAR, row 20 Solomon Is./PNG are per-capita-rate hotspots that M1 itself left with "absolute not extracted"; they would all be NA rows here and are omitted only to avoid a table of pure NAs — the four South-Asia + China + the two register settings above are the only rows M1 gave computable counts for, plus the structurally-instructive NA rows shown).

### Computable subtotal (the five rows M1 gave absolute counts for)

| Quantity | Value | Reproduction |
|----------|-------|--------------|
| Annual deaths in the 5 counted countries (India, China, Pakistan, Bangladesh, Nepal) | **287,500** | 166,000+72,600+24,200+20,900+3,800 |
| **Deaths avertable/yr (base)** across those 5 | **≈ 234,000** | 287,500×0.90×0.904 = 233,810 |
| Prevalent cases with extracted counts (India, Pakistan, Bangladesh, Nepal — China prevalence NA) | **14,362,700** | 10.5M+2.34M+1.30M+0.2227M |
| **Annual doses to close the gap** in those 4 | **≈ 168.0M** | 14,362,700×0.90×13 = 168,023,790 |
| **Annual drug cost @ $0.30/dose** | **≈ $50.4M** | 168.0M×$0.30 |
| Same doses @ $0.11 / @ $1.00 | **$18.5M / $168.0M** | 168.0M×0.11 ; ×1.00 |

These five countries alone (a *subset* of global burden) yield **~234,000 avertable deaths/yr at a drug cost on the order of $18M–$168M/yr** — i.e. the drug itself is so cheap that even the high-price, full-coverage bill is a rounding error against the lives at stake. **The deaths-per-dollar ratio is the headline: ~$215–$720 of drug per death avertable at base assumptions** ($50.4M / 234,000 ≈ $215; or up to $168M/234,000 ≈ $718 at $1/dose). This excludes all delivery/staffing cost — see limitations; the drug is the cheap part.

### Global cross-check (using M1's global GBD 2021 anchor)

M1's global anchor: **373,345 RHD deaths/yr, ~54.8M prevalent cases (GBD 2021)**. Applying the same base formula globally:

- **Global deaths avertable/yr (base):** 373,345 × 0.90 × 0.904 = **≈ 303,600**.
- **Global doses to close the gap:** 54.8M × 0.90 × 13 = **≈ 641M doses/yr** — note this *exceeds* CHAI's modeled ~200M-dose RHD need (M2), because my naive 13-doses × 90%-of-all-prevalent assumption is more aggressive than CHAI's clinical-need model (not every prevalent patient is an appropriate/active prophylaxis candidate). **I therefore anchor the cost on CHAI's ~200M-dose need, not my 641M:** 200M × $0.11–$1.00 = **$22M–$200M/yr** for the global RHD drug bill ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/), via M2). The discrepancy between 641M and 200M is itself a useful flag that "doses = prevalence × 13" over-counts; the CHAI figure is the better cost denominator.

---

## Sensitivity

The headline is **avertable deaths** and **total drug cost**. Both are soft; here is the low/base/high range.

**Avertable deaths (the 5 counted countries; 287,500 baseline deaths):**

| Scenario | Unprotected fraction | RRR applied | Deaths avertable/yr | Reproduction |
|----------|----------------------|-------------|----------------------|--------------|
| **Low** (efficacy halved + lower gap) | 0.70 | 0.45 (half of GOAL) | **≈ 90,600** | 287,500×0.70×0.45 |
| **Base** | 0.90 | 0.904 (GOAL) | **≈ 234,000** | 287,500×0.90×0.904 |
| **High** | 0.95 | 0.904 | **≈ 247,000** | 287,500×0.95×0.904 |

Globally (373,345 baseline deaths): **low ≈ 118,000 / base ≈ 304,000 / high ≈ 321,000** avertable deaths/yr (same multipliers).

The dominant uncertainty is the **efficacy extrapolation**, not the gap size: halving the RRR (the "latent-progression effect does not fully transfer to established-RHD mortality" scenario) roughly halves the benefit, while moving the unprotected fraction from 70% to 95% changes it far less. The low-case RRR of 0.45 is a deliberately pessimistic stand-in for "established symptomatic disease responds half as well as latent disease" — there is no trial to pin it, so it is a judgement bound, not a measured value [speculative bound].

**Total drug cost (global, on CHAI's 200M-dose need):**

| $/dose | Annual global RHD drug cost |
|--------|------------------------------|
| **$0.11 (low)** | **≈ $22M** |
| **$0.30 (base)** | **≈ $60M** |
| **$1.00 (high)** | **≈ $200M** |

Across the full plausible space, the global drug bill to close the RHD prophylaxis gap is **tens of millions to ~$200M/yr** against **~118,000–321,000 avertable deaths/yr** — a cost-per-death-averted (drug only) of roughly **$70–$1,700**. Even the worst corner (high price, low efficacy: $200M / 118,000 ≈ $1,700/death) is extraordinarily cheap by any global-health benchmark. The conclusion is robust to the sensitivity range; what is *not* robust is the precise death count, which the efficacy extrapolation could move by 2–3×.

---

## Assumptions box (every simplifying assumption)

1. **A1 — Latent→established and progression→death extrapolation.** GOAL's 90.4% RRR was measured for *echo progression of latent disease over 2 years*; I apply it to *annual deaths in established RHD*. There is no trial supporting this transfer. This is the single largest assumption and the reason the low-sensitivity case halves the RRR. ([NEJM 2021](https://www.nejm.org/doi/full/10.1056/NEJMoa2102074))
2. **A2 — Static population & burden.** GBD prevalence and death counts (M1) are held constant; no demographic growth, no incidence dynamics, no competing-risk or background-mortality adjustment. A single-year snapshot.
3. **A3 — Full adherence once "covered."** The model assumes a patient moved from "unprotected" to "protected" receives the full GOAL benefit, i.e. ~full adherence. Real-world adherence is far from 100% (M1: Fiji 7%, Australia 32%), so realized benefit is lower — this biases the benefit *upward*.
4. **A4 — $/dose held constant** across countries and time (base $0.30; range $0.11–$1.00). Ignores freight, cold-chain, wastage, and that US/HIC prices are ~100× higher; justified because burden is overwhelmingly LMIC.
5. **A5 — Coverage-baseline = ~90% unprotected** for countries M1 flagged "no register/no data," and 100%-minus-the-cited-coverage where M1 gave a figure (Australia 32%→68% unprotected; Fiji 7%→93%). The 90% default is a stated judgement, not a measured baseline; it is varied 70–95% in sensitivity. [speculative baseline]
6. **A6 — Doses = 13/patient-year** for everyone; ignores 10-weekly SCIP regimens now rolling out (M1, NZ) that would lower the dose count, and ignores partial-year enrollment.
7. **A7 — Drug cost only.** No delivery, staffing, register, cold-chain, or program cost is included. The true cost-of-action is higher; the drug is the cheap part (M2's whole point). Cost-per-death-averted figures are *drug-only* and understate program cost.
8. **A8 — NA rows are excluded, not imputed.** Countries where M1 had no extractable absolute count contribute zero to the computable subtotal, so the 234,000-deaths figure is a *floor over five countries*, not a global total; the global cross-check uses GBD's global anchor separately.

---

## Limitations & counter-evidence

1. **The benefit is an extrapolation a critic can reasonably reject.** A reviewer could argue that established-RHD valve damage is largely irreversible and that BPG prophylaxis prevents *recurrent rheumatic fever / further progression* rather than reversing existing mortality risk — in which case applying GOAL's latent-disease RRR to established-RHD *deaths* overstates avertable mortality. A naïve-realism critique of exactly this transfer has been published ([PMC10593280](https://pmc.ncbi.nlm.nih.gov/articles/PMC10593280/)). The low-sensitivity case (RRR 0.45) is my hedge; the honest position is that the *deaths* figure could be materially lower than base, even if the *direction* (large benefit, trivial drug cost) is secure.
2. **GBD burden is modeled, not measured (inherited from M1).** Prevalence/death counts carry wide uncertainty intervals (M1: India ~8.2M–13.2M prevalent), and several high-burden countries (Indonesia, DRC, Nigeria, Tanzania) had *no* extractable absolute count, so they sit as NA — the model is silent exactly where a chunk of the burden lives, and the 234,000 floor is therefore a substantial *under*-count of the true global avertable total.
3. **Doses-by-prevalence over-counts need.** My "54.8M × 13 = 641M doses" exceeds CHAI's modeled ~200M-dose RHD need by 3×, confirming that not every GBD-prevalent patient is an active prophylaxis candidate (age, severity, secular cure, mortality already occurred). I anchored cost on CHAI's 200M to avoid this, but the per-country dose columns still use the prevalence×13 basis and so over-state country-level dose need.
4. **Cost excludes the hard part.** Delivery — finding patients, running registers, cold chain, supervised injection (the AHA-advisory mitigation that M4 will cover) — dwarfs the drug cost and is omitted (A7). A funder reading "$60M closes the global gap" would be wrong: $60M buys the *molecule*, not the *program*. The drug being trivially cheap is precisely why the binding constraint is supply security (M2) and delivery (M1), not drug budget.
5. **Adherence reality undercuts the upper benefit.** M1's own coverage data (Fiji 7%, Australia 32%) show that "closing the gap" is not a switch; partial adherence yields partial benefit, so realized avertable deaths in practice will fall below even the base case until delivery improves. The model assumes the achievable, not the likely.
6. **Counter-evidence on the lever.** As M1 and M2 both noted, in some settings (Uganda) the binding constraint is *retention in care*, not drug availability or even adherence per se. A model that frames the gap purely as "deaths × efficacy × dose-cost" implicitly assumes drug-and-money is the lever; for some countries the lever is health-system enrollment, which no amount of cheap penicillin fixes.

---

## Source list (named, dated)

- **GOAL trial (efficacy input; 0.8% vs 8.3%, ~tenfold):** Beaton et al., "Secondary Antibiotic Prophylaxis for Latent Rheumatic Heart Disease," *NEJM* 2021;385:2211–2221 — [NEJM](https://www.nejm.org/doi/full/10.1056/NEJMoa2102074); plain-language figures via [Cincinnati Children's Science Blog](https://scienceblog.cincinnatichildrens.org/in-uganda-rheumatic-heart-disease-research-reaches-its-goal/)
- **Burden input (all prevalence/death counts):** M1 scorecard — `artifacts/2026-06-25-m1-coverage-stockout-scorecard.md` (cites GBD 2021 / GBD 2015; global anchor 373,345 deaths / 54.8M prevalent, 2021)
- **$/dose and global ~200M-dose need:** CHAI/Oxford, *International Health* 2024;16(3):279 — [PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/) (via M2); LMIC "<US$1/dose"; ~200M RHD doses needed. CHAI ~$0.11 LMIC price via [PAHO/WHO 2017](https://www.paho.org/en/news/27-12-2017-shortages-benzathine-penicillin-how-big-problem-and-why-it-matters). US Bicillin price context: [GoodRx](https://www.goodrx.com/bicillin-l-a)
- **13-dose schedule / coverage definition:** [NZ adherence review, PMC8048926](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8048926/) (via M1)
- **Latent→established extrapolation critique (counter-evidence):** [PMC10593280](https://pmc.ncbi.nlm.nih.gov/articles/PMC10593280/)
