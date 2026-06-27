# M5 — Ranked accountability docket: which vehicle families to target, what risk a controlled-deorbit fix retires, and who bears the exported burden

**Problem:** Uncontrolled rocket-body reentries — the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M5 (the decision-grade docket synthesizing M1–M4, framed for FAA / ICAO / UN COPUOS / Outer Space Institute action).
**Inputs (no new numbers introduced; every figure traces to these):**
- **M3 — Per-reentry casualty risk and accountability attribution** (`artifacts/2026-06-26-m3-per-reentry-risk-and-attribution.md`). Source of every risk figure in the target list: per-family summed risk ΣE_a and share of fleet risk (M3 Table 2 §3b), per-launching-state share (§3a), per-operator share (§3c), count-exceeding-threshold, the fleet total ΣE_a = 0.2080, and the 77.8% threshold-exceedance share.
- **M4 — Exported-risk overlay by country** (`artifacts/2026-06-27-m4-exported-risk-overlay-by-country.md`). Source of the over-exposed-states summary: the borne-exposure ranking E_c (§2), the generated-vs-borne comparison (§3), and the families/inclinations driving each city's exposure.
- **M2 — Per-rocket-body classified inventory** (`artifacts/2026-06-26-m2-per-rocket-body-classified-inventory.md`). Source of the compliance-status signals: the controlled (status `D`/`DSO`) vs uncontrolled (`R`) labels per family, including the 13 controlled Falcon 9 second stages.
- **M1 — Methodology and Source Register** (`artifacts/2026-06-26-m1-methodology-source-register.md`). The 1×10⁻⁴ (1-in-10,000) compliance threshold (NASA-STD-8719.14, adopted US/France/Japan/ESA) and the casualty-risk model behind every E_a.

**Author:** generator routine | **Date:** 2026-06-27.

> **Reading guide.** §1 is the headline ask in three sentences. §2 is the **ranked target list** — vehicle families ordered by aggregate casualty risk a controlled-deorbit fix would retire ("risk-retired-if-fixed"), each labelled compliant or not. §3 names the **over-exposed states** that import this risk. §4 is the **feasibility note**: the fix is already routine for a named compliant family. §5 is **limitations + what would change the ranking**. All figures trace to M1–M4; none is newly computed here.

---

## 1. The ask, in three sentences

1. **A small set of heavy, uncontrolled upper stages dominates the exported casualty risk.** The top five vehicle families — Soyuz Blok-I, CZ-3B, Falcon 9, CZ-2F, H-IIA/B — account for **0.1163 of the fleet's 0.2080 decade-cumulative expected casualties, i.e. 55.9% of all attributed risk** (M3 Table 2 §3b: 19.0% + 15.6% + 9.3% + 6.5% + 5.6%). Retiring those five through controlled deorbit retires the majority of the hazard.
2. **The fix exists and is routine.** Controlled second-stage deorbit to a remote-ocean target is the *standard, demonstrated* disposal mode for Falcon 9 — itself the #3 risk contributor — and for the DSO-disposed Centaur, CZ-5 second stage, and Ariane 5 ESC families (M2 §"Controlled" 58 bodies; SpaceX disposal statement, §4). This is not a technology gap; it is a compliance gap.
3. **The risk is exported.** **77.8% of these uncontrolled stages breach the agreed 1-in-10,000 line** (M3 §1c), and the burden lands disproportionately on Global-South states — **Indonesia, Bangladesh, Brazil, Pakistan, Mexico, Nigeria and others that generated 0% of it** (M4 §3) — making this a textbook case for a binding controlled-reentry standard at COPUOS / ICAO / national licensing (FAA, the analogous European bodies).

---

## 2. Target list — vehicle families ranked by risk-retired-if-fixed

Ranked by **risk retired if fixed** = the family's decade-summed casualty risk ΣE_a (M3 Table 2 §3b), which is exactly the risk that converting its uncontrolled stages to controlled deorbit would retire (controlled stages are removed from the exposure pool — the controlled `D`/`DSO` baseline carries no uncontrolled-reentry casualty risk, M2 §classification rule). "% of fleet risk retired" and "count >threshold" are M3 Table 2 §3b verbatim. **Compliance status** is assigned from M2's per-family control labels: *Non-compliant* = the family appears only as uncontrolled (status `R`) in M2; *Demonstrated-capable but non-compliant in practice* = the family has both controlled (`D`/`DSO`) and uncontrolled instances in M2; *(controlled baseline)* families (pure `D`/`DSO`) are not targets and are listed in §2c as proof points, not in the target table.

Top 20 families shown (these carry 0.1903 of the 0.2080 fleet total = **91.5% of all attributed risk**); the remaining 34 families each contribute ≤0.5% and are summarised below the table. Launching state and dominant operator are from M3 (§3a/§3c) for each family's primary owner.

### 2a. The ranked target table

| Rank | Vehicle family | Launch state | Operator (M3 §3c) | Risk retired if fixed — ΣE_a (M3 §3b) | % of fleet risk retired | Bodies >1-in-10,000 / total (M3 §3b) | Compliance status (M2) |
|---:|---|---|---|---:|---:|---:|---|
| 1 | **Soyuz (Blok-I)** | RU | RVSNR / VVKO(V) | **0.0396** | **19.0%** | 119 / 119 | **Non-compliant** — all uncontrolled; every body breaches threshold |
| 2 | **CZ-3B** | CN | CASC | **0.0324** | **15.6%** | 53 / 53 | **Non-compliant** — all uncontrolled; every body breaches |
| 3 | **Falcon 9** | US | SPX | **0.0193** | **9.3%** | 35 / 35 | **Demonstrated-capable, non-compliant in practice** — 13 controlled `D` bodies in M2 vs 35 uncontrolled (see §4) |
| 4 | **CZ-2F** | CN | CALT | **0.0134** | **6.5%** | 14 / 14 | **Non-compliant** — all uncontrolled |
| 5 | **H-IIA/B** | J | MHI | **0.0116** | **5.6%** | 15 / 15 | **Non-compliant** — all uncontrolled |
| 6 | **CZ-2C** | CN | CASC | **0.0108** | **5.2%** | 20 / 20 | **Non-compliant** — all uncontrolled |
| 7 | **CZ-5B** | CN | CNSA | **0.0096** | **4.6%** | 4 / 4 | **Non-compliant** — 4 bodies, the single highest per-body risk in the ledger (E_a ≈ 2.4×10⁻³, 24× threshold) |
| 8 | **CZ-7** | CN | CNSA | **0.0092** | **4.4%** | 9 / 9 | **Non-compliant** — all uncontrolled |
| 9 | **CZ-2D** | CN | CASC | **0.0075** | **3.6%** | 18 / 18 | **Non-compliant** — all uncontrolled |
| 10 | **GSLV** | IN | ISRO | **0.0067** | **3.2%** | 10 / 10 | **Non-compliant** — all uncontrolled |
| 11 | **Electron** | NZ | RLABN | **0.0056** | **2.7%** | **0 / 75** | Non-compliant in mode, **but 0 bodies breach threshold** — low-priority target (small kick stages demise) |
| 12 | **CZ-4B** | CN | CASC | **0.0049** | **2.3%** | 26 / 26 | **Non-compliant** — all uncontrolled |
| 13 | **Antares** | US | NGISW / OATKW / OSCW | **0.0042** | **2.0%** | 17 / 17 | **Non-compliant** — all uncontrolled |
| 14 | **CZ-7A** | CN | CASC | **0.0037** | **1.8%** | 6 / 6 | **Non-compliant** — all uncontrolled |
| 15 | **Centaur** | US | ULAL | **0.0025** | **1.2%** | 5 / 5 | **Demonstrated-capable, non-compliant in practice** — DSO disposal exists in M2 for the family; these 5 uncontrolled |
| 16 | **PSLV** | IN | ISRO | **0.0020** | **1.0%** | 7 / 7 | **Non-compliant** — all uncontrolled |
| 17 | **Zenit** | RU | VVKOV | **0.0019** | **0.9%** | 2 / 2 | **Non-compliant** — all uncontrolled |
| 18 | **CZ-3C** | CN | CASC | **0.0018** | **0.9%** | 3 / 3 | **Non-compliant** — all uncontrolled |
| 19 | **CZ-5** | CN | CNSA | **0.0018** | **0.9%** | 2 / 2 | **Demonstrated-capable** — CZ-5 second stage appears as DSO (controlled) in M2; these 2 core stages uncontrolled |
| 20 | **Ariane 5** | F | AE / AESP | **0.0018** | **0.9%** | 2 / 2 | **Demonstrated-capable, non-compliant in practice** — ESC stage disposed to Point Nemo/heliocentric (DSO) in M2; these 2 uncontrolled |

**Remaining 34 families:** each ≤0.8% of fleet risk; together **0.0177 (8.5% of fleet risk)**. Notable entries (all M3 §3b): Yuanzheng YZ kick stage 0.8%, CZ-11 0.6%, Kuaizhou/KT 0.5% (1 of 27 breaches), Delta 0.5%, CZ-6 0.5%, Zhuque 0.5%, LVM3 0.4%, Falcon Heavy 0.4% (1 body; note 1 controlled Falcon Heavy in M2), Proton-M 0.3%, H3 0.3%, the Iranian/DPRK/KSLV families ≤0.3% each (mostly below threshold). The smallest ~20 families are sub-200 kg kick stages that largely fall below the 1-in-10,000 line (M3 §1c).

### 2b. What the ranking says for action

- **The top 2 families alone (Soyuz Blok-I + CZ-3B) retire 34.6% of fleet risk** (19.0% + 15.6%), and **both are fully non-compliant — 172 stages, every one above threshold.** They are the highest-leverage targets and the hardest cases (no in-family controlled precedent).
- **Falcon 9 (#3, 9.3%) is the highest-value *immediately-actionable* target**: the fix is already in routine use on the same hardware (13 controlled vs 35 uncontrolled in M2, §4). Closing Falcon 9 alone retires nearly a tenth of fleet risk with **zero new technology**.
- **CZ-5B (#7) is the highest *per-body* priority**: 4 bodies, 4.6% of fleet risk, the single most-reported uncontrolled reentries of the decade, each at ~24× the threshold (M3 §3 note 5). Per-stage, it is the most dangerous object class in the ledger.
- **Electron (#11) is a deliberate *non*-target**: 75 uncontrolled bodies but **0 above threshold** (M3 §3b) — high body-count, negligible per-body risk. A standard should not waste enforcement on it; this is the ranking distinguishing *mode* non-compliance from *consequential* risk.

### 2c. The compliant baseline (proof points, not targets)

M2 lists **58 controlled bodies** (status `D`/`DSO`) that already meet the standard and carry no uncontrolled-reentry casualty risk — the existence proof that the fix works at scale:
- **Falcon 9: 13 controlled second stages** (M2, e.g. NORAD 40391, 42690, 53366, 61732 — launch and reentry the same day, the signature of a deorbit burn).
- **Falcon Heavy: 1 controlled** (NORAD 58050).
- **DSO-disposed families:** Centaur, CZ-5 second stage, Ariane 5 ESC — disposed to graveyard / Point Nemo / heliocentric via active burn (M2 §classification, status `DSO`).

These prove the target families are being asked to do something **already routine elsewhere in the fleet**, not something novel (§4).

---

## 3. Exported-risk summary — who imports the hazard they did not create (from M4)

M4 overlaid each family's risk onto ground-track latitude × population. The states bearing the **highest exposure while generating ~0% of the risk** (M4 §2 ranking, §3 generated-vs-borne):

| Over-exposed state (city) | Borne exposure E_c, rel. (M4 §2) | Generated risk share (M3 §3a / M4 §3a) | Contributing families/inclinations driving its exposure (M4 §2) |
|---|---:|---:|---|
| **Indonesia** (Jakarta, rank 1) | **1.000 (highest on Earth)** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), Falcon 9 (53°) over the ±6° tropical band |
| **Bangladesh** (Dhaka, rank 2) | **0.915** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) — sits at the ~24°N CZ-3B turning-latitude *maximum* |
| **Brazil** (São Paulo, rank 3) | **0.821** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) — 24°S turning-latitude peak |
| **Pakistan** (Karachi, rank 5) | **0.702** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) — highest per-capita ε in the table (0.0024) |
| **Mexico** (Mexico City, rank 6) | **0.687** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) |
| **Nigeria** (Lagos, rank 12) | **0.512** | **0.0%** | CZ-3B (27°), Soyuz Blok-I (62°), Falcon 9 (53°) |
| **Philippines / Colombia / DR Congo / Thailand / Egypt** | 0.37–0.54 | **0.0% each** | CZ-3B (27°), Soyuz Blok-I (62°), GSLV (19°) / Ariane 5 (6°) |

**The clearest case (M4 §3b):** Indonesia bears the **highest exposure of any country on Earth (Jakarta E_c = 1.000) while generating 0% of the fleet risk** — the hazard imported almost entirely from **Chinese CZ-3B/CZ-2F (China 50.2% generated) and Russian Soyuz Blok-I (Russia 20.7% generated)** ground tracks crossing the tropics. **The inverse is Russia:** it *generated* 20.7% of the risk yet its capital Moscow has the **lowest per-capita exposure (ε = 0.0005) in the entire table** — the largest generated-minus-borne gap in the ledger (M4 §3b).

This reproduces the published Global-South inequity: rocket bodies are **~3× more likely to land at equatorial than northern latitudes** (Byers, Wright & Boley 2022; M4 §3c reproduces it bottom-up at ε(Jakarta)/ε(Moscow) = 3.44). **The states with the loudest standing to demand a binding standard at COPUOS are exactly those with no launch program of their own** — Indonesia, Bangladesh, Brazil, Pakistan, Nigeria — and the families to name in that demand are **Soyuz Blok-I and the CZ-3B/CZ-2F/CZ-2C Chinese GTO and LEO stages**.

---

## 4. Feasibility note — the fix is already routine (named compliant family + source)

**Controlled deorbit of an upper stage is not a research problem; it is the standard disposal mode for Falcon 9 — the #3 risk family in this very ledger.** After payload separation, the Falcon 9 second stage performs a controlled retrograde **deorbit burn** that targets a destructive reentry over a remote, pre-notified area of the South Pacific (Point Nemo region), with propellant passivation to prevent on-orbit explosion. SpaceX states this is the planned, nominal procedure: after the September 2024 Crew-9 launch, *"Falcon 9's second stage was disposed in the ocean as planned, but experienced an off-nominal deorbit burn … the second stage safely landed in the ocean, but outside of the targeted area"* ([SpaceX, 28 Sep 2024](https://x.com/SpaceX/status/1840245345118498987); coverage: [SpaceNews, 2024-09-29](https://spacenews.com/spacex-pauses-falcon-9-launches-after-upper-stage-deorbit-anomaly/); [Spaceflight Now, 2024-09-29](https://spaceflightnow.com/2024/09/29/spacex-grounds-its-falcon-rocket-fleet-after-upper-stage-misfire/)). That the *exception* — a burn landing outside the target box — grounded the fleet shows controlled disposal is the **expected baseline**, not a stretch goal.

This is corroborated inside the ledger: **M2 records 13 controlled (status `D`) Falcon 9 second stages** alongside the 35 uncontrolled ones (M2 §"Controlled"). The same hardware, same operator, does both. The 35 uncontrolled Falcon 9 stages (mostly early high-energy / GTO missions) are therefore **uncontrolled by exception, not by incapacity** (M3 §3 note 3).

**Additional in-fleet proof points (M2, status `DSO`):** the **Centaur** upper stage, the **CZ-5 second stage**, and the **Ariane 5 ESC** stage are all disposed via an active burn to a graveyard / Point-Nemo / heliocentric trajectory (M2 §classification rule). So at least four families in the ledger already demonstrate controlled disposal. The standard being asked of Soyuz Blok-I, CZ-3B, CZ-2F and the rest is **a thing the fleet already does routinely**.

---

## 5. Limitations & counter-evidence, and what would change the ranking

### 5a. Numbered limitations (carried from M1–M4; the ranking is the deliverable, not the absolute magnitudes)

1. **Absolute risk is order-of-magnitude; the *ranking* is the robust product (M3 Lim. 1).** Every ΣE_a here inherits M3's casualty-area (A_c) uncertainty, which scales the output linearly and is only constrained to ±a factor of ~2–3. The numbers in §2 are the M3 figures *unchanged*; read them as an ordering and a relative apportionment, not as precise expected body counts.

2. **Compliance status is family-level, inferred from M2's control labels.** "Non-compliant" means *every* M2 instance of the family was uncontrolled (status `R`); "demonstrated-capable" means M2 also shows controlled instances. This is a fair status flag for a standard-setting target list, but it is not a per-launch compliance audit — a given operator may have changed practice mid-decade (e.g. SpaceX's shift toward routine deorbit), which the family-level flag blurs.

3. **The China/Russia split (hence the rank of CZ vs Soyuz families) is the quantity most sensitive to method (M3 Lim. 4, §4).** This ledger's 50.2% China / 20.7% Russia sits below Pardini & Anselmo's published ~62% / ~18% because of the mass^(2/3) casualty-area law and the 2013–2024 window. A steeper A_c–mass law would push the heavy Chinese stages (CZ-5B, CZ-3B) up the list. The rank *ordering* (Soyuz Blok-I and CZ-3B at the top, Falcon 9 third) is robust; the exact gaps between them are not.

4. **Exposure is a latitude-band likelihood, not a per-country impact probability (M4 Lim. 1).** The §3 over-exposed-states ranking resolves risk by latitude × population only; it ignores longitude, decay-day geometry, and that ~71% of any latitude band is ocean. It answers "which populations sit under the over-flown bands," not "the impact probability on this city this decade."

5. **No realised casualty to date (M1/M3/M4 Lim. 6).** No confirmed human casualty has resulted from any of the 559 uncontrolled reentries. The entire docket is *expected* risk measured against the agreed 1-in-10,000 line (77.8% of stages breach it, M3 §1c), not a body count. A reader can fairly argue the realised harm is zero so far; the counter is that the standard is a published, pre-agreed line and the aviation-collision channel is rising (Aerospace Corp.; *Sci. Rep.* 2024, M3 Lim. 6).

6. **Window and snapshot dependence (M3 Lim. 7).** Shares are computed on M2's 2013–2024 GCAT snapshot. The 456 still-in-orbit bodies (e.g. nine 6,000 kg CZ-6A second stages, M2 §4) are future uncontrolled reentries not yet scored; as they decay, China's share — and CZ-6A's rank — will rise. A different decade window shifts the China/Russia/USA split by several points (the Pardini 2010–2022 vs this 2013–2024 comparison shows this directly).

### 5b. What would change the ranking (≥2 conditions; four given)

1. **A steeper casualty-area–mass law (or per-object demise simulation).** If A_c rose faster than mass^(2/3) — as Pardini & Anselmo's per-object demise modelling effectively implies — the heaviest stages (**CZ-5B**, the 21,600 kg core; **CZ-3B**; Zenit; Proton-M) would gain risk share and climb, plausibly lifting CZ-5B above several mid-table families and pushing China's share back toward the published ~62% (M3 Lim. 4, §4). The Falcon 9 / Soyuz ordering near the top is less sensitive because those are mid-mass stages.

2. **Per-body (not per-family) inclination.** Risk here uses one characteristic inclination per family (M3 Lim. 3). Resolving each body's actual GCAT inclination would re-weight the *exported-risk* geography in §3 (sharpening the turning-latitude peaks over Dhaka/Karachi) and could re-rank low-vs-high-inclination families at the margin, though M3 notes it would not move the family/state aggregates materially.

3. **Extending the window or adding the still-in-orbit backlog.** Scoring the 456 still-in-orbit bodies as they decay (M3 Lim. 7) would add the **CZ-6A** second stages and other recent heavy Chinese hardware to the target list, raising China's share and likely inserting CZ-6A into the top 10. Conversely, restricting to 2010–2022 (Pardini's window) would drop the 2023–2024 Soyuz/Indian/Japanese surge and *raise* China's relative dominance.

4. **A surviving-mass / dense-component correction.** E_a should scale with *ground-reaching* mass, not total dry mass (M3 Lim. 5). Families with high dense-component fractions that survive reentry — **CZ-5B** (large engines, COPVs), heavy **Centaur**/Proton hardware — are likely *under*-weighted here; a demise-fraction correction would push them up and could move CZ-5B from rank 7 toward the top tier on a realised-hazard basis, reinforcing its already-highest per-body standing.

**None of these conditions overturns the headline:** under every plausible variation, **a small number of heavy uncontrolled Chinese and Russian upper stages plus the early Falcon 9 stages dominate the exported casualty risk; the large majority of uncontrolled stages breach the agreed 1-in-10,000 line; the controlled-deorbit fix is already routine for at least one top-contributing family (Falcon 9); and the burden falls on Global-South states that generated none of it.** The variations move *which* heavy family is #1 and the exact China/Russia gap — not the existence of a short, named, fixable target list.

---

## Source list (dated)

- **M3 — Per-reentry casualty risk and accountability attribution** (this problem), `artifacts/2026-06-26-m3-per-reentry-risk-and-attribution.md`. — every risk figure in §1–§2: per-family ΣE_a and fleet-share (Table 2 §3b), per-state share (§3a), per-operator (§3c), 77.8% threshold-exceedance (§1c), fleet ΣE_a = 0.2080, CZ-5B highest-per-body note (§3).
- **M4 — Exported-risk overlay by country** (this problem), `artifacts/2026-06-27-m4-exported-risk-overlay-by-country.md`. — §3 over-exposed states: borne exposure E_c (§2), generated-vs-borne (§3a/b), Global-South ~3× finding (§3c).
- **M2 — Per-rocket-body classified inventory** (this problem), `artifacts/2026-06-26-m2-per-rocket-body-classified-inventory.md`. — §2/§4 compliance labels: 559 uncontrolled (`R`), 58 controlled (`D`/`DSO`) including 13 Falcon 9 + 1 Falcon Heavy controlled second stages; DSO disposal for Centaur / CZ-5 S2 / Ariane 5 ESC.
- **M1 — Methodology and Source Register** (this problem), `artifacts/2026-06-26-m1-methodology-source-register.md`, §B–C. — the 1×10⁻⁴ threshold (NASA-STD-8719.14, adopted US/France/Japan/ESA) and the casualty-risk model.
- SpaceX, post-Crew-9 second-stage disposal statement (28 Sep 2024). https://x.com/SpaceX/status/1840245345118498987. — Falcon 9 second stage "disposed in the ocean as planned" via a deorbit burn; the controlled-deorbit proof-of-concept is the nominal procedure.
- SpaceNews, "SpaceX pauses Falcon 9 launches after upper stage deorbit anomaly" (2024-09-29). https://spacenews.com/spacex-pauses-falcon-9-launches-after-upper-stage-deorbit-anomaly/. — corroborates routine controlled deorbit; an off-nominal burn grounded the fleet (the exception proves the baseline).
- Spaceflight Now, "SpaceX grounds its Falcon rocket fleet after upper stage misfire" (2024-09-29). https://spaceflightnow.com/2024/09/29/spacex-grounds-its-falcon-rocket-fleet-after-upper-stage-misfire/. — same event; targeted deorbit over remote ocean is the standard disposal.
- Byers, M., Wright, E., Boley, A. "Unnecessary risks created by uncontrolled rocket reentries." *Nature Astronomy* 6, 1093–1097 (2022). DOI [10.1038/s41550-022-01718-8](https://doi.org/10.1038/s41550-022-01718-8); arXiv:2210.02188. — the Global-South ~3× inequity underlying §3 (via M4 §3c).
- Pardini, C., Anselmo, L. *J. Space Safety Engineering* 11(2):181–191 (2024). https://www.sciencedirect.com/science/article/pii/S2468896724000077; CNR focus https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites. — the published ~62% CN / ~18% RU / ~14% US casualty-risk split and ~84% threshold-exceedance (the M3 reconciliation comparator cited in §5).
