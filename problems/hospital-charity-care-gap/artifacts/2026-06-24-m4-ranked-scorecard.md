# M4 — Ranked non-compliance / inaccessibility scorecard

**Problem:** Charity care that nonprofit hospitals are legally required to give — and mostly don't.
**Milestone:** M4 — combine the M2 FAP/PLS accessibility scores and the M3 Schedule H charity-care ratios into a single ranked scorecard naming the hospitals most likely to be under-serving eligible patients, with a transparent combination method and an explicit limitations section.
**Date:** 2026-06-24.
**Inputs (read in full; no number below is new):**
- M2 accessibility/compliance: `artifacts/2026-06-24-m2-fap-pls-scoring.md` (D1–D9 scored from public FAP/PLS text, max 28; D10 deferred to M3).
- M3 charity-care ratios: `artifacts/2026-06-24-m3-schedule-h-charity-ratio.md` (FY2023 Schedule H Part I Line 7a-e ÷ total functional expenses; peer quartiles; "filing unavailable" `0*` and governance-inapplicable `n/a` conventions).
- M1 rubric/sample for numbering: `artifacts/2026-06-23-m1-rubric-and-sample.md`.

Every M2 score and every M3 ratio used here is copied from those two artifacts. No FAP was re-scored and no charity-care dollar figure was re-derived. The only new numbers are the two normalized sub-scores and the combined concern score, each computed by an explicit formula shown in the Method section so an evaluator can re-derive every rank.

---

## How to read this scorecard (one-paragraph summary)

The scorecard is split into **three tiers** because the 28 hospitals carry different evidence. **Tier A (18 hospitals)** has *both* an M2 accessibility score and a usable M3 charity-care ratio; these are ranked by a combined concern score that weights the two signals 50/50. **Tier B (5 hospitals)** has an M2 score but **no usable Schedule H** ("filing unavailable" in M3); these are ranked on M2 accessibility only, with the data gap flagged — a missing filing is **not** evidence of stinginess. **Tier C (5 hospitals)** are governance non-filers (one for-profit, four public) that file no Schedule H at all and are *legally* outside the charity-care ratio; these are also ranked on M2 only and must never be cited for low charity-care spending. Worst-first within each tier. The single worst-flagged hospitals overall are **Grady Memorial** (0.00% ratio, but driven by public offsetting funding — read the caveat), **Penn/HUP** (0.39%, a $1.2B academic hospital in the bottom charity quartile with application-only-ish disclosure), and **Henry Ford/Ascension Providence** (0.30%, bottom quartile). The most defensible "spends far below peers" flags — large, well-resourced systems with no safety-net offset excuse — are **Penn/HUP and NewYork-Presbyterian**.

---

## Tier A — both signals present (M2 accessibility + M3 charity ratio): worst first

Ranked by **Combined concern = 0.5 × Inaccessibility + 0.5 × Low-charity** (both 0–1, higher = worse). Formulas in Method. "M3 flag" is M3's own peer-quartile label.

| Rank | # | Hospital | ST | M2 (D1–D9, /28) | M3 ratio % | M3 peer flag | Inacc. (0–1) | Low-charity (0–1) | **Combined** | Single most actionable issue (traceable to M2 quote / M3 figure) |
|----:|---|----------|----|----:|----:|------|----:|----:|----:|---|
| 1 | 26 | Grady Memorial | GA | 10 | 0.00 | bottom quartile | 0.643 | 1.000 | **0.821** | Lowest accessibility in the sample (M2=10) **and** 0.00% net charity ratio — but M3 shows $142.9M gross charity fully offset by GA DSH/indigent funding, so the 0.00% is **offset-driven, not absence of care**. Actionable issue from M2: D5=0 application-only, county-residency-gated — *"call … to schedule a time to meet with a Financial Counselor."* |
| 2 | 12 | HUP / Penn Medicine | PA | 17 | 0.39 | bottom quartile | 0.393 | 0.860 | **0.627** | Charity care only **0.39% of a $1.18B expense base** (M3, $4.59M), bottom quartile, with weak disclosure: D5=2 (no enrollment-proxy PE found), D6=1 *"in-person … or by mail by calling a financial counselor,"* D9=1 English-only. A large academic hospital with no safety-net-offset excuse. |
| 3 | 15 | Ascension Providence → Henry Ford Providence | MI | 21 | 0.30 | bottom quartile | 0.250 | 0.892 | **0.571** | **Lowest charity ratio of any cleanly-attributable filer, 0.30%** (M3, $2.71M / $904.5M). M2 D5=2 vendor "presumptive scoring," D6=1; scored from Ascension's national template (flagged). The 0.30% is the single most actionable figure. |
| 4 | 28 | Carilion Roanoke Memorial | VA | 16 | 0.89 | bottom quartile | 0.429 | 0.681 | **0.555** | Bottom-quartile ratio **0.89%** (M3) plus asset-gated, documentation-heavy access: M2 D6=1 *"must complete a FAA, provide required documentation, and … validation with external agencies,"* and a 100% free tier gated by *"available assets of less than $25,000."* |
| 5 | 22 | FirstHealth Moore Regional | NC | 13 | 1.28 | below median | 0.536 | 0.541 | **0.538** | Stated income **free-care floor of only 100% FPL** in policy text (M2 D3=0) — far below the 250% Dollar For benchmark — despite a 1.28% ratio. Note counter-evidence: third-party data say effective reach ~204% FPL, so D3=0 may understate practice (see Limitations). |
| 6 | 10 | Cleveland Clinic | OH | 16 | 1.08 | below median | 0.429 | 0.613 | **0.521** | Application-only disclosure: M2 D5=0 *"you are required to cooperate with our Medicaid screening process"* (no PE language located), D6=1, D7=1; ratio just above the 1.0% floor at 1.08% (M3). |
| 7 | 13 | Massachusetts General / MGB | MA | 22 | 0.51 | bottom-quartile-equiv. | 0.214 | 0.817 | **0.516** | **System group-return aggregate, 0.51%** ($21.6B MGB return; MGH not isolable — M3 caveat). Strong FAP text (M2=22) but the system-wide charity ratio sits in the bottom band. Label as *system*, not MGH-specific. |
| 8 | 9 | Atrium Wake Forest Baptist | NC | 19 | 0.90 | below median | 0.321 | 0.677 | **0.499** | Below-median ratio **0.90%** (M3, NC Baptist Hospital) and thin disclosure: M2 D2=1 (no standalone PLS on page read), D7=1 (AGB method not stated), D9=1 (English-only). |
| 9 | 14 | NewYork-Presbyterian | NY | 24 | 0.87 | bottom quartile | 0.143 | 0.688 | **0.416** | **$84.8M of charity care but only 0.87% of a $9.76B expense base** (M3) — bottom quartile despite large absolute dollars; among the most defensible "below peers" flags. Strong FAP text (M2=24), so the gap is in spending, not disclosure. |
| 10 | 27 | Sentara Norfolk General | VA | 16 | 1.67 | above median | 0.429 | 0.401 | **0.415** | Above-median ratio (1.67%) but low accessibility: M2 D1=1 (PLS image-only, *"not machine-extractable"*), D6=1 asset test *"less than $50,000 in available assets,"* D9=1. The image-only PLS is itself a 501(r) widely-available concern. |
| 11 | 16 | CommonSpirit / Dignity Health | TX/AZ | 20 | 1.35 | at median | 0.286 | 0.516 | **0.401** | Median ratio (1.35%, **Dignity-wide aggregate**, not St. Joseph's Phoenix alone — M3 caveat) with application-led access: M2 D5=2, D6=1 *"Completed a Financial Assistance Application and provided supporting documentation."* |
| 12 | 18 | Banner UMC Phoenix | AZ | 18 | 1.63 | above median | 0.357 | 0.416 | **0.386** | Above-median ratio but **application-only public summary**: M2 D5=0 (no PE in the PLS read), D6=1 with advance-deposit for non-emergent services. System-wide filer (Banner Health). |
| 13 | 4 | UNC Health Rex | NC | 24 | 1.91 | above median | 0.143 | 0.315 | **0.229** | Lower-ranked concern: strong shared UNC system FAP (D5=4 HASP PE) but M2 flagged D6=1 (application surfaced less directly on the Rex billing page) and a 1.91% ratio. Near-duplicate of UNC Med Ctr policy (#3). |
| 14 | 5 | Moses Cone (Cone Health) | NC | 22 | 3.64 | top quartile | 0.214 | 0.000 | **0.107** | Low concern: top-quartile charity ratio (3.64%); the only flag is M2 D5=2 vendor FAS scoring rather than enumerated HASP enrollment proxies. |
| 15 | 2 | Duke University Hospital | NC | 23 | 3.45 | top quartile | 0.179 | 0.000 | **0.089** | Low concern: top-quartile 3.45% ratio + full HASP PE (M2 D5=4, *"no application process is required of NC residents"*). Minor flag: D4=2 cliff at 300%. |
| 16 | 6 | Novant Forsyth | NC | 23 | 2.86 | top quartile | 0.179 | 0.000 | **0.089** | Low concern: top-quartile 2.86% + full HASP PE (D5=4). Minor flag: D2=1 (no separate standalone PLS on page read). |
| 17 | 7 | ECU Health Medical Center | NC | 24 | 2.73 | above median | 0.143 | 0.022 | **0.082** | Low concern: 2.73% (just under top quartile) + full HASP PE and 100% free care to 300% FPL (D3=4). Minor flag: D1=1 (current unified FAP took site-search to locate). |
| 18 | 8 | WakeMed Raleigh | NC | 25 | 5.54 | top quartile | 0.107 | 0.000 | **0.054** | **Best in sample**: highest charity ratio (5.54%) and second-highest accessibility (M2=25) with full HASP PE and enumerated 120-day ECA period. Included for completeness; not a concern target. |

---

## Tier B — M2 scored, M3 "filing unavailable" (data gap, ranked on M2 only)

These five hospitals have an M2 accessibility score but **no usable facility-level Schedule H** in M3 (990EZ group return, parent with no Schedule H, absent from the IRS e-file XML, or unresolved EIN). M3 records them `0*`, meaning **"no usable filing located, NOT a confirmed near-zero spend."** Ranked here on **Inaccessibility (M2 only)**; the charity-care half is shown as a gap, not a zero. Per M3's explicit instruction, these zeros must be read as missing data, not measured non-compliance.

| Rank (within tier) | # | Hospital | ST | M2 (/28) | M3 ratio | Inacc. (0–1) | Single most actionable issue (M2 only) |
|----:|---|----------|----|----:|------|----:|---|
| B1 | 19 | Corewell Butterworth | MI | 16 | **gap** — `0*`; M3: $5.4B operating entity filed a FY2023 990 with **no Schedule H block in its e-file XML** (notable, not yet a finding) | 0.429 | M2 D6=1 *"apply within 240 days,"* D7=1, D9=1 (English-only); the missing Schedule H from a $5.4B operator is itself worth a regulator's second look. |
| B2 | 17 | AdventHealth Orlando | FL | 18 | **gap** — `0*`; Orlando entity absent from e-file XML, mgmt-corp 990 has no Schedule H | 0.357 | M2 D1=1 FAP *"fragmented across many facility/region PDFs"* (Orlando packet 403'd), D9=1 English-only. |
| B3 | 20 | Cape Fear Valley | NC | 19 | **gap** — `0*`; filing entity not resolved to a Schedule-H e-file this milestone (candidate EIN 56-0845796) | 0.321 | M2 D6=1 *"complete a financial assistance application and provide documentation … mailed to PO Box 2000,"* D7=1, D9=1 — despite full HASP PE (D5=4). |
| B4 | 11 | UPMC Presbyterian | PA | 22 | **gap** — `0*`; parent 25-1423657 files no Schedule H; operating Shadyside 25-0965480 absent from e-file XML | 0.214 | M2 D2=1 (no standalone PLS), D8=1 (ECAs in separate policy HS-RE0724, not enumerated). Strong D5=4 PE text otherwise. |
| B5 | 1 | Atrium Health (CMC) | NC | 26 | **gap** — `0*`; Charlotte-Mecklenburg Hospital Authority files **990EZ group returns**, no facility Schedule H e-filed | 0.071 | Highest M2 in the sample (26) tied with UNC; only flag is D5=2 (third-party FAS vendor scoring rather than enumerated HASP proxies). Data gap, not a concern target. |

---

## Tier C — governance non-filers (no Schedule H by entity type; ranked on M2 only)

These five file **no Form 990 Schedule H at all** by governance type — one for-profit and four public hospitals (M3 `n/a`, *not* `0`). The charity-care ratio is **legally inapplicable**, so they cannot be ranked or cited on charity spending. Ranked on **Inaccessibility (M2 only)**.

| Rank (within tier) | # | Hospital | ST | M2 (/28) | Why no ratio | Inacc. (0–1) | Single most actionable issue (M2 only) |
|----:|---|----------|----|----:|------|----:|---|
| C1 | 25 | Parkland Health | TX | 11 | public hospital district — no 990 | 0.607 | **Lowest M2 in the sample (11).** D5=0 application-only + *"requires proof of Dallas County residency,"* D4=1 (discount tops at 250% FPL), D6=1. Residency gate is an access barrier beyond the rubric. |
| C2 | 21 | Mission Hospital (HCA) | NC | 15 | for-profit — no Schedule H | 0.464 | D5=0 application-only — *"you must complete a financial assistance application"* — the **only NC hospital in the sample with no presumptive-eligibility pathway**, consistent with HASP binding nonprofits but not HCA's for-profit Mission. |
| C3 | 24 | Cook County (Stroger) | IL | 15 | public — no 990 | 0.464 | D5=2 but **Cook-County-residency-gated**, D6=1 *"go into one of the Cook County Health sites to meet with a Financial Counselor"* (in-person application). |
| C4 | 23 | NYC H+H (Bellevue) | NY | 22 | public benefit corp — no 990 | 0.214 | Strong access on most dimensions (M2=22); only flag is D6=1 in-person financial-counselor application, mitigated by immigration-protected, no-data-sharing design. |
| C5 | 3 | UNC Medical Center | NC | 26 | state governmental entity (EIN 56-1118388) — files no 990 | 0.071 | Highest M2 (26) with full HASP PE (D5=4, 120-day ECA period). Its private sister entity **Rex (56-1509260) does file** and appears in Tier A as #4. Not a concern target. |

---

## Completeness check — all 28 sampled hospitals are placed

- **18 in Tier A** (both signals): #2, 4, 5, 6, 7, 8, 9, 10, 12, 13, 14, 15, 16, 18, 22, 26, 27, 28.
- **5 in Tier B** (M2 only, filing unavailable): #1, 11, 17, 19, 20.
- **5 in Tier C** (M2 only, governance non-filer): #3, 21, 23, 24, 25.
- 18 + 5 + 5 = **28. No sampled hospital is dropped.** Every hospital scored in both M2 and M3 (Tier A) is ranked by the combined method; every hospital scored in only M2 is included in Tier B or C with the M3 gap and its reason stated explicitly.

---

## Method — how the two inputs were combined (re-derivable)

**Goal:** a single concern ranking where higher = "more likely under-serving eligible patients," combining (i) how inaccessible/non-compliant the disclosed FAP/PLS is and (ii) how low the charity-care spend is relative to peers — without letting *missing data* masquerade as low spend.

**Step 1 — Normalize M2 into an inaccessibility score (0–1, higher = worse).** Using the M2 total over D1–D9 (max 28):

> **Inaccessibility = (28 − M2_total) / 28**

This is a linear inversion of the M2 accessibility score. Example: Grady M2=10 → (28−10)/28 = **0.643**; WakeMed M2=25 → (28−25)/28 = **0.107**.

**Step 2 — Normalize M3 into a low-charity score (0–1, higher = worse).** Using M3's own peer-relative anchor (Q3 = upper-quartile ratio = 2.79%) as the "fully adequate" point and 0% as the worst:

> **Low-charity = clamp( (2.79 − ratio%) / 2.79 , 0, 1 )**

A hospital at or above the top quartile (≥2.79%) scores 0 (no charity-spend concern); a hospital at 0% scores 1. Example: Penn 0.39% → (2.79−0.39)/2.79 = **0.860**; WakeMed 5.54% → clamped to **0.000**; Duke 3.45% → clamped to **0.000**. (The Q3 anchor is taken verbatim from M3's peer-comparison section; nothing new is computed about the ratios themselves.)

**Step 3 — Combine, 50/50, for Tier A only:**

> **Combined concern = 0.5 × Inaccessibility + 0.5 × Low-charity**

Equal weights because the two inputs measure two distinct halves of the same failure (a patient can be under-served either because the policy is inaccessible *or* because the hospital simply spends little), and neither M1, M2, nor M3 establishes a basis for preferring one over the other. The 50/50 split is a stated choice, not a derived optimum; a reader who prefers, say, 70% charity-weighting can re-run Step 3 with the published sub-scores. Tier A is sorted by Combined concern descending. Every Combined value in the Tier A table equals 0.5 × its Inacc. column + 0.5 × its Low-charity column — re-derivable by hand.

**Step 4 — Tiering rule for the data-gap and non-filer rows (stated so it is reproducible):**
- A hospital enters **Tier A** iff M3 gives it a *usable computed ratio* (the 17 cleanly-attributable filers **plus** the MGB system aggregate #13, which M3 reports as a real, if system-level, 0.51% — 18 rows).
- A hospital enters **Tier B** iff M3 marks it **"filing unavailable" / `0*`** (no usable Schedule H located). **It is ranked on Inaccessibility only**; its Low-charity half is left blank, *not* set to 1. Setting `0*` to a low-charity of 1 would rank a hospital as a bad actor on the strength of a missing filing — explicitly forbidden by the spec and by M3. Within Tier B, sort by Inaccessibility descending.
- A hospital enters **Tier C** iff M3 marks it **`n/a` (governance non-filer)** — for-profit or public, files no Schedule H by entity type. Same M2-only ranking rule as Tier B; the charity ratio is legally inapplicable, so these rows are never compared on spend. Within Tier C, sort by Inaccessibility descending.

**Why three tiers instead of one combined column for all 28:** any single ranking would have to assign the 10 non-Tier-A hospitals a charity-care value, and the only honest value for "no usable filing" or "files no Schedule H" is *unknown*, not *zero*. Forcing them into one column would either (a) drop them to the bottom on imputed-zero charity (libelling five hospitals over missing data) or (b) silently impute a charity value (inventing a number). Tiering keeps the combination mechanical for the 18 rows that have both signals and ranks the rest on the one signal they do have, with the gap visible.

**Special read-with-caution flag inside Tier A — Grady (#26).** Grady ranks #1 by the mechanical formula (M2=10, ratio=0.00%). But M3 documents that Grady's $142.9M *gross* financial-assistance cost is **fully offset by Georgia DSH / Fulton–DeKalb indigent-care funding**, so *net* Line 7a = $0 by accounting, not by absence of care. The formula cannot see this; the table footnotes it and the Limitations section treats Grady as "ratio 0.00% but offset-driven," i.e. a structural artifact, not a stinginess finding. Penn/HUP (#2) and NewYork-Presbyterian (#9) are the more defensible "spends far below peers" flags because they are large, well-resourced, and carry no safety-net-offset explanation.

---

## Sources / traceability

Every value in this scorecard traces to one of the two input artifacts; nothing is newly measured here.

- **M2 column (D1–D9 totals, max 28) and every FAP/PLS quote** in the "actionable issue" cells: `artifacts/2026-06-24-m2-fap-pls-scoring.md`, Part A table (totals) and Part B per-hospital evidence appendix (quotes, keyed by the same hospital number used here).
- **M3 ratio %, peer flag, "filing unavailable" `0*`, governance `n/a`, the Q3=2.79% quartile anchor, and the Grady offset explanation:** `artifacts/2026-06-24-m3-schedule-h-charity-ratio.md`, Core table, Peer-comparison section, and EIN-reconciliation table.
- **Dimension numbering (D1–D10) and the 28-hospital frozen sample:** `artifacts/2026-06-23-m1-rubric-and-sample.md`.
- **Normalized sub-scores and Combined concern:** computed in this artifact by the Step 1–3 formulas above from the M2 and M3 values; no external data.

---

## Limitations & counter-evidence

1. **Missing filings are not low spending — five hospitals could be libelled if Tier B is misread.** Tier B (#1 Atrium CMC, #11 UPMC, #17 AdventHealth Orlando, #19 Corewell, #20 Cape Fear Valley) carry M3's `0*` for *"no usable facility-level Schedule H located,"* which the M1 rule mechanically scores 0 but which M3 explicitly says **"must be read as missing data, not measured non-compliance."** This scorecard ranks them on M2 only and never assigns them a low-charity penalty. A hostile reader who pulls one of these hospitals' actual consolidated Schedule H could find a perfectly adequate ratio buried in a group return. The single genuinely *suggestive* gap is Corewell's $5.4B operating entity having no Schedule H block in its e-file XML at all (M3) — that is a reason to look, not a finding.

2. **The charity ratio measures absorbed cost, not free care delivered — Grady is the proof.** M3's numerator (Line 7a-e) is charity care **net of direct offsetting revenue** (Medicaid charity, DSH, county indigent-care funding). Grady's 0.00% reflects $142.9M of gross charity fully reimbursed by Georgia/county funds, not absence of care. NewYork-Presbyterian's low 0.87% is also partly a Medicaid-heavy-mix artifact. So the bottom-quartile and Grady #1 flags identify hospitals **worth auditing**, not proven under-spenders, and safety-net/publicly-funded hospitals must not be ranked as "stingy" on the net ratio alone.

3. **Three Tier-A ratios are system/group aggregates, not the named facility.** #13 MGB (0.51%) is the entire 17-hospital MGB group return ($21.6B), not Mass General alone (MGH not isolable in the e-file XML); #16 Dignity (1.35%) spans Dignity's multi-state hospitals, not St. Joseph's Phoenix; #6 Novant and #18 Banner are system-wide filers. A generous local FAP can be buried inside a low system average and vice versa. These rows are labeled "(system)" and their rank should be read as a system observation.

4. **Single filing year and fiscal-year skew.** Every M3 ratio is FY2023 only, with fiscal-year-ends spanning June/September/December; charity care swings year-to-year with Medicaid policy and one-time write-offs. A single atypical year can mis-rank a hospital. Bottom-quartile flags should be confirmed against a 3-year average before any name is published or referred.

5. **FAP text ≠ actual screening practice, in both directions — FirstHealth (#5 in Tier A) shows it.** FirstHealth scores D3=0 because its *policy text* states free care only "at or below 100% FPL," yet M3-cited third-party data put its *effective* reach at ~204% FPL — so its rank may overstate the problem. Conversely, the NC hospitals' model D5=4 PE language does not prove their billing offices actually auto-grant. M2 measures **disclosed** accessibility (what a regulator can cite); M3's dollars are the partial corrective.

6. **Sample selection inflates the NC cluster and excludes the worst actors.** The top of the "best" end is dominated by NC HASP-bound hospitals that are *legally required* to carry the D5=4 PE language and to deliver charity care — so NC scoring well is partly a mandate artifact, not virtue. The sample over-represents large web-publishing systems (M1's stated bias), meaning even the low scorers here are likely **more** accessible than the absent small/rural hospitals. Read every result as "among prominent web-publishing systems, these rank worst," not "worst in America." The motivating 71%-billed / $14B aggregate traces to a single advocacy source (Dollar For, *Bridging the Chasm*, 2024); this scorecard scores each hospital on its own retrieved text and filing, so it does not depend on that aggregate being exact, but the problem's framing does.

7. **The 50/50 weighting and the Q3 anchor are stated choices, not derived optima.** Equal weighting and the top-quartile "fully adequate" anchor are defensible but contestable; a reader who weights charity spend more heavily, or anchors low-charity to the median rather than Q3, would shift mid-table ranks (the top and bottom of Tier A are robust to either choice; the middle — #7 through #12 — is sensitive). All sub-scores are published so the combination can be re-run under different weights.

### Which regulator each tier is most actionable for

- **Tier A bottom-quartile, well-resourced, no-offset rows (Penn/HUP #2, NewYork-Presbyterian #9, and the system aggregates MGB #7 / Dignity #11):** most actionable for the **IRS TE/GE division** as 501(r)/community-benefit audit-targeting candidates — these are the cleanest "large nonprofit, charity care far below peers, no safety-net-offset excuse" cases. The **Lown Institute** "fair share" frame (community benefit vs. the value of the tax exemption — M3's alternative-denominator caveat) sharpens exactly these targets.
- **Tier A low-accessibility rows regardless of ratio (Cleveland Clinic #6, Carilion #4, Sentara #10, FirstHealth #5):** most actionable for **state Attorneys General** (consumer-protection / nonprofit-oversight authority over deceptive or inaccessible disclosure) and for **Dollar For**, whose patient-navigation work directly targets application-only / documentation-heavy / asset-gated FAPs (D5=0, D6=1). The image-only PLS (Sentara) and 100%-FPL stated floor (FirstHealth) are concrete AG-citable disclosure defects.
- **Tier B (filing-unavailable):** most actionable for **the IRS and state charity regulators as a transparency question first** — why a $5.4B operator (Corewell) or a major authority (Atrium CMC's 990EZ group return) has no parseable facility Schedule H — not as a charity-spend enforcement target yet.
- **Tier C (governance non-filers):** the for-profit Mission/HCA (#C2) is outside 501(r) entirely and is most actionable for **state AGs / state charity-care statutes** (e.g. NC's HASP, which binds nonprofits but not HCA — the substantive D5=0 contrast). The public hospitals (Parkland, Cook County, NYC H+H) are most actionable for **local/state oversight and advocacy navigation** (residency gates, in-person-only application), not federal 501(r), since they file no 990.
