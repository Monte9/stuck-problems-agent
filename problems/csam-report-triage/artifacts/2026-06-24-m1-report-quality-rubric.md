# M1 — CyberTipline Report-Quality Rubric

**Problem:** CSAM report triage — turning ~21M CyberTipline reports into a ranked rescue docket.
**Milestone:** M1 — a scoring rubric defining what a "complete," actionable CyberTipline report contains, grounded in the Stanford Internet Observatory (SIO) 2024 report and 18 U.S.C. § 2258A.
**Date:** 2026-06-24.
**Author:** generator subagent (desk research; all quantitative/legal claims sourced inline).

---

## 1. Purpose and scope

A CyberTipline report is mandatory under federal law when a U.S. provider obtains actual knowledge of apparent CSAM (18 U.S.C. § 2258A(a)). But the statute makes almost all of the *contents* of a report **discretionary** — subsection (b) opens with the words that the listed facts "may, at the sole discretion of the provider, include the following information" ([18 U.S.C. § 2258A(b)](https://www.law.cornell.edu/uscode/text/18/2258A)). That gap between *mandatory to report* and *optional to detail* is the structural source of the noise problem: a provider can satisfy the statute by filing a thin report.

The SIO 2024 study, based on interviews with platforms, NCMEC, and 60+ law-enforcement respondents, found that **only 49% of 2022 CyberTipline reports were actionable** ([SIO 2024, p. 1](https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf)), and that "the core issue extends beyond volume: officers struggle to triage and prioritize these reports" because "[n]othing in the reports would have indicated which should be prioritized" (SIO 2024, p. 5).

This rubric operationalizes the SIO "what makes a report actionable" standard plus the § 2258A(b) content categories into a **0–100 completeness/quality score** per report. It is a *report-quality* score (is this report well-formed and investigable?), **not** a *priority* score (is this a child in imminent danger?). Priority/triage feature design is M3; this rubric is consumed there as one input.

Each dimension is scored **present / partial / absent**, mapping to a fraction of the dimension's weight:

| Score level | Fraction of weight | Meaning |
|---|---|---|
| **Present** | 1.0 | Field populated with usable, investigable data. |
| **Partial** | 0.5 | Field present but degraded (e.g., login IP instead of upload IP; coarse geo only; hash without file). |
| **Absent** | 0.0 | Field missing, empty, or filled with non-actionable filler. |

Dimension score = weight × fraction. Total = sum across all 8 dimensions (0–100).

---

## 2. The rubric

8 dimensions. Weights sum to **exactly 100**.

| # | Dimension | Description (what "present" means) | Statutory / SIO basis (with citation) | Weight | How scored (present / partial / absent) |
|---|-----------|-------------------------------------|----------------------------------------|:------:|------------------------------------------|
| **D1** | **Offender / involved-individual identity** | Identifying info for the person who appears to have uploaded/transmitted the content: account ID, email, URL, payment info, self-reported identity. | **18 U.S.C. § 2258A(b)(1)**: report may include "information relating to the identity of any individual who appears to have violated… which may… include the electronic mail address, Internet Protocol address, uniform resource locator, payment information…, or any other identifying information" ([Cornell LII](https://www.law.cornell.edu/uscode/text/18/2258A)). SIO: actionable reports "provide offender information (including location information…)" ([SIO 2024, p. 76](https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf)). | **18** | **Present**: ≥1 strong identifier (email/account/payment). **Partial**: only a weak/self-reported handle. **Absent**: no identifying info. |
| **D2** | **Upload-IP / network locator quality** | An IP address that ties the *upload/transmission event* to a subscriber — specifically an **upload IP**, not merely a login IP. | **§ 2258A(b)(1)** (IP as identifier) and **(b)(3)** (geographic location "which may include the Internet Protocol address"). SIO singles this out: actionable reports need "an upload IP address," noting one platform "initially only provided login IP addresses, which are less helpful than the IP addresses used during the upload" (SIO 2024, pp. 24, 76). | **16** | **Present**: upload/transmission IP with timestamp. **Partial**: login/registration IP only, or IP without time. **Absent**: no IP. |
| **D3** | **The associated file / chat content (not a hash alone)** | The actual reported media file, or the full chat/DM text — the evidentiary object itself. | **§ 2258A(b)(4)** ("[a]ny visual depiction of apparent child pornography or other content") and **(b)(5)** ("the complete communication…") ([Cornell LII](https://www.law.cornell.edu/uscode/text/18/2258A)). SIO is explicit: reports are more actionable when they provide "the associated file (**a hash alone is insufficient**) or chat" ([SIO 2024, p. 76](https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf)). | **14** | **Present**: file/chat attached. **Partial**: hash/identifier only, no file or chat body. **Absent**: neither file, hash, nor chat. |
| **D4** | **"File Viewed by Company" / human-review flag** | Accurate indication that a human at the provider reviewed *this exact file*, which lets NCMEC view it and law enforcement triage without first obtaining a warrant. | SIO 2024: an accurate "File Viewed by Company" check "greatly increase[s] (1) NCMEC['s ability] to identify new victims, (2)… to accurately escalate the report, (3) the likelihood that law enforcement will investigate…, and (4)… to accurately triage among reports" ([SIO 2024, p. 76](https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf)). Flag must be checked "if and only if a human reviewed the file" (p. 76). | **14** | **Present**: flag accurately set true, this-file review. **Partial**: ambiguous (prior-review-of-similar, or unstated). **Absent**: not human-reviewed / flag false. |
| **D5** | **Incident time (date/time + time zone + definition)** | When the upload/transmission occurred, with a date-time stamp, time zone, and a stated definition of how the platform defines "incident time." | **§ 2258A(b)(2)**: "information relating to when and how a customer or subscriber… uploaded, transmitted, or received content… including a **date and time stamp and time zone**" ([Cornell LII](https://www.law.cornell.edu/uscode/text/18/2258A)). SIO: actionable reports include "the time of the incident (including a field describing how the platform defines the incident time)" (SIO 2024, p. 76). | **12** | **Present**: timestamp + time zone + definition. **Partial**: timestamp without time zone or definition. **Absent**: no time. |
| **D6** | **Victim / geographic-location info** | Location signals for victim or involved individual: verified address, area/zip code, or geo-identifying info — supporting jurisdiction routing. | **§ 2258A(b)(3)**: geographic location "which may include the Internet Protocol address or verified address, or… at least one form of geographic identifying information, including area code or zip code" ([Cornell LII](https://www.law.cornell.edu/uscode/text/18/2258A)). SIO: actionable reports include "victim information (including location information)" (SIO 2024, p. 76). | **10** | **Present**: verified address or specific geo. **Partial**: coarse geo (area/zip only). **Absent**: none. |
| **D7** | **Classification / disposition flags (Meme, Generative-AI, severity)** | Correct use of the structured flags that let NCMEC/LE *deprioritize noise and surface real cases*: "Potential Meme," "Generative AI," severity. | SIO 2024: lists "Potential Meme," "Generative AI," and "File Viewed by Company" as "important fields"; platforms submitting memes "often fail to check the 'Suspected Meme' box," causing law enforcement to "mistakenly prioritize these cases" (SIO 2024, pp. 6, 76). Maps to the de-confliction/triage burden the report centers. | **9** | **Present**: meme/GAI/severity flags set accurately. **Partial**: some flags, accuracy unclear. **Absent**: flags blank where applicable (e.g., unflagged meme). |
| **D8** | **Provider contact + preservation/timeliness integrity** | A durable provider contact (role address, not an individual) and a report filed promptly with content preserved, so follow-up subpoenas/warrants can land. | **§ 2258A(a)(1)** (report "as soon as reasonably possible after obtaining actual knowledge") and **§ 2258A(h)(1)** (submission "shall be treated as a request to preserve the contents… for 1 year," as amended by the REPORT Act of 2024) ([Cornell LII](https://www.law.cornell.edu/uscode/text/18/2258A)). SIO: maintain a "dedicated email address… such as ncmec@[company].com" not an individual's, given turnover (SIO 2024, p. 78). | **7** | **Present**: role contact + timely + preserved. **Partial**: individual contact, or delayed filing. **Absent**: no usable contact / stale. |
| | | | **TOTAL** | **100** | |

**Dimensions citing a specific § 2258A subsection or named SIO standard:** D1 (b)(1), D2 (b)(1)/(b)(3), D3 (b)(4)/(b)(5), D5 (b)(2), D6 (b)(3), D8 (a)(1)/(h)(1) — **six** dimensions cite subsection-level statute; D4 and D7 cite named SIO actionability standards. (Done-criterion required ≥4.)

### Why these weights

The top three weighted dimensions (D1 offender identity 18, D2 upload-IP 16, D3 file/chat 14 = 48% of the score) are the three SIO names first when defining actionability ("offender information… upload IP address… the associated file… or chat"; [SIO 2024, p. 76](https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf)). D4 (human-review flag) is weighted equal to D3 because SIO ties it directly to all four of NCMEC/LE's downstream abilities including triage. Classification flags (D7) and contact/preservation (D8) are real but lower-leverage for a *single* report's investigability, so they carry the smallest weights. The weights are a defensible reading of SIO's ordering, not a measured optimum — see Limitations.

---

## 3. Worked examples

### Example A — High-quality report (a well-formed provider report)

*Scenario:* A large provider's trust-and-safety team detects a user uploading a novel CSAM image. A human moderator reviews the exact file, files via the NCMEC API with full fields populated.

| Dim | Weight | What the report contains | Level | Fraction | Score |
|-----|:------:|--------------------------|-------|:--------:|:-----:|
| D1 Offender identity | 18 | Verified account email + payment-method token | Present | 1.0 | 18.0 |
| D2 Upload-IP | 16 | Upload IP `203.0.113.x` with upload timestamp | Present | 1.0 | 16.0 |
| D3 File/chat | 14 | Actual image file attached | Present | 1.0 | 14.0 |
| D4 File-Viewed flag | 14 | "File Viewed by Company" accurately TRUE (this exact file) | Present | 1.0 | 14.0 |
| D5 Incident time | 12 | Date-time + time zone (UTC) + "incident = upload event" definition | Present | 1.0 | 12.0 |
| D6 Victim/geo | 10 | Verified billing address (state + city) | Present | 1.0 | 10.0 |
| D7 Classification flags | 9 | Meme=false, GenAI=false, severity tag set; all accurate | Present | 1.0 | 9.0 |
| D8 Contact/preservation | 7 | Role address `childsafety@provider.com`; filed same day; preserved | Present | 1.0 | 7.0 |
| | | | | **TOTAL** | **100.0** |

**Total = 18 + 16 + 14 + 14 + 12 + 10 + 9 + 7 = 100 / 100.** A maximally actionable report.

A more realistic "good but imperfect" variant: suppose D2 carries only a **login** IP (Partial → 8.0) and D6 is **area code only** (Partial → 5.0). Total = 100 − 8 − 5 = **87 / 100**. Still clearly investigable.

### Example B — Low-quality "noise" report

*Scenario:* An automated pipeline auto-files a hash match for a widely-circulated image. No human reviewed the file; the meme box is left unchecked; only a login IP and a self-reported handle are present. (This is the SIO "two reports look identical but one leads nowhere" failure mode; SIO 2024, p. 5, and the kind of unactionable bulk-AI filing exemplified by the Amazon AI Services 1.1M-report episode the problem brief flags.)

| Dim | Weight | What the report contains | Level | Fraction | Score |
|-----|:------:|--------------------------|-------|:--------:|:-----:|
| D1 Offender identity | 18 | Self-reported display name only ("user_8842") | Partial | 0.5 | 9.0 |
| D2 Upload-IP | 16 | Login IP only, no upload IP, no time on it | Partial | 0.5 | 8.0 |
| D3 File/chat | 14 | Hash value only; no file, no chat | Partial | 0.5 | 7.0 |
| D4 File-Viewed flag | 14 | Not human-reviewed; flag FALSE | Absent | 0.0 | 0.0 |
| D5 Incident time | 12 | No timestamp | Absent | 0.0 | 0.0 |
| D6 Victim/geo | 10 | None | Absent | 0.0 | 0.0 |
| D7 Classification flags | 9 | Meme box left UNCHECKED on a known meme; GenAI blank | Absent | 0.0 | 0.0 |
| D8 Contact/preservation | 7 | Generic portal auto-filing, individual contact, no preservation note | Partial | 0.5 | 3.5 |
| | | | | **TOTAL** | **27.5** |

**Total = 9 + 8 + 7 + 0 + 0 + 0 + 0 + 3.5 = 27.5 / 100.** A noise report: technically statute-compliant (a mandatory hash-match filing) but near-useless for triage and, because the meme box is unchecked, actively misleading (SIO 2024, p. 6: unchecked-meme reports cause LE to "mistakenly prioritize these cases").

**Spread:** high-quality 100 (realistic variant 87) vs. noise 27.5 — a ~60-point separation, which is the rubric's job: surface the difference SIO says nothing in the raw report currently surfaces.

---

## 4. Limitations & counter-evidence

Concrete ways this rubric could **mis-score** real reports:

1. **High completeness ≠ live victim (false high).** The rubric scores *form quality*, not danger. A perfectly-filled report about an old, widely-known image (high D1–D8) would score ~100 yet lead "nowhere," while a sparse report about active hands-on abuse could score low. SIO's central finding is exactly that two reports "look very similar" but diverge on investigation (SIO 2024, pp. 5, 81). A high score here must **not** be read as high priority — that is M3's job, and conflating them would re-create the triage error this work is meant to fix.

2. **Rewards box-checking, punishes the honestly-constrained (false low / gameable).** D4 ("File Viewed by Company") and D3 (attach the file) can be high-risk for a provider to satisfy: viewing/attaching content has Fourth-Amendment and liability dimensions (the M4 topic), and SIO notes providers "may still have legitimate reasons to choose to not have humans review some or all files" (SIO 2024, p. 76). A privacy-cautious or small provider could file a genuinely-useful report that the rubric scores low. Conversely, a sender optimizing for the *score* could check "File Viewed" inaccurately — the rubric cannot detect a false flag from the report text alone.

3. **Weights are an editorial reading, not a validated model.** The 18/16/14/14/12/10/9/7 split is a defensible ordering of SIO's prose, but SIO gives a qualitative list, not weights. Different reasonable readers would assign different numbers; the present/partial/absent → 1.0/0.5/0.0 step function is also coarse (e.g., a login IP and a missing IP both differ from an upload IP, but "partial = 0.5" flattens many degradation gradients). No ground-truth dataset of report→outcome was available to calibrate these weights, so the absolute 0–100 number should be treated as ordinal (good vs. noise), not cardinal.

4. **Statute permits the very thinness the rubric penalizes (legitimacy gap).** Because § 2258A(b) makes the content fields discretionary ("at the sole discretion of the provider"; [18 U.S.C. § 2258A(b)](https://www.law.cornell.edu/uscode/text/18/2258A)), a report that scores 27/100 here can be fully legally compliant. The rubric measures *actionability*, which the statute does not require; using it to grade or sanction senders (M2/M5) needs that distinction kept explicit, or it will mischaracterize lawful-but-thin filings as failures.

5. **Field semantics vary by platform (cross-sender comparability).** "Incident time," IP fields, and even severity tags are defined differently across providers — SIO documents that platforms disagree on what an "incident" is and that NCMEC will not put actionability guidance "in writing" (SIO 2024, pp. 25, 76). The same nominal field can be Present at one sender and effectively Absent at another, so a single numeric score is less comparable across senders than it looks — a caution that propagates directly into the M2 per-sender scorecard.

---

## 5. Source list

- **18 U.S.C. § 2258A** — Reporting requirements of providers. Cornell Legal Information Institute: https://www.law.cornell.edu/uscode/text/18/2258A (subsections cited: (a)(1) duty/timeliness; (b)(1) identity; (b)(2) time; (b)(3) geographic location; (b)(4) visual depiction; (b)(5) complete communication; (h)(1) 1-year preservation as amended by the REPORT Act of 2024).
- **Stanford Internet Observatory / Cyber Policy Center (2024)**, *The Strengths and Weaknesses of the Online Child Safety Ecosystem* ("How to Fix the Online Child Exploitation Reporting System"), Grossman, Pfefferkorn, Thiel, Shah, DiResta, Perrino, Cryst, Stamos, Hancock; April 22, 2024. Full PDF: https://stacks.stanford.edu/file/druid:pr592kc5483/cybertipline-paper-2024-04-22.pdf (cited: p. 1 49%-actionable figure; p. 5–6 triage findings/meme box; p. 76 actionability standard, "hash alone is insufficient," File-Viewed-by-Company, important flags; p. 77 deconfliction; p. 78 dedicated contact). Landing page: https://cyber.fsi.stanford.edu/publication/how-fix-online-child-exploitation-reporting-system
