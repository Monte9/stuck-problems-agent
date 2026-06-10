# Spec: lead poisoning in low- and middle-income countries

## Objective
"Unstuck" here means compressing the desk-research grind that currently strands small field teams: turning scattered blood-lead surveys, product-testing datasets, and trade data into (1) a defensible ranked answer to "in which countries, and against which sources, should the next field team point its XRF guns?", and (2) a regulator-ready evidence dossier for the single best target — the Bangladesh turmeric playbook rebuilt for one new country. The end artifacts serve two audiences: funders deciding where marginal philanthropic dollars go now that the government multiplier is gone (Open Philanthropy / LEAF, LEEP, Pure Earth), and the national regulator in the chosen target country who needs a citable evidence base to act.

## Milestones

### M1: Data landscape inventory
- **Task:** Compile an inventory of publicly available blood-lead surveillance datasets and product-contamination datasets (paint, spices, cookware, cosmetics, battery-recycling site assessments) relevant to LMICs, and map which high-burden countries have usable data versus none.
- **Skill:** none — freeform
- **Artifact format:** `artifacts/YYYY-MM-DD-m1-data-landscape.md`. Two tables: (A) dataset inventory with columns: dataset name, custodian, years covered, sample type (blood / product / environmental), country coverage, access URL or citation; (B) country coverage matrix for at least the 25 highest-burden LMICs (burden per GBD or the UNICEF/Pure Earth "Toxic Truth" rankings) with columns: country, est. mean child BLL or % children >5 µg/dL (with source), blood-lead data available (Y/N/partial), product-testing data available (Y/N/partial). Plus a limitations section.
- **Done-criteria:**
  - Table A lists at least 12 distinct datasets/surveys, each with a working URL or full citation and a stated year range.
  - Table B covers at least 25 named LMICs, and every burden figure cites its source inline.
  - At least 5 countries are explicitly flagged as high-burden with no usable blood-lead data (the measurement gap the brief describes).
  - A limitations section names at least 3 concrete gaps or staleness risks in the inventory (e.g., paywalled data, pre-2020 surveys).

### M2: Priority-country shortlist
- **Task:** Using the M1 artifact as input, define an explicit scoring rubric (burden x data gap x tractability x absence of existing programs) and apply it to produce a ranked shortlist of 10 candidate countries for new source-attribution work, identifying the top 3.
- **Skill:** none — freeform
- **Artifact format:** `artifacts/YYYY-MM-DD-m2-priority-shortlist.md`. Sections: rubric definition (criteria, weights, scoring scale); ranked table of 10 countries with per-criterion scores and total; one-paragraph rationale per top-3 country; limitations section.
- **Done-criteria:**
  - The rubric is stated before the scores: every criterion has a defined scale and weight, and the total is reproducible arithmetic from the per-criterion scores.
  - Every per-criterion score for the top 3 countries is justified by at least one inline citation or an explicit pointer to a row in the M1 artifact.
  - The table contains exactly 10 countries, all drawn from or reconciled against M1's Table B (any country not in M1 gets a cited burden figure here).
  - Existing program presence (LEEP, Pure Earth, Stanford/Unleaded, UNICEF) is checked and stated per top-3 country with a citation or "none found as of <date>".

### M3: Source-attribution profiles for the top 3 countries
- **Task:** For each of the top 3 countries from M2, rank the candidate exposure sources (paint, spices/food, informal battery recycling, cookware/ceramics, cosmetics, water/other) by likelihood of being a dominant contributor, with an evidence grade per source, and recommend the first targets for field XRF testing.
- **Skill:** none — freeform
- **Artifact format:** `artifacts/YYYY-MM-DD-m3-source-profiles.md`. One section per country, each containing: a ranked source table with columns: source, evidence grade (A = direct local measurement / B = regional or analogous evidence / C = inference only), key evidence with citation, suggested first XRF/field targets; plus a per-country limitations note. A shared evidence-grade legend at top.
- **Done-criteria:**
  - Each of the 3 countries has at least 4 candidate sources rated, and every rated source has at least 1 inline citation.
  - Every evidence grade conforms to the stated A/B/C legend, and no grade-A claim rests solely on evidence from a different country.
  - Each country section ends with a "point the XRF here first" recommendation naming at least 2 concrete product categories or site types and the locality/market type to sample.
  - Each country section states at least 1 thing that field testing must resolve that desk research cannot.

### M4: Regulatory evidence dossier for the #1 country
- **Task:** Draft a Bangladesh-playbook-style evidence dossier for the top-ranked country and its top-ranked source from M3: the document a national regulator and an implementing NGO would need to start enforcement — existing law and responsible agency, evidence of contamination, supply-chain structure, named precedents, and a sequenced intervention plan.
- **Skill:** none — freeform
- **Artifact format:** `artifacts/YYYY-MM-DD-m4-evidence-dossier.md`. Sections: executive summary (<=1 page); the contamination evidence; legal/regulatory landscape (statute or standard, responsible agency, current enforcement status); supply-chain map in prose or table; intervention sequence modeled step-by-step on the Bangladesh turmeric case with explicit adaptations; key actors to engage; risks and unknowns.
- **Done-criteria:**
  - The responsible national agency and the specific statute, standard, or regulation (with number/year where it exists, or an explicit "no standard exists" finding) are named with citations.
  - Every factual claim in the contamination-evidence section has an inline citation; no uncited prevalence numbers.
  - The intervention sequence has at least 5 ordered steps, each mapped to its Bangladesh-playbook analog or marked as a deliberate departure with a stated reason.
  - The risks section names at least 3 country-specific failure modes (not generic ones), each tied to a cited fact about the country.

### M5: Funder-facing action brief
- **Task:** Synthesize M1-M4 into a short brief for a philanthropic funder (Open Philanthropy / LEAF-style) arguing where the next marginal dollars should go, with concrete fundable line items and cost anchors.
- **Skill:** none — freeform
- **Artifact format:** `artifacts/YYYY-MM-DD-m5-funder-brief.md`. Max ~1,500 words of body text: the case in one page; 3-5 fundable line items (what, who could execute, rough cost with cited comparator, expected output); explicit dependencies on field labor and regulator will that money alone cannot buy; appendix listing the four prior artifacts by path.
- **Done-criteria:**
  - Contains at least 3 fundable line items, each with a rough cost figure anchored to a cited real-world comparator (e.g., the Bangladesh program cost, a LEEP country-program budget, a Pure Earth rapid market screening).
  - Explicitly cites all four prior artifacts by file path and uses at least one specific finding from each.
  - Contains a section stating what the brief's recommendations do NOT solve (the field-labor and regulator-will constraints from the problem brief), with at least 2 named residual bottlenecks.
  - Body text is under 1,600 words (appendix excluded), verifiable by word count.
