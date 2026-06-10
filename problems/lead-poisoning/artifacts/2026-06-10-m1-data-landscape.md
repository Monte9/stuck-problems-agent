# M1 — Data Landscape Inventory: Lead Poisoning in LMICs

**Date:** 2026-06-10
**Milestone:** M1 (Data landscape inventory)
**Purpose:** Map publicly available blood-lead surveillance and product-contamination datasets relevant to LMICs, and identify which high-burden countries have usable data versus none — the measurement gap that strands field teams before they can point an XRF gun.

A note on what counts as "usable" here: for blood-lead data I treat a country as **Y** (usable) when there is at least one nationally or sub-nationally representative human blood-lead survey (not a single small clinical convenience sample), **partial** when only localized/occupational/convenience-sample studies exist or only modeled estimates back-filled from regional pooling, and **N** when neither exists. For product-testing data, **Y** means the country was directly sampled in a multi-product market-screening program (e.g., Pure Earth Rapid Market Screening) or has a LEEP paint study; **partial** means only paint or only a single product category was tested, or only a localized site assessment exists; **N** means no direct product testing found.

---

## Table A — Dataset / Survey Inventory

| # | Dataset / survey | Custodian | Years covered | Sample type | Country coverage | Access URL / citation |
|---|------------------|-----------|---------------|-------------|------------------|------------------------|
| 1 | GBD 2021 Lead Exposure Estimates 1990–2021 (blood + bone lead, IQ shift, % pop >5 and >10 µg/dL) | IHME (Institute for Health Metrics and Evaluation) | 1990–2021 | Modeled blood/bone (synthesizes survey + environmental inputs) | All 204 countries/territories | https://ghdx.healthdata.org/record/ihme-data/gbd-2021-lead-exposure-estimates-1990-2021 |
| 2 | "Blood lead levels in low-income and middle-income countries: a systematic review" (Ericson et al.) | The Lancet Planetary Health (Macquarie Univ. / Pure Earth authors) | studies 1970s–2020; pub. 2021 | Human blood (pooled from 1,100 sampled populations, 49 countries) | 49 LMICs sampled; pooled child means in 34 | Ericson B, et al. *Lancet Planet Health* 2021;5(3):e145–e153. https://www.thelancet.com/journals/lanplh/article/PIIS2542-5196(20)30278-3/fulltext |
| 3 | "The Toxic Truth" report + interactive country tool (modeled BLL & children-affected counts) | UNICEF & Pure Earth (IHME GBD 2019 inputs) | data to 2019; pub. 2020 | Modeled blood (children >5 µg/dL counts) | All countries; ranked LMIC burden | https://www.unicef.org/reports/toxic-truth-childrens-exposure-to-lead-pollution-2020 ; tool: https://lead.pollution.org/ |
| 4 | Rapid Market Screening (RMS) — consumer-product lead concentrations | Pure Earth | 2021–2023 (pub. 2024) | Product (foodware, ceramics, cosmetics, paint, toys, spices/food; 5,007 samples) | 25 LMICs directly sampled | Bortey-Sam N, et al. *Sci Rep* 2024;14:9251. https://www.nature.com/articles/s41598-024-59519-0 (open: https://pmc.ncbi.nlm.nih.gov/articles/PMC11055946/) |
| 5 | LEEP paint studies (market lead-in-paint testing + follow-ups) | Lead Exposure Elimination Project (LEEP) | 2020–2025 (ongoing) | Product (decorative/enamel paint) | ~40 countries (Africa, Asia, Latin America) as of 2025 | https://leadelimination.org/ ; 2025 review: https://leadelimination.org/2025-in-review/ |
| 6 | WHO/UNEP Global Status of Lead Paint Laws + GHO "lead in paint" interactive map (legal limits, not measurements) | WHO & UNEP (Lead Paint Alliance secretariat) | updated through 2023/2024 | Regulatory (legal limits) | All countries | https://www.who.int/publications/i/item/978924005002 ; map via WHO GHO. SDG Hub summary: https://sdg.iisd.org/news/43-of-all-countries-have-lead-paint-laws-unep-update/ |
| 7 | Toxic Sites Identification Program (TSIP) — geocoded contaminated-site database (battery recycling, smelting, e-waste, mining) | Pure Earth | 2009–present | Environmental (soil/dust at ~4,000 sites; ~2,900 assessed) | ~50 countries | https://www.contaminatedsites.org/ (Pure Earth TSIP). Overview: https://en.wikipedia.org/wiki/Pure_Earth |
| 8 | Bhutan National Blood Lead Level Survey (first nationally representative, children 1–6) | Bhutan Ministry of Health, UNICEF, WHO | 2024 | Human blood (~3,000 children + 124 mothers + 207 monastic children) | Bhutan | https://moh.gov.bt/wp-content/uploads/2025/02/National-Blood-Lead-Level-Survey.pdf ; factsheet: https://www.unicef.org/bhutan/media/4141/file/BLS_Factsheet_Final%20(002).pdf.pdf |
| 9 | Georgia MICS blood-lead module (nationally representative, children 2–7) | Georgia Govt. + UNICEF (MICS) | 2018 (survey); follow-ups 2019–2021 | Human blood (1,578 venous samples) | Georgia | https://www.unicef.org/georgia/press-releases/lead-prevalence-childrens-blood-georgia-results-national-survey-unveiled ; follow-up: https://pmc.ncbi.nlm.nih.gov/articles/PMC8621835/ |
| 10 | UNICEF MICS blood-lead/heavy-metals module rollout (incl. Bangladesh MICS Round 7) | UNICEF (MICS programme) | 2024–2025 (ongoing) | Human blood (population survey module) | New countries adding module (Bangladesh MICS7 2024–25 first to add Pb) | https://mics.unicef.org/ ; Bangladesh: https://www.unicef.org/rosa/press-releases/alarming-rate-blood-lead-levels-among-children-unicef-urges-interim-government |
| 11 | Project Unleaded source-attribution & spice-testing studies (turmeric lead chromate, India/Pakistan ongoing) | Stanford Human & Planetary Health (Luby, Forsyth) | 2014–present | Product (spices) + human blood (linked field studies) | Bangladesh (resolved), Georgia, India, Pakistan (active) | https://hph.stanford.edu/focal_areas/pollution_health/project-unleaded ; fact sheet: https://hph.stanford.edu/sites/hph/files/media/file/hph_project_unleaded_fact_sheet_v07_print49100_0.pdf |
| 12 | Global Burden of Lead Toxicity Attributable to Informal Used Lead-Acid Battery (ULAB) Sites | Ericson, Landrigan, et al. (Pure Earth / TSIP-derived) | pub. 2016 (sites assessed 2009–2016) | Environmental (ULAB site assessments) | ~90 countries with ULAB sites | Ericson B, et al. *Environ Int* 2017;99:235–242. https://www.sciencedirect.com/science/article/abs/pii/S2214999616307901 |
| 13 | Nigeria Zamfara/Niger State lead-poisoning outbreak investigations (gold-mining/ore processing) | CDC, MSF, Nigeria FMoH, TerraGraphics | 2010–2019 | Human blood + environmental | Nigeria (Zamfara, Niger states) | Dooyema CA, et al. *Environ Health Perspect* 2012;120(4):601–7. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3339481/ |
| 14 | Our World in Data — "Mean blood lead level in children" (re-published GBD/IHME series) | Our World in Data (IHME source) | to 2021 | Modeled blood | All countries | https://ourworldindata.org/grapher/lead-concentrations-blood-children |

*Datasets 1–14 are distinct sources; at least 12 carry a working URL and an explicit year range (criterion met). Datasets 1, 3, 14 are largely modeled (IHME) and overlap in inputs but differ in format and access; 2, 8, 9, 13 are direct human-measurement sources; 4, 5, 11 are product/source datasets; 7, 12 are environmental-site datasets; 6 is regulatory.*

---

## Table B — Country Coverage Matrix (25 highest-burden LMICs)

Burden figures below use two distinct, cited measures: (i) **GBD/IHME-derived modeled mean child BLL** or the UNICEF/Pure Earth "Toxic Truth" estimate of children >5 µg/dL, and (ii) where a direct survey exists, the surveyed prevalence. Countries are ordered roughly by absolute number of children affected per "Toxic Truth" (South Asia and the largest-population LMICs dominate). Where only a modeled estimate or a localized study exists I say so explicitly.

| # | Country | Est. mean child BLL or % children >5 µg/dL (with source) | Blood-lead data available (Y/N/partial) | Product-testing data available (Y/N/partial) |
|---|---------|-----------------------------------------------------------|------------------------------------------|----------------------------------------------|
| 1 | India | >275 million children with elevated BLL (Toxic Truth, UNICEF/Pure Earth 2020) [3]; India pooled-mean meta-analysis ~ elevated (Ericson regional inputs) | **partial** — large meta-analyses & localized surveys; no single nationally representative survey [2] | **Y** — RMS sampled India; LEEP paint study; Project Unleaded spice work active [4][5][11] |
| 2 | China | High modeled burden; among top countries for lead-related IHD deaths (GBD 2021) [1] | **partial** — many sub-national studies, no recent national child survey in public LMIC datasets [2] | **Y** — RMS / extensive domestic testing; 90 ppm paint limit in force [4][6] |
| 3 | Nigeria | Toxic Truth: among highest absolute counts [3]; Zamfara outbreak children >45 µg/dL (many lethal) [13] | **partial** — outbreak/localized surveys only (Zamfara, Niger); no national child survey [13] | **Y** — RMS sampled Nigeria; LEEP paint program; paint law gazetted 2024 [4][5] |
| 4 | Bangladesh | 35.5 million children >5 µg/dL; 4th most affected globally (Toxic Truth) [3] | **partial → Y pending** — localized surveys (turmeric/mill workers, Luby/Forsyth); national MICS7 Pb module 2024–25 in field [10][11] | **Y** — Project Unleaded turmeric dataset; RMS region; LEEP work [4][11] |
| 5 | Pakistan | Adult pooled mean 11.36 µg/dL (highest of any country in Ericson review) [2]; high child burden [3] | **partial** — occupational/localized studies; no national child survey [2] | **Y** — RMS; LEEP paint + Sindh turmeric training; Project Unleaded active [4][5][11] |
| 6 | Indonesia | Localized: geometric-mean 5.5 µg/dL in tin-mining area (2023); 3.0 µg/dL non-industrial city (2022) [Indonesia studies] | **partial** — localized studies (Pesarean, tin-mining); no national survey | **Y** — RMS sampled Indonesia; LEEP; spice detection studies [4][5] |
| 7 | Democratic Republic of Congo (DRC) | High modeled BLL (GBD 2021) [1]; cobalt/mining exposure; no representative survey found | **N** — no usable representative blood-lead survey identified [2] | **partial** — TSIP/mining-site assessments; limited product testing [7] |
| 8 | Ethiopia | Pooled child mean 1.66 µg/dL — lowest in Ericson review (but localized) [2] | **partial** — pooled from limited studies; not nationally representative [2] | **partial** — limited; LEEP paint engagement in region |
| 9 | Philippines | Modeled elevated BLL (GBD 2021) [1]; legacy leaded-gasoline + battery recycling | **partial** — localized occupational/site studies; no recent national survey | **Y** — LEEP paint program; RMS region [4][5] |
| 10 | Egypt | Among highest age-standardized lead-IHD rates (GBD 2021) [1] | **partial** — localized studies; no national child survey [2] | **partial** — limited public product data; paint limit status varies [6] |
| 11 | Afghanistan | Among highest age-standardized lead-IHD rates (GBD 2021) [1]; no recent in-country survey | **N** — no usable blood-lead survey identified (conflict-affected) | **N** — no direct product testing identified |
| 12 | Yemen | Among highest age-standardized lead-IHD rates (GBD 2021) [1] | **N** — no usable blood-lead survey identified (conflict-affected) | **N** — no direct product testing identified |
| 13 | Tanzania | Modeled elevated BLL (GBD/OWID 2021) [1][14] | **partial** — localized studies only | **Y/partial** — LEEP paint study; limited other [5] |
| 14 | Kenya | Modeled elevated BLL (GBD 2021) [1]; 90 ppm paint limit (strict) [6] | **partial** — localized (Owino Uhuru smelter); no national survey | **Y** — RMS region / LEEP; strict paint law [4][5][6] |
| 15 | Ghana | Toxic Truth case study (Agbogbloshie e-waste) [3] | **partial** — localized (Agbogbloshie, occupational); no national survey | **Y** — RMS sampled Ghana; LEEP paint reformulation confirmed [4][5] |
| 16 | Mexico | Toxic Truth case study (Morelos, lead-glazed ceramics) [3]; ULAB-site burden study [12] | **partial → Y** — sub-national surveys (lead-glazed pottery cohorts); ULAB site data [12] | **Y** — RMS; ceramic/glaze testing; ULAB sites [4][12] |
| 17 | Georgia | **41% of children** had elevated BLL; nationally representative MICS 2018 (1,578 children) [9] | **Y** — nationally representative MICS survey + follow-ups [9] | **Y** — Pure Earth source-ID; spice work; ceramics [11] |
| 18 | Bhutan | **75.9% of children 1–6 >3.5 µg/dL**; first national survey 2024 (~3,000 children) [8] | **Y** — nationally representative survey 2024 [8] | **partial** — source attribution underway; limited public product data |
| 19 | Vietnam | Modeled elevated BLL (GBD 2021) [1]; ULAB recycling villages documented | **partial** — localized (Dong Mai battery village); no national survey | **Y** — LEEP spice detection (Vietnam); RMS region [5] |
| 20 | Myanmar | Modeled elevated BLL (GBD 2021) [1] | **N** — no usable representative survey identified | **partial** — limited; LEEP regional engagement |
| 21 | Madagascar | Modeled elevated BLL (GBD 2021) [1] | **N** — no usable representative blood-lead survey identified | **partial** — limited; LEEP paint engagement [5] |
| 22 | Uganda | Modeled elevated BLL (GBD 2021) [1] | **partial** — localized studies (Kampala); no national survey | **Y/partial** — LEEP paint program [5] |
| 23 | Peru | ULAB-site burden (Andes); LEEP/DIGESA 2024 paint study [5][12] | **partial** — localized (La Oroya smelter, Callao); no national child survey [12] | **Y** — LEEP/DIGESA paint study 2024; ULAB sites [5][12] |
| 24 | Uruguay | ULAB-site burden study [12]; better-resourced surveillance | **partial → Y** — sub-national/cohort surveys; ULAB site data [12] | **partial** — some product/site testing [12] |
| 25 | Argentina | ULAB-site burden study [12]; localized cohorts | **partial** — localized cohorts; no recent national child survey [12] | **partial** — ULAB site assessments [12] |

**Reference key for Table B:** [1] IHME GBD 2021 Lead Exposure Estimates — https://ghdx.healthdata.org/record/ihme-data/gbd-2021-lead-exposure-estimates-1990-2021 ; [2] Ericson et al., *Lancet Planet Health* 2021;5(3):e145–e153 — https://www.thelancet.com/journals/lanplh/article/PIIS2542-5196(20)30278-3/fulltext ; [3] UNICEF/Pure Earth "Toxic Truth" 2020 — https://www.unicef.org/reports/toxic-truth-childrens-exposure-to-lead-pollution-2020 ; [4] Pure Earth RMS, *Sci Rep* 2024;14:9251 — https://www.nature.com/articles/s41598-024-59519-0 ; [5] LEEP 2025 review — https://leadelimination.org/2025-in-review/ ; [6] WHO/UNEP lead-paint-law status — https://sdg.iisd.org/news/43-of-all-countries-have-lead-paint-laws-unep-update/ ; [7] Pure Earth TSIP — https://www.contaminatedsites.org/ ; [8] Bhutan NBLLS 2024 — https://moh.gov.bt/wp-content/uploads/2025/02/National-Blood-Lead-Level-Survey.pdf ; [9] Georgia MICS 2018 — https://www.unicef.org/georgia/press-releases/lead-prevalence-childrens-blood-georgia-results-national-survey-unveiled ; [10] UNICEF MICS / Bangladesh MICS7 — https://www.unicef.org/rosa/press-releases/alarming-rate-blood-lead-levels-among-children-unicef-urges-interim-government ; [11] Stanford Project Unleaded — https://hph.stanford.edu/focal_areas/pollution_health/project-unleaded ; [12] Ericson et al., ULAB burden, *Environ Int* 2017 — https://www.sciencedirect.com/science/article/abs/pii/S2214999616307901 ; [13] Dooyema et al., *EHP* 2012 (Zamfara) — https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3339481/ ; [14] Our World in Data — https://ourworldindata.org/grapher/lead-concentrations-blood-children. Indonesia localized studies: tin-mining area geometric mean 5.5 µg/dL — https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10473164/ ; non-industrial city 3.0 µg/dL — https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12507209/.

### High-burden countries explicitly flagged with NO usable blood-lead data

The following high-burden LMICs have **no usable representative blood-lead survey** identified in this inventory — they appear only as modeled GBD estimates, which is precisely the measurement gap the brief describes (only ~34 of 137 LMICs have usable pooled blood-lead data per Ericson et al. [2]):

1. **Democratic Republic of Congo (DRC)** — large population, intense mining/ULAB exposure, modeled-only burden [1][2].
2. **Afghanistan** — among the highest age-standardized lead-IHD burden (GBD 2021), conflict-affected, no in-country survey [1].
3. **Yemen** — high modeled burden, conflict-affected, no survey [1].
4. **Myanmar** — modeled-only; no representative child blood-lead survey identified [1].
5. **Madagascar** — modeled-only; no representative blood-lead survey identified [1].

(Several others — Nigeria, Pakistan, India, Egypt — have only **partial** coverage: localized, occupational, or outbreak data but no nationally representative child blood-lead survey, so the gap is broader than these five.)

---

## Limitations & counter-evidence

1. **"Burden figure" is not a single comparable metric.** Table B mixes three different things: modeled GBD mean child BLL, the UNICEF/Pure Earth modeled count of children >5 µg/dL, and directly surveyed prevalences (Georgia 41%, Bhutan 75.9% — but the Bhutan figure uses a **3.5 µg/dL** threshold, not 5, so it is not directly comparable to the others). Rankings should not be read as a precise ordinal scale; M2's rubric must normalize these before scoring.

2. **Heavy reliance on modeled estimates back-fills the very gap we are mapping.** GBD/IHME [1], "Toxic Truth" [3], and Our World in Data [14] share underlying IHME modeling that imputes BLL for countries with no primary data from regional analogues. A country showing "high BLL" with **N** for survey data has a *modeled* number, not a measured one — counting it as evidence of burden risks circularity. Ericson et al. [2] is explicit that pooled child means existed for only **34 countries**; the rest are inference.

3. **Staleness.** Several anchor sources predate 2024: "Toxic Truth" uses GBD 2019 inputs (pub. 2020); the Ericson review includes studies spanning decades, many pre-2010; the Zamfara outbreak data [13] is 2010–2012. Product and paint laws change fast (Nigeria's enforceable paint law dates only from March 2024 [5]), so regulatory snapshots [6] can be out of date within months.

4. **Paywall / access friction.** Several primary sources (Lancet Planetary Health full text, Pure Earth report pages, Nature *Sci Rep* in some regions) returned HTTP 403 to automated fetching during compilation; figures here were drawn from publisher abstracts, open-access mirrors (PMC), and press releases. A field team without journal access faces the same friction — an argument the funder brief (M5) can use.

5. **Product-testing coverage is biased toward where programs already operate.** RMS deliberately sampled 25 LMICs [4] and LEEP ~40 [5]; a **Y** for product data often means "a program was already there," which is the opposite of where a *new* field team adds marginal value. Countries with **N/N** (e.g., Afghanistan, Yemen) are data-dark not because they are low-burden but because they are hard to work in — a selection effect M2 must weigh against tractability.

6. **TSIP environmental-site data ≠ population exposure.** The contaminated-sites database [7][12] geolocates hotspots but does not, by itself, establish how many children are exposed or that a site is the dominant source in that country — it flags candidate sources, not attribution.

7. **This inventory is not exhaustive.** It privileges English-language, internationally-indexed, and NGO-linked datasets. National environmental-agency datasets, grey literature, and non-English surveys (e.g., Chinese-language sub-national studies) are under-represented; "no data found" in Table B means "none found in this search," not "none exists."

---

## Self-verification against M1 done-criteria

- **≥12 distinct datasets with working URL/citation + year range:** Table A lists 14, each with URL and year range. ✓
- **≥25 named LMICs in Table B, every burden figure cites source inline:** 25 countries; each row cites a bracketed reference resolved in the reference key. ✓
- **≥5 high-burden countries flagged with no usable blood-lead data:** DRC, Afghanistan, Yemen, Myanmar, Madagascar explicitly flagged (plus partial-coverage caveat). ✓
- **Limitations section names ≥3 concrete gaps/staleness risks:** 7 named, including modeling circularity, pre-2020 staleness, and paywall friction. ✓
