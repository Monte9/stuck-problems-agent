# M3 — Triage Feature Schema for Ranking the Rescue Queue

**Problem:** CSAM Report Triage — turning 21M CyberTipline reports into a ranked rescue docket
**Milestone:** M3 — Prioritization / triage feature schema that ranks incoming reports into a rescue-priority queue
**Date:** 2026-06-24
**Builds on:** M1 completeness rubric (`artifacts/2026-06-24-m1-report-quality-rubric.md`) and M2 per-sender noise-tax scorecard (`artifacts/2026-06-24-m2-sender-noise-scorecard.md`)

---

## 0. What this schema is, and how it differs from M1

M1 scored **completeness** ("is this report investigable at all?"). M3 scores **rescue priority** ("of the investigable reports, which one most plausibly points at a child who can be helped *now*?"). These are different axes, and the difference is the whole point of the project. SIO frames the unsolved problem precisely as separating two reports that "look very similar" where one leads to "someone who was unwillingly spammed with CSAM" and the other "could lead to the discovery of someone abusing a child" (SIO 2024, Conclusion §8.2, p. 80, https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf).

A complete report (M1 = 95/100) about a long-deduplicated viral meme should sink in *this* queue; an incomplete-but-novel report carrying a self-generating-minor distress signal should rise. So M3 reuses M1's field-presence facts as *inputs* but re-weights them around imminence, novelty, jurisdiction, and sender reliability rather than around completeness.

**Design constraint inherited from the pipeline:** NCMEC already triages by escalation. It logged **63,892** reports as "urgent" or involving a child in imminent danger that were escalated for priority handling in 2023 (NCMEC 2023 CyberTipline Report, p. 9, https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf). This schema is a documented, auditable reconstruction of *that kind of* triage decision, not a claim to reproduce NCMEC's internal model (which is not public — see Limitations).

**Scope note on legality:** several features below (especially anything that depends on a human having *viewed* content, F2/F9) carry Fourth-Amendment / private-search-doctrine constraints that bound how they may be computed and used. Those constraints are deliberately deferred to M4; this artifact flags the touch-points but does not resolve them.

---

## 1. The feature table

Eight features across the four mandated signal families plus four additional features. **Direction** (+ raises priority, − lowers it). **Weight** is the maximum absolute points the feature can contribute; weights are the author's allocation (`[speculative]` on exact magnitudes — see §4), with the *ordering* of magnitudes justified per row. **Avail.** = available at intake (I) directly from report fields, or requires Enrichment/lookup (E).

| # | Feature | Signal family | What it captures | Data source / where it comes from | Value type / range | Dir. & weight | Avail. | Rationale |
|---|---------|--------------|------------------|-----------------------------------|--------------------|:------------:|:------:|-----------|
| **F1** | **Imminent-danger flag** | Imminent-danger | Report asserts a child is in active/ongoing danger (live abuse, sextortion-with-threat, self-harm, travel-to-meet, production-in-progress) | CyberTipline report narrative + the report-type/urgency field the platform sets; NCMEC's own "urgent / imminent danger" escalation category (NCMEC 2023 report, p. 9, https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf) | Categorical: None=0 / Indicator-present=1 / Explicit-imminent=2 | **+ 30** (15 pts per level) | **I** | Rescue is time-bound; an in-progress harm dominates any archival-content signal. Highest single weight by design — this is the one axis where a false negative can mean a child is harmed before the queue is worked. |
| **F2** | **Sextortion / enticement / first-person-contact indicator** | Imminent-danger (additional) | Evidence of an offender in two-way contact with a victim (grooming, sextortion demands, enticement), vs. passive possession/sharing | Report narrative, chat/communication field (M1 D6), report-type taxonomy ("online enticement" is a distinct CyberTipline category — NCMEC 2023 report, p. 6, https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf) | Binary: 0 / 1 | **+ 15** | **I** | A live offender–victim channel is both higher-harm and more time-sensitive than static CSAM trading; online enticement reports rose sharply (NCMEC reported a >300% rise in online-enticement reports 2021→2023, NCMEC 2023 report, p. 6). Separated from F1 because contact can be present without an explicit imminence assertion. |
| **F3** | **Novel-vs-known-hash status** | Novel-vs-known-hash | Whether the file is new to NCMEC's hash corpus (potential new victim) or a known/previously-classified duplicate | Enrichment: match the report's file/hash against NCMEC + industry hash sets (PhotoDNA / NCMEC hash sharing). NCMEC labeled 10.6M files and de-duplicates via hash matching before analyst review (NCMEC 2023 report, p. 11, same URL) | Categorical: Known-duplicate=0 / Partial-match=1 / Novel (no match)=2 | **+ 20** (10 pts per level) | **E** | A novel image is the strongest single signal of an *unidentified* victim; a known-hash duplicate has, by definition, already been seen and is far more likely to be re-circulation than new abuse. This is the axis that should sink the viral-meme noise that M1/M2 flagged. Requires a hash lookup — not knowable at intake. |
| **F4** | **U.S.-actionable jurisdiction** | Jurisdiction | Whether the offense/uploader resolves to a U.S. location an ICAC task force can act on (vs. routes abroad / unresolvable) | Enrichment: geolocate the upload/login IP (M1 D4) and any address; cross-reference ICAC regional coverage. NCMEC: **>91%** of 2023 reports resolved/referred outside the U.S.; ~1M of 36M+ resolved to a U.S. state, and origin of ~200k of those could not be confirmed (NCMEC 2023 report, pp. 15–16, same URL) | Categorical: Foreign/unresolvable=0 / U.S.-coarse=1 / U.S.-specific (state/county)=2 | **+ 16** (8 pts per level) | **E** | For a *U.S.* (ICAC) rescue queue, a foreign-resolving report is not actionable here regardless of severity (it routes to Interpol I-24/7) — so jurisdiction is a gating multiplier on usable priority. Not a moral discount; a routing fact. Positive direction because the queue is the U.S. docket; a parallel foreign queue would invert it. |
| **F5** | **Sender reliability (consumes M2 noise-tax tier)** | Sender-reliability | Prior-probability that *this sender's* reports carry actionable substance, from the M2 per-sender scorecard | **M2 scorecard** (`artifacts/2026-06-24-m2-sender-noise-scorecard.md`), keyed on the report's submitting-ESP field (present in every report) | Ordinal tier → points (table below); range −12 … +6 | **± (−12 … +6)** | **I** (tier lookup) / tier itself is **E**-derived in M2 | A report's source is a strong prior on whether its other fields are trustworthy or substantive. M2 already graded every named sender; M3 just looks up the tier. This is the explicit consumption point — see §1.1. |
| **F6** | **Report completeness (M1 score, banded)** | Sender-reliability / quality (additional) | The M1 0–100 completeness score, banded — a proxy for "can this even be worked if prioritized?" | Enrichment: run the **M1 rubric** (`artifacts/2026-06-24-m1-report-quality-rubric.md`) over the report's fields | Banded: <30→0 / 30–69→1 / ≥70→2 | **+ 10** (5 pts per band) | **E** (M1 must be scored) | A high-priority signal is wasted if the report has no file, no ID, no location to act on. Completeness is a *secondary* multiplier on actionability, deliberately weighted below imminence/novelty so a thin-but-novel report still beats a complete-but-stale one. |
| **F7** | **Victim-age / self-generated-by-young-minor indicator** | Victim-vulnerability (additional) | Whether the victim is indicated to be a young child or a self-generating minor under coercion (higher vulnerability) | Report narrative + victim-information field (M1 D7); CyberTipline self-generated-content flag where present | Categorical: Unknown=0 / Minor=1 / Young-child/coerced-self-gen=2 | **+ 8** (4 pts per level) | **I** | Younger and coerced-self-generating victims are higher-vulnerability and higher-rescue-value; NCMEC tracks self-generated content as a distinct, growing category. Lower weight than imminence/novelty because it modulates value rather than time-criticality, and is often unknown at intake. |
| **F8** | **Duplicate-burst / viral-meme penalty** | Noise-suppression (additional) | Whether this report is one of a known viral-duplicate burst or self-labeled meme/GAI-no-victim — the M1/M2 noise archetype | "Potential Meme" / "Generative AI" flags (M1 D8); NCMEC "informational vs referral" classification (NCMEC 2023 report, p. 8, same URL); enrichment: burst-count of identical hashes in the recent queue | Categorical: 0 (no) / 1 (flagged/suspected) / 2 (confirmed viral-dup or no-victim GAI) | **− 18** (−9 per level) | **I** for self-flags / **E** for burst-count | This is the dedicated counter-weight to the Amazon-AI-Services 1.1M "no actionable information" episode (M2 rank 1) and viral memes. Strong *negative* weight so a confirmed no-victim duplicate is pushed down even if other fields are complete. Self-flags are at intake; confirming a viral burst needs a lookup. |

### 1.1 Sender-reliability feature (F5) — explicit consumption of the M2 scorecard

F5 reads the submitting ESP off the report and maps it to its **M2 noise-tax tier**, using the exact tiers M2 assigned (`artifacts/2026-06-24-m2-sender-noise-scorecard.md`, §2). The mapping:

| M2 noise-tax tier (from M2 scorecard) | Example senders M2 placed here | F5 points |
|---|---|:---:|
| **SEVERE** | Amazon AI Services (M2 rank 1 — 1.1M reports, "no actionable information," 2025) | **−12** |
| **HIGH** (incl. NCMEC-named deficiency cohort) | Grindr (M2 rank 2), TMTG/Truth Social (rank 4), and the NCMEC-named cohort — Lightspeed Systems, Megapersonals, Redgifs, Internet Archive, gayboystube, ThumbSnap, BigBang Media, Fediverse Communications, JMS Internet, New Meta AB (M2 rank 5) — all on NCMEC's p.9 "consistently lack substantive information" list, >80% location-deficient | **−8** |
| **HIGH (self-corrected)** | Snapchat (M2 rank 3 — admitted prior over-reporting, recalibrated 2024) | **−4** |
| **MODERATE / OPAQUE** | WhatsApp, TikTok, X Corp, Imgur, Discord (M2 ranks 6–11) — high volume, no deficiency flag, no published field-quality data | **0** (neutral prior) |
| **GOOD-FAITH / LOW tax** | Facebook, Instagram, Google, Microsoft (M2 ranks 8, 12–14) — human review, files attached, de-duplication/bundling, no deficiency flag | **+6** |
| **Unknown sender** (not in M2) | any ESP M2 did not score | **0** |

This is a *prior*, not a verdict on the individual report: a SEVERE-tier sender can still file a genuine report, but the −12 reflects M2's finding that the base rate of actionable substance from that sender is very low. The asymmetry (−12 floor vs +6 ceiling) is deliberate — M2's signal is much stronger on the bad side (NCMEC explicitly names deficient senders; "good-faith" is inferred from program design, M2 §4) so the upside prior is capped tighter than the downside.

---

## 2. The scoring / ranking function

The priority score is a plain weighted sum of the eight features, evaluated in a fixed order with explicit tie-breaks so that two readers reach the **identical** ordering.

### 2.1 Definitions (every term)

For a report *r*, read or look up these eight integer feature levels:

- `F1 ∈ {0,1,2}` imminent-danger level
- `F2 ∈ {0,1}` sextortion/enticement/contact present
- `F3 ∈ {0,1,2}` novelty (0 known-dup, 2 novel)
- `F4 ∈ {0,1,2}` U.S.-actionable jurisdiction
- `F5 ∈ {SEVERE,HIGH,HIGH-SC,OPAQUE,GOODFAITH,UNKNOWN}` → mapped to points via the §1.1 table
- `F6 ∈ {0,1,2}` M1-completeness band
- `F7 ∈ {0,1,2}` victim-vulnerability level
- `F8 ∈ {0,1,2}` duplicate/viral/no-victim level

### 2.2 The function

```
PRIORITY(r) =
      15 * F1            # +0 / +15 / +30
    + 15 * F2            # +0 / +15
    + 10 * F3            # +0 / +10 / +20
    +  8 * F4            # +0 / +8  / +16
    +  SENDER(F5)        # one of {-12, -8, -4, 0, +6}  (per §1.1 table)
    +  5 * F6            # +0 / +5  / +10
    +  4 * F7            # +0 / +4  / +8
    -  9 * F8            # -0 / -9  / -18
```

`SENDER(F5)` is the lookup in the §1.1 table: SEVERE=−12, HIGH=−8, HIGH-SC=−4, OPAQUE=0, GOODFAITH=+6, UNKNOWN=0.

**Theoretical range:** minimum = 0+0+0+0+(−12)+0+0+(−18) = **−30**; maximum = 30+15+20+16+6+10+8+0 = **+105**. Scores are reported as raw integers (not normalized) so the arithmetic is auditable.

### 2.3 Ranking rule + deterministic tie-breaks

Sort reports by `PRIORITY(r)` **descending**. To guarantee two readers produce the *same* order on ties, break ties in this fixed lexicographic order (higher value first at each step):

1. Higher `F1` (imminent danger) — life-safety wins ties.
2. Then higher `F3` (novelty) — new victim wins.
3. Then higher `F4` (U.S.-actionable) — workable-here wins.
4. Then higher `F6` (completeness) — investigable wins.
5. Then **lower** report ID / earlier intake timestamp (FIFO) — fully arbitrary deterministic final key, so no genuine tie ever remains.

This makes the ordering a total order: any two readers applying §2.2 + §2.3 to the same reports get byte-identical rankings.

---

## 3. Three worked example reports, scored end-to-end

Three deliberately contrasting reports, including the M2/M1 noise archetype.

### Report A — "Live sextortion, novel image, Grindr-sourced, U.S."
A platform files a report: an account is actively sextorting a teenager (explicit threats to release images unless more are sent), narrative asserts ongoing danger. One attached image is novel (no hash match). Upload IP resolves to a specific U.S. county. Submitting ESP = **Grindr** (M2 rank 2 — HIGH tier, NCMEC-named deficiency cohort). The report itself happens to be well-populated: file + chat + IP present → M1 score ≈ 82 (band 2). Victim indicated as a 15-year-old (minor). Not a duplicate/meme.

| Feature | Level | Calc | Pts |
|---|:--:|---|:--:|
| F1 imminent danger | 2 (explicit) | 15×2 | **+30** |
| F2 sextortion/contact | 1 | — | **+15** |
| F3 novelty | 2 (novel) | 10×2 | **+20** |
| F4 jurisdiction | 2 (U.S.-specific) | 8×2 | **+16** |
| F5 sender (Grindr→HIGH) | HIGH | §1.1 | **−8** |
| F6 completeness (≈82→band 2) | 2 | 5×2 | **+10** |
| F7 victim vuln (minor) | 1 | 4×1 | **+4** |
| F8 duplicate/viral | 0 | −9×0 | **0** |
| **PRIORITY(A)** | | 30+15+20+16−8+10+4−0 | **= 87** |

The HIGH-tier sender penalty (−8) correctly *dents* but does not erase the priority of a genuine live-rescue report — exactly the intended behavior: the M2 prior is a thumb on the scale, not a veto.

### Report B — "Complete, human-reviewed, but a known viral duplicate from a good-faith sender, U.S."
Facebook (M2 GOOD-FAITH tier) files a fully-populated, human-reviewed report with file, account ID, upload IP (U.S. state-level), timestamp → M1 ≈ 95 (band 2). But the file is a **known-hash duplicate** (matches NCMEC corpus) and is in fact a long-viral meme; the "Potential Meme" flag is set and the queue shows a large identical-hash burst → F8 confirmed viral-dup. No imminence, no contact, no victim-vulnerability signal (re-circulation of old content).

| Feature | Level | Calc | Pts |
|---|:--:|---|:--:|
| F1 imminent danger | 0 | — | **0** |
| F2 sextortion/contact | 0 | — | **0** |
| F3 novelty | 0 (known-dup) | 10×0 | **0** |
| F4 jurisdiction | 1 (U.S.-coarse) | 8×1 | **+8** |
| F5 sender (Facebook→GOODFAITH) | GOODFAITH | §1.1 | **+6** |
| F6 completeness (≈95→band 2) | 2 | 5×2 | **+10** |
| F7 victim vuln | 0 | — | **0** |
| F8 duplicate/viral | 2 (confirmed) | −9×2 | **−18** |
| **PRIORITY(B)** | | 0+0+0+8+6+10+0−18 | **= 6** |

This is the headline behavior: a report that scores **95/100 on M1 completeness** scores **6 on M3 priority**. Completeness ≠ priority. The viral-duplicate penalty (−18) plus zero novelty/imminence sinks it, even though it is a model-quality report from the best sender. This is precisely the "buried by noise" inversion M1 §4 warned about, now operationalized.

### Report C — "Amazon-AI-Services-style automated dump, no actionable info, GAI no-victim"
An automated pipeline (submitting ESP = **Amazon AI Services**, M2 rank 1, SEVERE tier) files a report on a GAI-flagged image with no human review, hash only, no file, login-IP only resolving to a foreign/unresolvable location, no narrative → M1 ≈ 15 (band 0). "Generative AI" flag set; NCMEC's characterization of this sender's cohort is "no actionable information," apparent no real victim → F8 level 2.

| Feature | Level | Calc | Pts |
|---|:--:|---|:--:|
| F1 imminent danger | 0 | — | **0** |
| F2 sextortion/contact | 0 | — | **0** |
| F3 novelty | 0 (no file to match / treated as known-dup-equivalent, no novel-victim signal) | 10×0 | **0** |
| F4 jurisdiction | 0 (foreign/unresolvable) | 8×0 | **0** |
| F5 sender (Amazon AI→SEVERE) | SEVERE | §1.1 | **−12** |
| F6 completeness (≈15→band 0) | 0 | 5×0 | **0** |
| F7 victim vuln | 0 | — | **0** |
| F8 duplicate/viral/no-victim | 2 (confirmed GAI no-victim) | −9×2 | **−18** |
| **PRIORITY(C)** | | 0+0+0+0−12+0+0−18 | **= −30** |

This hits the theoretical floor (−30). The SEVERE sender prior and the no-victim GAI penalty both fire; nothing positive offsets them. This report sinks to the absolute bottom of the queue — the intended fate of the 1.1M-report episode.

### 3.1 Resulting ranking (provably consistent with §2)

| Rank | Report | PRIORITY | Why it sits here |
|:--:|---|:--:|---|
| 1 | **A** (live sextortion, novel, U.S.) | **87** | Highest by raw score; live-rescue + novel victim dominate even a HIGH-tier sender penalty. |
| 2 | **B** (complete viral duplicate, good sender) | **6** | High completeness, but zero imminence/novelty and a −18 viral penalty leave only +24 of positives. |
| 3 | **C** (automated GAI no-info, SEVERE sender) | **−30** | Floor: SEVERE sender prior + no-victim GAI penalty, no positive signal. |

Ordering 87 > 6 > −30 is a strict total order; no tie-breaks were needed. Every figure above is the direct sum shown in each report's table, so the order **follows mechanically** from §2.2 — two readers given A, B, C and this schema produce exactly this ranking.

---

## 4. Limitations & counter-evidence

**Mis-ranking failure modes (concrete):**

1. **The weights are an analyst allocation, not an empirically validated model.** The *ordering* of magnitudes (imminence > novelty > jurisdiction > sender/completeness > vulnerability, with a large viral penalty) is defensible from SIO/NCMEC's qualitative emphasis on imminent danger (NCMEC 2023 report, p. 9) and de-duplication (p. 11). But the exact coefficients (15/15/10/8/5/4/9 and the −12…+6 sender band) are `[speculative]`. SIO explicitly notes outcome data is missing — ICAC Task Forces lack outcome transparency (SIO 2024, §8.1.4, p. 80), so there is no arrest/rescue ground truth to fit weights against. A report could be mis-ranked relative to another purely because of an unvalidated weight.

2. **F1/F2 (imminence, contact) rely on the platform's narrative, which is gameable and uneven.** An imminent-danger level is only as good as the field the reporting platform populates; a high-quality platform that writes rich narratives will have F1 detected, a terse automated reporter with a genuinely urgent case may show F1=0 and be under-ranked. This *interacts perversely* with F5: a SEVERE/HIGH sender that actually catches a live case may be doubly penalized (low narrative + negative sender prior). The schema mitigates this only via the F1 tie-break, not in the base score.

3. **F3 novelty depends on hash-corpus coverage and viewing constraints.** "Novel" means "no match in the hash sets we check." A new victim's image that *happens* to match an unrelated hash, or a genuinely novel image the system cannot hash (e.g., never decrypted, E2EE — see M2 WhatsApp row), is mis-scored. Worse, computing F3/F6 may require *viewing* or hashing content in ways that implicate the private-search doctrine and Fourth-Amendment limits (Ackerman/Wilson line) — these constraints are M4's subject and could legally bar some of the enrichment this schema assumes.

4. **F4 jurisdiction is a U.S.-centric routing fact, not a severity judgment — and it can be self-fulfilling.** A foreign-resolving live-rescue case scores F4=0 and drops in *this* (U.S./ICAC) queue, which is correct for routing but means the schema must be paired with a parallel foreign-referral queue or it will systematically deprioritize non-U.S. children. Given >91% of reports resolve outside the U.S. (NCMEC 2023, pp. 15–16), F4 is doing heavy lifting and any geolocation error (VPN, CGNAT, login-vs-upload IP — M1 D4 caveat) flips a case's queue.

5. **F5 imports every limitation of M2.** The sender tiers are M2's *characterizations*, not measured per-report rates; "good-faith" is inferred from program design, "opaque" reflects absence of a negative signal (M2 §4). NCMEC's deficiency list is from the 2023 report and is binary, and a sender could have left/joined it since. A genuinely reformed SEVERE-tier sender is penalized on stale priors until M2 is refreshed. The −12 floor on one feature can, with F8, alone reach the −30 score floor — meaning sender identity plus a no-victim flag can bottom-rank a report before any positive signal is even considered, which is intended for the Amazon case but is a blunt instrument for edge cases.

**Counter-evidence / scope caveats:**

- **This is not NCMEC's actual model.** NCMEC's internal escalation logic (how it produced the 63,892 urgent escalations) is not public; deliberately so in part for Fourth-Amendment reasons (M1 §4, M4). This schema is a defensible *reconstruction* of that kind of triage from public signals, not a claim of fidelity to NCMEC's process.
- **F6 reuses M1 bands, which already collapse field quality** (M1 §4: an upload IP behind CGNAT scores the same as a residential one). So F6 inherits that over-crediting, and a report can earn the +10 completeness band on technically-present-but-dead fields.
- **Banding hides within-band differences.** F3, F6, F7, F8 are bucketed for inter-rater reproducibility; two reports differing only in within-band detail score identically and rely on the §2.3 tie-breaks, which are themselves coarse (and the final FIFO key is admittedly arbitrary). The schema trades fine discrimination for determinism on purpose.
- **The +105 / −30 range is not normalized.** Raw scores are kept for auditability, but they should not be read as a percentage or probability; PRIORITY=87 does not mean "87% urgent." It is an ordinal rank key only.
- **Recency of inputs:** the imminent-danger escalation count (63,892), the referral/informational split, the >91%-foreign and 10.6M-labeled-files figures are from the **NCMEC 2023 CyberTipline Report** (https://www.ncmec.org/content/dam/missingkids/pdfs/2023-CyberTipline-Report.pdf) — older than 12 months and cited as *design basis*, not current-state statistics. The SIO blueprint (April 2024) is likewise design basis. The Amazon AI Services 1.1M figure feeding F5 is the 2025 figure from M2 (NCMEC 2026 first-look, https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data).

---

### Run-log summary

I built an 8-feature rescue-priority schema (four mandated families — imminent-danger F1, novel-vs-known-hash F3, jurisdiction F4, sender-reliability F5 — plus four additions: enticement/contact F2, M1-completeness band F6, victim-vulnerability F7, and a dedicated viral-duplicate/no-victim penalty F8), with each row marked intake-vs-enrichment, a plain weighted-sum scoring function `PRIORITY = 15·F1 + 15·F2 + 10·F3 + 8·F4 + SENDER(F5) + 5·F6 + 4·F7 − 9·F8` (range −30…+105) plus a fully deterministic tie-break chain so two readers reach byte-identical orderings, and three worked reports scoring 87 / 6 / −30. F5 consumes the M2 scorecard directly by mapping each sender's M2 noise-tax tier to points (Amazon AI Services SEVERE = −12 … Facebook good-faith = +6), with an intentionally asymmetric band because M2's bad-side signal (NCMEC's named deficiency list) is far stronger than its inferred good-side. The most striking result is Report B: a model-quality report scoring 95/100 on the M1 completeness rubric collapses to a priority of 6 once the viral-duplicate penalty and zero novelty/imminence are applied — the schema operationalizes the exact "complete-but-worthless vs. thin-but-novel" inversion that M1 and SIO flagged as the core unsolved triage problem, and it does so while a HIGH-tier sender penalty merely dents (does not erase) a genuine live-rescue case.
