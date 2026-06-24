# M3 — Triage Feature Schema for Ranking the Rescue Queue

**Problem:** CSAM Report Triage — turning 21M CyberTipline reports into a ranked rescue docket
**Milestone:** M3 — Prioritization / triage feature schema for ranking the rescue queue
**Date:** 2026-06-24
**Builds on:** M1 completeness rubric (`artifacts/2026-06-24-m1-report-quality-rubric.md`) and M2 sender noise-tax scorecard (`artifacts/2026-06-24-m2-sender-noise-scorecard.md`)

---

## 0. What this schema does, and the line it must not cross

M1 answered *"is this report complete enough to work?"* (a 0–100 completeness score). M2 answered *"which senders systematically submit non-actionable noise?"* (a 5-tier sender reliability ranking). **M3 answers a third, distinct question: given a queue of reports that have already been received, in what order should an ICAC/NCMEC analyst pull them?**

The critical design constraint, named explicitly by the Stanford Internet Observatory, is that completeness and priority are *not the same thing*: *"Two reports can look very similar, and yet if both were investigated one would lead to someone who was unwillingly spammed with CSAM and the other could lead to the discovery of someone abusing a child"* (SIO 2024, §8.2, p. 80, https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf). A fully-complete report about a long-viral deduplicated meme can score 95/100 on M1 completeness yet belong at the *bottom* of the rescue queue. So this schema deliberately separates **rescue urgency** (is a child in danger now? is this a novel offender?) from **workability** (completeness + sender reliability). The two combine multiplicatively, not additively (see §2), so that a high-urgency report is never buried by a low completeness score, and a complete-but-stale report never floats to the top.

**Scope honesty up front:** This is a *desk-research design*, not a deployed model. No weight here is fit to outcome data (arrests, rescues), because — as SIO documents — that outcome data does not exist publicly: ICAC Task Forces do not publish per-report disposition (SIO 2024, §8.1.4, p. 80). Every weight below is therefore an explicit analyst allocation marked `[speculative]` on its exact value; what is *sourced* is the direction (sign) and relative ordering of each feature, and the existence of the underlying signal. The point of stating them explicitly is reproducibility (§3), not empirical optimality (§4).

---

## 1. The feature table

Ten features across four mandated signal families (imminent-danger, novelty, jurisdiction, sender reliability) plus six additional features. Each row gives: what it captures, where it comes from in a report, value type/range, the **encoding** used by the scoring function in §2, the **direction and weight** of its effect, whether it is available **at intake** or needs **enrichment/lookup**, and a rationale with citation.

Direction key: ↑ = raises priority, ↓ = lowers priority. Weights are the coefficients used verbatim in the §2 function.

| # | Feature | What it captures | Data source / where in a report | Value type & encoding (the exact numbers §2 uses) | Direction & weight | Intake vs. enrichment | Rationale (with citation) |
|---|---------|------------------|---------------------------------|---------------------------------------------------|:------------------:|-----------------------|---------------------------|
| **F1** | **Imminent-danger flag** | An explicit signal that a child is in active/immediate danger (e.g. an enticement-in-progress, self-harm/sextortion, abuse-in-progress, "child appears to be at the location now") | Reporter free-text / "additional information" field; NCMEC's own urgent-escalation designation; enticement report type | Categorical → {none = 0, contextual cue = 1, explicit imminent flag = 2} | ↑ **w = 40** | **Intake** (the flag/keywords arrive with the report); NCMEC's own "urgent" tagging is intake-time analyst triage | This is the family the whole queue exists to surface. NCMEC made **63,892** urgent/imminent-danger escalations to law enforcement in 2023 — the reports where time-to-action maps directly onto child safety (NCMEC 2023 CyberTipline Report, p. 9, https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf). SIO frames sextortion/enticement as the categories where delay is most harmful (SIO 2024, §2, p. 18). Highest single weight by design. |
| **F2** | **Novelty: novel vs. known-hash status** | Whether the file is unknown to hash databases (potential *new* abuse / un-rescued victim) vs. a match to known, already-catalogued CSAM (potential duplicate) | Hash-match result against NCMEC/industry hash sets (PhotoDNA, NCMEC hash list); "Potential Meme"/viral flag in report | Categorical → {known-hash duplicate = 0, partial/unverified = 1, novel/no-match = 2} | ↑ **w = 30** | **Enrichment/lookup** — requires running the file/hash against NCMEC + industry hash databases after intake | Novel content disproportionately signals a victim not yet identified; known-hash matches are often viral redistribution. NCMEC labeled 10.6M files and uses hash matching specifically to suppress known duplicates before analyst review (NCMEC 2023 report, p. 11, same URL). SIO's core "spammed vs. abusing a child" distinction (§8.2, p. 80) is in large part the novel-vs-known axis. |
| **F3** | **U.S.-actionable jurisdiction** | Whether the report resolves to a U.S. location an ICAC team can act on, vs. resolving abroad (routed to Interpol/foreign LE) | Upload-IP geolocation (M1 D4); subscriber address; country resolution | Categorical → {resolves outside U.S. = 0, U.S. but unconfirmed/coarse = 1, confirmed U.S. state = 2} | ↑ **w = 15** | **Enrichment/lookup** — geolocation of the upload IP / address resolution happens post-intake | For a U.S. ICAC queue, a non-U.S. report is not directly actionable. **>91% of 2023 reports resolved/referred outside the U.S.**; only ~1M of 36M+ resolved to a U.S. state, and ~200k of those had unconfirmable origin (NCMEC 2023 report, pp. 15–16, same URL). This is the single largest structural filter (M2 §2 "diagnostic row"). Weighted below F1/F2 because it gates *who* acts, not *whether a child is in danger*. |
| **F4** | **Sender reliability (consumes M2 scorecard)** | A prior on whether *this sending platform's* reports are typically actionable, taken directly from the M2 noise-tax tiering | **The M2 scorecard's per-sender Noise-Tax tier** (`artifacts/2026-06-24-m2-sender-noise-scorecard.md`, §2), keyed on the reporting ESP name in the report header | Ordinal map from M2 tier → multiplier-base score: {Severe = 0, High = 1, Moderate/Opaque = 2, Good-faith-high-volume = 3} (see §1.1) | ↑ **w = 10** | **Enrichment/lookup** — requires a join from the report's ESP-name field to the M2 lookup table | Directly implements the spec's "consuming the M2 scorecard as the sender-reliability input." A report from Amazon AI Services (M2 rank 1, "Severe," 1.1M reports with *no actionable information*, NCMEC 2026 first-look, https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data) gets the lowest sender prior; a report from Meta/Facebook (M2 "Good-faith-high-volume," human review + files) gets the highest. See §1.1 for the exact crosswalk. |
| **F5** | **Report completeness (consumes M1 rubric)** | The M1 0–100 investigability score for *this* report — does it carry the file, human-review flag, who/where/when? | **M1 completeness rubric** total (`artifacts/2026-06-24-m1-report-quality-rubric.md`, §2), computed on the report's fields | Continuous 0–100, rescaled to 0–2 by `M1_total / 50` (capped at 2.0) | ↑ **w = 12** | **Mixed:** the field presence is **intake**, but computing the M1 score (esp. D2 human-review accuracy, D4 upload-vs-login IP) may need light enrichment | A report you cannot work cannot rescue anyone regardless of urgency. M1 §2 weights the *file* (D1, 20pts) and *human-review flag* (D2, 15pts) highest precisely because SIO says those most change downstream outcomes (SIO 2024 §8.1.1, p. 76). Rescaled to 0–2 so it sits on the same scale as F1–F4. |
| **F6** | **Victim-identification signal** | Direct presence of victim identity/location data, or a self-generated-minor indicator (a specific, often-rescuable child) | M1 D7 (victim info) field; reporter notes; self-gen indicator | Binary → {absent = 0, present = 1} | ↑ **w = 8** | **Intake** (the victim field is populated by the reporter at submission) | A report that already points at a specific identifiable child collapses the investigative distance to rescue. SIO lists "victim information (including location information)" as a distinct actionability field and ties NCMEC's victim-ID mandate to it (SIO 2024 §8.1.1, p. 76). Separate from F1: a victim can be identifiable without being in *imminent* danger. |
| **F7** | **Offender-identifier strength** | Whether a strong, resolvable identifier (upload IP, email, account ID) on the apparent offender exists — the lead investigators actually pull | M1 D3 (offender ID) + D4 (geolocation) fields | Categorical → {none/weak = 0, one strong identifier = 1, multiple strong = 2} | ↑ **w = 6** | **Mixed:** identifier presence is **intake**; verifying it is resolvable (not CGNAT/VPN/defunct) needs **enrichment** | The classic investigative "who." 18 U.S.C. 2258A(b)(1) lists email/IP/URL/payment/username as the discretionary identity fields (https://www.law.cornell.edu/uscode/text/18/2258A). M1's own limitation #3 warns Present/Absent over-credits dead identifiers (CGNAT, VPN), so this feature is deliberately low-weight and flags the enrichment need. |
| **F8** | **Duplicate-burst suppression** | Whether this report is one of a large burst of near-identical reports about the same content/offender already in the queue (e.g. the Belgian "500 reports on one offender in five months" pattern) | Cross-report dedup against the live queue (hash + offender-ID clustering) | Continuous penalty: `−min(duplicate_count_in_queue, 10) × 0.5`, i.e. 0 to −5 | ↓ **w = 1** (applied as a direct additive penalty, pre-scaled — see §2) | **Enrichment/lookup** — requires comparing against other reports already in the queue | Prevents one viral file or one already-known offender from flooding the top of the queue with redundant entries. SIO documents *"over 500 distinct CyberTipline reports about a single offender within a span of five months"* (SIO 2024, via Techdirt 2024-04-25, https://www.techdirt.com/2024/04/25/the-problems-of-the-ncmec-cybertipline-apply-to-all-stakeholders/). The *first* report of a burst should rank high (via F2/F1); the 2nd–Nth should not re-consume top slots. |
| **F9** | **Content-type severity / GAI status** | Whether content is flagged as Generative-AI (often no real victim) vs. apparent real-child abuse; and report-type severity (enticement/CSAM production > possession/redistribution) | M1 D8 classification flags ("Generative AI," "Potential Meme"); report category | Categorical → {flagged GAI-only, no real-victim nexus = −1; ordinary CSAM = 0; production/hands-on/enticement type = +1} | ↑/↓ **w = 7** | **Intake** (the GAI/meme/category flags are set by the reporter); accuracy may need **enrichment** | The 1.1M Amazon AI Services episode is the canonical "GAI-only, no actionable information" flood (NCMEC 2026 first-look, https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data). GAI-only content with no real-child nexus should be *deprioritized* (negative); apparent hands-on production should be *elevated*. SIO §8.1.1 lists "Generative AI"/"Potential Meme" as provenance fields (p. 76). |
| **F10** | **Report freshness / age** | How recently the incident occurred — recent uploads are more likely to have a live, locatable offender and preserved evidence | Incident timestamp (M1 D5) vs. report receipt date | Continuous → {≤7 days = 2, ≤90 days = 1, >90 days or unknown = 0} | ↑ **w = 5** | **Intake** (the incident timestamp is in the report); requires no lookup, just a date diff | Evidence-preservation windows and offender locatability decay with time. 18 U.S.C. 2258A(h) sets the provider preservation period (amended to 1 year; M1 §4 notes the 90-day→1-year change), so reports aging past the original 90-day window risk lost subscriber data (https://www.law.cornell.edu/uscode/text/18/2258A). The 7/90-day thresholds are `[speculative]` operational cutoffs; the *direction* (fresher = higher) is the sourced claim. |

**Family coverage check (done-criterion 1):** imminent-danger = **F1**; novel-vs-known-hash = **F2**; jurisdiction = **F3**; sender reliability = **F4**. Additional features (≥2 required, 6 provided): **F5** completeness, **F6** victim-ID, **F7** offender-ID strength, **F8** duplicate-burst, **F9** content-type/GAI, **F10** freshness. Every row names a data source and an intake-vs-enrichment classification.

### 1.1 The M2 → F4 sender-reliability crosswalk (the hard done-criterion)

F4 does not invent a sender prior — it **reads the M2 scorecard's Noise-Tax tier for the reporting ESP** and maps it to a 0–3 base. The crosswalk, applied by joining the report's ESP-name header to M2 §2:

| M2 Noise-Tax tier (M2 §2) | Example M2 senders | F4 raw value | Interpretation |
|---------------------------|--------------------|:------------:|----------------|
| **Severe** | Amazon AI Services (rank 1, 1.1M no-info reports) | **0** | Strongest negative prior; this ESP's reports are presumptively non-actionable |
| **High** (incl. named-deficiency list) | Grindr, Snapchat (pre-recalibration), TMTG/Truth Social, the NCMEC-named p.9 cohort | **1** | NCMEC has named these as consistently lacking substantive information (NCMEC 2023, p. 9) |
| **Moderate / Opaque** | WhatsApp, TikTok, Google, X, Imgur, Discord, Microsoft | **2** | No deficiency flag, no published quality rate — presumptively workable |
| **Good-faith high-volume** | Facebook, Instagram (Meta: human review, files, bundling) | **3** | Strongest positive prior; quality-conscious reporting |

So a report submitted by **Amazon AI Services** enters F4 with raw value **0** (× w=10 → contributes 0 to the urgency-adjacent block), while an otherwise identical report from **Facebook** enters with raw value **3** (→ contributes 30). This is the M2 output flowing directly into the M3 rank, exactly as the spec requires. Senders absent from the M2 table default to the "Moderate/Opaque" value of 2 (stated assumption, matching M2's treatment of unflagged senders).

---

## 2. The ranking function (fully deterministic)

The function is built so that two readers, given identical feature encodings, compute identical scores and therefore identical orderings.

**Step 1 — encode each feature** to the exact numeric value defined in its §1 row (F1–F7, F9–F10 to their categorical/continuous encodings; F4 via the §1.1 crosswalk; F5 via `M1_total/50` capped at 2.0).

**Step 2 — compute the weighted Priority Score:**

```
RAW = w1·F1 + w2·F2 + w3·F3 + w4·F4 + w5·F5 + w6·F6 + w7·F7 + w9·F9 + w10·F10

with weights:
  w1(F1 imminent)      = 40
  w2(F2 novelty)       = 30
  w3(F3 jurisdiction)  = 15
  w4(F4 sender/M2)     = 10
  w5(F5 completeness)  = 12
  w6(F6 victim-ID)     = 8
  w7(F7 offender-ID)   = 6
  w9(F9 content-type)  = 7
  w10(F10 freshness)   = 5

PRIORITY = RAW + F8_penalty
where F8_penalty = −min(duplicate_count_in_queue, 10) × 0.5   (range 0 to −5)
```

**Step 3 — rank** reports by `PRIORITY`, descending. Ties (equal PRIORITY) break by, in order: (a) higher F1, then (b) higher F2, then (c) lower F8 duplicate count. This tie-break chain guarantees a total order.

**Why additive-within-an-urgency-design rather than purely multiplicative.** I considered making completeness/sender a *multiplier* on urgency (so a complete imminent-danger report from a good sender dominates). I rejected pure multiplication because it lets a single zero (e.g. a Severe sender, F4=0) zero out a genuine imminent-danger report — exactly the failure SIO warns against (a real victim buried because the platform is a known noise source). The weighted-sum keeps F1 (imminent, max contribution 80) structurally dominant over the entire workability block (F4+F5+F6+F7 max = 10·3 + 12·2 + 8 + 6·2 = 30+24+8+12 = 74), so no completeness/sender deficit can on its own outrank a fully-flagged imminent-danger case. The maximum possible RAW is `40·2 + 30·2 + 15·2 + 10·3 + 12·2 + 8 + 6·2 + 7·1 + 5·2 = 80+60+30+30+24+8+12+7+10 = 261`.

**Determinism note:** every encoding is a closed enumerated set or a stated formula, so there is no scorer discretion left. Two readers handed the three example reports in §3 will produce the byte-identical arithmetic shown there.

---

## 3. Three example reports — scored, with full per-feature arithmetic

The three are chosen to stress the design: **R1** an imminent-danger sextortion case from a mediocre sender; **R2** a complete-but-known-meme report from a *good* sender (the M1-high / M3-low trap); **R3** a novel-content report from the **Severe** Amazon AI Services sender (the M2 noise archetype). The ordering below must follow purely from §2.

### R1 — Active sextortion, child possibly at location now (sender: Snapchat / M2 "High")

Scenario: A user-report-driven CyberTip describes an ongoing financial-sextortion thread, attaches the chat and the file, includes the offender account + an upload IP resolving to a confirmed U.S. state, names a self-identified minor victim with a city, timestamped 2 days ago. ESP = Snapchat (M2 "High", F4=1). One related duplicate already in queue.

| Feature | Encoding (per §1) | Value | Weight | Contribution |
|---|---|:---:|:---:|:---:|
| F1 imminent | explicit imminent flag (active sextortion, "at location now") | 2 | 40 | **80** |
| F2 novelty | file is novel (no hash match) | 2 | 30 | **60** |
| F3 jurisdiction | confirmed U.S. state | 2 | 15 | **30** |
| F4 sender (M2) | Snapchat → "High" → 1 | 1 | 10 | **10** |
| F5 completeness | M1 ≈ 92/100 → 92/50 = 1.84 | 1.84 | 12 | **22.08** |
| F6 victim-ID | victim named + city → present | 1 | 8 | **8** |
| F7 offender-ID | account + upload IP → multiple strong | 2 | 6 | **12** |
| F9 content-type | enticement/sextortion type → +1 | 1 | 7 | **7** |
| F10 freshness | 2 days → ≤7 days → 2 | 2 | 5 | **10** |
| F8 penalty | 1 duplicate → −min(1,10)×0.5 | — | — | **−0.5** |
| **PRIORITY** | | | | **80+60+30+10+22.08+8+12+7+10−0.5 = 238.58** |

### R2 — Fully-complete report about a long-viral known meme (sender: Facebook / M2 "Good-faith")

Scenario: A meticulously-completed report from Meta/Facebook — file attached, human-reviewed, full who/where/when, U.S. upload IP — but the file is a hash-match to a years-old viral known-CSAM meme (the M1-high/M3-low trap). Not imminent. No specific live victim beyond the depicted (already-identified, historical) one. Incident date unknown/old. It's part of a 40-report duplicate burst of the same meme.

| Feature | Encoding (per §1) | Value | Weight | Contribution |
|---|---|:---:|:---:|:---:|
| F1 imminent | no danger cue | 0 | 40 | **0** |
| F2 novelty | known-hash duplicate | 0 | 30 | **0** |
| F3 jurisdiction | confirmed U.S. state | 2 | 15 | **30** |
| F4 sender (M2) | Facebook → "Good-faith" → 3 | 3 | 10 | **30** |
| F5 completeness | M1 ≈ 95/100 → capped at 2.0 | 2.0 | 12 | **24** |
| F6 victim-ID | depicted victim already historically ID'd, no *new* victim → absent | 0 | 8 | **0** |
| F7 offender-ID | redistributor account + IP → multiple strong | 2 | 6 | **12** |
| F9 content-type | ordinary known CSAM (not GAI, not production) | 0 | 7 | **0** |
| F10 freshness | incident date old/unknown → 0 | 0 | 5 | **0** |
| F8 penalty | 40 duplicates → −min(40,10)×0.5 = −5 | — | — | **−5** |
| **PRIORITY** | | | | **0+0+30+30+24+0+12+0+0−5 = 91** |

This is the schema working as designed: R2 scores **95/100 on M1 completeness** (near-perfect) but lands far below R1 because it is non-novel, non-imminent, victim-less, stale, and duplicate-penalized. Completeness alone does not buy rescue priority.

### R3 — Novel-content report from Amazon AI Services (M2 "Severe"), thin fields

Scenario: An automated report from **Amazon AI Services** (M2 rank 1, "Severe"). The flagged file does *not* match a known hash (novel), and is flagged "Generative AI." No human review, no file attached (hash + classifier output only), only a coarse/login IP that does not confirm a U.S. state, no victim data, no timestamp semantics. Not imminent. No queue duplicates.

| Feature | Encoding (per §1) | Value | Weight | Contribution |
|---|---|:---:|:---:|:---:|
| F1 imminent | no danger cue | 0 | 40 | **0** |
| F2 novelty | no hash match → novel | 2 | 30 | **60** |
| F3 jurisdiction | login IP only, U.S. unconfirmed → 1 | 1 | 15 | **15** |
| F4 sender (M2) | Amazon AI Services → "Severe" → 0 | 0 | 10 | **0** |
| F5 completeness | M1 ≈ 12/100 (no file, no review) → 12/50 = 0.24 | 0.24 | 12 | **2.88** |
| F6 victim-ID | none | 0 | 8 | **0** |
| F7 offender-ID | weak account ID only | 0 | 6 | **0** |
| F9 content-type | flagged GAI-only, no real-victim nexus → −1 | −1 | 7 | **−7** |
| F10 freshness | no usable timestamp → 0 | 0 | 5 | **0** |
| F8 penalty | 0 duplicates | — | — | **0** |
| **PRIORITY** | | | | **0+60+15+0+2.88+0+0−7+0+0 = 70.88** |

Note the design tension R3 exposes: novelty (F2=60) pulls it *up*, but the GAI flag (F9=−7), Severe sender (F4=0), and near-zero completeness (F5=2.88) hold it down. If the GAI flag were *wrong* (a real novel victim mislabeled as GAI), the schema would under-rank it — see Limitations #2.

### Resulting ranking (done-criteria 3 & 4)

| Rank | Report | PRIORITY | Why it sits here |
|:---:|---|:---:|---|
| **1** | **R1** (imminent sextortion) | **238.58** | Imminent-danger flag (F1=80) + novelty + U.S. + victim-ID dominate. The rescue case. |
| **2** | **R2** (complete known-meme) | **91** | High completeness + good sender + U.S., but zero urgency/novelty and a −5 duplicate penalty keep it well below R1. |
| **3** | **R3** (novel GAI-flagged, Severe sender) | **70.88** | Novelty alone (60) cannot overcome a wrong-content GAI penalty, Severe-sender prior, and near-zero completeness. |

**Order: R1 > R2 > R3.** This follows mechanically from the §2 arithmetic shown (238.58 > 91 > 70.88); any reader applying the encodings reproduces it. The result is intuitively correct: the only report with a child in active danger ranks first; a flawless-but-stale duplicate beats a thin novel-but-likely-synthetic report; and the M2 "Severe" Amazon archetype is correctly pushed to the bottom *despite* its novelty, which is exactly the noise-suppression behavior M2 motivated.

---

## 4. Limitations & counter-evidence

**Where this schema can mis-rank a real report:**

1. **No weight is fit to outcome data — they are analyst allocations.** The exact coefficients (40/30/15/12/10/8/7/6/5) are `[speculative]`. Only their *signs* and *relative ordering* are sourced (imminent > novelty > jurisdiction is defensible from NCMEC's urgent-escalation emphasis and the >91%-international structural filter; the precise gaps are not). SIO documents that the outcome data needed to calibrate these — per-report arrest/rescue dispositions from ICAC Task Forces — is not published (SIO 2024 §8.1.4, p. 80). Until it is, this schema is a *defensible default*, not an optimized model, and two reasonable analysts could pick different weights and reorder *close* cases (R2 vs R3 are only ~20 points apart and could flip under modest reweighting).

2. **F9 (GAI flag) and F2 (novelty) interact dangerously when the GAI flag is wrong.** A *real* novel abuse image mis-flagged as "Generative AI" gets F9=−7 and would be under-ranked — the catastrophic error. The schema trusts a reporter-set provenance flag that the 1.1M Amazon AI Services episode shows is exactly the field under volume pressure. M1's limitation #1 (gameable flags) applies here too: the GAI penalty rewards correct labeling and punishes the mislabeled victim. Operationally, F9's negative branch should arguably require *human confirmation* before it deprioritizes a novel file, which this static schema does not enforce.

3. **F4 imports every M2 limitation wholesale.** M2's sender tiers are themselves the *author's* characterization (M2 §3), the deficiency list is a binary 2023 snapshot (M2 Limitations #2), and "Moderate/Opaque" reflects *absence of a negative signal*, not evidence of quality. So F4 can be stale (a sender that left/joined NCMEC's list since 2023) or mis-calibrated (an opaque sender defaulted to 2 could really be excellent or terrible). The default-to-2 rule for unlisted senders is a stated assumption, not a measurement.

4. **Several "intake" features actually need enrichment to be trustworthy.** F3 (jurisdiction), F2 (hash lookup), F7-verification (resolvable vs CGNAT/VPN), and F8 (cross-queue dedup) all require post-intake processing. A queue that ranks *at intake* before enrichment would have to treat these as provisional, and the ordering could change once enrichment completes — i.e. the rank is not stable until lookups finish. The table marks these honestly, but it means "the queue order" is a moving target during enrichment, not a one-shot computation.

5. **Additive weighting can still let a stack of medium features approximate a real urgency signal — or fail to.** Because F1's max contribution (80) is large but finite, a contrived report with high novelty + U.S. + complete + good sender + production-type (60+30+24+30+7 = 151) could outrank a *contextual-cue-only* imminent case (F1=1 → 40, plus weak other features). I judged contextual-cue imminent cases *should* sometimes sit below a strong novel-production case, but reasonable people disagree; a strict "any imminent flag floats to top" lexicographic rule is an alternative design this rejects in favor of a graded score. The choice is explicit so it can be audited.

6. **Legal-admissibility constraints are deliberately out of scope here and may forbid some of this.** Whether NCMEC/ICAC may *act on* F2 (hash-matching), F4 (sender-reliability scoring), or F5 (viewing the file to score completeness) without implicating the private-search doctrine / Fourth Amendment is **M4's job**, not M3's. This schema specifies *what to rank on*; M4 will annotate which of these features or steps are legally constrained (e.g. whether scoring completeness requires viewing content in a way that converts NCMEC into a government agent). A feature being computable does not mean it is admissibly usable — that gap is the explicit handoff to M4.

**Counter-evidence / scope caveats:**

- **The three example reports are constructed, not drawn from real CyberTipline data**, which is non-public. They are designed to exercise the schema's intended behaviors (imminent-on-top, complete-meme-demoted, severe-sender-suppressed), so they *confirm the schema does what it was built to do* rather than independently *validating* the weights. That is a demonstration, not an evaluation.
- **The 63,892 urgent-escalation and >91%-international figures are 2023** (NCMEC 2023 report) — the most recent NCMEC report with this field-level breakdown; the 1.1M Amazon figure is 2025 (NCMEC 2026 first-look). The cross-year mix mirrors M2's and is disclosed per-cell. No figure is presented as a year other than its source's.
- **Multiplicative vs. additive is a genuine design fork.** I chose weighted-sum to protect imminent-danger cases from zero-multipliers, but a multiplicative urgency×workability model is equally defensible and would rank differently when an urgent report comes from a Severe sender. The choice is stated (§2) so a reviewer can substitute the alternative and re-derive.

---

### Run-log summary

I produced a 10-feature triage schema (the four mandated families — F1 imminent-danger, F2 novel-vs-known-hash, F3 jurisdiction, F4 sender-reliability — plus six more: completeness, victim-ID, offender-ID strength, duplicate-burst penalty, content-type/GAI, and freshness), with F4 wired directly to the M2 noise-tax tiers via an explicit crosswalk (Severe→0, High→1, Moderate/Opaque→2, Good-faith→3) so that an Amazon AI Services report enters with the lowest sender prior and a Facebook report with the highest. The ranking function is a fully-specified weighted sum (imminent w=40 down to freshness w=5) plus a duplicate penalty and a stated tie-break chain, and I scored three constructed reports end-to-end with per-feature arithmetic yielding R1 (238.58) > R2 (91) > R3 (70.88). What surprised me while building it was how hard the F9 GAI feature fights the F2 novelty feature: the *novel* archetype report (R3) is exactly the one most likely to be a synthetic GAI false-alarm, so the two highest-signal "this might be a new victim" features point in opposite directions on the same report, and the only honest resolution — making the GAI deprioritization require human confirmation — is something a static feature schema can specify but cannot itself enforce, which is a clean seed for M4's human-in-the-loop / admissibility constraints.
