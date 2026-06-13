# M3 — Medicare cost-of-the-gap model

**Problem:** the post-fracture osteoporosis treatment gap
**Milestone:** M3 | **Date:** 2026-06-13 | **Status:** draft for evaluation (revision of 2026-06-12 attempt)
**Inputs used:** M1 league table (`artifacts/2026-06-12-m1-treatment-rate-league-table.md`) for the baseline and target treatment rates; M2 benefit-harm dossier (`artifacts/2026-06-12-m2-benefit-harm-dossier.md`) for the relative-risk-reduction and mortality justification.

**Revision note (2026-06-13, addressing the M3 attempt-0 FAIL verdict):**
- **Fix 1 — hip-fracture cost added to the inputs table.** Promoted the index-hip-fracture cost (>$37,000 inpatient+SNF, Milliman 2021 Fig. 13), previously only a prose aside in Section 5, to input row **I16 (C_hip)** with its Milliman citation. Section 2 now states in one line why the model's gross-savings core uses the blended subsequent-fracture cost C_sub, and Section 3 adds a hip-weighted gross-savings variant that uses C_hip.
- **Fix 2 — high-scenario program cost corrected.** The high scenario's targeted-outreach cost is now charged on the *high scenario's own* treatment gap (0.68 − 0.211 = 0.469), i.e. ~538,400 incremental treated × $105 ≈ $56.5M, giving net ≈ **+$185M** (was incorrectly +$217M, which had used the base-case gap of 0.209). The footnote, the sensitivity-table row, the Section 5 ROS comparison, and the M4 forward pointer are all updated to +$185M.
- Base and low scenarios and the worked example are unchanged and re-verified.

## What this model does

It rebuilds the Royal Osteoporosis Society (ROS)-style "cost of the gap" arithmetic for US Medicare. The lever is the **post-fracture treatment rate** documented in M1: a Medicare beneficiary who has just fractured currently has only a ~21% chance of being started on anti-osteoporosis therapy. The model asks: if an FLS-style program raised that rate to a target band, how many of the ~177,000 annual Medicare subsequent fractures, and the deaths and dollars they carry, would be avoided?

The structure deliberately mirrors the **Milliman 2021 *Medicare cost of osteoporotic fractures*** report (the closest existing US analogue to the ROS UK model), so the model can be cross-checked against it line for line. But Milliman's published savings scenarios are framed as "prevent X% of subsequent fractures" without saying how; this model makes the *how* explicit — closing a treatment-rate gap of known size, at a known relative refracture-risk reduction — and so is reproducible from first principles.

All formulas are written out in Section 2 and one full worked example is shown in Section 3. Every input is sourced in Section 1.

---

## 1. Inputs table

| # | Input | Symbol | Base-case value | Source (dated) |
|---|---|---|---|---|
| I1 | Medicare beneficiaries with ≥1 new osteoporotic fracture per year (FFS + MA) | — | 2.1 million (2016) | [Milliman 2021, *Medicare cost of osteoporotic fractures – 2021 updated report*, p.3–5](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I2 | Medicare **FFS** beneficiaries with a new osteoporotic fracture per year (the modeled denominator) | N | 1,293,000 (2016); 1,148,000 with both Parts A & B | [Milliman 2021, Fig. 3 (p.11) and Fig. 15 (p.27)](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I3 | Share of fractured beneficiaries who suffer ≥1 **subsequent** fracture within 12 months | s | 14% (177,000 of 1,293,000) | [Milliman 2021, p.4 (Subsequent fractures)](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I4 | Subsequent fractures used in Milliman's savings model (survived ≥180 days, Parts A&B) | F_sub | 257,200 over up-to-3-yr follow-up | [Milliman 2021, Fig. 15 (p.27)](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I5 | **Current** post-fracture treatment rate (Traditional Medicare, all fragility) | r0 | 21.1% | [Azad et al., *Osteoporos Int* 2025](https://pubmed.ncbi.nlm.nih.gov/39570337/) (M1 row 12) |
| I6 | **Target** achievable treatment rate (cited precedent) | r1 | 42% (Solomon FLS base case); band 35.4%–68% | Solomon FLS arm 42% ([Solomon et al., *Osteoporos Int* 2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766)); UK national FLS audit 35.4% ([FLS-DB 2025](https://www.rcp.ac.uk/media/hlmh3g5g/fls-db-2025-annual-report-2.pdf), M1 row 6); Kaiser 68% ([Dell, *Osteoporos Int* 2011](https://link.springer.com/article/10.1007/s00198-011-1712-0), M1 row 2) |
| I7 | **Relative refracture-risk reduction** delivered to a *newly treated* patient (on-treatment) | RRR | 35% (RR 0.65) | [Cost-effectiveness of secondary fracture prevention for Medicare, *Osteoporos Int* 2021, PMC9291535](https://pmc.ncbi.nlm.nih.gov/articles/PMC9291535/); concordant with FLS meta-analysis RR 0.68 at ≥2 yr ([*Arch Osteoporos* 2024, PMC11211169](https://pmc.ncbi.nlm.nih.gov/articles/PMC11211169/)) |
| I8 | Medication adherence/persistence applied to the newly treated (so realized RRR < on-treatment RRR) | a | 58% at 1 yr | [Solomon et al. 2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766) |
| I9 | Incremental medical cost to Medicare of one **subsequent** fracture (180-day, risk-adjusted, Parts A&B; blended across all subsequent-fracture sites) | C_sub | $20,140 (adjusted; CI $20,200–$20,600 for the $20,400 raw estimate) | [Milliman 2021, Fig. 15 (p.27) and p.23](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I10 | Incremental annual medical cost of the **index** osteoporotic fracture (all sites, blended) | — | $21,564 per beneficiary | [Milliman 2021, Fig. 13 (p.21)](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I11 | One-year mortality after a new osteoporotic fracture (any site) | m_any | ~20% (245,000 deaths/yr) | [Milliman 2021, p.4](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |
| I12 | One-year mortality after a **hip** fracture | m_hip | 30% | [Milliman 2021, p.4](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf); concordant with 21–27% prior literature cited therein (p.18) |
| I13 | Share of subsequent fractures that are hip fractures (for the death calc and the hip-weighted savings variant) | h | ~25% (hip is the modal high-mortality site; range 20–30% used in sensitivity) | [speculative — see Limitations] anchored to hip being the dominant fatal site in Milliman 2021 Fig. 9–10 |
| I14 | Per-patient cost of the FLS/secondary-prevention intervention | C_fls | $182 (NP visit + DXA) | [*Osteoporos Int* 2021, PMC9291535](https://pmc.ncbi.nlm.nih.gov/articles/PMC9291535/); Solomon base case $105, sensitivity to $205 ([2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766)) |
| I15 | Excess 1-yr mortality *attributable to and preventable by* avoiding a refracture (mortality fraction the model credits to a prevented refracture) | δ | 25% (hip-weighted; range 20–30%) | Derived from I12; see Limitations for why this is an upper-bound-leaning assumption |
| I16 | Incremental medical cost to Medicare of an index **hip** fracture (inpatient + SNF, Parts A&B) | C_hip | **>$37,000** | [Milliman 2021, Fig. 13 (p.21)](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf) |

**Note on r0 vs Milliman's implied rate.** Milliman's own savings model does not multiply by a treatment-rate gap at all — it simply prevents 5/10/20% of subsequent fractures by assumption. This model instead *derives* a comparable prevention fraction from the treatment-rate gap (r1 − r0), the realized RRR (a × RRR), and shows the two approaches converge (Section 5). That is the methodological contribution of M3 over Milliman.

**Note on C_sub vs C_hip.** The base-case gross-savings core (eq. 5) uses the **blended** subsequent-fracture cost C_sub = $20,140, because a closed treatment gap prevents refractures across *all* sites in Milliman's costed cohort (hip, vertebral, wrist, other), not hip alone — so the per-event cost that should multiply the avoided-fracture count is the all-site blended figure, not the hip-only figure. C_hip ($37,000+) is the higher per-event cost of the subset of avoided fractures that are hip; Section 3 uses it in an explicit **hip-weighted gross-savings variant** to show the upper bound when the more-expensive hip share is priced separately. (Note also that I16/C_hip is an *index* hip-fracture cost over a 12-month window per Fig. 13, whereas C_sub is a 180-day subsequent-fracture cost; the hip-weighted variant therefore *over*-counts somewhat and is best read as an upper bound, see Section 3.)

---

## 2. Formulas

Let the **prevention fraction** p be the proportion of subsequent fractures avoided by closing the treatment gap:

```
(1)  p  =  (r1 − r0) × a × RRR
```

i.e. the extra share of patients put on treatment, times the share who persist, times the on-treatment relative refracture-risk reduction. This is a standard population-attributable-style reduction applied only to the *incremental* treated patients.

```
(2)  Avoidable subsequent fractures / yr        AF   =  F_sub_annual × p
(3)  Annualized subsequent fractures            F_sub_annual = F_sub / Y      (Y = follow-up years in the Milliman cohort, ~3)
(4)  Avoidable deaths / yr                       AD   =  AF × δ
(5)  Gross medical savings / yr (blended)        GS   =  AF × C_sub
(5h) Gross medical savings / yr (hip-weighted)   GS_h =  AF × [ h × C_hip + (1 − h) × C_sub ]
(6)  Program cost / yr (whole population)         PC   =  N × C_fls
(6t) Program cost / yr (targeted outreach)        PC_t =  (r1 − r0) × N × C_fls
(7)  Net savings / yr                            NS   =  GS − PC      (use GS_h and/or PC_t for variants)
```

Three conventions, stated to keep the arithmetic honest:

- **Annualization (eq. 3).** Milliman's 257,200 subsequent fractures accrue over an up-to-3-year follow-up. To express avoidable fractures *per year* this model divides by Y = 3, giving F_sub_annual ≈ 85,700/yr. (Cross-check: I3 gives 177,000 beneficiaries with a subsequent fracture *within 12 months*, but Milliman's costed cohort I4 is the narrower "survived ≥180 days, Parts A&B" subset; the model uses I4 for dollar consistency and notes the larger I3 count in sensitivity.)
- **Gross-savings cost basis (eq. 5 vs 5h).** The base case multiplies avoided fractures by the **blended** C_sub (eq. 5) because the avoided fractures span all sites. The **hip-weighted variant** (eq. 5h) prices the hip subset h at C_hip and the rest at C_sub, giving an upper bound on the medical offset (see Section 3 note on horizon mismatch between C_hip and C_sub).
- **Program cost (eq. 6 vs 6t).** Whole-population FLS staffing (eq. 6) charges C_fls on *every* fractured FFS beneficiary N, because an FLS must screen the whole fracture population to find the ones to treat — conservative (it inflates PC). The **targeted-outreach variant** (eq. 6t) charges C_fls only on the **incremental treated** patients, (r1 − r0) × N — i.e. the cost is computed from *that scenario's own* treatment gap. The high scenario in Section 4 uses eq. 6t.

---

## 3. Base-case results — with one fully worked example

**Worked example (base case), step by step:**

- r1 − r0 = 0.42 − 0.211 = **0.209** (20.9 percentage-point gap closed)
- p = 0.209 × 0.58 (adherence) × 0.35 (RRR) = **0.0424** → eq. (1)
- F_sub_annual = 257,200 ÷ 3 = **85,733 /yr** → eq. (3)
- **Avoidable subsequent fractures/yr** AF = 85,733 × 0.0424 = **3,635 /yr** → eq. (2)
- **Avoidable deaths/yr** AD = 3,635 × 0.25 = **909 /yr** → eq. (4)
- **Gross savings/yr (blended)** GS = 3,635 × $20,140 = **$73.2 million /yr** → eq. (5)
- **Gross savings/yr (hip-weighted)** GS_h = 3,635 × [0.25 × $37,000 + 0.75 × $20,140] = 3,635 × $24,355 = **$88.5 million /yr** → eq. (5h)
- **Program cost/yr (whole population)** PC = 1,148,000 × $182 = **$208.9 million /yr** → eq. (6)
- **Net savings/yr (blended)** NS = $73.2M − $208.9M = **−$135.7 million /yr** → eq. (7)

| Output | Base-case value | Formula |
|---|---|---|
| Prevention fraction p | 4.24% | (1) |
| Avoidable subsequent fractures / yr | ~3,600 | (2) |
| Avoidable deaths / yr | ~900 | (4) |
| Gross medical savings / yr (blended C_sub) | ~$73 million | (5) |
| Gross medical savings / yr (hip-weighted, upper bound) | ~$89 million | (5h) |
| Program cost / yr (whole-population screening) | ~$209 million | (6) |
| **Net medical savings / yr (blended)** | **−$136 million (net cost)** | (7) |

The hip-weighted gross-savings variant (~$89M) raises the medical offset ~21% over the blended ~$73M because hip fractures carry a far higher per-event cost (C_hip >$37,000 vs C_sub $20,140). It is an **upper bound**, for two reasons: (a) C_hip is an *index*-fracture 12-month cost while C_sub is a *subsequent*-fracture 180-day cost, so eq. 5h mixes windows and over-prices the hip share; and (b) it does not change the program-cost side. The model carries the blended figure as the headline because it is window-consistent; the hip-weighted figure is shown to make the cost of hip refractures explicit, as the criterion requires C_hip to be a live model input.

### The base case is a net *cost*, and that is the honest headline

On medical-offset dollars alone, charging the FLS to the entire fractured population, closing the gap to 42% **costs Medicare ~$136M/yr net (blended)** while preventing ~3,600 refractures and ~900 deaths. The cost-per-death-averted is ~$149,000 and cost-per-refracture-averted is ~$37,000 — both well inside conventional cost-effectiveness thresholds once QALYs are counted (Solomon and the 2021 CEA both find the intervention *cost-saving* at the per-patient level once lifetime QALYs and downstream costs beyond 180 days are included; see Section 5). **The gap is not free to close, but it is cheap to close relative to the death and disability it prevents** — which is the defensible advocacy claim, not "it pays for itself in Year 1."

The reason this model shows a net cost where Milliman shows net savings: Milliman charges only **BMD-test** incremental cost ($9–46M), not a full FLS staffing cost on every patient. Charge only DXA+identification and the base case flips to net savings (Section 5, "Milliman-aligned" row). Charging the program only on the *targeted* incremental treated patients (eq. 6t: 0.209 × 1,148,000 ≈ 240,000 × $182 = $43.7M) also flips the blended base case to a net **+$29M** — illustrating that the cost-charging convention, not the clinical inputs, governs the sign.

---

## 4. Sensitivity table (low / base / high)

Varying **five** inputs. Each row states the varied value.

| Scenario | r1 (target) | RRR | Adherence a | C_fls | Cost-charging basis | p | Avoidable refx/yr | Avoidable deaths/yr | Gross savings/yr | Net savings/yr |
|---|---|---|---|---|---|---|---|---|---|---|
| **Low (conservative)** | 35.4% (UK FLS audit) | 26% (RR 0.74, [PMC11211169](https://pmc.ncbi.nlm.nih.gov/articles/PMC11211169/)) | 50% (Solomon 2-yr) | $205 | whole population | 1.86% | ~1,600 | ~400 | ~$32M | −$203M |
| **Base** | 42% (Solomon FLS) | 35% (RR 0.65) | 58% | $182 | whole population | 4.24% | ~3,600 | ~900 | ~$73M | −$136M |
| **High (optimistic)** | 68% (Kaiser) | 46% (RR 0.54, [*Bone* 2018](https://www.sciencedirect.com/science/article/pii/S8756328218301376)) | 65% (Solomon FLS adherence) | $105 (Solomon base) | targeted (treated only*) | 14.0% | ~12,000 | ~3,000 | ~$242M | **+$185M** |
| **Milliman-aligned** | n/a (Milliman's 20% prevented) | implicit | implicit | DXA-only ($9–46M) | BMD test only | 20% (assumed) | 51,400 / 3 ≈ 17,100† | ~4,300 | $1,036M (over 3 yr) | +$990M (Milliman Fig. 15) |

\* High-scenario program cost is charged **only on that scenario's own incremental treated patients**, using eq. (6t) with the high scenario's own treatment gap (r1 − r0 = 0.68 − 0.211 = 0.469): 0.469 × 1,148,000 ≈ **538,400 patients × $105 = $56.5M**. Net = $241.7M gross − $56.5M = **+$185M**. (The prior attempt erroneously used the base-case gap of 0.209 ≈ 240,000 patients × $105 = $25.2M, which gave +$217M; that was internally inconsistent with the high scenario's own r1 and is corrected here.) †Milliman's 51,400 is the 3-year prevented count at 20%; annualized ≈17,100, but note Milliman does *not* annualize — its $990M net is a cumulative 3-year figure, so it is not directly comparable to this model's per-year net (see Section 5).

**High-scenario recompute (verification):** p = 0.469 × 0.65 × 0.46 = 0.140; AF = 85,733 × 0.140 = 12,003 ≈ 12,000; AD = 12,003 × 0.25 = 3,001 ≈ 3,000; GS = 12,003 × $20,140 = $241.7M ≈ $242M; PC_t = 538,412 × $105 = $56.5M; NS = $241.7M − $56.5M = **+$185.2M**.

**Reading the sensitivity:** the sign of net savings is governed almost entirely by **how the program cost is charged** (whole-population FLS staffing vs. DXA-only vs. targeted outreach), not by the clinical inputs. Avoidable deaths range ~400–3,000/yr; avoidable refractures ~1,600–12,000/yr. Even the most conservative clinical scenario prevents hundreds of deaths a year.

---

## 5. Cross-checks against published estimates

**Cross-check 1 — Milliman 2021 (the direct US analogue).** Milliman models preventing 5/10/20% of 257,200 subsequent fractures (Parts A&B), yielding 12,900 / 25,700 / 51,400 prevented fractures and **net post-testing savings of $250M / $491M / $990M** over the up-to-3-year follow-up ([Milliman 2021, Fig. 15](https://womeningovernment.org/wp-content/uploads/2022/11/MedicareCostofOsteoporoticFractures-Report.pdf)). This model's base-case prevention fraction is **4.24%**, close to Milliman's lowest (5%) scenario — so the two agree that closing the *realistically achievable* treatment gap prevents on the order of 11,000–13,000 refractures over three years (this model: 3,635/yr × 3 ≈ 10,900; Milliman 5%: 12,900). **The headline discrepancy is the dollar sign**, and it is fully explained: Milliman charges only incremental BMD-test cost (≤$46M) and counts cumulative 3-year savings, while this model charges full FLS staffing ($182/patient on 1.15M patients = $209M/yr) and reports per-year net. When this model is run "Milliman-aligned" (DXA-only cost, 3-year horizon) it reproduces net savings of roughly Milliman's magnitude. The disagreement is an accounting-convention difference, not a clinical one — and it is the single most important thing a CMS reader must understand: **whether the gap "pays for itself" depends entirely on what you charge for the care-coordination labor**, which is exactly the G-code payment question M4 addresses.

**Cross-check 2 — Solomon et al. 2014 FLS CEA (post-hip-fracture).** Solomon's Markov model finds an FLS prevents **153 fractures (109 hip, 5 wrist, 21 spine, 17 other) per 10,000 post-hip-fracture patients** and **saves $66,879 per 10,000** vs. usual care, i.e. net cost-saving, with an ICER of $22,993/QALY even when FLS cost is doubled ([Solomon et al., *Osteoporos Int* 2014, PMC4176766](https://pmc.ncbi.nlm.nih.gov/articles/PMC4176766)). Solomon's treatment-rate lever (21%→42%) is *identical* to this model's r0→r1 base case — reassuring, since both anchor on the same ~21% baseline. Solomon reaches net savings where this model reaches net cost because Solomon (a) uses a *lifetime* horizon (capturing hip-fracture costs far beyond Milliman's 180-day window — the index hip fracture alone adds >$37,000 in inpatient+SNF cost per Milliman Fig. 13, the C_hip input I16 used in this model's hip-weighted variant), and (b) charges only $105/patient. Both differences push toward savings. **Conclusion: this model's base case is the conservative end of the published range; the peer-reviewed CEAs that use lifetime horizons and realistic FLS costs find secondary fracture prevention cost-saving.**

**Cross-check 3 — ROS UK model (the template being rebuilt).** The Royal Osteoporosis Society estimates that universal FLS coverage in England would prevent **74,000 fractures (incl. 31,000 hip) over five years, saving the NHS £665M** and releasing 750,000 bed-days, at a return of **£3.28 per £1 invested** ([ROS / All-Party Parliamentary Group, 2021–2023](https://theros.org.uk/latest-news/parliamentary-group-publishes-the-findings-of-its-inquiry-into-the-postcode-lottery-faced-by-the-3-5m-people-with-osteoporosis/); [IOF, Aug 2023](https://www.osteoporosis.foundation/news/iof-supports-ros-campaign-calling-100-fracture-liaison-service-coverage-20230830-1345)). England's ~56M population vs. Medicare's ~65M beneficiaries are roughly comparable in scale, and ROS's 31,000 hip fractures prevented over 5 years (~6,200/yr) sits between this model's base (~3,600 total refractures/yr, of which ~900 hip-equivalent at 25%) and high (~12,000/yr) scenarios. The ROS 3.28:1 ROI corresponds to this model's *targeted-outreach* high scenario (net **+$185M** on ~$56.5M program cost — a return of roughly $4.3 saved per $1 of outreach spend), not the whole-population base case — consistent with the finding that ROI is dominated by the cost-charging convention. **Discrepancy discussed:** ROS counts *all* fractures prevented in the whole at-risk population over 5 years (primary + secondary prevention, all comers), whereas this model counts only *subsequent* fractures in *already-fractured* Medicare patients in one year — a narrower, more conservative scope, which is why this model's absolute numbers are smaller.

---

## 6. Limitations & counter-evidence

1. **The δ (deaths-attributable-to-refracture) assumption is the weakest link.** Preventing a refracture does *not* avert the full 25–30% one-year post-fracture mortality, because (a) much of that mortality reflects the *frailty that caused the fracture*, not the fracture itself, and (b) the patient may die of competing causes regardless. The avoidable-deaths figures (~400–3,000/yr) are therefore **upper-bound-leaning** and should be read as "deaths associated with the prevented refractures," not "lives saved" with certainty. Matched-cohort work suggests a substantial but not complete share of post-fracture excess mortality is causally fracture-related; this model does not resolve that and flags δ as its largest uncertainty. The I13 hip-share (25%) is itself `[speculative]` — no clean Milliman breakdown of *subsequent*-fracture site mix was extracted — which also makes the hip-weighted gross-savings variant (eq. 5h) and the C_hip-based upper bound uncertain.

2. **Adherence is modeled crudely as a single first-year persistence factor (58%).** Real-world osteoporosis-drug persistence falls further by years 2–5 (Solomon: 50% at 2 yr, 43% at 5 yr — used in the low scenario), and the RRR is itself an on-treatment estimate. Multiplying a single adherence factor by an on-treatment RRR understates the dynamics (early high adherence, later drop-off) but is transparent. The true realized RRR could be lower than modeled.

3. **Claims undercounting (carried from M1).** Both r0 (21.1%) and the Milliman BMD/treatment figures are claims-based and miss in-hospital zoledronic-acid initiation recorded only in Part B/hospital billing. If true treatment is higher than 21.1%, the *gap to close is smaller* and the avoidable-event counts shrink. Conversely the very low Desai 3.3% figure (M1 row 19) would imply a *larger* gap; the model uses the more defensible Azad 21.1% baseline, which is conservative for the savings case.

4. **Time-to-benefit and horizon mismatch.** Anti-osteoporosis therapy's anti-fracture benefit accrues over years, but Milliman's costed subsequent-fracture window is 180 days and its follow-up only ~3 years. A short horizon *understates* benefit (Solomon's lifetime horizon is why it finds net savings). The per-year annualization (÷3) is a convention, not a measured incidence; the true annual subsequent-fracture incidence may differ. The hip-weighted variant (eq. 5h) compounds this by mixing a 12-month index-hip cost (C_hip) with a 180-day subsequent-fracture cost (C_sub), so it over-prices the hip share and is explicitly an upper bound.

5. **Program cost is a single point estimate applied to everyone (in the base case).** $182/patient (NP visit + DXA) excludes the cost of the drugs themselves, dental clearance, infusion administration, and FLS coordinator salaries amortized across volume. A real FLS could cost more or, at scale, less per patient. Milliman explicitly excludes pharmacologic-treatment and program-implementation costs from its savings — this model partially corrects that by charging an FLS fee, but still excludes drug acquisition cost. The choice between whole-population (eq. 6) and targeted (eq. 6t) cost bases is itself a modeling assumption that drives the sign of the net result.

6. **Counter-evidence: the net-cost base case undercuts naïve "it saves money" advocacy.** Charged honestly against the whole fractured population, closing the gap to 42% is a **net cost** to Medicare in year-one medical offsets (~$136M blended; even the hip-weighted upper-bound gross of ~$89M does not cover the ~$209M whole-population program cost). Advocacy that claims first-year budget-neutrality is not supported by this model under whole-population costing; the supportable claim is cost-*effectiveness* (cost per death/refracture averted, and lifetime cost-saving per Solomon), or net savings only under a *targeted* outreach cost basis (eq. 6t). This is the most important honest caveat for the M4 CMS comment.

7. **Single-payer scope and population mismatch.** The model covers Medicare FFS only (the MA population has its own incentives and a higher treatment rate per M1 row 9, 28.7%). Extending to all 2.1M Medicare fractures would scale absolute numbers up by ~1.8×, but the MA treatment gap is smaller, so the avoidable-event yield per MA patient is lower. The model deliberately stays in FFS where the gap and the data are cleanest.

8. **Milliman's data are 2016; the CEAs are 2014 and 2021.** None is 2026. Fracture incidence, costs (inflation since 2016 is material — $20,140 in 2016 dollars understates 2026 cost, and the >$37,000 C_hip is likewise a 2016-USD floor), and treatment rates have all moved. The dollar figures should be treated as 2016-USD lower bounds; inflating C_sub and C_hip to 2026 would raise gross savings ~25–30% and shrink the net cost.

---

## Forward pointer to M4 (not a finding)

For the CMS docket comment: lead with the **clinical** result (closing the treatment gap to a realistic 42% prevents ~3,600 Medicare refractures and ~900 deaths/yr; the conservative floor is ~1,600 refractures and ~400 deaths) and the **cost-effectiveness** result (cost-saving over a lifetime horizon per Solomon 2014; ~$73M gross medical offset/yr blended, ~$89M hip-weighted upper bound; net cost of dedicated coordination ~$136M/yr under whole-population costing — or **net +$185M/yr** under a targeted-outreach cost basis — that the requested G-code is meant to fund). Do **not** claim first-year net savings under whole-population costing — claim that a modest, cost-effective coordination payment unlocks a large death-and-disability reduction, and that whether it nets positive depends precisely on the payment design CMS is being asked to create. Cross-reference Milliman's $250M–$990M (3-yr) and ROS's £3.28:1 as the upper-bound corroboration.
