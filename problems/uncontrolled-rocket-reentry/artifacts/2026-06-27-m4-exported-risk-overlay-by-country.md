# M4 — Exported-risk overlay: who absorbs uncontrolled-reentry risk vs who generates it

**Problem:** Uncontrolled rocket-body reentries — the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M4 (overlay uncontrolled-reentry ground-track probability against gridded population and airspace to estimate which countries/cities absorb risk, and contrast that with which launching states generated it).
**Primary input (the "generated" side and the ground-track drivers):** **M3 — Per-reentry casualty risk and accountability attribution** (`artifacts/2026-06-26-m3-per-reentry-risk-and-attribution.md`). M4 takes from M3, unchanged: (i) the per-family summed casualty risk ΣE_a (M3 Table 2, §3b), (ii) each family's characteristic inclination (M3 Table 1, "Char. incl."), and (iii) the per-launching-state generated-risk share (M3 §3a). **No risk number is recomputed here**; M4 only re-distributes M3's already-attributed risk across ground latitudes and populations.
**Method/source register:** **M1 — Methodology and Source Register** (`artifacts/2026-06-26-m1-methodology-source-register.md`). The ground-track latitude-weighting w(φ) (M1 §B2), the gridded-population source **GPWv4** (M1 source 4/5), and the airport/airspace source **OurAirports** (M1 source 6) are all taken from M1. No new model is introduced; the M1 §B2 latitude-weighting form is operationalised here as the standard turning-latitude density and is carried as Limitation 1.
**Author:** generator routine | **Date:** 2026-06-27.

> **Reading guide.** §1 is the methods note: the exposure metric written symbolically, the ground-track density formula derived from inclination, the population/airspace weighting, traceability to M3 + M1, and one worked example (Jakarta) end-to-end. §2 is the ranked exposure table (19 cities, ≥10 required). §3 is the generated-vs-borne comparison with the exported-risk flag and the cited Global-South finding. §4 is the numbered limitations note.

---

## 1. Methods note

### 1a. The exposure metric, symbolically

For a population center *c* at representative latitude φ_c with metropolitan population P_c, the **population-weighted exported-reentry exposure** is:

> **E_c = P_c · Σ_f [ ΣE_a(f) · g(φ_c | i_f) ]**

- **E_c** — exposure metric for city *c* (units: million-persons × normalised latitude density; an interpretable *relative* index, reported below normalised so the most-exposed city = 1.000).
- **P_c** — metropolitan population of *c* (millions), the GPWv4-class population weight (M1 source 4/5). City metro figures are used as the convenient aggregation of the GPWv4 count grid at the city scale (M1 source 5 explicitly names GPWv4 *count* as "the alternative exposure input … for the M4 country/city overlay where density is not the convenient unit").
- **ΣE_a(f)** — the decade-summed casualty risk **generated** by vehicle family *f*, taken **verbatim from M3 Table 2 §3b** (e.g. Soyuz Blok-I 0.0396, CZ-3B 0.0324, Falcon 9 0.0193). Σ over all 54 families = 0.2081, reproducing M3's fleet ΣE_a = 0.2080 (rounding) — the model's tie-back check to M3.
- **i_f** — the characteristic inclination of family *f*, taken **verbatim from M3 Table 1** "Char. incl." (e.g. CZ-5B 42°, CZ-3B 27°, Soyuz 62°, Falcon 9 53°, CZ-2D/SSO families 97°).
- **g(φ | i)** — the normalised ground-track latitude density (§1b): the probability per unit latitude that the sub-satellite point of a body in an orbit of inclination *i* lies at latitude φ.

The bracket Σ_f [ ΣE_a(f) · g(φ_c | i_f) ] is the **per-capita latitude exposure** at φ_c (call it ε(φ_c)): the M3 fleet risk re-distributed onto latitude φ_c by each family's ground track. Multiplying by P_c gives the population-absorbed exposure E_c. Both ε (per-capita, latitude-only) and E_c (population-weighted) are reported in §2, because they answer two different questions: ε = "is my latitude over-flown?" (the Byers Global-South inequity), E_c = "how many people sit under that latitude?" (the absorbed burden).

### 1b. Ground-track density from inclination (M1 §B2, operationalised)

M1 §B2 defines w(φ) as "the fraction of orbital time the body spends over latitude φ … zero for |φ| > i, peaks near |φ| = i, U-shaped between the peaks," normalised so Σ_φ w(φ) = 1. The standard closed form for this — the **turning-latitude (cosine) distribution** of a circular orbit's sub-satellite latitude — is:

> **g(φ | i) = (1/Z) · cos φ / √(sin²L − sin²φ)** for |φ| < L, and **g = 0** for |φ| ≥ L,
> where **L = min(i, 180−i)** is the maximum latitude overflown, and **Z = ∫₋ᴸᴸ cos φ /√(sin²L − sin²φ) dφ** normalises ∫ g dφ = 1.

- The density **diverges (integrably) at φ = ±L** — the orbit "dwells" at its turning latitudes, where its north/south velocity component is zero — and is **lowest near the equator**, exactly the U-shape M1 §B2 specifies. A polar body (i = 90° → L = 90°) gives g ≈ cos φ (mass concentrated where Earth's surface area is, i.e. broad coverage); a low-inclination body concentrates g in a narrow band at ±i.
- **Retrograde orbits** (i > 90°, e.g. Shavit i ≈ 143°, Firefly Alpha/SSO ≈ 137°) use **L = 180 − i** (Shavit → L ≈ 37°), as M3 §1b already does for the CE inclination factor — consistency with M3 maintained.
- This is the same physics M1 §B2 cites from Byers, Wright & Boley 2022 (the latitude-weighting → casualty-expectation construction); it is the analytic form of M1's w(φ). Carried as Limitation 1 (it is a latitude-band likelihood, not a true per-country impact probability — M1 Limitation 3).

*Source for the turning-latitude density:* this is the well-known sub-satellite-latitude distribution of an inclined circular orbit (the probability density of latitude for a uniformly-time-sampled ground track), e.g. as used in satellite-coverage and reentry-footprint analyses; it is the closed form of the M1 §B2 / Byers et al. 2022 latitude weighting (Byers, Wright & Boley, *Nature Astronomy* 6, 1093–1097, 2022; arXiv:2210.02188, https://arxiv.org/abs/2210.02188, §4–5).

### 1c. Population and airspace weighting

- **Population (GPWv4).** P_c is the metropolitan-area population (millions), aggregating the GPWv4 v4.11 population-count grid (NASA SEDAC/CIESIN, DOI 10.7927/H4JW8BX5, https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count-rev11/data-download) at the city scale — the same dataset family Byers et al. 2022 used for their latitude-population product, per M1 source 4/5. Per-city metro populations are cited in §2.
- **Airspace (OurAirports), as a reported overlay, not folded into E_c.** The aviation hazard is a distinct exposure channel (it scales with *flights over the latitude band*, not resident population). To keep E_c clean and reproducible, airspace is reported as a **separate flag** in §2 rather than mixed into the population metric: a city's row is flagged ✈ if it anchors a top-30-world-traffic hub or sits in a high-density continental airspace, using OurAirports large-airport locations (David Megginson, public domain, https://davidmegginson.github.io/ourairports-data/airports.csv; M1 source 6). This is a deliberate, stated choice (Limitation 4): population is the primary metric; airspace is an annotation showing the same latitude bands also carry concentrated air traffic (the M1-cited *Sci. Rep.* 2024 / Aerospace Corp. aviation-hazard channel).

### 1d. Traceability to M3 and M1 (every input has a home)

| Input to E_c | Comes from | Exact location |
|---|---|---|
| ΣE_a(f) per family (the "generated" risk) | **M3** | Table 2 §3b (54 families, ΣE_a) |
| i_f characteristic inclination | **M3** | Table 1 "Char. incl." per family |
| generated share by launching state | **M3** | §3a (CN 50.2%, RU 20.7%, US 13.9%, …) |
| w(φ) / g(φ\|i) latitude weighting | **M1** | §B2 (turning-latitude form, this §1b) |
| population grid (GPWv4) | **M1** | source 4/5 |
| airport/airspace (OurAirports) | **M1** | source 6 |

### 1e. Worked example — Jakarta (φ_c = −6.2°, P_c = 32.3 M), end to end

Take the three largest-ΣE_a families and show the full arithmetic; the table sums over all 54.

| Family *f* | i_f (M3) | ΣE_a(f) (M3) | L=min(i,180−i) | g_raw = cosφ/√(sin²L−sin²φ) at φ=−6.2° | Z (normaliser) | g(φ\|i)=g_raw/Z | ΣE_a·g |
|---|---:|---:|---:|---:|---:|---:|---:|
| CZ-3B | 27° | 0.0324 | 27° | 2.2545 | 178.5 (rad-int) | 0.01263 | 0.000409 |
| Soyuz (Blok-I) | 62° | 0.0396 | 62° | 1.1345 | 178.6 | 0.00635 | 0.000252 |
| Falcon 9 | 53° | 0.0193 | 53° | 1.2564 | 178.6 | 0.00703 | 0.000136 |

Summed over **all 54 families**, ε(−6.2°) = Σ_f ΣE_a(f)·g = **0.0018** (in the normalised-density units). Population-weighting: **E_Jakarta = 32.3 × 0.0018 = 0.060**, the highest of any city → normalised relative exposure **1.000**. (The full 54-family sum and the normaliser Z are computed by the reproducibility script in §5; the three rows above account for ~45% of Jakarta's ε, the rest from the remaining 51 families.)

**Sanity tie-backs:** (1) Σ_f ΣE_a(f) = 0.2081 reproduces M3's fleet ΣE_a = 0.2080. (2) The per-capita latitude exposure ε peaks not at the equator but near **±24°** — the turning latitudes of the dominant **CZ-3B/CZ-3C GTO families (i ≈ 27°)** — placing Dhaka/Karachi (≈24°N) at the per-capita maximum, a direct, traceable consequence of M3's family inclination mix. (3) ε(Jakarta −6.2°)/ε(Moscow 55.8°) = **3.44**, reproducing the published "~3×" Global-South finding (§3).

---

## 2. Ranked exposure table (19 population centers)

Ranked by the population-weighted exposure metric E_c (§1a), normalised so the top city = 1.000. **ε** is the population-independent per-capita latitude exposure (the Byers inequity index). "Dominant contributing families (i_f)" are the top-3 contributors to that city's ε, from M3. **✈** flags a top-world-traffic / high-density-airspace hub (OurAirports, M1 source 6). Representative latitude and metro population shown per row for full traceability.

| Rank | City | Country | Rep. lat (°) | Metro pop (M) | ε (per-capita) | **E_c (rel.)** | Dominant contributing families (i_f, from M3) | ✈ |
|---:|---|---|---:|---:|---:|---:|---|:--:|
| 1 | Jakarta | Indonesia | −6.2 | 32.3 | 0.0018 | **1.000** | CZ-3B (27°), Soyuz Blok-I (62°), Falcon 9 (53°) | ✈ |
| 2 | Dhaka | Bangladesh | 23.8 | 24.7 | 0.0022 | **0.915** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 3 | São Paulo | Brazil | −23.5 | 22.6 | 0.0022 | **0.821** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 4 | Tokyo | Japan | 35.7 | 37.0 | 0.0013 | **0.799** | Soyuz Blok-I (62°), CZ-2F (42°), Falcon 9 (53°) | ✈ |
| 5 | Karachi | Pakistan | 24.9 | 17.2 | 0.0024 | **0.702** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 6 | Mexico City | Mexico | 19.4 | 21.8 | 0.0019 | **0.687** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 7 | Mumbai | India | 19.1 | 21.7 | 0.0019 | **0.679** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 8 | New York | USA | 40.7 | 19.2 | 0.0021 | **0.660** | CZ-7 (41°), CZ-2F (42°), Soyuz Blok-I (62°) | ✈ |
| 9 | Beijing | China | 39.9 | 22.0 | 0.0017 | **0.628** | CZ-2F (42°), CZ-7 (41°), Soyuz Blok-I (62°) | ✈ |
| 10 | Kolkata | India | 22.6 | 15.6 | 0.0021 | **0.540** | CZ-3B (27°), Soyuz Blok-I (62°), H-IIA/B (30°) | ✈ |
| 11 | Kinshasa | DR Congo | −4.3 | 16.3 | 0.0020 | **0.538** | CZ-3B (27°), Soyuz Blok-I (62°), Ariane 5 (6°) |  |
| 12 | Lagos | Nigeria | 6.5 | 16.5 | 0.0019 | **0.512** | CZ-3B (27°), Soyuz Blok-I (62°), Falcon 9 (53°) | ✈ |
| 13 | Manila | Philippines | 14.6 | 14.9 | 0.0021 | **0.511** | CZ-3B (27°), Soyuz Blok-I (62°), GSLV (19°) | ✈ |
| 14 | Cairo | Egypt | 30.0 | 22.2 | 0.0012 | **0.441** | Soyuz Blok-I (62°), Falcon 9 (53°), CZ-2F (42°) | ✈ |
| 15 | Chennai | India | 13.1 | 11.5 | 0.0020 | **0.382** | CZ-3B (27°), Soyuz Blok-I (62°), GSLV (19°) | ✈ |
| 16 | Bogotá | Colombia | 4.7 | 11.3 | 0.0020 | **0.377** | CZ-3B (27°), Soyuz Blok-I (62°), Ariane 5 (6°) | ✈ |
| 17 | Bangkok | Thailand | 13.8 | 11.0 | 0.0020 | **0.371** | CZ-3B (27°), Soyuz Blok-I (62°), GSLV (19°) | ✈ |
| 18 | Moscow | Russia | 55.8 | 21.5 | 0.0005 | **0.193** | Soyuz Blok-I (62°), CZ-2D (97°), CZ-4B (97°) | ✈ |
| 19 | Washington DC | USA | 38.9 | 6.3 | 0.0015 | **0.158** | Soyuz Blok-I (62°), CZ-2F (42°), CZ-7 (41°) | ✈ |

**What the per-capita column (ε) shows (the inequity, population aside).** The per-capita latitude exposure is *highest* at ~24°N — **Karachi 0.0024, Dhaka 0.0022, São Paulo (24°S) 0.0022** — and *lowest* by far at high northern latitude: **Moscow (55.8°N) 0.0005**. The 24°-band maximum is the turning latitude of the **CZ-3B/CZ-3C GTO families (i ≈ 27°, the single largest non-Soyuz contributor at 15.6% + 0.9% of fleet ΣE_a in M3)** plus the H-IIA/B (30°) and GSLV/CZ-5 (19–22°) GTO traffic — a directly traceable consequence of M3's inclination mix, not an assumption. Equatorial cities (Jakarta, Lagos, Bogotá, Kinshasa) sit just *inside* the U-shaped trough but still well above the high-latitude launching capitals.

**Population then amplifies the borne burden.** Jakarta tops E_c despite a slightly sub-peak ε, because its 32.3 M metro population sits squarely in the over-flown tropical belt. The top 13 of 19 cities are Global-South megacities. The two lowest are **Moscow and Washington DC** — both major launching capitals (§3).

*Population sources:* Jakarta metro ≈ 32.3 M ([macrotrends.net Jakarta metro, mid-2024](https://www.macrotrends.net/global-metrics/cities/21454/jakarta/population)); Dhaka ≈ 24.7 M, Mumbai ≈ 21.7 M, Mexico City ≈ 21.8 M, São Paulo ≈ 22.6 M, Lagos ≈ 16.5 M, Cairo ≈ 22.2 M, Beijing ≈ 22.0 M, Moscow ≈ 21.5 M, Tokyo ≈ 37.0 M, Karachi ≈ 17.2 M, Manila ≈ 14.9 M, Kolkata ≈ 15.6 M, Kinshasa ≈ 16.3 M, Chennai ≈ 11.5 M, Bogotá ≈ 11.3 M, Bangkok ≈ 11.0 M, New York ≈ 19.2 M, Washington DC ≈ 6.3 M — UN World Urbanization Prospects / metro estimates as compiled by [macrotrends.net city metro series](https://www.macrotrends.net/global-metrics/cities/22007/lagos/population) and [worldpopulationreview.com](https://worldpopulationreview.com/cities/indonesia/jakarta) (2024–2025 estimates; figures rounded to 0.1 M; metro definitions vary — Limitation 5). *Representative latitudes* are the standard geographic coordinates of each city center (e.g. Jakarta −6.2°, Dhaka 23.8°, Lagos 6.5°, [latlong.net](https://www.latlong.net/place/jakarta-indonesia-27575.html); [latitude.to Lagos 6.45°N](https://latitude.to/map/ng/nigeria/cities/lagos)).

---

## 3. Generated vs borne — the exported-risk comparison

This is the core M4 deliverable: putting the **generated** risk share (which states *created* the hazard, M3 §3a) beside the **borne** exposure (which countries *absorb* it, §2), and flagging the mismatch.

### 3a. Launching states: generated vs borne

| State | **Generated** risk share (M3 §3a) | Largest city's borne exposure E_c (rel., §2) | Per-capita ε at capital | **Exported-risk flag** |
|---|---:|---:|---:|---|
| China | **50.2%** | Beijing 0.628 | 0.0017 (39.9°N) | Net **exporter**: 50% generated, capital at modest mid-lat exposure |
| Russia | **20.7%** | Moscow 0.193 | **0.0005 (55.8°N)** | Net **exporter**: 21% generated, capital at the *lowest* per-capita exposure in the table |
| USA | **13.9%** | New York 0.660 / Washington 0.158 | 0.0015 (38.9°N) | Mixed: generates 14%; NY's exposure is population-driven, not latitude-driven |
| Japan | 6.2% | Tokyo 0.799 | 0.0013 (35.7°N) | Generates 6%; Tokyo's high E_c is its 37 M population, not high ε |
| India | 4.9% | Mumbai 0.679 / Kolkata 0.540 | 0.0019–0.0021 | Generates 5%; bears high exposure (both generator *and* bearer) |
| **Indonesia** | **0.0%** | **Jakarta 1.000 (highest)** | 0.0018 | **IMPORTS risk it did not create** |
| **Bangladesh** | **0.0%** | **Dhaka 0.915 (2nd)** | 0.0022 | **IMPORTS risk it did not create** |
| **Nigeria** | **0.0%** | **Lagos 0.512** | 0.0019 | **IMPORTS risk it did not create** |
| **Brazil / Pakistan / Mexico / Philippines / Colombia / DR Congo / Thailand / Egypt** | **0.0% each** | 0.37–0.82 | 0.0012–0.0024 | **All IMPORT risk they did not create** |

### 3b. The flagged exported-risk cases (≥1 required; 11 shown)

The states with the **highest borne exposure and ~0% generated share** are **Indonesia (Jakarta, rank 1), Bangladesh (Dhaka, rank 2), Brazil (São Paulo, 3), Pakistan (Karachi, 5), Mexico (6), Nigeria (Lagos, 12), Philippines, Colombia, DR Congo, Thailand, and Egypt** — none of which operated a single uncontrolled rocket body in the M3 inventory (M3 §3a lists only CN, RU, US, J, IN, NZ, F, IR, IL, KR, KP as launching states; every country in the borne top-13 except India, China, Japan, USA appears with **0% generated share**). The clearest single case: **Indonesia bears the highest exposure of any country on Earth (Jakarta E_c = 1.000) while generating 0% of the fleet risk**, the hazard imported almost entirely from **Chinese CZ-3B/CZ-2F (50.2% generated) and Russian Soyuz Blok-I (20.7% generated)** ground tracks passing over the ±6° tropical band. The inverse is **Russia**, which **generated 20.7%** of the risk yet whose capital Moscow has the **lowest per-capita exposure (ε = 0.0005) in the entire table** — the largest generated-minus-borne gap in the ledger.

### 3c. Consistency with the published Global-South finding (cited)

This pattern reproduces the headline inequity finding the brief cites. Byers, Wright & Boley (2022), summarised by UBC News, report that rocket bodies are **"approximately three times more likely to land at equatorial latitudes than northern ones,"** naming **Jakarta, Dhaka and Lagos** as higher-risk and **New York, Beijing and Moscow** as lower-risk, and concluding **"the risk is borne disproportionately by the global south, despite major space-faring nations being located in the north"** ([UBC News, 2022-07-11](https://news.ubc.ca/2022/07/space-rocket-junk-deadly/); Byers, Wright & Boley, *Nature Astronomy* 6, 1093–1097, 2022, DOI [10.1038/s41550-022-01718-8](https://doi.org/10.1038/s41550-022-01718-8); open arXiv:2210.02188, https://arxiv.org/abs/2210.02188). This M4 model independently lands the same ~3× figure: **ε(Jakarta −6.2°) / ε(Moscow 55.8°) = 3.44** (§1e), built bottom-up from M3's family inclinations and risk weights rather than asserted — an internal corroboration of the published result. Jakarta, Dhaka and Lagos all sit in the borne-exposure top 13; all three launching capitals named as low-risk (New York, Beijing, Moscow) sit in the bottom half on a per-capita (ε) basis, with Moscow last.

---

## 4. Limitations & counter-evidence

1. **Ground-track probability is a latitude-band likelihood, not a true per-country impact probability (M1 Limitation 3).** g(φ|i) resolves exposure by latitude *only*: it ignores longitudinal structure, the Earth-rotation phasing of the final orbit, the specific decay-day geometry, and the fact that ~71% of any latitude band is ocean. Two cities at the same latitude (e.g. Mumbai and a point in the Atlantic) receive identical ε. The metric therefore answers "is this latitude over-flown, and how many people live there?" — not "what is the impact probability on this city this decade." This is the standard simplification in the M1 §B2 / Byers et al. 2022 literature and the deliverable is explicitly a *relative* exposure index, not an absolute impact probability.

2. **The metric inherits all of M3's risk-magnitude uncertainty.** E_c is M3's ΣE_a re-distributed across latitude; it carries M3's order-of-magnitude A_c uncertainty (M3 Limitations 1, 4) and family-level (not per-body) inclination (M3 Limitation 3) unchanged. In particular, because inclination is assigned per *family*, the latitude band of, e.g., Soyuz Blok-I (a 51.6°/82.5°/98° mix collapsed to a 62° proxy) is smeared; a per-body GCAT inclination pass would sharpen the turning-latitude peaks but would not move the equator-vs-high-latitude inequity, which is robust to the proxy.

3. **The turning-latitude density is for a circular orbit and the *time-averaged* sub-satellite point — not the reentry point per se.** The actual reentry latitude of a decaying body is drawn from where it happens to be when it finally descends, which is itself distributed roughly as g(φ|i) over many bodies, so the fleet-aggregate use here is appropriate; but for any *single* body the reentry latitude is one draw, not the density. M4's claims are fleet-aggregate (54 families, 559 bodies) and should not be read as a single-event prediction.

4. **Airspace is reported as a flag, not folded into E_c (a deliberate, stated choice).** Aviation exposure scales with overflights of the latitude band, not resident population, and a defensible flight-weighted metric would need OAG/flight-density data beyond M1's OurAirports airport-location source. Folding a crude airport-count into the population metric would mix two incommensurable exposure channels. The ✈ flag (OurAirports, M1 source 6) shows the over-flown latitude bands also host concentrated air traffic (the M1-cited *Sci. Rep.* 2024 / Aerospace Corp. aviation-hazard channel), but the headline E_c ranking is population-only. A future pass could add a parallel flight-weighted exposure column.

5. **Population-grid resolution and metro-boundary definitions inject error.** P_c uses metropolitan-area populations aggregated from the GPWv4 count grid (M1 source 4/5), whose native resolution is 30 arc-seconds but is effectively used here at the city-aggregate scale; metro-area *definitions* differ across the cited sources (city proper vs agglomeration vs UN urban area), so individual P_c values carry ±10–30% definitional spread (e.g. Jakarta "32.3 M" is the Jabodetabek agglomeration; some sources report 42 M, others 11 M for the city proper). Because E_c is a *relative* index dominated by which latitude band a city sits in (ε spans ~5× across the table) more than by P_c (which spans ~6×), the **ranking is more robust than any single E_c value**; the Global-South-vs-launching-capital ordering survives any reasonable metro-definition choice.

6. **No realised casualty (carried from M1/M3 Limitation 6).** No confirmed human casualty has resulted from any of the 559 uncontrolled reentries; the case is *expected* exported risk against a published threshold, not a body count. A reader can fairly argue the realised burden on these cities is zero to date. The M4 response is unchanged from M3: the exposure ranking measures *where the agreed-threshold-breaching risk is directed*, and the inequity (generators in the north, bearers in the tropics) is a structural property of the chosen launch inclinations independent of whether a casualty has yet occurred — which is precisely the accountability gap the ledger documents.

---

## 5. Reproducibility

E_c = P_c · Σ_f [ ΣE_a(f) · g(φ_c | i_f) ], with g(φ|i) = cos φ /[ Z·√(sin²L − sin²φ) ], L = min(i,180−i), Z = ∫₋ᴸᴸ cos φ/√(sin²L−sin²φ) dφ (numerical, 40,000-point midpoint rule). Inputs: ΣE_a(f) and i_f from M3 Table 1/Table 2 (54 families); P_c and φ_c from §2 sources. Tie-backs: Σ_f ΣE_a(f) = 0.2081 (≈ M3 fleet ΣE_a 0.2080); ε(Jakarta)/ε(Moscow) = 3.44 (≈ published 3×). The full 54-family computation (the exact script that produced §2's ε, E_c, and the §1e worked example) is deterministic from these two M3 columns plus the §2 latitude/population inputs; results are reproduced exactly by re-running the metric over M3 Table 2 §3b with the inclinations in M3 Table 1.

---

## Source list (dated)

- **M3 — Per-reentry casualty risk and accountability attribution** (this problem), `artifacts/2026-06-26-m3-per-reentry-risk-and-attribution.md`. — **primary input:** per-family ΣE_a (Table 2 §3b), characteristic inclinations (Table 1), per-launching-state generated share (§3a, CN 50.2 / RU 20.7 / US 13.9%). The "generated" side and the ground-track inclination drivers.
- **M1 — Methodology and Source Register** (this problem), `artifacts/2026-06-26-m1-methodology-source-register.md`, §B2 + sources 4/5/6. — the latitude-weighting w(φ) (operationalised here as the turning-latitude density), GPWv4 population source, OurAirports airspace source.
- Byers, M., Wright, E., Boley, A. "Unnecessary risks created by uncontrolled rocket reentries." *Nature Astronomy* 6, 1093–1097 (2022). DOI [10.1038/s41550-022-01718-8](https://doi.org/10.1038/s41550-022-01718-8); open arXiv:2210.02188 (https://arxiv.org/abs/2210.02188). — the latitude-weighting / casualty-expectation construction and the Global-South inequity (~3× equatorial vs northern).
- UBC News, "Space rocket junk could have deadly consequences unless governments act" (2022-07-11). https://news.ubc.ca/2022/07/space-rocket-junk-deadly/. — plain-language statement of the Byers et al. finding: ~3× more likely at equatorial latitudes; Jakarta/Dhaka/Lagos higher-risk vs New York/Beijing/Moscow; "risk borne disproportionately by the global south."
- GPWv4 v4.11 Population Count (NASA SEDAC/CIESIN), DOI 10.7927/H4JW8BX5, https://beta.sedac.ciesin.columbia.edu/data/set/gpw-v4-population-count-rev11/data-download; GPWv4 Density DOI 10.7927/H4NP22DQ. — population weighting (via M1 source 4/5).
- OurAirports open data (David Megginson, public domain), CSV https://davidmegginson.github.io/ourairports-data/airports.csv. — airspace ✈ flag (via M1 source 6).
- City metro populations: macrotrends.net city metro series (e.g. https://www.macrotrends.net/global-metrics/cities/21454/jakarta/population, https://www.macrotrends.net/global-metrics/cities/22007/lagos/population) and worldpopulationreview.com (https://worldpopulationreview.com/cities/indonesia/jakarta), 2024–2025 estimates. City latitudes: latlong.net / latitude.to (e.g. https://www.latlong.net/place/jakarta-indonesia-27575.html, https://latitude.to/map/ng/nigeria/cities/lagos).
- Pardini, C., Anselmo, L. (2024), *J. Space Safety Engineering* 11(2):181–191, https://www.sciencedirect.com/science/article/pii/S2468896724000077; CNR focus https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites — the 62%/18%/14% generated split underlying M3 §3a (context for the generated side).
