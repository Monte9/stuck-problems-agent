# M1 — Methodology and Source Register

**Problem:** Uncontrolled rocket-body reentries — building the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M1 (analytic backbone for M2–M5).
**Author:** generator routine | **Date:** 2026-06-26.

This document defines, for the whole downstream ledger: (A) the open data sources and which field each supplies; (B) the casualty-risk model, written out with every variable defined and cited; (C) the controlled-vs-uncontrolled classification rule with its observable signals and a default rule for ambiguous cases; and (D) the scope (study window, unit of analysis) plus a numbered limitations list. M2–M5 must name this document as their methodological input and may not silently introduce a new method.

---

## A. Data-source register

Each row names an open catalog/dataset, a working URL, and the **single downstream field** it supplies to the ledger. URLs were resolved on 2026-06-26.

| # | Source | URL | Access | Downstream field it supplies |
|---|--------|-----|--------|------------------------------|
| 1 | **GCAT — General Catalog of Artificial Space Objects** (Jonathan McDowell), CC-BY, v1.8.0 updated 2026-06-23 | https://planet4589.org/space/gcat/ | Open download (TSV) | **Primary spine of the M2 inventory:** object type (`R`/`R/B` = rocket stage vs payload), COSPAR/NORAD ID, launch date, decay/reentry date, orbital inclination, and dry mass where listed. Cited per its CC-BY licence. |
| 2 | **Space-Track SATCAT** (US Space Force, 18th/19th Space Defense Squadron) | https://www.space-track.org/ | Free registration required (login-gated; not anonymously fetchable — see Limitation 5) | Cross-check of NORAD ID, international designator, object type (`R/B`), launch and **decay/reentry date & status** ("still in orbit" vs decayed). |
| 3 | **CelesTrak SATCAT** (T.S. Kelso) | https://celestrak.org/satcat/search.php | Open | Secondary, login-free cross-check for reentry date/status and object type when Space-Track access is unavailable. |
| 4 | **GPWv4 — Gridded Population of the World v4.11, Population Density** (NASA SEDAC / CIESIN Columbia), DOI 10.7927/H4NP22DQ | https://doi.org/10.7927/H4NP22DQ — download: https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-density/data-download | Open (NASA Earthdata login for bulk) | **Exposure weighting:** population density ρ(lat) by latitude band, the term multiplied against the ground-track weighting function in the casualty model (Section B). Same dataset used by Byers et al. 2022. |
| 5 | **GPWv4 — Population Count v4.11** (NASA SEDAC / CIESIN), DOI 10.7927/H4JW8BX5 | https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count-rev11/data-download | Open | Alternative exposure input (counts per cell) for the M4 country/city overlay where density is not the convenient unit. |
| 6 | **OurAirports open data** (David Megginson; airport data public domain / DAFIF) | https://ourairports.com/data/ — direct CSV: https://davidmegginson.github.io/ourairports-data/airports.csv | Open (public domain) | **Aviation-hazard overlay for M4:** airport locations (lat/lon, type, scheduled-service flag) to weight reentry ground tracks against busy airspace. |
| 7 | **ESA DISCOS — Database and Information System Characterising Objects in Space** | https://discosweb.esoc.esa.int/ | Free account (API) | Cross-reference for **per-body dry/reentry mass** and vehicle-family attribution where GCAT mass is blank. |
| 8 | **NASA-STD-8719.14C — Process for Limiting Orbital Debris** (agency standard) | https://standards.nasa.gov/standard/OSMA/NASA-STD-871914 (record: https://standards.globalspec.com/std/13301450/nasa-std-8719-14) | Open (record); PDF via NASA standards portal | **Casualty-area definition and the 1-in-10,000 (1×10⁻⁴) threshold** that defines compliance (Section B). |
| 9 | **FAA AC 431.35-2A — Expected Casualty Calculations for Commercial Space Launch and Reentry** | https://www.faa.gov/about/office_org/headquarters_offices/ast/licenses_permits/media/Ac4311fn.pdf | Open (PDF; 403 on automated fetch this run — see Limitation 5) | Regulatory-grade statement of the **expected-casualty Eₐ formula** (casualty area × population density × impact probability). |

**Note on mass references (downstream M2/M3 input):** GCAT (1) and DISCOS (7) are the primary per-body dry-mass sources. Where neither lists a value, M2 will fall back to **published vehicle-family dry-mass references** (e.g. manufacturer/agency spec sheets and the masses tabulated in Pardini & Anselmo 2024, S2468896724000077) and flag the row as estimated. Every mass cell in M2 must carry its own source per the M2 done-criteria.

---

## B. Casualty-risk model (adopted formula, written out)

The ledger adopts the standard published **expected-casualties / casualty-area** approach used across NASA, FAA, ESA and The Aerospace Corporation reentry-risk work. It is stated below at two levels: (B1) the per-reentry expected-casualty definition (NASA/FAA form, used for the per-body 1-in-10,000 compliance flag in M3), and (B2) the latitude-resolved casualty-expectation form (Byers/Boley/Pardini form, used for ground-track-and-population exposure in M3/M4).

### B0. Casualty area Aᶜ (the common input)

The **debris casualty area** is the total ground area within which a person would be struck by a lethal fragment, summed over all fragments surviving to the ground:

> **Aᶜ = Σᵢ ( √Aₕ + √Aᵢ )²**

- **Aᶜ** — total debris casualty area (m²).
- **Aᵢ** — projected cross-sectional area of the *i*-th surviving fragment (m²).
- **Aₕ** — projected cross-sectional area of a standing human; modelled as a 0.36 m² circle, tangential to the debris. (NASA-STD-8719.14 / NSS 1740.14; the 0.36 m² value is explicitly reaffirmed in Byers, Wright & Boley 2022.)
- The sum runs over the *n* fragments that survive atmospheric demise (fragments with impact kinetic energy ≥ 15 J are conventionally counted as lethal).

*Sources:* NASA-STD-8719.14 casualty-area definition Aᶜ = Σ(√Aₕ + √Aᵢ)² with Aₕ = 0.36 m² (https://orbitaldebris.jsc.nasa.gov/reentry/orsat.html; standard record https://standards.globalspec.com/std/13301450/nasa-std-8719-14); the 0.36 m² human circle restated verbatim in Byers, Wright & Boley, *Nature Astronomy* 6, 1093–1097 (2022), arXiv:2210.02188 (§"Casualty expectation modelling … modelled as a 0.36 m² circle").

### B1. Per-reentry expected casualties Eₐ (NASA/FAA compliance form)

For the per-body compliance flag (above/below the threshold), expected casualties are casualty area weighted by the population density along the possible impact footprint:

> **Eₐ = Σ_k P_impact(k) · ρ_pop(k) · Aᶜ**

- **Eₐ** — expected number of casualties for the reentry event (dimensionless probability for Eₐ ≪ 1).
- **P_impact(k)** — probability that debris impacts ground cell *k* (from the reentry footprint / ground-track distribution; for an uncontrolled reentry this is governed by orbital inclination, see B2).
- **ρ_pop(k)** — population density in cell *k* (persons · m⁻²), from GPWv4 (sources 4/5).
- **Aᶜ** — debris casualty area from B0 (m²).

The **compliance threshold** is the published industry standard adopted by the US, France, Japan and ESA: an uncontrolled reentry should have **Eₐ < 1×10⁻⁴ (1-in-10,000)**; above that, a controlled deorbit is required.

*Sources:* FAA AC 431.35-2A "Expected Casualty Calculations for Commercial Space Launch and Reentry" (https://www.faa.gov/about/office_org/headquarters_offices/ast/licenses_permits/media/Ac4311fn.pdf); NASA-STD-8719.14 1×10⁻⁴ threshold (https://orbitaldebris.jsc.nasa.gov/reentry/orsat.html). The 1-in-10,000 threshold and its adoption by the US/France/Japan/ESA is summarised in Pardini & Anselmo, "The risk of casualties from the uncontrolled re-entry of spacecraft and orbital stages," *Journal of Space Safety Engineering* 11(2):181–191 (2024) (https://www.sciencedirect.com/science/article/pii/S2468896724000077).

### B2. Latitude-resolved casualty expectation (Byers/Boley form, used for exposure)

Because an abandoned rocket body's reentry latitude is set by its **orbital inclination**, the impact-probability term P_impact is, for an uncontrolled body, a **latitude weighting function** w(φ): the fraction of orbital time the body spends over latitude φ. For inclination *i*, w(φ) is zero for |φ| > i, peaks near |φ| = i, and is U-shaped between the peaks; a body at i = 0° gives w concentrated at the equator, a polar (i = 90°) body gives w ≈ constant over all latitudes. w is normalised so Σ_φ w(φ) = 1 per body. The casualty expectation per unit casualty area is then:

> **CE = Σ_φ w(φ) · ρ_pop(φ)**  ,  and per reentry  **Eₐ ≈ CE · Aᶜ**

- **CE** — casualty expectation per m² of casualty area (m⁻²); the quantity Byers et al. report (e.g. ≈ 0.01 m⁻² for the long-lived ≤600 km-perigee population on the 2020 world population).
- **w(φ)** — normalised latitude weighting function from orbital inclination (defined above).
- **ρ_pop(φ)** — population density at latitude φ (GPWv4).
- Multiplying CE by an assumed casualty area (Byers et al. use a conservative Aᶜ = 10 m², noting real rocket-body casualty areas often run 20–40 m²) yields per-reentry expected casualties; summing over a fleet yields the ~10%-chance-of-one-or-more-casualties-per-decade headline figure.

*Sources:* Byers, Wright & Boley, "Unnecessary risks created by uncontrolled rocket reentries," *Nature Astronomy* 6, 1093–1097 (2022), DOI 10.1038/s41550-022-01718-8; open versions arXiv:2210.02188 and AMOS 2022 (https://amostech.com/TechnicalPapers/2022/SSA-SDA/Byers.pdf). The latitude weighting function, the CE = Σ w(φ)·ρ(φ) construction, the 10 m² casualty-area assumption, and the "~10% chance of one or more casualties over a decade" are stated in §4–5 of that paper.

**Which form is used where.** M3 produces the per-body **Eₐ and 1-in-10,000 flag** using B1 (with B0 casualty area) and uses B2 to make P_impact tractable from inclination + GPWv4. M4 uses the B2 latitude weighting function directly to build the country/city exposure overlay. Both must show or make traceable the input values (Aᶜ, inclination, ρ_pop) per their done-criteria.

---

## C. Controlled-vs-uncontrolled classification rule

Each rocket body in M2 is labelled **controlled**, **uncontrolled**, or **still-in-orbit** (no reentry yet). The label is assigned from observable, catalog-derivable signals, in priority order.

### Signals indicating **CONTROLLED**
1. **Operator-declared controlled reentry** — public statement, mission press kit, or agency record that the stage was deliberately deorbited (e.g. Falcon 9 second-stage disposal burns).
2. **Targeted-ocean (SPOUA / "Point Nemo") disposal** — reentry footprint over the South Pacific Ocean Uninhabited Area, the standard graveyard corridor; reentry over SPOUA is strong evidence of a deliberate burn.
3. **Propulsive / restartable stage with retained-fuel disposal capability** — a stage design known to perform deorbit burns (re-ignitable engine + reserve propellant), where the catalog shows a short, targeted descent consistent with a commanded burn.

### Signals indicating **UNCONTROLLED**
4. **Time-in-orbit before decay ≥ the dwell threshold** — the primary, catalog-derivable signal. Following Byers et al. 2022, a rocket-body reentry is treated as **uncontrolled if the span between launch date and reentry date is ≥ 7 days** (the authors note 3–7-day cutoffs give comparable results; 7 days is the conservative choice, classifying ≈70% of historic deorbits as uncontrolled). A deliberate deorbit is normally executed within minutes-to-hours of payload separation, not days/weeks/years later.
5. **No disposal capability** — spent stage with no re-ignitable propulsion or no reserve propellant (vehicle-family attribute); cannot perform a controlled deorbit.
6. **Random / non-targeted decay** — natural orbital decay with a reentry footprint not aligned to any ocean disposal zone.

### Default rule for ambiguous / unknown cases
- If launch and reentry dates are both known: apply signal 4 (the **≥7-day rule**) as the deciding test. < 7 days → candidate controlled (confirm with signals 1–3); ≥ 7 days → **uncontrolled**.
- If the body has **not yet reentered** ("still in orbit"): label **still-in-orbit**; for risk purposes it is treated as a *future uncontrolled* body **only if** it has no disposal capability and a perigee low enough to decay within the modelled horizon (Byers et al. use perigee ≤ 600 km as the proxy for "will reasonably reenter"). Bodies above that are carried but flagged as long-horizon.
- If control status genuinely cannot be resolved from any signal above, the body is **defaulted to UNCONTROLLED** and explicitly flagged `control_basis = default-uncontrolled`. Rationale: this is the conservative, risk-inclusive choice consistent with the literature's ~70% uncontrolled baseline, and it never lets an unverified stage escape the ledger by assumption. The count of default-uncontrolled rows must be reported in M2 so the assumption's weight is visible.

*Sources:* the ≥7-day launch-to-reentry uncontrolled definition and the ~70% uncontrolled fraction: Byers, Wright & Boley 2022, arXiv:2210.02188 §4. SPOUA/Point Nemo as the targeted ocean disposal zone and Falcon 9 second-stage controlled deorbit as the in-fleet proof-of-concept: Pardini & Anselmo 2024 (https://www.sciencedirect.com/science/article/pii/S2468896724000077), which reports controlled reentries were ~62% of returned mass in 2019–2023, ~31% from Falcon 9 second stages alone. Perigee ≤ 600 km long-lived-population proxy: Byers et al. 2022 §5.

---

## D. Scope

### Primary study window: **1 January 2013 – 31 December 2024** (≈12 years, "the past decade")
- **Justification.** The brief and decision-grade audience ("abandoned rocket bodies of the past decade") motivate a ~decade window ending at the most recent complete calendar year (2024). This window (i) fully contains the **2010–2022** window of Pardini & Anselmo 2024 from 2013 onward and the **2019–2023** returned-mass window of S2468896724000077, so both can be used as published sanity checks in M2/M3 against overlapping sub-periods, and (ii) captures the megaconstellation transition (post-2019) that drives the Aerospace aviation-hazard projections. A secondary reconciliation sub-window of **2010–2022** is retained explicitly to line up row-for-row with Pardini & Anselmo's 84%/80% and 62%/18%/14% attribution figures.
- M2 will report counts for the full 2013–2024 window and separately for the 2010–2022 and 2019–2023 reconciliation sub-windows.

### Unit of analysis: **one abandoned rocket body / upper stage**
- **Included:** orbital rocket stages — upper stages and core/booster stages that reached orbit and were abandoned (GCAT object type `R`/`R/B`; Space-Track `R/B`). One row per catalogued rocket-body object.
- **Excluded:**
  - **Payloads / satellites** (the ledger is about the *launcher's* abandoned hardware; satellite reentry risk is a related but distinct accountability question and is out of scope for the per-vehicle-family compliance ledger). The casualty model in B applies equally to satellites, but attribution to *launch vehicle families* requires the unit be the stage.
  - **Suborbital stages** that never achieved orbit (no orbital reentry risk of the kind modelled).
  - **Mission-related debris and fragmentation debris** (adapters, covers, explosion fragments) — not whole abandoned stages.
  - **Stages that performed an immediate controlled deorbit** are *included as rows* but labelled `controlled` (they are the compliance baseline, not the hazard).
- Inclusion/exclusion counts must reconcile in M2 (included + excluded = catalog total for the window, with reasons), per the M2 done-criteria.

---

## Limitations & counter-evidence

1. **The ≥7-day proxy mislabels some bodies.** Using launch-to-reentry span as the controlled/uncontrolled discriminator is a catalog-derivable heuristic, not ground truth. It can misclassify (a) deliberately *delayed* controlled deorbits (rare, but they exist) as uncontrolled, and (b) very-low-orbit stages that decay naturally within 7 days as controlled. Byers et al. note 3–7-day cutoffs give comparable aggregate results, but individual rows carry error. Mitigation: signals 1–3 (operator declaration, SPOUA footprint, disposal capability) override the time test where available, and the default-uncontrolled count is reported.

2. **Casualty area Aᶜ is the dominant uncertainty in the risk numbers.** The model's output scales linearly with Aᶜ, yet per-body Aᶜ requires fragment-level demise simulation (ORSAT-class tools) not available in open catalogs. The ledger will use published per-family casualty-area estimates and conservative defaults (Byers et al.'s 10 m² is acknowledged by the authors as likely an *under*estimate; real bodies reach 20–40 m²). Absolute Eₐ values are therefore order-of-magnitude; **relative** ranking across vehicle families (the docket's actual deliverable) is far more robust than any single absolute figure. NASA itself notes statistical uncertainty "makes additional refinement of the equation" of limited value (Byers et al. 2022, quoting the standard).

3. **Ground-track probability is reduced to a latitude weighting function.** The B2 model resolves exposure by latitude band from inclination only; it does not capture longitudinal structure, Earth-rotation phasing of the final orbit, or the specific decay-day geometry. This is the standard simplification in the cited literature but means M4's country/city exposure is a *latitude-band likelihood*, not a true per-country impact probability. GPWv4 grid resolution (30 arc-second native, often aggregated to coarser bands) further smooths sub-national exposure.

4. **Mass and control-status coverage is incomplete and source-dependent.** GCAT/DISCOS leave dry mass blank for some stages, especially older Soviet/Chinese hardware; control status is rarely declared by non-Western operators. Rows relying on family-level mass estimates or the default-uncontrolled rule will be flagged, but they inject systematic uncertainty precisely into the high-risk Chinese/Russian families that dominate the attribution (per Pardini & Anselmo's 62%/18% finding) — i.e. uncertainty is correlated with the bodies that matter most.

5. **Two key sources are access-gated, not openly fetchable.** Space-Track SATCAT (source 2) requires free registration and is login-gated (anonymous fetch returns no content), and the FAA AC PDF (source 9) returned HTTP 403 to automated retrieval on 2026-06-26. Both are genuinely public, but downstream milestones relying on them must authenticate manually; CelesTrak (source 3) and GCAT (source 1) provide login-free substitutes for the reentry-status field, and the FAA formula is independently corroborated by the NASA-standard and Byers/Pardini citations above.

6. **Counter-evidence on the headline harm.** No confirmed human casualty from a rocket-body reentry has yet occurred (Byers et al. explicitly note "no such event occurred, or at least was reported"). The case rests on *expected* risk exceeding a published threshold and on near-miss/property-damage events, not on a body count. A reader could argue the realised risk is acceptably low; the ledger's response is that the published 1-in-10,000 standard is precisely the agreed line, that ~80–84% of uncontrolled stages exceed it (Pardini & Anselmo 2024), and that the aviation-collision probability is rising (~1-in-125,000/yr in 2021 toward 7×10⁻⁴/yr by 2035, Aerospace Corp.; 26% annual chance of a busy-airspace closure for the northeastern US, *Sci. Rep.* 2024, s41598-024-84001-2) — but the absence of a realised casualty is a fair and stated counterpoint.

---

## Source list (dated)

- Byers, M., Wright, E., Boley, A. "Unnecessary risks created by uncontrolled rocket reentries." *Nature Astronomy* 6, 1093–1097 (2022). DOI 10.1038/s41550-022-01718-8. Open: arXiv:2210.02188 (https://arxiv.org/abs/2210.02188); AMOS 2022 (https://amostech.com/TechnicalPapers/2022/SSA-SDA/Byers.pdf). — risk formula, 0.36 m² human area, ≥7-day rule, latitude weighting, ~10%/decade, latitude inequity (Jakarta/Dhaka/Lagos/Bogotá/Mexico City ≥3× Washington/NY/Beijing/Moscow).
- Pardini, C., Anselmo, L. "The risk of casualties from the uncontrolled re-entry of spacecraft and orbital stages." *Journal of Space Safety Engineering* 11(2):181–191 (2024). https://www.sciencedirect.com/science/article/pii/S2468896724000077. — 1-in-10,000 threshold & its adopters; ~80% (2021) of orbital-stage uncontrolled reentries exceeding threshold; 62% Chinese / 18% Russian-Soviet / 14% American risk split; ~62% of 2019–2023 returned mass controlled, ~31% from Falcon 9 second stages.
- CNR research focus page summarising Pardini & Anselmo (2024-era). https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites. — 84% exceeding threshold (2010–2022) and the 62%/18%/14% attribution.
- "Airspace closures due to reentering space objects." *Scientific Reports* 14 (2024), s41598-024-84001-2. https://www.nature.com/articles/s41598-024-84001-2. — 26% annual busy-airspace chance (NE US); 128 rocket bodies abandoned in 2023; ~2300 rocket bodies in orbit (June 2024).
- "Uncontrolled re-entries of space objects and aviation safety" (Aerospace Corp. aviation-collision modelling). *Acta Astronautica* (2024), S0094576524002807. https://www.sciencedirect.com/science/article/pii/S0094576524002807. — fatal-collision probability ~8×10⁻⁶/yr (2021) → 7×10⁻⁴/yr by 2035 with megaconstellations.
- NASA-STD-8719.14 "Process for Limiting Orbital Debris" — casualty-area Aᶜ = Σ(√Aₕ+√Aᵢ)², Aₕ=0.36 m², 1×10⁻⁴ threshold. https://orbitaldebris.jsc.nasa.gov/reentry/orsat.html ; record https://standards.globalspec.com/std/13301450/nasa-std-8719-14.
- FAA AC 431.35-2A "Expected Casualty Calculations for Commercial Space Launch and Reentry." https://www.faa.gov/about/office_org/headquarters_offices/ast/licenses_permits/media/Ac4311fn.pdf.
- GCAT (McDowell) https://planet4589.org/space/gcat/ (v1.8.0, 2026-06-23); Space-Track https://www.space-track.org/; CelesTrak SATCAT https://celestrak.org/satcat/search.php; GPWv4 density DOI 10.7927/H4NP22DQ (https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-density/data-download); GPWv4 count DOI 10.7927/H4JW8BX5; OurAirports https://ourairports.com/data/ (CSV https://davidmegginson.github.io/ourairports-data/airports.csv); ESA DISCOS https://discosweb.esoc.esa.int/.
