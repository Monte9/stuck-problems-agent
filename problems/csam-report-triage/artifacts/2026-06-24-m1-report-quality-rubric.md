# M1 — CyberTipline Report-Completeness Rubric

**Problem:** CSAM Report Triage — turning 21M CyberTipline reports into a ranked rescue docket
**Milestone:** M1 — Report-quality rubric grounded in the SIO 2024 blueprint + 18 U.S.C. 2258A
**Date:** 2026-06-24

---

## 1. What this rubric is and is not

This is a **completeness/actionability** scoring rubric: given one CyberTipline report, it produces a 0–100 score for how investigable that report is, based on the fields that NCMEC and law enforcement say make a report worth working. It is **not** a measure of the severity of the underlying conduct (a fully-completed report about an old, deduplicated meme can score high on completeness yet be low priority — that prioritization layer is M3). The rubric here answers a narrower question the SIO report flagged as unsolved: *"Two reports can look very similar, and yet if both were investigated one would lead to someone who was unwillingly spammed with CSAM and the other could lead to the discovery of someone abusing a child"* (SIO 2024, Conclusion §8.2, p. 80, https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf). Completeness is a necessary precondition for telling those two apart.

### Statutory framing that shapes the whole rubric

18 U.S.C. 2258A separates a **mandatory duty** from **discretionary contents**:

- **2258A(a)(1)** — a provider with actual knowledge of an apparent CSAM violation "shall, as soon as reasonably possible … take the actions described," i.e. the *quantity* of reporting is compelled (https://www.law.cornell.edu/uscode/text/18/2258A).
- **2258A(b)** — the report "may, at the **sole discretion of the provider**, include the following information" (chapeau of subsection (b), https://www.law.cornell.edu/uscode/text/18/2258A). Every quality field below — identity, timestamps, geolocation, the actual file, the full communication — is **optional under the statute**.

This (a)-mandatory / (b)-discretionary split is the root cause the rubric measures: the law forces volume but makes every quality dimension voluntary. That is exactly the gap SIO names — *"There are no legal requirements regarding what information an ESP must include in a CyberTipline report, resulting in significant disparities in the volume, content and quality of reports"* (SIO 2024, summarized in HSToday, 2024-04, https://www.hstoday.us/subject-matter-areas/cybersecurity/stanford-report-calls-for-overhaul-of-online-child-exploitation-reporting-system/).

---

## 2. The rubric

Each dimension is scored **Present (full points) / Partial (half, rounded down) / Absent (0)**. Weights sum to 100. Definitions of Partial are given per row so two scorers reach the same number.

| # | Dimension | What it captures | Statutory / SIO basis (citation) | Weight | Scoring: Present / Partial / Absent |
|---|-----------|------------------|----------------------------------|:------:|-------------------------------------|
| D1 | **Actual file included** (not hash alone) | The report carries the suspected image/video itself, not merely a hash fingerprint | 18 U.S.C. **2258A(b)(4)** ("any visual depiction of apparent child pornography or other content," https://www.law.cornell.edu/uscode/text/18/2258A); SIO §8.1.1 platform rec: *"the associated file (a hash alone is insufficient)"* (p. 76) | **20** | Present = file attached. Partial = hash + thumbnail/derivative only. Absent = hash value only |
| D2 | **Human review flag set correctly** ("File Viewed by Company") | Whether a human at the platform reviewed *this exact file*, accurately signalled | SIO §8.1.1: check the box *"if and only if a human reviewed the file associated with this report"* (p. 76); SIO: an accurate flag increases NCMEC's ability to identify new victims, escalate, and lets LE triage (p. 76). Field implements the discretionary review under 2258A(b) | **15** | Present = box accurately reflects a human having viewed the exact file. Partial = human reviewed a prior copy of the image but not this exact file (per SIO this should *not* be checked). Absent = no human review / flag absent |
| D3 | **Offender identity & contact info** ("who") | Email, IP, URL, payment, username, or other identifying data on the apparent offender | 18 U.S.C. **2258A(b)(1)** (identity incl. "electronic mail address, Internet Protocol address, uniform resource locator, payment information …," https://www.law.cornell.edu/uscode/text/18/2258A); SIO "who" component (p. 76) | **15** | Present = ≥1 strong identifier (IP/email/account ID). Partial = weak identifier only (screen name with no resolvable handle). Absent = none |
| D4 | **Upload geolocation** ("where") | Location of the involved individual/site, ideally an **upload** IP (not just login IP) | 18 U.S.C. **2258A(b)(3)** (geographic location incl. IP or "at least one form of geographic identifying information," https://www.law.cornell.edu/uscode/text/18/2258A); SIO §8.1.1: *"location information, particularly an upload IP address"*; SIO field-quality finding that login-IP-only reports go uninvestigated (p. 41/§5.4) | **15** | Present = upload IP or verified address. Partial = login IP or coarse geo only. Absent = no location data |
| D5 | **Incident timestamp + timezone semantics** ("when") | When/how content was uploaded/transmitted, with timezone and a definition of "incident time" | 18 U.S.C. **2258A(b)(2)** ("information relating to when and how a customer or subscriber … uploaded, transmitted, or received content," with time/timezone, https://www.law.cornell.edu/uscode/text/18/2258A); SIO §8.1.1: *"the time of the incident (including a field describing how the platform defines the incident time)"* (p. 76) | **10** | Present = timestamp + timezone + defined incident semantics. Partial = bare timestamp, no timezone/definition. Absent = no time data |
| D6 | **Complete communication / chat context** ("what") | The full surrounding communication or chat, not just an isolated file | 18 U.S.C. **2258A(b)(5)** ("the complete communication containing any visual depiction … including any data or information regarding the transmission," https://www.law.cornell.edu/uscode/text/18/2258A); SIO §8.1.1: *"…or chat"* listed alongside the file as actionability-enhancing; SIO NCMEC rec for a *"dedicated field and standard structured data format … to submit chat text and associated metadata"* (p. 78) | **10** | Present = full communication/chat thread attached. Partial = partial excerpt/metadata only. Absent = isolated file, no context |
| D7 | **Victim information** | Identity / location data on the apparent victim (vs. offender) | SIO §8.1.1: *"victim information (including location information)"* as a distinct actionability field (p. 76); supports NCMEC's victim-identification mandate (rescue is the goal of D2 per SIO p. 76) | **8** | Present = victim identifier or location. Partial = indirect victim signal (e.g. self-generated indicator). Absent = none |
| D8 | **Content-classification flags** (GAI / Potential Meme / known-vs-novel) | Correct use of the "Generative AI," "Potential Meme," and viral/known-content signals | SIO §8.1.1 lists *"Potential Meme," "Generative AI"* as *"other important fields"* and urges provenance signalling (p. 76); these flags are how the 1.1M Amazon-style and viral-meme noise is meant to be self-labelled (SIO p. 76; NCMEC 2026 GAI data, https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data) | **7** | Present = applicable flags set and plausibly correct. Partial = some flags set/missing inconsistently. Absent = no classification flags despite content type warranting them |
| | | | **Total** | **100** | |

**Why D1 and D2 carry the most weight.** SIO repeatedly singles out the actual-file inclusion and the accurate human-review flag as the two factors that most change downstream outcomes — NCMEC victim identification, accurate escalation, and law-enforcement triage all hinge on them (SIO §8.1.1, p. 76). D3–D5 (who/where/when) are the classic investigative triad; D6–D8 add context and noise-suppression. Weights are the author's allocation reflecting that ordering; the *relative ranking* of D1/D2 over the rest is sourced to SIO, the **exact numbers are [speculative]** (a defensible analyst judgment, not a figure SIO publishes).

---

## 3. Worked examples

### Example A — High-quality report (platform that manually reviews and files via the API)

Scenario: A mid-size social platform's trust-and-safety analyst manually reviews a newly-detected upload, files via the NCMEC reporting API with all fields populated, attaches the file and the surrounding DM thread, includes the uploader's account email + upload IP, a timestamped event in UTC with a defined "upload time," flags it as non-GAI/non-meme, and notes the victim appears to be a self-generating minor with a location hint.

| Dimension | Weight | Finding | Award |
|-----------|:------:|---------|:-----:|
| D1 Actual file | 20 | File attached | **20** (Present) |
| D2 Human-review flag | 15 | Analyst viewed this exact file; box accurately set | **15** (Present) |
| D3 Offender ID | 15 | Account email + upload IP | **15** (Present) |
| D4 Upload geolocation | 15 | Upload IP present | **15** (Present) |
| D5 Timestamp + TZ | 10 | UTC timestamp + defined incident time | **10** (Present) |
| D6 Complete communication | 10 | Full DM thread attached | **10** (Present) |
| D7 Victim info | 8 | Victim location hint + self-gen indicator | **8** (Present) |
| D8 Classification flags | 7 | GAI/meme flags set (both false), correctly | **7** (Present) |
| **Total** | **100** | | **100 / 100** |

**Score: 100/100.** This is the SIO "who/what/where/when + reviewed file" ideal.

### Example B — Low-quality "noise" report (automated hash-only dump, no human review)

Scenario: An automated pipeline files a report on a hash match against a known-CSAM list. No human viewed the file. Only a login IP (not upload IP) and a bare epoch timestamp are present. No chat context, no victim data. The content is in fact a long-viral known meme, but no classification flag is set. This is the archetype of the 1.1M-report Amazon AI Services episode in spirit — automated, no actionable information (NCMEC 2026, https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data).

| Dimension | Weight | Finding | Award |
|-----------|:------:|---------|:-----:|
| D1 Actual file | 20 | Hash value only, no file | **0** (Absent) |
| D2 Human-review flag | 15 | No human review | **0** (Absent) |
| D3 Offender ID | 15 | Account ID present but no IP/email; weak identifier only | **7** (Partial, 15/2=7) |
| D4 Upload geolocation | 15 | Login IP only, not upload IP | **7** (Partial, 15/2=7) |
| D5 Timestamp + TZ | 10 | Bare epoch, no timezone/definition | **5** (Partial, 10/2=5) |
| D6 Complete communication | 10 | None | **0** (Absent) |
| D7 Victim info | 8 | None | **0** (Absent) |
| D8 Classification flags | 7 | Viral meme, but no "Potential Meme" flag set | **0** (Absent) |
| **Total** | **100** | | **19 / 100** |

**Score: 19/100.** Sum: 0+0+7+7+5+0+0+0 = 19. A report like this consumes triage capacity while carrying almost no investigative value — the "noise tax" M2 will quantify. Note the rubric still credits the partial identifiers (D3–D5): it measures completeness, not the separate (M3) question of whether this is worth working *given* it is a known-meme duplicate.

---

## 4. Limitations & counter-evidence

**Mis-scoring failure modes (concrete):**

1. **Completeness ≠ truthfulness; a gameable flag inflates D2.** The rubric awards 15 points for an accurately-set "File Viewed by Company" box, but it cannot detect a *miscalibrated* flag. SIO explicitly warns the box should be checked *"if and only if a human reviewed the file associated with this report"* and that checking it for a previously-seen (but not this-exact) file is wrong (SIO §8.1.1, p. 76). A platform that over-checks the box scores high here yet feeds NCMEC false confidence — the rubric rewards the lie. Any operational use needs a separate audit/trust signal (which is precisely the M2 sender-reliability input).

2. **High completeness on a duplicate/known-meme report scores high but may be near-worthless to rescue triage.** Because the rubric scores fields, a fully-populated report about a long-deduplicated viral image (the kind SIO and NCMEC flag as overwhelming volume) can score 90+ while pointing at no rescuable child. Conversely, the Belgian example — *"over 500 distinct CyberTipline reports about a single offender within a span of five months"* (SIO, via Techdirt 2024, https://www.techdirt.com/2024/04/25/the-problems-of-the-ncmec-cybertipline-apply-to-all-stakeholders/) — shows completeness and novelty are orthogonal. The rubric must not be read as a priority score; novelty/deduplication is an M3 feature, not an M1 dimension.

3. **The Present/Partial/Absent buckets collapse field quality that matters operationally.** D4 awards full points for "upload IP present," but an upload IP behind CGNAT or a VPN is far less actionable than a residential one, and the rubric cannot see that. Same for D3 (an email at a defunct domain scores as a strong identifier). The three-bucket scheme was chosen for inter-rater reproducibility, but it systematically over-credits technically-present-but-investigatively-dead fields.

4. **Weights are an analyst allocation, not an empirically validated model.** Only the *ordering* (D1/D2 highest) is sourced to SIO's qualitative emphasis (p. 76); the specific 20/15/15/15/10/10/8/7 split is `[speculative]`. A report could be mis-ranked relative to another purely because of an unvalidated weight, and SIO publishes no field-importance coefficients to calibrate against. Until outcome data (does field X correlate with arrests?) exists — which SIO says is itself missing because ICAC Task Forces lack outcome transparency (SIO §8.1.4, p. 80) — the weights cannot be empirically defended.

5. **The statute's discretion means "Absent" can be lawful, so a 0 is not a compliance verdict.** Every D-row except the existence of *a* report is optional under 2258A(b)'s "sole discretion of the provider" language (https://www.law.cornell.edu/uscode/text/18/2258A). A report scoring 26/100 may be fully statutorily compliant. Reading a low completeness score as a legal failing would be wrong and could chill the *voluntary* over-reporting that, per SIO, is itself legally load-bearing — courts treat platform reporting as voluntary precisely to keep evidence admissible under the Fourth Amendment (SIO §8.1, Fourth-Amendment discussion p. 78; treated in depth in M4).

**Counter-evidence / scope caveats:**

- **Sourcing gap on the underlying report:** The SIO field-importance recommendations are drawn from the public PDF (druid:pr592kc5483, dated 2024-04-22). The exact CyberTipline API field names ("File Viewed by Company," "Potential Meme," "Generative AI") are quoted from SIO's description of the NCMEC API documentation, not from the API spec directly, which is access-controlled; field labels could have changed since April 2024 `[speculative on currency]`.
- **Recency:** The volume context (21.3M reports; 1.1M no-actionable Amazon AI Services reports) is from NCMEC's 2026 first-look at 2025 data (https://www.missingkids.org/blog/2026/the-work-never-stops-first-look-at-ncmecs-2025-data), current as of this artifact. The SIO blueprint is April 2024 — older than 12 months — and is cited as the *design* basis, not as a current-state statistic.
- **2258A subsection lettering** is taken from the Cornell LII consolidated text (https://www.law.cornell.edu/uscode/text/18/2258A) as of 2026-06; the (a)/(b)(1)-(5) structure and the "sole discretion of the provider" chapeau were verified against that text. The preservation period was amended from 90 days to 1 year (subsection (h)); note SIO's April-2024 recommendations still reference the *then*-current 90-day baseline (SIO §8.1.1/§8.1.3), a discrepancy that reflects the law changing after the report.

---

### Run-log summary

I built an 8-dimension completeness rubric (weights summing to 100) that scores a single CyberTipline report 0–100 on investigability, anchoring six of the eight dimensions to subsection-level provisions of 18 U.S.C. 2258A — (b)(1) identity, (b)(2) timing, (b)(3) geolocation, (b)(4) the file, (b)(5) the complete communication — and to named SIO 2024 platform recommendations (the "who/what/where/when," the "hash alone is insufficient," and the "File Viewed by Company if and only if" rules). Two end-to-end worked examples score 100/100 and 19/100. The most surprising find from reading the actual SIO PDF (which I had to extract locally after the FSI site returned 403) was the legal load-bearing nature of *voluntariness*: NCMEC deliberately will not publish the "top-priority fields" platforms should complete, because doing so risks a "platforms are agents of the government" Fourth-Amendment argument that could make millions of reports inadmissible — so the single most useful quality-standardization fix is the one NCMEC is structurally barred from issuing itself, which is why SIO routes it to a non-NCMEC NGO. That tension (quality standards are needed but cannot come from the obvious actor) directly seeds M4 and M5.
