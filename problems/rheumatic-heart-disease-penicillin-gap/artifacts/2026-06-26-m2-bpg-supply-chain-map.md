# M2 — BPG supply-chain concentration map

**Problem:** Rheumatic heart disease — the penicillin gap
**Milestone:** M2 (map the global BPG supply chain end-to-end; expose single points of failure)
**Date:** 2026-06-26
**Author:** generator (autonomous loop)

## What this artifact is

A structured supply-chain brief for benzathine penicillin G (BPG / benzathine benzylpenicillin), the molecule that delivers RHD secondary prophylaxis. It traces the chain from upstream — the small number of surviving active-pharmaceutical-ingredient (API) makers — down through finished-dose (finished pharmaceutical product, FPP) suppliers by region, lays the documented shortage events on a dated timeline, states the global demand-vs-need gap, and names where the chain is one failure away from rupture.

It builds on the M1 scorecard (`artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`), which established the burden and the country-level stockout picture. M1's documented stockouts (Congo, Nigeria, Ethiopia, Mozambique, Uganda, Brazil, South Africa, Australia, Eritrea, the US 2023–25 shortage) are reused here as part of the timeline; this artifact adds the upstream-manufacturer dimension M1 did not cover.

> **Anchor source.** The single most authoritative recent synthesis of this supply chain is the peer-reviewed Clinton Health Access Initiative (CHAI)-linked analysis **Khdemiri/CHAI et al., "Securing the supply of benzathine penicillin: a global perspective on risks and mitigation strategies to prevent future shortages," *International Health* (Oxford), 2024, 16(3):279** ([PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/); [Oxford Academic](https://academic.oup.com/inthealth/article/16/3/279/7288044)). Most of the structural figures below trace to it; secondary-market detail comes from API/FPP databases and regulator notices, each cited inline.

---

## (a) BPG API manufacturers — the upstream chokepoint

The peer-reviewed CHAI analysis states plainly: **"By 2016, only three Chinese API manufacturers remained, continuing to supply to the global market today."** API manufacturing is described as **"concentrated in two regions of China"** ([CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). So the authoritative *count* of globally-supplying BPG API makers is **three**, all in China — this is the headline single point of failure.

The CHAI paper does **not** name the three. The names below are assembled from trade/regulatory databases and a 2017 Al Jazeera supply-chain investigation, and should be read as the *publicly identifiable* candidates, not a regulator-certified roster (see Limitations).

| # | API manufacturer | Country / location | Basis for naming | Citation |
|---|------------------|--------------------|------------------|----------|
| 1 | **North China Pharmaceutical Group / NCPC Semisyntech** | China — Shijiazhuang, Hebei Province | Named in Al Jazeera supply-chain investigation as one of the "three Chinese" + four-company global set; established penicillin producer | [Al Jazeera 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage); [North China Pharmaceutical Co. profile](https://baike.baidu.com/en/item/North%20China%20Pharmaceutical%20Co.,%20Ltd./35729) |
| 2 | **CSPC Pharmaceutical Group Ltd.** | China — Shijiazhuang, Hebei Province | Named in Al Jazeera investigation; CSPC produces penicillin API and formulations | [Al Jazeera 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage); [CSPC — Wikipedia](https://en.wikipedia.org/wiki/CSPC_Pharmaceutical_Group) |
| 3 | **Jiangxi Dongfeng Pharmaceutical Co. / LLC** | China — Leping City, Jiangxi Province | Named in Al Jazeera investigation; holds US Drug Master File(s) and lists Penicillin G Benzathine among exported APIs | [Al Jazeera 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage); [Jiangxi Dongfeng DMF, Pharmacompass](https://www.pharmacompass.com/us-drug-master-files-dmfs/jiangxi-dongfeng-pharmaceutical-llc); [APIs list, apicule](https://apicule.com/api-suppliers/jiangxi-dongfeng-pharmaceutical-llc/) |
| (4) | **Sandoz GmbH** | Austria — Kundl | Al Jazeera's 2017 piece described a *four*-company global set (3 Chinese + Sandoz/Austria). The CHAI 2024 paper's "three" likely refers specifically to *API* makers supplying the open global market; Sandoz's Kundl site is a strategically important EU penicillin hub but its role as an open-market *BPG-API* seller (vs. captive FPP feedstock) is ambiguous in public sources — see Limitations. | [Al Jazeera 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage) |

**Reading:** Whether the true number is **3 or 4**, the structural fact is identical — global BPG API rests on a handful of plants, overwhelmingly in two Chinese provinces (Hebei, Jiangxi). The CHAI paper attributes this attrition to the molecule being off-patent, low-margin, with poor demand visibility ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)); the Al Jazeera/WHO framing adds that surviving plants reportedly run at a fraction of capacity because demand data are too thin to justify investment ([Al Jazeera 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage)).

---

## (b) Finished-dose (FPP) suppliers / products by region

CHAI estimated **"at least 30 companies were producing the finished pharmaceutical product (FPP) in 2016"** ([CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). The FPP layer is therefore *broader* than the API layer — but it sits entirely on top of the 3-API chokepoint, and is itself concentrated by region: a few quality-assured (stringent-regulator-approved) products for high-income markets at high prices, and many lower-priced products (<$1/dose) for LMIC markets with weaker regulatory oversight ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). In the **USA "one supplier controls the entire market"** ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)).

| Product (brand) | Supplier / marketer | Region / market | Citation |
|-----------------|---------------------|------------------|----------|
| **Bicillin L-A** | **Pfizer** (sole US supplier; also Canada) | USA, Canada — prefilled syringe | [Pfizer Canada — Bicillin L-A](https://www.pfizer.ca/en/our-products/bicillin-l-penicillin-g-benzathine); [CHAI/Oxford 2024 "one supplier controls the entire US market"](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/); [ASHP shortage detail](https://www.ashp.org/drug-shortages/current-shortages/drug-shortage-detail.aspx?id=909) |
| **Extencilline** (powder + diluent, 1.2M & 2.4M IU vials) | **Delpharm/Delbert**, distributed by **Provepharm**; manufactured in **Italy** for the French marketer | France (origin); imported into Australia & USA during shortages | [Provepharm — Extencilline](https://www.us.provepharm.com/extencilline12); [Australia TGA shortage notice](https://www.tga.gov.au/safety/shortages/information-about-major-medicine-shortages/about-2024-2025-shortage-bicillin-l-benzathine-benzylpenicillin-tetrahydrate-prefilled-syringe-injection) |
| **Lentocilin** (1.2M IU vials) | **Laboratórios Atral S.A.** (Portugal); imported into the US by **Mark Cuban Cost Plus Drug Co. (MCCPDC)** during the 2023–25 shortage | Portugal (origin); USA (shortage import) | [Benzathine benzylpenicillin — Wikipedia, brand list](https://en.wikipedia.org/wiki/Benzathine_benzylpenicillin); [ASHP shortage detail](https://www.ashp.org/drug-shortages/current-shortages/drug-shortage-detail.aspx?id=909) |
| **Retarpen** | **Sandoz** (Austria) | Austria and exported (also marketed in Costa Rica, Dominican Republic per brand lists) | [Benzathine benzylpenicillin — Wikipedia, brand list](https://en.wikipedia.org/wiki/Benzathine_benzylpenicillin) |
| **Penadur** | Marketed historically by **Wyeth/Pfizer** lineage (Switzerland/various) | Europe / various | [Benzathine benzylpenicillin — Wikipedia, brand list](https://en.wikipedia.org/wiki/Benzathine_benzylpenicillin) |
| **Brancaster** (benzathine benzylpenicillin powder) | Imported FPP listed on the Australian Register of Therapeutic Goods to cover the 2023–25 Bicillin shortage | Australia (Section 19A import) | [Australia MJA 2025, PMC11910946](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11910946/); [TGA shortage notice](https://www.tga.gov.au/safety/shortages/information-about-major-medicine-shortages/about-2024-2025-shortage-bicillin-l-benzathine-benzylpenicillin-tetrahydrate-prefilled-syringe-injection) |
| **Benzetacil** (regional brand) | Marketed in **Brazil / Latin America** | Brazil, LatAm | [Benzathine benzylpenicillin — Wikipedia, brand list](https://en.wikipedia.org/wiki/Benzathine_benzylpenicillin) |

That is **7 named finished-dose products/suppliers across ≥4 regions** (North America, Western Europe, Australia/Pacific, Latin America) — comfortably above the ≥5 required. Note that several of these (Extencilline, Lentocilin, Brancaster) only appear in the US/Australian markets *as shortage-import substitutes for Bicillin L-A*, which is itself evidence of the concentration this milestone is meant to expose.

---

## (c) Dated timeline of documented shortage / stockout events (≥8 entries)

| Year | Place / scope | Event | Source |
|------|---------------|-------|--------|
| **2014–2016** | Global — **39 of 95 responding countries** | WHO multi-country survey: 39 countries reported a BPG shortage during this window (named incl. Congo, Nigeria, Ethiopia, Mozambique, South Africa, Brazil, Uganda, Eritrea) | [Nurse-Findlay et al., PLOS Med 2017, PMC5744908](https://pmc.ncbi.nlm.nih.gov/articles/PMC5744908/) |
| **2015** | **Brazil** | Brazil issued a 2015 technical note recommending alternative regimens for non-pregnant women amid BPG shortage; congenital syphilis rose from 4.0 (2012) to 6.5 (2015) per 1,000 live births | [Nurse-Findlay et al., PLOS Med 2017, PMC5744908](https://pmc.ncbi.nlm.nih.gov/articles/PMC5744908/) |
| **2016** | **Latin America & Caribbean** (PAHO survey, 41 countries/territories) | PAHO survey found **5 countries** reporting BPG shortages (incl. Brazil) | [Nurse-Findlay et al., PLOS Med 2017, PMC5744908](https://pmc.ncbi.nlm.nih.gov/articles/PMC5744908/) |
| **2017** | **Americas (PAHO region)** | PAHO issued a regional statement/alert on the scope and impact of benzathine penicillin shortages | [PAHO, 27 Dec 2017](https://www.paho.org/en/news/27-12-2017-shortages-benzathine-penicillin-how-big-problem-and-why-it-matters) |
| **2019** | **Global (WHO follow-up survey)** | Follow-up survey identified **six countries still reporting shortages** — fewer than 2014–16 but persistent | [CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/) |
| **2023 (from ~Apr/May)** | **USA** | FDA-listed Bicillin L-A shortage (Pfizer sole supplier); CHAI 2024 noted it was expected to persist through mid-2024; driven partly by demand surge from a syphilis epidemic | [CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/); [ASHP shortage detail](https://www.ashp.org/drug-shortages/current-shortages/drug-shortage-detail.aspx?id=909) |
| **2023 (late) – 2025** | **Australia** | TGA notified of Bicillin L-A stockout; powdered imports (Brancaster, Extencilline) listed from Jan 2024; prompted calls for sovereign manufacturing | [Australia MJA 2025, PMC11910946](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11910946/); [TGA shortage notice](https://www.tga.gov.au/safety/shortages/information-about-major-medicine-shortages/about-2024-2025-shortage-bicillin-l-benzathine-benzylpenicillin-tetrahydrate-prefilled-syringe-injection) |
| **July 2025** | **USA** | **Pfizer recall** of multiple Bicillin L-A lots (10 Jul 2025) due to particulates in prefilled syringes; **FDA drug-shortage alert 14 Jul 2025** | [New Mexico DOH alert](https://www.nmhealth.org/publication/view/general/9308/); [CDC NCHHSTP Bicillin updates](https://www.cdc.gov/nchhstp/whats-new/bicillin-updates.html); [Minnesota DOH recall notice](https://www.health.state.mn.us/diseases/syphilis/hcp/bicillin.pdf) |

**Entry count: 8 dated events** (each with year, place, source), spanning 2014→2025. Supporting country-level detail for Congo/Nigeria/Ethiopia/Mozambique/Uganda/South Africa/Eritrea sits inside the 2014–16 WHO-survey row (all enumerated in M1's scorecard, same [PMC5744908](https://pmc.ncbi.nlm.nih.gov/articles/PMC5744908/) source).

---

## (d) The global demand-vs-need gap (CHAI figures)

Per the CHAI/Oxford 2024 analysis ([PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)):

- **Estimated global market demand (2016):** **74–100 million doses** (standardized to 1.2-million-unit doses) — explicitly described as **"less than half of what is required."**
- **Estimated need for RHD alone:** **~200 million annual doses** of 1.2-million-unit BPG.
- **Estimated need for syphilis:** **>6 million annual doses** of 2.4-million-unit BPG.

So the headline gap is roughly **74–100M doses *demanded/produced* against ~200M doses *needed* for RHD** — i.e. realized demand is on the order of **one-third to one-half of true clinical need**, before even counting syphilis. CHAI ties this directly to the upstream collapse: low, poorly-visible demand signals to API makers reinforce the off-patent, low-margin disincentive, which keeps the surviving three plants under-producing — a self-reinforcing under-supply loop ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)).

(Burden cross-check from M1: GBD 2021 puts RHD at ~54.8M prevalent cases / 373,345 deaths — consistent in order of magnitude with a 9-figure annual-dose need, since each prophylaxis patient needs ~13 doses/year. See `artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`.)

---

## (e) Single-point-of-failure analysis

The BPG chain is an hourglass with a dangerously thin neck. At the bottom, demand is enormous and geographically diffuse (54.8M RHD patients, mostly South Asia and sub-Saharan Africa, per M1). At the top, finished-dose supply looks superficially diverse — CHAI counts ≥30 FPP makers and at least seven distinct branded products reach market (Bicillin L-A, Extencilline, Lentocilin, Retarpen, Penadur, Benzetacil, regional generics). But **every one of those products is reconstituted from API that traces to just three plants in two Chinese provinces** ([CHAI/Oxford 2024, PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). A regulatory action, environmental-compliance shutdown, raw-material disruption, or commercial exit at any one of those three sites removes a third or more of the world's BPG API at a stroke — and because the molecule is low-margin and off-patent, there is no idle capacity or new entrant queued to absorb the loss. The neck narrows again downstream in the richest markets: in the **USA a single FPP supplier (Pfizer/Bicillin L-A) controls the entire market**, so a single recall — exactly what happened in **July 2025** (particulates) — tipped the country straight into shortage during a syphilis epidemic ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/); [CDC Bicillin updates](https://www.cdc.gov/nchhstp/whats-new/bicillin-updates.html)). The system has thus failed at **both** ends of the hourglass within the last decade: upstream (the 2014–16, 39-country shortage tied to API/FPP fragility) and downstream (the 2023–25 single-supplier US/Australia shortage). The structural lesson for a funder is that capacity-building money buys the most resilience at the API neck — adding even one quality-assured non-Chinese API line, or guaranteeing volume to keep the three Chinese lines producing at capacity, addresses the failure mode that all 30+ FPP makers silently share.

---

## Limitations & uncertainty

1. **The three API makers are counted authoritatively but named only inferentially.** The peer-reviewed CHAI source gives the *number* ("three Chinese API manufacturers") and the *region* ("two regions of China") but **does not name the companies** ([PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)). The specific names — North China Pharmaceutical/NCPC, CSPC, Jiangxi Dongfeng — come from a 2017 Al Jazeera investigation and trade databases, not from the regulatory/CHAI source, and could be partially out of date (a 2017 roster may not be the 2024–26 roster). I could **not independently confirm** that these three, and only these three, are the current open-market BPG-API suppliers.

2. **The "3 vs 4 / role of Sandoz" ambiguity is unresolved.** Al Jazeera's 2017 account described a *four*-company global set (3 Chinese + Sandoz/Austria), while CHAI's 2024 paper says *three Chinese*. Whether Sandoz Kundl sells BPG API on the open market, supplies only its own FPP (Retarpen), or has exited BPG API entirely is **not confirmable** from the sources located. This directly affects the single-point-of-failure count (a fourth, non-Chinese source would materially reduce concentration risk).

3. **The "≥30 FPP companies" figure is a 2016 CHAI estimate, now ~10 years old.** The finished-dose landscape almost certainly shifted with the 2023–25 shortage (entrants like MCCPDC importing Lentocilin, exits, recalls). The named-product table is a *spot list of identifiable brands*, not a current exhaustive census; brand-to-manufacturer mappings from drug-name databases (e.g. Wikipedia/Drugs.com lists) can lag corporate changes.

4. **Demand-vs-need figures are 2016-vintage CHAI modeling.** The 74–100M-demanded vs ~200M-needed RHD figures are explicitly framed as 2016 estimates with acknowledged poor demand visibility ([CHAI/Oxford 2024](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/)); the *need* figure is a modeled clinical requirement, not measured procurement, and the gap should be read as order-of-magnitude.

5. **Counter-evidence on framing supply as the sole bottleneck.** M1 showed that in several settings the binding constraint is register enrollment, retention, or adherence — not molecule availability (e.g. Uganda ~91% adherence among retained patients despite documented stockouts). A perfectly resilient API supply would not, by itself, close the prophylaxis gap; this milestone maps the *supply* failure mode, which is necessary but not sufficient.

---

## Source list (named, dated)

- **CHAI/Oxford supply-chain analysis (anchor; 3 API makers, ≥30 FPP makers, 74–100M vs 200M doses, US single supplier, 2019 six-country survey):** Khemiri et al. / CHAI, *International Health* 2024, 16(3):279 — [PMC10987389](https://pmc.ncbi.nlm.nih.gov/articles/PMC10987389/) / [Oxford Academic](https://academic.oup.com/inthealth/article/16/3/279/7288044)
- **Al Jazeera supply-chain investigation (names 3 Chinese + Sandoz; under-capacity claim), 2017:** [Al Jazeera, 21 May 2017](https://www.aljazeera.com/features/2017/5/21/why-is-the-world-suffering-from-a-penicillin-shortage)
- **WHO 2014–2016 multi-country shortage survey (39/95 countries; PAHO 5-country; Brazil 2015 note):** Nurse-Findlay et al., PLOS Med 2017 — [PMC5744908](https://pmc.ncbi.nlm.nih.gov/articles/PMC5744908/)
- **PAHO 2017 regional shortage statement:** [PAHO, 27 Dec 2017](https://www.paho.org/en/news/27-12-2017-shortages-benzathine-penicillin-how-big-problem-and-why-it-matters)
- **US Bicillin L-A shortage / ASHP listing:** [ASHP drug-shortage detail](https://www.ashp.org/drug-shortages/current-shortages/drug-shortage-detail.aspx?id=909)
- **July 2025 Pfizer recall (particulates) + FDA shortage alert:** [New Mexico DOH](https://www.nmhealth.org/publication/view/general/9308/); [CDC NCHHSTP Bicillin updates](https://www.cdc.gov/nchhstp/whats-new/bicillin-updates.html); [Minnesota DOH](https://www.health.state.mn.us/diseases/syphilis/hcp/bicillin.pdf)
- **Australia 2023–25 shortage + sovereign-manufacturing call:** MJA 2025 — [PMC11910946](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11910946/); [TGA shortage notice](https://www.tga.gov.au/safety/shortages/information-about-major-medicine-shortages/about-2024-2025-shortage-bicillin-l-benzathine-benzylpenicillin-tetrahydrate-prefilled-syringe-injection)
- **Finished-dose products/brands:** [Pfizer Canada — Bicillin L-A](https://www.pfizer.ca/en/our-products/bicillin-l-penicillin-g-benzathine); [Provepharm — Extencilline](https://www.us.provepharm.com/extencilline12); [Benzathine benzylpenicillin — Wikipedia](https://en.wikipedia.org/wiki/Benzathine_benzylpenicillin)
- **API-maker profiles:** [Jiangxi Dongfeng DMF (Pharmacompass)](https://www.pharmacompass.com/us-drug-master-files-dmfs/jiangxi-dongfeng-pharmaceutical-llc); [CSPC — Wikipedia](https://en.wikipedia.org/wiki/CSPC_Pharmaceutical_Group); [North China Pharmaceutical profile](https://baike.baidu.com/en/item/North%20China%20Pharmaceutical%20Co.,%20Ltd./35729)
- **Burden cross-reference:** M1 scorecard — `artifacts/2026-06-25-m1-coverage-stockout-scorecard.md`
