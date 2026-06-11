# Spec: CBT-I undertreatment — converting "covered and proven" into "ordered"

## Objective
"Unstuck" means a payer, formulary committee, or health-system pharmacy lead can act on CBT-I without commissioning their own research: they hold a single dossier that (a) quantifies what continued status-quo prescribing costs their population, (b) compares the FDA-cleared digital CBT-I products on evidence, regulatory status, and the 2025 CMS reimbursement pathway in enough detail to write a coverage policy, and (c) gives clinicians a concrete deprescribing-and-substitution pathway for the highest-harm group (older long-term z-drug/benzodiazepine users). The end artifact serves a payer or formulary decision-maker; the intermediate artifacts also serve health-services researchers. Everything is desk research over published literature, regulatory filings, and coding documents — no new data collection.

## Milestones

### M1: Cost-of-inaction baseline
- **Task:** Build a quantified, fully cited baseline of the gap: chronic insomnia prevalence, hypnotic prescribing volume and duration (US, with z-drug/benzodiazepine breakdown where published), documented harms in older adults, CBT-I receipt rates, and trained-provider supply — culminating in a per-100,000-adults cost-of-inaction estimate with explicit arithmetic.
- **Skill:** none — freeform
- **Artifact format:** Markdown report with (1) a summary table of key quantities (prevalence, % receiving CBT-I, hypnotic prescription volume, harm effect sizes, provider counts), each row with value, year, population, and source link; (2) a worked cost-of-inaction model per 100,000 adults showing every input and calculation step; (3) a limitations section.
- **Done-criteria:**
  - Every numeric claim in the summary table has a working citation (URL or DOI) to a primary or peer-reviewed/governmental source, with publication year stated.
  - The cost-of-inaction model shows its arithmetic line by line; an evaluator can reproduce the final figure from the stated inputs alone.
  - At least one sensitivity check is included (e.g., low/high prevalence or cost assumptions) producing a stated range, not just a point estimate.
  - The report includes a limitations section naming at least three specific weaknesses of the estimate (e.g., data vintage, US-only sources, productivity-cost attribution).

### M2: Digital CBT-I product and reimbursement dossier
- **Task:** Produce a head-to-head dossier of FDA-cleared or formerly cleared digital CBT-I products (at minimum Somryst and Sleepio/SleepioRx), covering regulatory status and history, pivotal-trial evidence with effect sizes, current commercial availability, list pricing where published, and the exact 2025 CMS coding/reimbursement pathway (HCPCS codes, payment status, which payers have adopted).
- **Skill:** none — freeform
- **Artifact format:** Markdown dossier with a comparison table (rows: product; columns: FDA status + clearance number/date, pivotal trials with N and primary-outcome effect size, availability/prescription model, price if published, applicable billing codes) followed by a narrative section on the CMS 2025 reimbursement mechanism and a limitations section.
- **Done-criteria:**
  - Each product's FDA status cites the FDA database entry or official FDA/company documentation by clearance number or date; products whose clearance lapsed or whose maker exited the market are flagged as such with a source.
  - Each product row cites at least one pivotal trial with sample size and primary-outcome result (effect size or between-group difference), linked to the publication or registry entry.
  - The reimbursement section names the specific HCPCS code(s) or CMS rule establishing 2025 coverage for digital mental-health treatments, with a link to the CMS document or an authoritative secondary source, and states what is and is not yet covered (e.g., Medicare vs. commercial).
  - Any fact that could not be verified (e.g., unpublished pricing) is explicitly marked "not found" rather than omitted or guessed.

### M3: Deprescribing-and-substitution brief for older long-term hypnotic users
- **Task:** Write a clinician-facing brief targeting adults 65+ on long-term z-drugs/benzodiazepines: the harm evidence, the case for substitution with CBT-I (digital or stepped-care), and a concrete tapering-plus-CBT-I pathway assembled from published deprescribing guidelines and trials (e.g., EMPOWER, existing deprescribing algorithms), including what step is delivered by whom.
- **Skill:** none — freeform
- **Artifact format:** Markdown brief with (1) a one-page harm summary table (outcome, effect size, source); (2) a stepped substitution pathway presented as an ordered list or table (step, action, who delivers it, evidence source); (3) a section on contraindications and when not to apply the pathway; (4) limitations.
- **Done-criteria:**
  - The harm table contains at least four distinct adverse outcomes (e.g., fractures, falls, cognitive effects, motor-vehicle accidents) each with a quantitative effect size and citation.
  - Every step in the substitution pathway cites at least one published guideline, trial, or deprescribing algorithm; no step is invented without a source.
  - The pathway specifies the delivering role for each step (e.g., GP, nurse, pharmacist, digital program, sleep specialist) — no step says only "clinician".
  - The brief includes an explicit contraindications/exclusions section citing at least one source (e.g., when CBT-I alone is inappropriate, comorbid conditions requiring specialist referral).

### M4: Integrated payer/formulary action dossier
- **Task:** Synthesize M1–M3 into a single decision-ready dossier for a payer or formulary committee: a one-page executive summary with the cost-of-inaction figure and recommended coverage actions, the product comparison, the substitution pathway, and a pre-empted objections section answering the likely pushbacks (adherence/dropout in digital CBT-I, market withdrawal risk, member-engagement costs, evidence quality).
- **Skill:** none — freeform
- **Artifact format:** Markdown dossier: executive summary (max ~1 page) with 3-5 numbered recommended actions; body sections drawing on the M1-M3 artifacts (cited by path); an objections-and-responses table (objection, evidence-based response, source); appendix listing all sources.
- **Done-criteria:**
  - The executive summary states the per-100,000 cost-of-inaction range from M1 and lists 3-5 recommended actions, each phrased as something a payer can do (e.g., "add HCPCS code X to covered benefits"), not generic advice.
  - The dossier explicitly references all three prior artifacts by file path and does not contradict their numbers; any updated figure is flagged with a reason.
  - The objections table contains at least four distinct objections, each with a cited response; at least one objection concerns digital CBT-I dropout/adherence and at least one concerns product market availability.
  - Every recommendation in the executive summary traces to evidence presented in the body (an evaluator can find the supporting section for each).
