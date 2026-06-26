# M2 — Per-rocket-body classified inventory

**Problem:** Uncontrolled rocket-body reentries — the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M2 (row-level inventory of abandoned rocket bodies, classified controlled / uncontrolled / still-in-orbit).
**Input milestone:** **M1 — Methodology and Source Register** (`artifacts/2026-06-26-m1-methodology-source-register.md`). This artifact uses **only** M1's data sources (GCAT spine; Space-Track / CelesTrak cross-check; DISCOS / family dry-mass references), M1's controlled-vs-uncontrolled classification rule (six observable signals, the ≥7-day default test, default-to-uncontrolled for unresolved cases), M1's pinned **2013–2024** study window, and M1's **stage-not-payload** unit of analysis. No new method is introduced; where M1's rule needed a concrete catalog operationalisation, that operationalisation is stated explicitly in §2.
**Author:** generator routine | **Date:** 2026-06-26.

> **Reading guide.** The **centerpiece of this artifact is §3, the full one-row-per-rocket-body table covering all 1,073 bodies** in the window (split into three sub-tables by control label for readability; every individual body is its own row with NORAD, COSPAR, family, operator, launch state, dry mass + source, launch date, reentry date/status, and label). §4 is a *secondary* family-aggregated census. §5 is coverage/reconciliation, §6 the independent published sanity checks, then Limitations.

---

## 1. How this inventory was built (data + method, both traceable to M1)

**Spine.** The inventory is built from **GCAT** (M1 source 1), file `tsv/cat/satcat.tsv` from https://planet4589.org/space/gcat/ , downloaded 2026-06-26 (catalog header timestamp "Updated 2026 Jun 26 1346:41"). GCAT carries, per object: NORAD/Satcat number, COSPAR/international designator (`Piece`), object `Type`, `Name` (vehicle/stage), launching `State`, `Owner` (operator), `DryMass`, launch date `LDate`, decay date `DDate`, `Status`, orbital inclination `Inc`, and `Perigee`. These are exactly the M2-required attributes; the per-row **operator** column is GCAT `Owner` (distinct from launching `State`).

**Unit of analysis (from M1 §D).** One row per **orbital rocket stage / upper stage** — GCAT `Type` beginning `R` followed by a stage digit (`R1`,`R2`,`R3`,`R4`,`R5`). Payloads (`Type P*`), debris (`D*`), and components/adapters (`C*`) are excluded by M1's rule. Suborbital sounding-rocket entries (GCAT's separate `rcat.tsv`) are excluded — they never achieved orbit, per M1's exclusion of suborbital stages.

**Window (from M1 §D):** launch date `LDate` in **2013-01-01 … 2024-12-31**.

**Population produced by this filter: 1,073 orbital rocket bodies.** This is the M2 total population for the window (reconciliation in §5). The filter and classifier were re-run from a fresh GCAT download on 2026-06-26; the counts below (1,073 = 559 + 58 + 456) reproduce exactly.

**Mass source per row.** Dry mass is taken from GCAT's `DryMass` field, sourced by McDowell from manufacturer/agency spec sheets and cross-referenced to ESA DISCOS (M1 sources 1 and 7). GCAT populates a non-blank dry-mass value for **all 1,073** rows in this window, so no family-estimate fallback was needed. The per-row mass basis is therefore "**GCAT `DryMass`**" (stated in the table's column header). **Note on "dry/reentry mass":** the M2 format names "dry/reentry mass." The table reports **dry mass** (GCAT `DryMass`). A **reentry/surviving mass** (mass of fragments reaching the ground) is *not* a field in any open catalog — it requires fragment-level demise simulation (ORSAT-class, M1 Limitation 2) — so it is **not available per row**; this is flagged here rather than silently omitted, and surviving mass / casualty area is the explicit job of M3.

---

## 2. Control label assignment (M1 rule, operationalised on GCAT `Status`)

M1's rule (M1 §C) classifies each body **controlled**, **uncontrolled**, or **still-in-orbit** from observable, catalog-derivable signals. GCAT's `Status` field is the cleanest single catalog realisation of those signals, and maps to M1's rule as follows:

| GCAT `Status` | Meaning (GCAT phases doc) | M1 signal it realises | M1 label |
|---|---|---|---|
| `R` | Reentered — destroyed in atmosphere after **natural orbital decay** | Signal 6 (random/non-targeted decay) + signal 4 (dwell ≥ threshold for the long-lived majority) | **uncontrolled** |
| `D` | Deorbited — destroyed in atmosphere via **active deorbit maneuver** | Signal 1/3 (operator-declared / propulsive disposal) | **controlled** |
| `DSO` | Disposed to graveyard / escape / sub-orbital-disposal trajectory via an **active burn** (Centaur, CZ-5 S2, Ariane-5 ESC to Point-Nemo or heliocentric) | Signal 2/3 (targeted disposal, restartable stage) | **controlled** |
| `O` | In orbit — not yet reentered | M1 "still-in-orbit" branch | **still-in-orbit** |

*GCAT Status definitions:* https://planet4589.org/space/gcat/web/intro/phases.html (R = "Reentered … after natural orbital decay"; D = "Deorbited … via active deorbit maneuver"; O = "In orbit").

**On the ≥7-day test (M1 signal 4).** M1 adopts a launch-to-reentry span ≥ 7 days as the *proxy* discriminator (Byers et al. 2022). Here the cleaner ground truth — GCAT `Status R` (natural decay) vs `D`/`DSO` (active burn) — is available directly, so the span is treated as a cross-check, not the deciding test. They agree for the long-lived majority: of the 559 status-`R` (uncontrolled) bodies, **445 (≈80%) also have span ≥ 7 days**. The **114 status-`R` bodies with span < 7 days are still labelled uncontrolled** — M1-consistent, not a deviation: status `R` is by definition *natural decay with no burn* (signal 6), and these are very-low-orbit stages (mostly Soyuz Blok-I third stages inserted into ~170 km orbits) that decay naturally within days. A short span here means "naturally short-lived low-perigee stage," not "commanded deorbit."

**Disposal-capability override (M1 signal 5) — the CZ-5B worked example.** The four Long March 5B core stages (NORAD 45601, 48275, 53240, 54217; 21,600 kg each — the largest objects in this inventory and the most-reported uncontrolled reentries of the decade) have launch-to-reentry spans of 4–10 days. A naive ≥7-day proxy would have mislabelled the span-4 and span-6 cores ("controlled?"). M1 signal 5 (no disposal capability) and GCAT `Status R` (natural decay) both override that: the CZ-5B core has no re-ignitable disposal system and reenters uncontrolled. All four are correctly **uncontrolled** with no manual override needed — the worked example M1 anticipated.

**Default-uncontrolled count (M1 transparency requirement).** M1 requires reporting how many rows rest on the "cannot resolve → default uncontrolled" fallback. Here **zero** rows required that genuine fallback: every reentered row carries a definite GCAT `Status` (R, D, or DSO). The 114 short-span `R` rows are labelled uncontrolled by *signal 6 (natural decay) actively present*, not by absence of information.

---

## 3. The full per-rocket-body inventory (1,073 rows — one row per body)

This is the M2 deliverable. **Every cell's mass basis is GCAT `DryMass`; every row's control label is GCAT `Status` mapped per §2.** The three sub-tables (uncontrolled / controlled / still-in-orbit) together contain all 1,073 bodies; within each, rows are sorted by vehicle family then launch date. Operator = GCAT `Owner` (e.g. CASC = China Aerospace Sci & Tech Corp; CNSA; SPX = SpaceX; RLABN = Rocket Lab; ULAL = ULA; MHI = Mitsubishi; ISRO; CASC/EXPACE = ExPace; VVKO/RVSNR = Russian Aerospace/Strategic-Rocket Forces; AE = ArianeGroup; KHRO/KHRR = Khrunichev; NPOL = NPO Lavochkin). Reentry mass / surviving mass is not a per-row catalog field (see §1) — the mass column is dry mass.


#### Uncontrolled — 559 bodies

| NORAD | COSPAR (Piece) | Vehicle family | Operator (Owner) | Launch state | Dry mass kg (GCAT DryMass) | Launch date | Reentry date / status | Label |
|---|---|---|---|---|---:|---|---|---|
| 39147 | 2013-016F | Antares | OSCW | US | 1,220 | 2013-04-21 | 2013-05-01 | uncontrolled |
| 39259 | 2013-051B | Antares | OSCW | US | 1,220 | 2013-09-18 | 2013-10-09 | uncontrolled |
| 39503 | 2014-003B | Antares | OSCW | US | 1,083 | 2014-01-09 | 2014-01-18 | uncontrolled |
| 40085 | 2014-039B | Antares | OSCW | US | 1,083 | 2014-07-13 | 2014-07-19 | uncontrolled |
| 41819 | 2016-062B | Antares | OATKW | US | 1,220 | 2016-10-17 | 2016-11-06 | uncontrolled |
| 43007 | 2017-071B | Antares | OATKW | US | 1,220 | 2017-11-12 | 2017-11-25 | uncontrolled |
| 43475 | 2018-046B | Antares | OATKW | US | 1,220 | 2018-05-21 | 2018-06-05 | uncontrolled |
| 43705 | 2018-092B | Antares | NGISW | US | 1,220 | 2018-11-17 | 2018-11-28 | uncontrolled |
| 44206 | 2019-022B | Antares | NGISW | US | 1,220 | 2019-04-17 | 2019-04-28 | uncontrolled |
| 44702 | 2019-071B | Antares | NGISW | US | 1,220 | 2019-11-02 | 2019-11-07 | uncontrolled |
| 45177 | 2020-011C | Antares | NGISW | US | 1,220 | 2020-02-15 | 2020-02-23 | uncontrolled |
| 46531 | 2020-069B | Antares | NGISW | US | 1,220 | 2020-10-03 | 2020-10-07 | uncontrolled |
| 47690 | 2021-013B | Antares | NGISW | US | 1,220 | 2021-02-20 | 2021-03-01 | uncontrolled |
| 49065 | 2021-072B | Antares | NGISW | US | 1,220 | 2021-08-10 | 2021-08-18 | uncontrolled |
| 51713 | 2022-015B | Antares | NGISW | US | 1,220 | 2022-02-19 | 2022-02-25 | uncontrolled |
| 54233 | 2022-149B | Antares | NGISW | US | 1,220 | 2022-11-07 | 2022-11-09 | uncontrolled |
| 57489 | 2023-110B | Antares | NGISW | US | 1,220 | 2023-08-02 | 2023-08-05 | uncontrolled |
| 39217 | 2013-038C | Ariane 5 | AE | F | 5,000 | 2013-07-25 | 2021-02-10 | uncontrolled |
| 44036 | 2019-007C | Ariane 5 | AESP | F | 5,000 | 2019-02-05 | 2024-08-15 | uncontrolled |
| 39454 | 2013-067D | Briz-KM | EUROK | RU | 2,370 | 2013-11-22 | 2022-08-01 | uncontrolled |
| 43531 | 2018-056C | CN commercial small (SMA/YL/OS-M) | CASC | CN | 550 | 2018-07-09 | 2019-03-12 | uncontrolled |
| 58761 | 2024-009D | CN commercial small (SMA/YL/OS-M) | CASC | CN | 1,000 | 2024-01-11 | 2024-06-29 | uncontrolled |
| 40929 | 2015-051E | CZ-11 | CASC | CN | 500 | 2015-09-25 | 2015-10-02 | uncontrolled |
| 43444 | 2018-040F | CZ-11 | CASC | CN | 500 | 2018-04-26 | 2018-04-29 | uncontrolled |
| 43945 | 2019-005D | CZ-11 | CASC | CN | 500 | 2019-01-21 | 2019-01-28 | uncontrolled |
| 44317 | 2019-032H | CZ-11 | CASC | CN | 500 | 2019-06-05 | 2021-03-12 | uncontrolled |
| 44535 | 2019-060B | CZ-11 | CASC | CN | 500 | 2019-09-19 | 2019-09-19 | uncontrolled |
| 45613 | 2020-032C | CZ-11 | CASC | CN | 500 | 2020-05-29 | 2022-04-29 | uncontrolled |
| 46463 | 2020-065K | CZ-11 | CASC | CN | 500 | 2020-09-15 | 2021-02-21 | uncontrolled |
| 47239 | 2020-094D | CZ-11 | CASC | CN | 500 | 2020-12-09 | 2020-12-22 | uncontrolled |
| 52154 | 2022-032B | CZ-11 | CASC | CN | 500 | 2022-03-30 | 2022-04-07 | uncontrolled |
| 52393 | 2022-046F | CZ-11 | CASC | CN | 500 | 2022-04-30 | 2022-05-29 | uncontrolled |
| 54022 | 2022-126C | CZ-11 | CASC | CN | 500 | 2022-10-07 | 2024-04-21 | uncontrolled |
| 58653 | 2023-206D | CZ-11 | CASC | CN | 500 | 2023-12-25 | 2024-01-18 | uncontrolled |
| 39364 | 2013-059B | CZ-2C | CNSA | CN | 4,006 | 2013-10-29 | 2024-06-29 | uncontrolled |
| 40306 | 2014-071B | CZ-2C | CNSA | CN | 4,006 | 2014-11-14 | 2023-01-21 | uncontrolled |
| 43031 | 2017-075D | CZ-2C | CASC | CN | 3,800 | 2017-11-24 | 2025-04-10 | uncontrolled |
| 43173 | 2018-011E | CZ-2C | CASC | CN | 3,800 | 2018-01-25 | 2023-12-23 | uncontrolled |
| 43521 | 2018-054D | CZ-2C | CASC | CN | 3,800 | 2018-06-27 | 2026-02-28 | uncontrolled |
| 43532 | 2018-056D | CZ-2C | CNSA | CN | 4,006 | 2018-07-09 | 2019-04-30 | uncontrolled |
| 43667 | 2018-083F | CZ-2C | CASC | CN | 3,800 | 2018-10-29 | 2019-02-05 | uncontrolled |
| 44452 | 2019-045D | CZ-2C | CASC | CN | 3,800 | 2019-07-26 | 2025-07-24 | uncontrolled |
| 45463 | 2020-021D | CZ-2C | CASC | CN | 3,800 | 2020-03-24 | 2024-04-25 | uncontrolled |
| 46811 | 2020-076E | CZ-2C | CASC | CN | 3,800 | 2020-10-26 | 2025-01-14 | uncontrolled |
| 49030 | 2021-065E | CZ-2C | CASC | CN | 3,800 | 2021-07-19 | 2026-01-26 | uncontrolled |
| 52323 | 2022-043D | CZ-2C | CASC | CN | 3,800 | 2022-04-29 | 2023-06-20 | uncontrolled |
| 53131 | 2022-082D | CZ-2C | CASC | CN | 3,800 | 2022-07-15 | 2024-04-30 | uncontrolled |
| 55240 | 2023-005B | CZ-2C | CASC | CN | 3,800 | 2023-01-12 | 2023-02-07 | uncontrolled |
| 55691 | 2023-025B | CZ-2C | CASC | CN | 3,800 | 2023-02-24 | 2026-02-12 | uncontrolled |
| 56734 | 2023-069D | CZ-2C | CASC | CN | 3,800 | 2023-05-21 | 2024-04-23 | uncontrolled |
| 57536 | 2023-116C | CZ-2C | CASC | CN | 3,800 | 2023-08-08 | 2024-12-24 | uncontrolled |
| 59229 | 2024-048B | CZ-2C | CASC | CN | 3,800 | 2024-03-13 | 2024-03-30 | uncontrolled |
| 60090 | 2024-116C | CZ-2C | CASC | CN | 3,800 | 2024-06-22 | 2024-08-04 | uncontrolled |
| 61620 | 2024-190D | CZ-2C | CASC | CN | 3,800 | 2024-10-23 | 2024-11-21 | uncontrolled |
| 40138 | 2014-051C | CZ-2D | CNSA | CN | 4,006 | 2014-09-04 | 2015-06-13 | uncontrolled |
| 41449 | 2016-023B | CZ-2D | CASC | CN | 4,006 | 2016-04-05 | 2016-04-18 | uncontrolled |
| 41902 | 2016-081E | CZ-2D | CNSA | CN | 4,006 | 2016-12-21 | 2020-03-21 | uncontrolled |
| 41910 | 2016-083D | CZ-2D | CNSA | CN | 4,006 | 2016-12-28 | 2017-01-23 | uncontrolled |
| 43101 | 2018-002C | CZ-2D | CNSA | CN | 4,006 | 2018-01-09 | 2023-06-22 | uncontrolled |
| 43916 | 2018-112H | CZ-2D | CASC | CN | 4,006 | 2018-12-29 | 2019-01-01 | uncontrolled |
| 45252 | 2020-014D | CZ-2D | CASC | CN | 4,006 | 2020-02-19 | 2023-02-18 | uncontrolled |
| 49392 | 2021-101C | CZ-2D | CASC | CN | 4,006 | 2021-11-06 | 2023-04-07 | uncontrolled |
| 55245 | 2023-006D | CZ-2D | CASC | CN | 4,006 | 2023-01-13 | 2024-02-17 | uncontrolled |
| 57455 | 2023-106D | CZ-2D | CASC | CN | 4,006 | 2023-07-26 | 2024-04-28 | uncontrolled |
| 57729 | 2023-130C | CZ-2D | CASC | CN | 4,006 | 2023-08-31 | 2024-06-23 | uncontrolled |
| 57887 | 2023-145B | CZ-2D | CASC | CN | 4,006 | 2023-09-17 | 2024-06-23 | uncontrolled |
| 57987 | 2023-152B | CZ-2D | CASC | CN | 4,006 | 2023-10-05 | 2024-08-04 | uncontrolled |
| 58142 | 2023-163B | CZ-2D | CASC | CN | 4,006 | 2023-10-23 | 2024-10-08 | uncontrolled |
| 58561 | 2023-194E | CZ-2D | CASC | CN | 4,006 | 2023-12-10 | 2024-09-24 | uncontrolled |
| 59286 | 2024-052G | CZ-2D | CASC | CN | 4,006 | 2024-03-21 | 2024-03-23 | uncontrolled |
| 59558 | 2024-075B | CZ-2D | CASC | CN | 4,006 | 2024-04-20 | 2025-05-22 | uncontrolled |
| 61445 | 2024-177B | CZ-2D | CASC | CN | 4,006 | 2024-09-27 | 2024-11-10 | uncontrolled |
| 39180 | 2013-029B | CZ-2F | CALT | CN | 5,500 | 2013-06-11 | 2013-06-21 | uncontrolled |
| 41766 | 2016-057B | CZ-2F | CALT | CN | 5,500 | 2016-09-15 | 2016-09-29 | uncontrolled |
| 41813 | 2016-061B | CZ-2F | CALT | CN | 5,500 | 2016-10-16 | 2016-11-03 | uncontrolled |
| 46390 | 2020-063B | CZ-2F | CALT | CN | 5,500 | 2020-09-04 | 2021-07-01 | uncontrolled |
| 48853 | 2021-053B | CZ-2F | CALT | CN | 5,500 | 2021-06-17 | 2021-07-03 | uncontrolled |
| 49327 | 2021-092B | CZ-2F | CALT | CN | 5,500 | 2021-10-15 | 2021-11-01 | uncontrolled |
| 52798 | 2022-060B | CZ-2F | CALT | CN | 5,500 | 2022-06-05 | 2022-06-20 | uncontrolled |
| 53358 | 2022-093B | CZ-2F | CALT | CN | 5,500 | 2022-08-04 | 2024-02-12 | uncontrolled |
| 54380 | 2022-162B | CZ-2F | CALT | CN | 5,500 | 2022-11-29 | 2022-12-11 | uncontrolled |
| 56766 | 2023-077F | CZ-2F | CALT | CN | 5,500 | 2023-05-30 | 2023-06-12 | uncontrolled |
| 58147 | 2023-164B | CZ-2F | CALT | CN | 5,500 | 2023-10-26 | 2023-11-03 | uncontrolled |
| 58574 | 2023-195B | CZ-2F | CALT | CN | 5,500 | 2023-12-14 | 2024-03-10 | uncontrolled |
| 59592 | 2024-078B | CZ-2F | CALT | CN | 5,500 | 2024-04-25 | 2024-05-06 | uncontrolled |
| 61686 | 2024-194D | CZ-2F | CALT | CN | 5,500 | 2024-10-29 | 2024-11-07 | uncontrolled |
| 43540 | 2018-057B | CZ-3A | CASC | CN | 2,800 | 2018-07-09 | 2019-12-04 | uncontrolled |
| 39482 | 2013-075B | CZ-3B | CASC | CN | 2,800 | 2013-12-20 | 2020-08-31 | uncontrolled |
| 40750 | 2015-037C | CZ-3B | CASC | CN | 2,800 | 2015-07-25 | 2026-04-07 | uncontrolled |
| 40893 | 2015-046B | CZ-3B | CASC | CN | 2,800 | 2015-09-12 | 2016-01-30 | uncontrolled |
| 40939 | 2015-053B | CZ-3B | CASC | CN | 2,800 | 2015-09-29 | 2016-04-08 | uncontrolled |
| 40983 | 2015-059B | CZ-3B | CASC | CN | 2,800 | 2015-10-16 | 2016-01-15 | uncontrolled |
| 41035 | 2015-067B | CZ-3B | CASC | CN | 2,800 | 2015-11-20 | 2016-07-03 | uncontrolled |
| 41104 | 2015-073B | CZ-3B | CASC | CN | 2,800 | 2015-12-09 | 2016-05-14 | uncontrolled |
| 41195 | 2015-083B | CZ-3B | CASC | CN | 2,800 | 2015-12-28 | 2020-10-28 | uncontrolled |
| 41239 | 2016-001B | CZ-3B | CASC | CN | 2,800 | 2016-01-15 | 2016-07-04 | uncontrolled |
| 41726 | 2016-048B | CZ-3B | CASC | CN | 2,800 | 2016-08-05 | 2017-07-21 | uncontrolled |
| 41883 | 2016-077B | CZ-3B | CASC | CN | 2,800 | 2016-12-10 | 2019-01-20 | uncontrolled |
| 41912 | 2017-001B | CZ-3B | CASC | CN | 2,800 | 2017-01-05 | 2020-01-21 | uncontrolled |
| 42764 | 2017-035B | CZ-3B | CASC | CN | 2,800 | 2017-06-18 | 2022-01-02 | uncontrolled |
| 43004 | 2017-069D | CZ-3B | CASC | CN | 2,800 | 2017-11-05 | 2021-09-22 | uncontrolled |
| 43040 | 2017-078B | CZ-3B | CASC | CN | 2,800 | 2017-12-10 | 2018-03-10 | uncontrolled |
| 43209 | 2018-018C | CZ-3B | CASC | CN | 2,800 | 2018-02-12 | 2021-05-03 | uncontrolled |
| 43451 | 2018-041B | CZ-3B | CASC | CN | 2,800 | 2018-05-03 | 2021-07-07 | uncontrolled |
| 43583 | 2018-062C | CZ-3B | CASC | CN | 2,800 | 2018-07-29 | 2019-07-20 | uncontrolled |
| 43604 | 2018-067C | CZ-3B | CASC | CN | 2,800 | 2018-08-24 | 2019-07-04 | uncontrolled |
| 43624 | 2018-072C | CZ-3B | CASC | CN | 2,800 | 2018-09-19 | 2023-08-18 | uncontrolled |
| 43684 | 2018-085B | CZ-3B | CASC | CN | 2,800 | 2018-11-01 | 2019-03-10 | uncontrolled |
| 43709 | 2018-093D | CZ-3B | CASC | CN | 2,800 | 2018-11-18 | 2019-10-28 | uncontrolled |
| 43921 | 2019-001B | CZ-3B | CASC | CN | 2,800 | 2019-01-10 | 2019-07-03 | uncontrolled |
| 44068 | 2019-012B | CZ-3B | CASC | CN | 2,800 | 2019-03-09 | 2023-12-16 | uncontrolled |
| 44338 | 2019-035B | CZ-3B | CASC | CN | 2,800 | 2019-06-24 | 2019-10-22 | uncontrolled |
| 44494 | 2019-053B | CZ-3B | CASC | CN | 2,800 | 2019-08-19 | 2023-05-26 | uncontrolled |
| 44545 | 2019-061D | CZ-3B | CASC | CN | 2,800 | 2019-09-22 | 2020-09-22 | uncontrolled |
| 44638 | 2019-070B | CZ-3B | CASC | CN | 2,800 | 2019-10-17 | 2024-11-01 | uncontrolled |
| 44710 | 2019-073B | CZ-3B | CASC | CN | 2,800 | 2019-11-04 | 2021-02-25 | uncontrolled |
| 44867 | 2019-090D | CZ-3B | CASC | CN | 2,800 | 2019-12-16 | 2025-11-08 | uncontrolled |
| 44979 | 2020-002B | CZ-3B | CASC | CN | 2,800 | 2020-01-07 | 2021-04-03 | uncontrolled |
| 45345 | 2020-017B | CZ-3B | CASC | CN | 2,800 | 2020-03-09 | 2025-10-28 | uncontrolled |
| 46611 | 2020-071B | CZ-3B | CASC | CN | 2,800 | 2020-10-11 | 2021-01-02 | uncontrolled |
| 46917 | 2020-082B | CZ-3B | CASC | CN | 2,800 | 2020-11-12 | 2021-02-28 | uncontrolled |
| 47232 | 2020-092B | CZ-3B | CASC | CN | 2,800 | 2020-12-06 | 2023-05-02 | uncontrolled |
| 47322 | 2021-003B | CZ-3B | CASC | CN | 2,800 | 2021-01-19 | 2022-03-28 | uncontrolled |
| 47614 | 2021-010B | CZ-3B | CASC | CN | 2,800 | 2021-02-04 | 2022-04-02 | uncontrolled |
| 48809 | 2021-047B | CZ-3B | CASC | CN | 2,800 | 2021-06-02 | 2022-08-09 | uncontrolled |
| 49063 | 2021-071B | CZ-3B | CASC | CN | 2,800 | 2021-08-05 | 2021-11-22 | uncontrolled |
| 49116 | 2021-077B | CZ-3B | CASC | CN | 2,800 | 2021-08-24 | 2021-11-13 | uncontrolled |
| 49126 | 2021-080B | CZ-3B | CASC | CN | 2,800 | 2021-09-09 | 2022-05-12 | uncontrolled |
| 49259 | 2021-087B | CZ-3B | CASC | CN | 2,800 | 2021-09-27 | 2022-08-14 | uncontrolled |
| 49506 | 2021-114B | CZ-3B | CASC | CN | 2,800 | 2021-11-26 | 2023-05-10 | uncontrolled |
| 50006 | 2021-124B | CZ-3B | CASC | CN | 2,800 | 2021-12-13 | 2024-02-03 | uncontrolled |
| 50575 | 2021-135B | CZ-3B | CASC | CN | 2,800 | 2021-12-29 | 2022-09-15 | uncontrolled |
| 53101 | 2022-078B | CZ-3B | CASC | CN | 2,800 | 2022-07-12 | 2023-10-20 | uncontrolled |
| 54231 | 2022-148B | CZ-3B | CASC | CN | 2,800 | 2022-11-05 | 2023-05-10 | uncontrolled |
| 54879 | 2022-178B | CZ-3B | CASC | CN | 2,800 | 2022-12-29 | 2023-06-30 | uncontrolled |
| 57625 | 2023-120B | CZ-3B | CASC | CN | 2,800 | 2023-08-12 | 2023-10-30 | uncontrolled |
| 58254 | 2023-172B | CZ-3B | CASC | CN | 2,800 | 2023-11-09 | 2024-04-22 | uncontrolled |
| 60328 | 2024-135B | CZ-3B | CASC | CN | 2,800 | 2024-08-01 | 2025-04-13 | uncontrolled |
| 61188 | 2024-168D | CZ-3B | CASC | CN | 2,800 | 2024-09-19 | 2025-09-19 | uncontrolled |
| 62189 | 2024-227B | CZ-3B | CASC | CN | 2,800 | 2024-12-03 | 2025-02-22 | uncontrolled |
| 40550 | 2015-019B | CZ-3C | CASC | CN | 2,800 | 2015-03-30 | 2016-03-23 | uncontrolled |
| 41325 | 2016-006C | CZ-3C | CASC | CN | 2,800 | 2016-02-01 | 2019-10-04 | uncontrolled |
| 49012 | 2021-063B | CZ-3C | CASC | CN | 2,800 | 2021-07-06 | 2022-05-29 | uncontrolled |
| 39359 | 2013-057B | CZ-4B | CNSA | CN | 1,000 | 2013-10-25 | 2025-09-10 | uncontrolled |
| 40120 | 2014-049C | CZ-4B | CNSA | CN | 1,000 | 2014-08-19 | 2017-05-27 | uncontrolled |
| 40145 | 2014-053C | CZ-4B | CNSA | CN | 1,000 | 2014-09-08 | 2014-10-23 | uncontrolled |
| 40363 | 2014-088B | CZ-4B | CNSA | CN | 1,000 | 2014-12-27 | 2015-02-24 | uncontrolled |
| 40702 | 2015-030B | CZ-4B | CNSA | CN | 1,000 | 2015-06-26 | 2015-09-08 | uncontrolled |
| 41027 | 2015-064B | CZ-4B | CNSA | CN | 1,000 | 2015-11-08 | 2015-12-26 | uncontrolled |
| 41559 | 2016-033D | CZ-4B | CNSA | CN | 1,000 | 2016-05-30 | 2017-01-08 | uncontrolled |
| 41635 | 2016-043B | CZ-4B | CNSA | CN | 1,000 | 2016-06-29 | 2022-04-06 | uncontrolled |
| 42762 | 2017-034E | CZ-4B | CNSA | CN | 1,000 | 2017-06-15 | 2018-08-25 | uncontrolled |
| 43586 | 2018-063B | CZ-4B | CNSA | CN | 1,000 | 2018-07-31 | 2018-11-04 | uncontrolled |
| 44210 | 2019-024D | CZ-4B | CNSA | CN | 1,000 | 2019-04-29 | 2020-07-04 | uncontrolled |
| 44707 | 2019-072E | CZ-4B | CNSA | CN | 1,000 | 2019-11-03 | 2020-04-08 | uncontrolled |
| 44888 | 2019-093K | CZ-4B | CNSA | CN | 1,000 | 2019-12-20 | 2026-01-27 | uncontrolled |
| 45858 | 2020-042C | CZ-4B | CNSA | CN | 1,000 | 2020-07-03 | 2024-10-19 | uncontrolled |
| 45942 | 2020-051D | CZ-4B | CNSA | CN | 1,000 | 2020-07-25 | 2021-09-09 | uncontrolled |
| 46397 | 2020-064B | CZ-4B | CNSA | CN | 1,000 | 2020-09-07 | 2021-01-01 | uncontrolled |
| 46481 | 2020-067D | CZ-4B | CNSA | CN | 1,000 | 2020-09-27 | 2025-03-04 | uncontrolled |
| 49073 | 2021-074C | CZ-4B | CNSA | CN | 1,000 | 2021-08-18 | 2022-09-03 | uncontrolled |
| 49493 | 2021-107B | CZ-4B | CNSA | CN | 1,000 | 2021-11-20 | 2022-01-26 | uncontrolled |
| 49964 | 2021-122D | CZ-4B | CNSA | CN | 1,000 | 2021-12-10 | 2022-04-29 | uncontrolled |
| 53349 | 2022-090D | CZ-4B | CNSA | CN | 1,000 | 2022-08-04 | 2023-01-17 | uncontrolled |
| 54819 | 2022-176B | CZ-4B | CNSA | CN | 1,000 | 2022-12-27 | 2023-02-16 | uncontrolled |
| 56233 | 2023-055B | CZ-4B | CNSA | CN | 1,000 | 2023-04-16 | 2023-04-26 | uncontrolled |
| 60250 | 2024-130B | CZ-4B | CNSA | CN | 1,000 | 2024-07-19 | 2024-08-23 | uncontrolled |
| 60467 | 2024-148K | CZ-4B | CNSA | CN | 1,000 | 2024-08-16 | 2024-12-20 | uncontrolled |
| 60951 | 2024-156G | CZ-4B | CNSA | CN | 1,000 | 2024-09-03 | 2025-03-09 | uncontrolled |
| 44623 | 2019-066B | CZ-4C | CNSA | CN | 1,000 | 2019-10-04 | 2025-12-05 | uncontrolled |
| 44820 | 2019-082B | CZ-4C | CNSA | CN | 1,000 | 2019-11-27 | 2024-11-10 | uncontrolled |
| 51285 | 2022-007B | CZ-4C | CNSA | CN | 1,000 | 2022-01-25 | 2026-01-24 | uncontrolled |
| 51823 | 2022-018B | CZ-4C | CNSA | CN | 1,000 | 2022-02-26 | 2025-04-30 | uncontrolled |
| 41839 | 2016-065B | CZ-5 | CNSA | CN | 5,100 | 2016-11-03 | 2024-07-12 | uncontrolled |
| 44911 | 2019-097B | CZ-5 | CNSA | CN | 5,100 | 2019-12-27 | 2022-05-02 | uncontrolled |
| 45601 | 2020-027C | CZ-5B | CNSA | CN | 21,600 | 2020-05-05 | 2020-05-11 | uncontrolled |
| 48275 | 2021-035B | CZ-5B | CNSA | CN | 21,600 | 2021-04-29 | 2021-05-09 | uncontrolled |
| 53240 | 2022-085B | CZ-5B | CNSA | CN | 21,600 | 2022-07-24 | 2022-07-30 | uncontrolled |
| 54217 | 2022-143B | CZ-5B | CNSA | CN | 21,600 | 2022-10-31 | 2022-11-04 | uncontrolled |
| 40913 | 2015-049Q | CZ-6 | CNSA | CN | 1,000 | 2015-09-19 | 2023-02-02 | uncontrolled |
| 43025 | 2017-074D | CZ-6 | CNSA | CN | 1,000 | 2017-11-21 | 2023-11-11 | uncontrolled |
| 46841 | 2020-079Q | CZ-6 | CNSA | CN | 1,000 | 2020-11-06 | 2020-12-21 | uncontrolled |
| 48257 | 2021-033K | CZ-6 | CNSA | CN | 1,000 | 2021-04-27 | 2024-02-09 | uncontrolled |
| 59681 | 2024-085E | CZ-6 | MAI | CN | 3,000 | 2024-05-07 | 2026-01-22 | uncontrolled |
| 41628 | 2016-042E | CZ-7 | CNSA | CN | 6,000 | 2016-06-25 | 2016-07-28 | uncontrolled |
| 42685 | 2017-021B | CZ-7 | CNSA | CN | 6,000 | 2017-04-20 | 2017-05-18 | uncontrolled |
| 48804 | 2021-046B | CZ-7 | CNSA | CN | 6,000 | 2021-05-29 | 2021-06-15 | uncontrolled |
| 49223 | 2021-085B | CZ-7 | CNSA | CN | 6,000 | 2021-09-20 | 2021-10-04 | uncontrolled |
| 52512 | 2022-050D | CZ-7 | CNSA | CN | 6,000 | 2022-05-09 | 2022-05-25 | uncontrolled |
| 54240 | 2022-152D | CZ-7 | CNSA | CN | 6,000 | 2022-11-12 | 2022-11-15 | uncontrolled |
| 56447 | 2023-063B | CZ-7 | CNSA | CN | 6,000 | 2023-05-10 | 2023-05-21 | uncontrolled |
| 58812 | 2024-013B | CZ-7 | CNSA | CN | 6,000 | 2024-01-17 | 2024-01-27 | uncontrolled |
| 61984 | 2024-211B | CZ-7 | CNSA | CN | 6,000 | 2024-11-15 | 2024-11-24 | uncontrolled |
| 47852 | 2021-019B | CZ-7A | CASC | CN | 2,800 | 2021-03-11 | 2022-11-22 | uncontrolled |
| 50323 | 2021-129C | CZ-7A | CASC | CN | 2,800 | 2021-12-23 | 2022-01-07 | uncontrolled |
| 53814 | 2022-112B | CZ-7A | CASC | CN | 2,800 | 2022-09-13 | 2022-10-13 | uncontrolled |
| 58205 | 2023-169B | CZ-7A | CASC | CN | 2,800 | 2023-11-03 | 2024-01-14 | uncontrolled |
| 60180 | 2024-122B | CZ-7A | CASC | CN | 2,800 | 2024-06-29 | 2025-10-28 | uncontrolled |
| 60607 | 2024-151B | CZ-7A | CASC | CN | 2,800 | 2024-08-22 | 2025-01-01 | uncontrolled |
| 47301 | 2020-102F | CZ-8 | CASC | CN | 2,800 | 2020-12-22 | 2023-03-16 | uncontrolled |
| 51842 | 2022-019U | CZ-8 | CASC | CN | 2,800 | 2022-02-27 | 2024-07-28 | uncontrolled |
| 39121 | 2013-011B | Centaur | ULAL | US | 2,020 | 2013-03-19 | 2014-11-23 | uncontrolled |
| 39257 | 2013-050B | Centaur | ULAL | US | 2,020 | 2013-09-18 | 2015-02-08 | uncontrolled |
| 40486 | 2015-011E | Centaur | ULAL | US | 2,020 | 2015-03-13 | 2017-08-26 | uncontrolled |
| 41894 | 2016-079B | Centaur | ULAL | US | 2,020 | 2016-12-18 | 2017-03-05 | uncontrolled |
| 41938 | 2017-004B | Centaur | ULAL | US | 2,020 | 2017-01-21 | 2019-11-19 | uncontrolled |
| 41333 | 2016-009B | DPRK (Unha/Chollima) | NADA | KP | 50 | 2016-02-07 | 2023-06-09 | uncontrolled |
| 39223 | 2013-041B | Delta | ULAB | US | 3,450 | 2013-08-08 | 2017-07-11 | uncontrolled |
| 40747 | 2015-036B | Delta | ULAB | US | 3,450 | 2015-07-24 | 2019-07-22 | uncontrolled |
| 43164 | 2018-010B | Electron | RLABN | NZ | 45 | 2018-01-21 | 2023-12-17 | uncontrolled |
| 43166 | 2018-010D | Electron | RLABN | NZ | 270 | 2018-01-21 | 2019-03-03 | uncontrolled |
| 43691 | 2018-088B | Electron | RLABN | NZ | 250 | 2018-11-11 | 2018-12-28 | uncontrolled |
| 43851 | 2018-104C | Electron | RLABN | NZ | 50 | 2018-12-16 | 2023-10-09 | uncontrolled |
| 43863 | 2018-104Q | Electron | RLABN | NZ | 250 | 2018-12-16 | 2019-01-30 | uncontrolled |
| 44074 | 2019-016B | Electron | RLABN | NZ | 40 | 2019-03-28 | 2021-06-25 | uncontrolled |
| 44075 | 2019-016C | Electron | RLABN | NZ | 250 | 2019-03-28 | 2019-04-15 | uncontrolled |
| 44227 | 2019-026C | Electron | RLABN | NZ | 45 | 2019-05-05 | 2023-09-15 | uncontrolled |
| 44228 | 2019-026D | Electron | RLABN | NZ | 250 | 2019-05-05 | 2019-05-17 | uncontrolled |
| 44368 | 2019-037D | Electron | RLABN | NZ | 50 | 2019-06-29 | 2022-04-14 | uncontrolled |
| 44372 | 2019-037H | Electron | RLABN | NZ | 250 | 2019-06-29 | 2020-03-16 | uncontrolled |
| 44496 | 2019-054B | Electron | RLABN | NZ | 50 | 2019-08-19 | 2025-02-12 | uncontrolled |
| 44500 | 2019-054F | Electron | RLABN | NZ | 250 | 2019-08-19 | 2020-11-05 | uncontrolled |
| 44635 | 2019-069B | Electron | RLABN | NZ | 250 | 2019-10-17 | 2023-09-13 | uncontrolled |
| 44825 | 2019-084B | Electron | RLABN | NZ | 50 | 2019-12-06 | 2020-11-08 | uncontrolled |
| 44826 | 2019-084C | Electron | RLABN | NZ | 250 | 2019-12-06 | 2019-12-18 | uncontrolled |
| 45111 | 2020-007B | Electron | RLABN | NZ | 40 | 2020-01-31 | 2026-03-21 | uncontrolled |
| 45112 | 2020-007C | Electron | RLABN | NZ | 250 | 2020-01-31 | 2020-02-22 | uncontrolled |
| 45729 | 2020-037G | Electron | RLABN | NZ | 250 | 2020-06-13 | 2020-07-08 | uncontrolled |
| 46270 | 2020-060C | Electron | RLABN | NZ | 250 | 2020-08-31 | 2020-09-19 | uncontrolled |
| 46823 | 2020-077L | Electron | RLABN | NZ | 250 | 2020-10-28 | 2020-11-11 | uncontrolled |
| 46824 | 2020-077M | Electron | RLABN | NZ | 50 | 2020-10-28 | 2024-01-14 | uncontrolled |
| 46929 | 2020-085A | Electron | RLABN | NZ | 50 | 2020-11-20 | 2023-09-21 | uncontrolled |
| 46930 | 2020-085B | Electron | RLABN | NZ | 250 | 2020-11-20 | 2020-11-30 | uncontrolled |
| 47254 | 2020-098B | Electron | RLABN | NZ | 40 | 2020-12-15 | 2024-01-10 | uncontrolled |
| 47255 | 2020-098C | Electron | RLABN | NZ | 250 | 2020-12-15 | 2020-12-28 | uncontrolled |
| 47348 | 2021-004C | Electron | RLABN | NZ | 250 | 2021-01-20 | 2021-09-16 | uncontrolled |
| 47970 | 2021-023F | Electron | RLABN | NZ | 250 | 2021-03-22 | 2022-01-15 | uncontrolled |
| 49053 | 2021-068B | Electron | RLABN | NZ | 250 | 2021-07-29 | 2021-11-15 | uncontrolled |
| 49054 | 2021-068C | Electron | RLABN | NZ | 40 | 2021-07-29 | 2022-10-13 | uncontrolled |
| 49472 | 2021-106D | Electron | RLABN | NZ | 250 | 2021-11-18 | 2021-11-30 | uncontrolled |
| 49473 | 2021-106E | Electron | RLABN | NZ | 40 | 2021-11-18 | 2021-11-22 | uncontrolled |
| 49952 | 2021-120D | Electron | RLABN | NZ | 250 | 2021-12-09 | 2021-12-17 | uncontrolled |
| 49953 | 2021-120E | Electron | RLABN | NZ | 40 | 2021-12-09 | 2021-12-20 | uncontrolled |
| 51848 | 2022-020B | Electron | RLABN | NZ | 40 | 2022-02-28 | 2024-05-21 | uncontrolled |
| 51849 | 2022-020C | Electron | RLABN | NZ | 250 | 2022-02-28 | 2022-03-15 | uncontrolled |
| 52198 | 2022-034D | Electron | RLABN | NZ | 250 | 2022-04-02 | 2022-04-06 | uncontrolled |
| 52199 | 2022-034E | Electron | RLABN | NZ | 40 | 2022-04-02 | 2022-04-11 | uncontrolled |
| 52428 | 2022-047AL | Electron | RLABN | NZ | 250 | 2022-05-02 | 2022-05-18 | uncontrolled |
| 52915 | 2022-070B | Electron | RLABN | NZ | 250 | 2022-06-28 | 2022-06-28 | uncontrolled |
| 53103 | 2022-079B | Electron | RLABN | NZ | 250 | 2022-07-13 | 2022-10-02 | uncontrolled |
| 53353 | 2022-091B | Electron | RLABN | NZ | 250 | 2022-08-04 | 2022-10-20 | uncontrolled |
| 53816 | 2022-113B | Electron | RLABN | NZ | 250 | 2022-09-15 | 2022-09-28 | uncontrolled |
| 54025 | 2022-127C | Electron | RLABN | NZ | 250 | 2022-10-07 | 2023-02-27 | uncontrolled |
| 54229 | 2022-147C | Electron | RLABN | NZ | 250 | 2022-11-04 | 2022-11-20 | uncontrolled |
| 55325 | 2023-011B | Electron | RLABN | NZ | 40 | 2023-01-24 | 2025-10-20 | uncontrolled |
| 55328 | 2023-011E | Electron | RLABN | NZ | 250 | 2023-01-24 | 2023-05-27 | uncontrolled |
| 55911 | 2023-035D | Electron | RLABN | NZ | 250 | 2023-03-16 | 2023-03-22 | uncontrolled |
| 55984 | 2023-041D | Electron | RLABN | NZ | 40 | 2023-03-24 | 2023-04-07 | uncontrolled |
| 55985 | 2023-041E | Electron | RLABN | NZ | 250 | 2023-03-24 | 2023-04-01 | uncontrolled |
| 56443 | 2023-062B | Electron | RLABN | NZ | 40 | 2023-05-08 | 2025-04-12 | uncontrolled |
| 56445 | 2023-062D | Electron | RLABN | NZ | 250 | 2023-05-08 | 2025-10-11 | uncontrolled |
| 56752 | 2023-073A | Electron | RLABN | NZ | 40 | 2023-05-26 | 2025-05-20 | uncontrolled |
| 56755 | 2023-073D | Electron | RLABN | NZ | 250 | 2023-05-26 | 2025-05-14 | uncontrolled |
| 57394 | 2023-100J | Electron | RLABN | NZ | 250 | 2023-07-18 | 2023-08-03 | uncontrolled |
| 57695 | 2023-126C | Electron | RLABN | NZ | 250 | 2023-08-23 | 2023-09-11 | uncontrolled |
| 58580 | 2023-196C | Electron | RLABN | NZ | 250 | 2023-12-15 | 2024-01-12 | uncontrolled |
| 58904 | 2024-022F | Electron | RLABN | NZ | 250 | 2024-01-31 | 2024-02-09 | uncontrolled |
| 58994 | 2024-034C | Electron | RLABN | NZ | 250 | 2024-02-18 | 2024-03-06 | uncontrolled |
| 59226 | 2024-047C | Electron | RLABN | NZ | 250 | 2024-03-12 | 2024-03-21 | uncontrolled |
| 59293 | 2024-053F | Electron | RLABN | NZ | 250 | 2024-03-21 | 2024-06-10 | uncontrolled |
| 59589 | 2024-077C | Electron | RLABN | NZ | 250 | 2024-04-23 | 2024-04-29 | uncontrolled |
| 59882 | 2024-099B | Electron | RLABN | NZ | 250 | 2024-05-25 | 2024-06-10 | uncontrolled |
| 59883 | 2024-099C | Electron | RLABN | NZ | 50 | 2024-05-25 | 2025-06-05 | uncontrolled |
| 59966 | 2024-108B | Electron | RLABN | NZ | 250 | 2024-06-05 | 2024-06-18 | uncontrolled |
| 59967 | 2024-108C | Electron | RLABN | NZ | 50 | 2024-06-05 | 2025-04-08 | uncontrolled |
| 60080 | 2024-114B | Electron | RLABN | NZ | 250 | 2024-06-20 | 2024-07-09 | uncontrolled |
| 60353 | 2024-137B | Electron | RLABN | NZ | 50 | 2024-08-02 | 2025-04-08 | uncontrolled |
| 60354 | 2024-137C | Electron | RLABN | NZ | 250 | 2024-08-02 | 2024-08-14 | uncontrolled |
| 60421 | 2024-142C | Electron | RLABN | NZ | 250 | 2024-08-11 | 2024-08-23 | uncontrolled |
| 61225 | 2024-172F | Electron | RLABN | NZ | 250 | 2024-09-20 | 2024-10-02 | uncontrolled |
| 61792 | 2024-201A | Electron | RLABN | NZ | 50 | 2024-11-05 | 2024-12-03 | uncontrolled |
| 61794 | 2024-201C | Electron | RLABN | NZ | 250 | 2024-11-05 | 2024-11-24 | uncontrolled |
| 62087 | 2024-219G | Electron | RLABN | NZ | 250 | 2024-11-25 | 2024-12-07 | uncontrolled |
| 62408 | 2024-248C | Electron | RLABN | NZ | 250 | 2024-12-21 | 2024-12-29 | uncontrolled |
| 43153 | 2018-007B | Epsilon | ISASJ | J | 185 | 2018-01-17 | 2024-08-22 | uncontrolled |
| 43154 | 2018-007C | Epsilon | ISASJ | J | 400 | 2018-01-17 | 2018-07-17 | uncontrolled |
| 43936 | 2019-003E | Epsilon | ISASJ | J | 185 | 2019-01-18 | 2024-11-12 | uncontrolled |
| 43939 | 2019-003H | Epsilon | ISASJ | J | 400 | 2019-01-18 | 2019-08-07 | uncontrolled |
| 49405 | 2021-102L | Epsilon | ISASJ | J | 400 | 2021-11-09 | 2022-01-20 | uncontrolled |
| 39116 | 2013-010B | Falcon 9 | SPX | US | 4,000 | 2013-03-01 | 2013-03-11 | uncontrolled |
| 39271 | 2013-055G | Falcon 9 | SPX | US | 4,000 | 2013-09-29 | 2025-02-08 | uncontrolled |
| 39461 | 2013-071B | Falcon 9 | SPX | US | 4,000 | 2013-12-03 | 2014-04-30 | uncontrolled |
| 39501 | 2014-002B | Falcon 9 | SPX | US | 4,000 | 2014-01-06 | 2014-05-28 | uncontrolled |
| 40108 | 2014-046B | Falcon 9 | SPX | US | 4,000 | 2014-08-05 | 2025-05-14 | uncontrolled |
| 40142 | 2014-052B | Falcon 9 | SPX | US | 4,000 | 2014-09-07 | 2014-12-28 | uncontrolled |
| 40373 | 2015-001D | Falcon 9 | SPX | US | 4,000 | 2015-01-10 | 2015-01-17 | uncontrolled |
| 40426 | 2015-010C | Falcon 9 | SPX | US | 4,000 | 2015-03-02 | 2023-12-18 | uncontrolled |
| 40589 | 2015-021B | Falcon 9 | SPX | US | 4,000 | 2015-04-14 | 2015-04-22 | uncontrolled |
| 41472 | 2016-028B | Falcon 9 | SPX | US | 4,000 | 2016-05-06 | 2017-09-16 | uncontrolled |
| 41553 | 2016-031B | Falcon 9 | SPX | US | 4,000 | 2016-05-27 | 2019-01-06 | uncontrolled |
| 41730 | 2016-050B | Falcon 9 | SPX | US | 4,000 | 2016-08-14 | 2016-09-26 | uncontrolled |
| 42071 | 2017-014B | Falcon 9 | SPX | US | 4,000 | 2017-03-16 | 2022-02-06 | uncontrolled |
| 42699 | 2017-025B | Falcon 9 | SPX | US | 4,000 | 2017-05-15 | 2022-05-06 | uncontrolled |
| 42802 | 2017-038B | Falcon 9 | SPX | US | 4,000 | 2017-06-23 | 2017-11-02 | uncontrolled |
| 42985 | 2017-067B | Falcon 9 | SPX | US | 4,000 | 2017-10-30 | 2018-10-27 | uncontrolled |
| 43230 | 2018-023C | Falcon 9 | SPX | US | 4,000 | 2018-03-06 | 2020-10-16 | uncontrolled |
| 43489 | 2018-049B | Falcon 9 | SPX | US | 3,000 | 2018-06-04 | 2019-03-23 | uncontrolled |
| 43588 | 2018-064B | Falcon 9 | SPX | US | 4,000 | 2018-08-07 | 2020-12-26 | uncontrolled |
| 43701 | 2018-090B | Falcon 9 | SPX | US | 4,000 | 2018-11-15 | 2019-04-15 | uncontrolled |
| 44050 | 2019-009C | Falcon 9 | SPX | US | 4,000 | 2019-02-22 | 2021-01-03 | uncontrolled |
| 45242 | 2020-012BS | Falcon 9 | SPX | US | 4,000 | 2020-02-17 | 2020-03-05 | uncontrolled |
| 45921 | 2020-048B | Falcon 9 | SPX | US | 4,000 | 2020-07-20 | 2025-05-19 | uncontrolled |
| 46669 | 2020-070BS | Falcon 9 | SPX | US | 4,000 | 2020-10-06 | 2020-10-30 | uncontrolled |
| 46803 | 2020-074BS | Falcon 9 | SPX | US | 4,000 | 2020-10-24 | 2020-11-16 | uncontrolled |
| 47782 | 2021-017BN | Falcon 9 | SPX | US | 4,000 | 2021-03-04 | 2021-03-26 | uncontrolled |
| 49130 | 2021-082A | Falcon 9 | SPX | US | 4,000 | 2021-09-14 | 2021-09-29 | uncontrolled |
| 50213 | 2021-126B | Falcon 9 | SPX | US | 4,000 | 2021-12-19 | 2022-03-08 | uncontrolled |
| 54248 | 2022-153C | Falcon 9 | SPX | US | 4,000 | 2022-11-12 | 2024-03-30 | uncontrolled |
| 55509 | 2023-017B | Falcon 9 | SPX | US | 4,000 | 2023-02-07 | 2024-12-10 | uncontrolled |
| 56758 | 2023-075B | Falcon 9 | SPX | US | 4,000 | 2023-05-27 | 2024-08-25 | uncontrolled |
| 57494 | 2023-112B | Falcon 9 | SPX | US | 4,000 | 2023-08-03 | 2023-09-21 | uncontrolled |
| 59347 | 2024-059B | Falcon 9 | SPX | US | 4,000 | 2024-03-30 | 2026-06-07 | uncontrolled |
| 62029 | 2024-214B | Falcon 9 | SPX | US | 4,000 | 2024-11-18 | 2025-04-14 | uncontrolled |
| 62458 | 2024-252E | Falcon 9 | SPX | US | 4,000 | 2024-12-29 | 2025-05-27 | uncontrolled |
| 44187 | 2019-021B | Falcon Heavy | SPX | US | 4,000 | 2019-04-11 | 2021-06-14 | uncontrolled |
| 53959 | 2022-122E | Firefly Alpha | FFLY | US | 909 | 2022-10-01 | 2022-10-07 | uncontrolled |
| 58617 | 2023-202B | Firefly Alpha | FFLY | US | 909 | 2023-12-22 | 2024-01-19 | uncontrolled |
| 41943 | 2017-006B | Fregat | NPOLO | RU | 1,050 | 2017-01-28 | 2024-06-25 | uncontrolled |
| 39499 | 2014-001B | GSLV | ISRO | IN | 2,500 | 2014-01-05 | 2014-06-08 | uncontrolled |
| 40881 | 2015-041B | GSLV | ISRO | IN | 2,500 | 2015-08-27 | 2018-03-02 | uncontrolled |
| 41753 | 2016-054B | GSLV | ISRO | IN | 2,500 | 2016-09-08 | 2019-04-29 | uncontrolled |
| 42696 | 2017-024B | GSLV | ISRO | IN | 2,500 | 2017-05-05 | 2017-10-10 | uncontrolled |
| 42748 | 2017-031B | GSLV | ISRO | IN | 4,400 | 2017-06-05 | 2018-02-08 | uncontrolled |
| 43242 | 2018-027B | GSLV | ISRO | IN | 2,500 | 2018-03-29 | 2019-12-04 | uncontrolled |
| 43699 | 2018-089B | GSLV | ISRO | IN | 4,400 | 2018-11-14 | 2019-05-12 | uncontrolled |
| 43865 | 2018-105B | GSLV | ISRO | IN | 2,583 | 2018-12-19 | 2019-04-05 | uncontrolled |
| 44442 | 2019-042B | GSLV | ISRO | IN | 4,400 | 2019-07-22 | 2019-10-16 | uncontrolled |
| 57321 | 2023-098B | GSLV | ISRO | IN | 4,400 | 2023-07-14 | 2023-11-15 | uncontrolled |
| 53387 | 2022-095D | Gravity-1 | XIDO | CN | 150 | 2022-08-09 | 2025-02-03 | uncontrolled |
| 57423 | 2023-103C | Gravity-1 | XIDO | CN | 150 | 2023-07-22 | 2024-11-07 | uncontrolled |
| 57796 | 2023-135E | Gravity-1 | XIDO | CN | 150 | 2023-09-05 | 2023-09-25 | uncontrolled |
| 58504 | 2023-189C | Gravity-1 | XIDO | CN | 150 | 2023-12-04 | 2024-09-30 | uncontrolled |
| 60751 | 2024-153G | Gravity-1 | XIDO | CN | 150 | 2024-08-29 | 2024-12-23 | uncontrolled |
| 39063 | 2013-002C | H-IIA/B | MHI | J | 4,000 | 2013-01-27 | 2015-02-04 | uncontrolled |
| 39580 | 2014-009J | H-IIA/B | MHI | J | 4,000 | 2014-02-27 | 2014-06-16 | uncontrolled |
| 40382 | 2015-004B | H-IIA/B | MHI | J | 4,000 | 2015-02-01 | 2022-12-01 | uncontrolled |
| 40539 | 2015-015B | H-IIA/B | MHI | J | 4,000 | 2015-03-26 | 2022-11-02 | uncontrolled |
| 42073 | 2017-015B | H-IIA/B | MHI | J | 4,000 | 2017-03-17 | 2023-12-10 | uncontrolled |
| 43067 | 2017-082C | H-IIA/B | MHI | J | 4,000 | 2017-12-23 | 2025-06-05 | uncontrolled |
| 43224 | 2018-021B | H-IIA/B | MHI | J | 4,000 | 2018-02-27 | 2024-04-27 | uncontrolled |
| 43496 | 2018-052B | H-IIA/B | MHI | J | 4,000 | 2018-06-12 | 2023-12-08 | uncontrolled |
| 45166 | 2020-009B | H-IIA/B | MHI | J | 4,000 | 2020-02-09 | 2024-04-22 | uncontrolled |
| 47203 | 2020-089B | H-IIA/B | MHI | J | 4,000 | 2020-11-29 | 2021-06-12 | uncontrolled |
| 50320 | 2021-128B | H-IIA/B | MHI | J | 4,000 | 2021-12-22 | 2022-02-09 | uncontrolled |
| 55330 | 2023-012B | H-IIA/B | MHI | J | 4,000 | 2023-01-26 | 2024-10-07 | uncontrolled |
| 57804 | 2023-137E | H-IIA/B | MHI | J | 4,000 | 2023-09-06 | 2025-01-03 | uncontrolled |
| 58763 | 2024-010B | H-IIA/B | MHI | J | 4,000 | 2024-01-12 | 2024-12-03 | uncontrolled |
| 61440 | 2024-176B | H-IIA/B | MHI | J | 4,000 | 2024-09-26 | 2026-06-14 | uncontrolled |
| 61734 | 2024-198B | H3 | MHI | J | 2,500 | 2024-11-04 | 2025-03-20 | uncontrolled |
| 58587 | 2023-199B | Hyperbola-1 | XJRY | CN | 200 | 2023-12-16 | 2024-04-07 | uncontrolled |
| 40388 | 2015-006B | Iranian (Simorgh/Safir/Qased/Qaem) | IRSA | IR | 390 | 2015-02-02 | 2015-03-07 | uncontrolled |
| 45530 | 2020-024B | Iranian (Simorgh/Safir/Qased/Qaem) | IRGC | IR | 100 | 2020-04-22 | 2023-03-19 | uncontrolled |
| 51955 | 2022-024B | Iranian (Simorgh/Safir/Qased/Qaem) | IRGC | IR | 100 | 2022-03-08 | 2025-04-28 | uncontrolled |
| 57963 | 2023-150B | Iranian (Simorgh/Safir/Qased/Qaem) | IRGC | IR | 100 | 2023-09-27 | 2024-12-06 | uncontrolled |
| NNA | 2024-236A | Iranian (Simorgh/Safir/Qased/Qaem) | IRSA | IR | 1,500 | 2024-12-06 | 2025-02-25 | uncontrolled |
| 54683 | 2022-167B | Jielong | CZHJ | CN | 500 | 2022-12-09 | 2023-10-06 | uncontrolled |
| 58926 | 2024-024K | Jielong | CZHJ | CN | 500 | 2024-02-03 | 2024-03-17 | uncontrolled |
| 61237 | 2024-173L | Jielong | CZHJ | CN | 500 | 2024-09-24 | 2025-10-18 | uncontrolled |
| 39069 | 2013-003B | KSLV | KARI | KR | 200 | 2013-01-30 | 2023-09-16 | uncontrolled |
| 41916 | 2017-002D | Kuaizhou/KT | EXPACE | CN | 50 | 2017-01-09 | 2017-07-17 | uncontrolled |
| 42062 | 2017-012B | Kuaizhou/KT | CASIC4A | CN | 100 | 2017-03-02 | 2017-04-08 | uncontrolled |
| 43637 | 2018-075B | Kuaizhou/KT | EXPACE | CN | 50 | 2018-09-29 | 2021-08-16 | uncontrolled |
| 44521 | 2019-058C | Kuaizhou/KT | EXPACE | CN | 50 | 2019-08-30 | 2023-08-20 | uncontrolled |
| 44778 | 2019-075B | Kuaizhou/KT | EXPACE | CN | 50 | 2019-11-13 | 2019-11-20 | uncontrolled |
| 44787 | 2019-077C | Kuaizhou/KT | EXPACE | CN | 50 | 2019-11-17 | 2024-12-14 | uncontrolled |
| 44837 | 2019-086B | Kuaizhou/KT | EXPACE | CN | 50 | 2019-12-07 | 2020-03-04 | uncontrolled |
| 44844 | 2019-087G | Kuaizhou/KT | EXPACE | CN | 50 | 2019-12-07 | 2020-12-28 | uncontrolled |
| 45025 | 2020-004B | Kuaizhou/KT | EXPACE | CN | 50 | 2020-01-16 | 2020-01-18 | uncontrolled |
| 45604 | 2020-028C | Kuaizhou/KT | EXPACE | CN | 50 | 2020-05-12 | 2020-07-08 | uncontrolled |
| 49257 | 2021-086B | Kuaizhou/KT | EXPACE | CN | 50 | 2021-09-27 | 2021-10-11 | uncontrolled |
| 49339 | 2021-097B | Kuaizhou/KT | EXPACE | CN | 50 | 2021-10-27 | 2021-10-30 | uncontrolled |
| 49502 | 2021-112B | Kuaizhou/KT | EXPACE | CN | 50 | 2021-11-24 | 2021-12-22 | uncontrolled |
| 52902 | 2022-066B | Kuaizhou/KT | EXPACE | CN | 50 | 2022-06-22 | 2022-06-23 | uncontrolled |
| 53759 | 2022-108C | Kuaizhou/KT | EXPACE | CN | 50 | 2022-09-06 | 2022-11-05 | uncontrolled |
| 53942 | 2022-118C | Kuaizhou/KT | EXPACE | CN | 50 | 2022-09-24 | 2023-11-06 | uncontrolled |
| 54589 | 2022-164B | Kuaizhou/KT | EXPACE | CN | 1,000 | 2022-12-07 | 2025-05-12 | uncontrolled |
| 55977 | 2023-039E | Kuaizhou/KT | EXPACE | CN | 50 | 2023-03-22 | 2023-03-23 | uncontrolled |
| 56875 | 2023-082B | Kuaizhou/KT | EXPACE | CN | 50 | 2023-06-09 | 2023-06-12 | uncontrolled |
| 57403 | 2023-101E | Kuaizhou/KT | EXPACE | CN | 50 | 2023-07-20 | 2023-07-25 | uncontrolled |
| 57631 | 2023-121F | Kuaizhou/KT | EXPACE | CN | 50 | 2023-08-14 | 2023-08-15 | uncontrolled |
| 58649 | 2023-205E | Kuaizhou/KT | EXPACE | CN | 50 | 2023-12-25 | 2024-02-14 | uncontrolled |
| 58664 | 2023-208E | Kuaizhou/KT | EXPACE | CN | 50 | 2023-12-27 | 2024-01-04 | uncontrolled |
| 58704 | 2024-004E | Kuaizhou/KT | EXPACE | CN | 50 | 2024-01-05 | 2024-01-15 | uncontrolled |
| 58757 | 2024-008B | Kuaizhou/KT | EXPACE | CN | 50 | 2024-01-11 | 2024-01-14 | uncontrolled |
| 61199 | 2024-170E | Kuaizhou/KT | EXPACE | CN | 50 | 2024-09-20 | 2025-04-20 | uncontrolled |
| 62191 | 2024-228B | Kuaizhou/KT | EXPACE | CN | 50 | 2024-12-04 | 2024-12-05 | uncontrolled |
| 56082 | 2023-043AN | LVM3 (GSLV Mk III) | NSIL/ISRO | IN | 4,400 | 2023-03-26 | 2024-06-14 | uncontrolled |
| 47316 | 2021-002H | LauncherOne | VORB | US | 200 | 2021-01-17 | 2023-06-07 | uncontrolled |
| 48871 | 2021-058A | LauncherOne | VORB | US | 200 | 2021-06-30 | 2023-08-25 | uncontrolled |
| 51101 | 2022-003H | LauncherOne | VORB | US | 200 | 2022-01-13 | 2023-10-04 | uncontrolled |
| 52946 | 2022-074C | LauncherOne | VORB | US | 200 | 2022-07-02 | 2023-12-07 | uncontrolled |
| 53304 | 2022-087F | Lijian-1/Kinetica | CASC | CN | 500 | 2022-07-27 | 2023-04-18 | uncontrolled |
| 56869 | 2023-081Z | Lijian-1/Kinetica | CASC | CN | 500 | 2023-06-07 | 2023-11-02 | uncontrolled |
| 58824 | 2024-016E | Lijian-1/Kinetica | CASC | CN | 500 | 2024-01-23 | 2024-06-24 | uncontrolled |
| 61263 | 2024-174F | Lijian-1/Kinetica | CASC | CN | 500 | 2024-09-24 | 2024-12-26 | uncontrolled |
| 61909 | 2024-205R | Lijian-1/Kinetica | CASC | CN | 500 | 2024-11-11 | 2025-04-20 | uncontrolled |
| 39248 | 2013-047B | Minotaur | OSCC | US | 140 | 2013-09-07 | 2013-11-27 | uncontrolled |
| 42927 | 2017-050G | Minotaur | OATKC | US | 723 | 2017-08-26 | 2024-02-12 | uncontrolled |
| 42994 | 2017-068H | Minotaur | OATKC | US | 202 | 2017-10-31 | 2025-01-04 | uncontrolled |
| 41172 | 2015-077G | PSLV | ISRO | IN | 920 | 2015-12-16 | 2023-01-16 | uncontrolled |
| 41620 | 2016-040X | PSLV | ISRO | IN | 920 | 2016-06-22 | 2023-05-19 | uncontrolled |
| 42052 | 2017-008DJ | PSLV | ISRO | IN | 920 | 2017-02-15 | 2024-10-06 | uncontrolled |
| 42796 | 2017-036AH | PSLV | ISRO | IN | 920 | 2017-06-23 | 2018-07-24 | uncontrolled |
| 43129 | 2018-004U | PSLV | ISRO | IN | 920 | 2018-01-12 | 2019-01-17 | uncontrolled |
| 43739 | 2018-096W | PSLV | ISRO | IN | 920 | 2018-11-29 | 2023-06-01 | uncontrolled |
| 44234 | 2019-028B | PSLV | ISRO | IN | 920 | 2019-05-22 | 2026-02-25 | uncontrolled |
| 48845 | 2021-051B | Pegasus | NGISC | US | 202 | 2021-06-13 | 2023-11-27 | uncontrolled |
| 49045 | 2021-066B | Proton-M | KHRO | RU | 4,185 | 2021-07-21 | 2021-08-06 | uncontrolled |
| 43202 | 2018-016B | SS-520 | ISASJ | J | 10 | 2018-02-03 | 2018-06-22 | uncontrolled |
| 55565 | 2023-019D | SSLV | ISRO | IN | 400 | 2023-02-10 | 2023-12-21 | uncontrolled |
| 55566 | 2023-019E | SSLV | ISRO | IN | 200 | 2023-02-10 | 2024-05-15 | uncontrolled |
| 60456 | 2024-147C | SSLV | ISRO | IN | 200 | 2024-08-16 | 2025-03-12 | uncontrolled |
| 60457 | 2024-147D | SSLV | ISRO | IN | 400 | 2024-08-16 | 2025-11-26 | uncontrolled |
| 39651 | 2014-019B | Shavit | ISA | IL | 100 | 2014-04-09 | 2014-05-30 | uncontrolled |
| 41760 | 2016-056B | Shavit | ISA | IL | 100 | 2016-09-13 | 2016-10-21 | uncontrolled |
| 45861 | 2020-044B | Shavit | ISA | IL | 100 | 2020-07-06 | 2021-01-27 | uncontrolled |
| 56084 | 2023-044B | Shavit | ISA | IL | 100 | 2023-03-28 | 2023-07-23 | uncontrolled |
| 39083 | 2013-007B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-02-11 | 2013-02-13 | uncontrolled |
| 39126 | 2013-013B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-03-28 | 2013-03-31 | uncontrolled |
| 39137 | 2013-015H | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2013-04-19 | 2013-08-03 | uncontrolled |
| 39149 | 2013-017B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-04-24 | 2013-04-26 | uncontrolled |
| 39171 | 2013-025B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-05-28 | 2013-05-31 | uncontrolled |
| 39178 | 2013-028B | Soyuz (Blok-I) | VVKO | RU | 2,710 | 2013-06-07 | 2013-07-28 | uncontrolled |
| 39187 | 2013-030B | Soyuz (Blok-I) | VVKO | RU | 2,710 | 2013-06-25 | 2013-09-25 | uncontrolled |
| 39220 | 2013-039B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-07-27 | 2013-07-30 | uncontrolled |
| 39264 | 2013-054B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-09-25 | 2013-09-28 | uncontrolled |
| 39374 | 2013-061B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-11-07 | 2013-11-09 | uncontrolled |
| 39457 | 2013-069B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2013-11-25 | 2013-11-28 | uncontrolled |
| 39493 | 2013-078D | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2013-12-28 | 2014-05-08 | uncontrolled |
| 39507 | 2014-005B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-02-05 | 2014-02-07 | uncontrolled |
| 39623 | 2014-013B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-03-25 | 2014-03-28 | uncontrolled |
| 39649 | 2014-018B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-04-09 | 2014-04-11 | uncontrolled |
| 39733 | 2014-025B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2014-05-06 | 2014-05-10 | uncontrolled |
| 39776 | 2014-031B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-05-28 | 2014-05-31 | uncontrolled |
| 40077 | 2014-037J | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2014-07-08 | 2014-07-10 | uncontrolled |
| 40096 | 2014-041B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2014-07-18 | 2014-10-31 | uncontrolled |
| 40098 | 2014-042B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-07-23 | 2014-07-25 | uncontrolled |
| 40247 | 2014-057B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-09-25 | 2014-09-28 | uncontrolled |
| 40293 | 2014-067B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2014-10-29 | 2014-10-30 | uncontrolled |
| 40313 | 2014-074B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-11-23 | 2014-11-26 | uncontrolled |
| 40359 | 2014-086B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2014-12-25 | 2015-08-01 | uncontrolled |
| 40361 | 2014-087B | Soyuz (Blok-I) | VVKO | RU | 2,710 | 2014-12-26 | 2015-01-09 | uncontrolled |
| 40393 | 2015-008B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-02-17 | 2015-02-19 | uncontrolled |
| 40421 | 2015-009B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2015-02-27 | 2016-03-02 | uncontrolled |
| 40543 | 2015-016B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-03-27 | 2015-03-29 | uncontrolled |
| 40620 | 2015-024B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2015-04-28 | 2015-04-29 | uncontrolled |
| 40668 | 2015-027B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2015-06-05 | 2015-06-09 | uncontrolled |
| 40700 | 2015-029B | Soyuz (Blok-I) | VVKOV | RU | 2,710 | 2015-06-23 | 2015-08-17 | uncontrolled |
| 40714 | 2015-031B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-07-03 | 2015-07-05 | uncontrolled |
| 40745 | 2015-035B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-07-22 | 2015-07-25 | uncontrolled |
| 40886 | 2015-043B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-09-02 | 2015-09-05 | uncontrolled |
| 40945 | 2015-055B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-10-01 | 2015-10-03 | uncontrolled |
| 41100 | 2015-071C | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2015-12-05 | 2016-03-16 | uncontrolled |
| 41125 | 2015-076B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2015-12-15 | 2015-12-17 | uncontrolled |
| 41178 | 2015-080B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2015-12-21 | 2015-12-23 | uncontrolled |
| 41387 | 2016-016B | Soyuz (Blok-I) | VVKOV | RU | 2,710 | 2016-03-13 | 2016-09-24 | uncontrolled |
| 41392 | 2016-018B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2016-03-18 | 2016-03-21 | uncontrolled |
| 41395 | 2016-020B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2016-03-24 | 2018-09-06 | uncontrolled |
| 41437 | 2016-022B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2016-03-31 | 2016-04-03 | uncontrolled |
| 41467 | 2016-026D | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2016-04-28 | 2016-04-30 | uncontrolled |
| 41640 | 2016-044B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2016-07-07 | 2016-07-10 | uncontrolled |
| 41671 | 2016-045B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2016-07-16 | 2016-07-19 | uncontrolled |
| 41821 | 2016-063B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2016-10-19 | 2016-10-23 | uncontrolled |
| 41865 | 2016-070B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2016-11-17 | 2016-11-21 | uncontrolled |
| 42057 | 2017-010B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2017-02-22 | 2017-02-24 | uncontrolled |
| 42683 | 2017-020B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2017-04-20 | 2017-04-23 | uncontrolled |
| 42757 | 2017-033B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2017-06-14 | 2017-06-17 | uncontrolled |
| 42800 | 2017-037C | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2017-06-23 | 2020-04-20 | uncontrolled |
| 42899 | 2017-043B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2017-07-28 | 2017-08-01 | uncontrolled |
| 42938 | 2017-054B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2017-09-12 | 2017-09-16 | uncontrolled |
| 42972 | 2017-065B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2017-10-14 | 2017-10-16 | uncontrolled |
| 43033 | 2017-076B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2017-12-02 | 2019-05-15 | uncontrolled |
| 43064 | 2017-081B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2017-12-17 | 2017-12-20 | uncontrolled |
| 43212 | 2018-019B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2018-02-13 | 2018-02-16 | uncontrolled |
| 43239 | 2018-026B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2018-03-21 | 2018-03-25 | uncontrolled |
| 43244 | 2018-028B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2018-03-29 | 2018-11-04 | uncontrolled |
| 43494 | 2018-051B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2018-06-06 | 2018-06-11 | uncontrolled |
| 43538 | 2018-058B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2018-07-09 | 2018-07-12 | uncontrolled |
| 43658 | 2018-082B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2018-10-25 | 2020-08-04 | uncontrolled |
| 43703 | 2018-091B | Soyuz (Blok-I) | ROSK | RU | 2,350 | 2018-11-16 | 2019-06-04 | uncontrolled |
| 43757 | 2018-098B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2018-12-03 | 2018-12-07 | uncontrolled |
| 44070 | 2019-013B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2019-03-14 | 2019-03-17 | uncontrolled |
| 44111 | 2019-019B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2019-04-04 | 2019-04-07 | uncontrolled |
| 44438 | 2019-041B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2019-07-20 | 2019-07-24 | uncontrolled |
| 44456 | 2019-047B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2019-07-31 | 2019-08-04 | uncontrolled |
| 44505 | 2019-055B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2019-08-22 | 2019-08-26 | uncontrolled |
| 44551 | 2019-064B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2019-09-25 | 2019-09-28 | uncontrolled |
| 44799 | 2019-079C | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2019-11-25 | 2020-07-18 | uncontrolled |
| 44834 | 2019-085B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2019-12-06 | 2019-12-10 | uncontrolled |
| 45477 | 2020-023B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2020-04-09 | 2020-04-12 | uncontrolled |
| 45596 | 2020-026B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2020-04-25 | 2020-04-28 | uncontrolled |
| 45938 | 2020-050B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2020-07-23 | 2020-07-27 | uncontrolled |
| 46614 | 2020-072B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2020-10-14 | 2020-10-18 | uncontrolled |
| 47547 | 2021-008B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-02-02 | 2022-03-03 | uncontrolled |
| 47619 | 2021-011B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-02-15 | 2021-02-17 | uncontrolled |
| 48160 | 2021-029B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-04-09 | 2021-04-13 | uncontrolled |
| 48866 | 2021-056B | Soyuz (Blok-I) | VVKOV | RU | 2,350 | 2021-06-25 | 2021-07-26 | uncontrolled |
| 48870 | 2021-057B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-06-29 | 2021-07-02 | uncontrolled |
| 49128 | 2021-081B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-09-09 | 2021-12-11 | uncontrolled |
| 49270 | 2021-089B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-10-05 | 2021-10-08 | uncontrolled |
| 49380 | 2021-098B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-10-28 | 2021-10-30 | uncontrolled |
| 49500 | 2021-111B | Soyuz (Blok-I) | ROSK | RU | 2,350 | 2021-11-24 | 2021-11-26 | uncontrolled |
| 49923 | 2021-119B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2021-12-08 | 2021-12-11 | uncontrolled |
| 51661 | 2022-014B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-02-15 | 2022-02-17 | uncontrolled |
| 52087 | 2022-028B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-03-18 | 2022-03-21 | uncontrolled |
| 52203 | 2022-036B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-04-07 | 2022-11-30 | uncontrolled |
| 52714 | 2022-054B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-05-19 | 2023-06-06 | uncontrolled |
| 52796 | 2022-059B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-06-03 | 2022-06-05 | uncontrolled |
| 53324 | 2022-089B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-08-01 | 2022-11-19 | uncontrolled |
| 53880 | 2022-116B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-09-21 | 2022-09-24 | uncontrolled |
| 54111 | 2022-137C | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-10-21 | 2022-11-03 | uncontrolled |
| 54156 | 2022-140B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-10-26 | 2022-10-28 | uncontrolled |
| 54382 | 2022-163B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2022-11-30 | 2023-05-22 | uncontrolled |
| 55561 | 2023-018B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-02-09 | 2023-02-11 | uncontrolled |
| 55689 | 2023-024B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-02-24 | 2023-02-26 | uncontrolled |
| 55979 | 2023-040B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-03-23 | 2023-11-22 | uncontrolled |
| 56092 | 2023-045B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-03-29 | 2023-07-03 | uncontrolled |
| 56741 | 2023-071B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-05-24 | 2023-05-26 | uncontrolled |
| 57692 | 2023-125B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-08-23 | 2023-08-25 | uncontrolled |
| 57863 | 2023-143B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-09-15 | 2023-09-18 | uncontrolled |
| 58149 | 2023-165B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-10-27 | 2024-04-12 | uncontrolled |
| 58436 | 2023-182B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-11-25 | 2024-03-02 | uncontrolled |
| 58461 | 2023-184B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-12-01 | 2023-12-03 | uncontrolled |
| 58615 | 2023-201B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-12-21 | 2024-07-14 | uncontrolled |
| 58659 | 2023-209B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2023-12-27 | 2024-05-03 | uncontrolled |
| 58930 | 2024-026B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-02-09 | 2024-06-10 | uncontrolled |
| 58962 | 2024-029B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-02-15 | 2024-02-17 | uncontrolled |
| 59295 | 2024-055B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-03-23 | 2024-03-25 | uncontrolled |
| 59372 | 2024-061B | Soyuz (Blok-I) | VVKOV | RU | 2,710 | 2024-03-31 | 2024-07-03 | uncontrolled |
| 59914 | 2024-103B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-05-30 | 2024-06-01 | uncontrolled |
| 60451 | 2024-145B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-08-15 | 2024-08-17 | uncontrolled |
| 61044 | 2024-162B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-09-11 | 2024-09-13 | uncontrolled |
| 61731 | 2024-197B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-10-31 | 2025-04-16 | uncontrolled |
| 62031 | 2024-215B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-11-21 | 2024-11-23 | uncontrolled |
| 62217 | 2024-230B | Soyuz (Blok-I) | RVSNR | RU | 2,350 | 2024-12-04 | 2025-05-07 | uncontrolled |
| 62431 | 2024-250B | Soyuz (Blok-I) | VVKOV | RU | 2,710 | 2024-12-25 | 2025-03-19 | uncontrolled |
| 39195 | 2013-032B | Strela | NPOMA | RU | 725 | 2013-06-27 | 2025-10-21 | uncontrolled |
| 40354 | 2014-084B | Strela | NPOMAO | RU | 725 | 2014-12-19 | 2024-10-12 | uncontrolled |
| 41044 | 2015-070B | Vega | AE | F | 660 | 2015-12-03 | 2017-03-16 | uncontrolled |
| 41102 | 2015-071D | Volga | RVSNR | RU | 900 | 2015-12-05 | 2015-12-08 | uncontrolled |
| 44425 | 2019-039E | Volga | RVSNR | RU | 1,120 | 2019-07-10 | 2025-07-14 | uncontrolled |
| 49386 | 2021-099D | Yuanzheng (YZ kick stage) | CASC | CN | 2,500 | 2021-11-03 | 2021-12-19 | uncontrolled |
| 52719 | 2022-056D | Yuanzheng (YZ kick stage) | CASC | CN | 2,500 | 2022-05-20 | 2022-05-21 | uncontrolled |
| 57318 | 2023-095C | Yuanzheng (YZ kick stage) | CASC | CN | 2,500 | 2023-07-09 | 2023-07-22 | uncontrolled |
| 58350 | 2023-176B | Yuanzheng (YZ kick stage) | CASC | CN | 2,500 | 2023-11-16 | 2023-11-21 | uncontrolled |
| 41107 | 2015-074C | Zenit | VVKOV | RU | 9,300 | 2015-12-11 | 2016-01-01 | uncontrolled |
| 43090 | 2017-086D | Zenit | VVKOV | RU | 8,300 | 2017-12-26 | 2018-01-27 | uncontrolled |
| 58556 | 2023-193D | Zhuque | LANDSP | CN | 5,000 | 2023-12-08 | 2025-02-02 | uncontrolled |
| 62113 | 2024-221C | Zhuque | LANDSP | CN | 5,000 | 2024-11-27 | 2024-12-24 | uncontrolled |

#### Controlled — 58 bodies

| NORAD | COSPAR (Piece) | Vehicle family | Operator (Owner) | Launch state | Dry mass kg (GCAT DryMass) | Launch date | Reentry date / status | Label |
|---|---|---|---|---|---:|---|---|---|
| 39176 | 2013-027B | Ariane 5 | AE | F | 3,057 | 2013-06-05 | 2013-06-06 | controlled |
| 43654 | 2018-080B | Ariane 5 | AESP | F | 5,000 | 2018-10-20 | 2018-10-20 | controlled |
| 50464 | 2021-130B | Ariane 5 | AESP | F | 5,000 | 2021-12-25 | 2021-12-26 | controlled |
| 56177 | 2023-053B | Ariane 5 | AESP | F | 5,000 | 2023-04-14 | 2023-04-14 | controlled |
| 44433 | 2019-040B | Blok DM (Proton/Zenit) | VVKOV | RU | 2,440 | 2019-07-13 | 2019-07-14 | controlled |
| 41389 | 2016-017B | Briz-M | KHRO | RU | 1,600 | 2016-03-14 | 2016-03-15 | controlled |
| 39459 | 2013-070B | CZ-3B | CASC | CN | 2,800 | 2013-12-01 | 2013-12-02 | controlled |
| 43846 | 2018-103B | CZ-3B | CASC | CN | 2,800 | 2018-12-07 | 2018-12-08 | controlled |
| 40284 | 2014-065B | CZ-3C | CASC | CN | 2,800 | 2014-10-23 | 2014-10-24 | controlled |
| 43473 | 2018-045D | CZ-4C | CNSA | CN | 1,000 | 2018-05-20 | 2018-05-21 | controlled |
| 45936 | 2020-049B | CZ-5 | CNSA | CN | 5,100 | 2020-07-23 | 2020-07-23 | controlled |
| 47098 | 2020-087B | CZ-5 | CNSA | CN | 5,100 | 2020-11-23 | 2020-11-25 | controlled |
| 59628 | 2024-083B | CZ-5 | CNSA | CN | 5,100 | 2024-05-03 | 2024-05-04 | controlled |
| 59277 | 2024-051B | CZ-8 | CASC | CN | 2,800 | 2024-03-20 | 2024-03-20 | controlled |
| 39085 | 2013-008B | Centaur | ULAL | US | 2,020 | 2013-02-11 | 2013-02-12 | controlled |
| 39379 | 2013-063B | Centaur | ULAL | US | 2,020 | 2013-11-18 | 2013-11-19 | controlled |
| 39631 | 2014-015B | Centaur | ULAL | US | 2,020 | 2014-04-03 | 2014-04-03 | controlled |
| 40116 | 2014-048B | Centaur | ULAL | US | 2,020 | 2014-08-13 | 2014-08-14 | controlled |
| 41758 | 2016-055B | Centaur | ULAL | US | 2,020 | 2016-09-08 | 2016-09-09 | controlled |
| 41856 | 2016-067J | Centaur | ULAL | US | 2,020 | 2016-11-11 | 2016-11-12 | controlled |
| 43460 | 2018-042D | Centaur | ULAL | US | 2,020 | 2018-05-05 | 2018-05-05 | controlled |
| 45168 | 2020-010B | Centaur | ULAL | US | 2,020 | 2020-02-10 | 2020-02-10 | controlled |
| 45984 | 2020-052B | Centaur | LMSSD | US | 2,020 | 2020-07-30 | 2020-07-30 | controlled |
| 49329 | 2021-093B | Centaur | ULAL | US | 2,020 | 2021-10-16 | 2021-10-16 | controlled |
| 58015 | 2023-154C | Centaur | ULAL | US | 2,020 | 2023-10-06 | 2023-10-07 | controlled |
| 58752 | 2024-006B | Centaur | ULAL | US | 5,500 | 2024-01-08 | 2024-01-08 | controlled |
| 40330 | 2014-077B | Delta | ULAB | US | 3,450 | 2014-12-05 | 2014-12-05 | controlled |
| 41880 | 2016-075B | Delta | ULAB | US | 3,450 | 2016-12-07 | 2016-12-08 | controlled |
| 42076 | 2017-016B | Delta | ULAB | US | 3,450 | 2017-03-19 | 2017-03-19 | controlled |
| 43593 | 2018-065B | Delta | ULAB | US | 3,450 | 2018-08-12 | 2018-08-12 | controlled |
| 43594 | 2018-065C | Delta | GSFC | US | 140 | 2018-08-12 | 2018-08-12 | controlled |
| 40391 | 2015-007B | Falcon 9 | SPX | US | 4,000 | 2015-02-11 | 2015-02-12 | controlled |
| 42690 | 2017-022B | Falcon 9 | SPX | US | 4,000 | 2017-05-01 | 2017-05-01 | controlled |
| 42933 | 2017-052B | Falcon 9 | SPX | US | 4,000 | 2017-09-07 | 2017-09-07 | controlled |
| 43218 | 2018-020D | Falcon 9 | SPX | US | 4,000 | 2018-02-22 | 2018-02-22 | controlled |
| 43436 | 2018-038B | Falcon 9 | SPX | US | 4,000 | 2018-04-18 | 2018-04-19 | controlled |
| 46985 | 2020-086B | Falcon 9 | SPX | US | 4,000 | 2020-11-21 | 2020-11-22 | controlled |
| 49498 | 2021-110B | Falcon 9 | SPX | US | 4,000 | 2021-11-24 | 2021-11-24 | controlled |
| 53366 | 2022-094B | Falcon 9 | SPX | US | 4,000 | 2022-08-04 | 2022-08-05 | controlled |
| 54698 | 2022-168C | Falcon 9 | SPX | US | 4,000 | 2022-12-11 | 2022-12-11 | controlled |
| 57210 | 2023-092B | Falcon 9 | SPX | US | 4,000 | 2023-07-01 | 2023-07-02 | controlled |
| 58964 | 2024-030B | Falcon 9 | SPX | US | 4,000 | 2024-02-15 | 2024-02-15 | controlled |
| 61732 | 2024-180B | Falcon 9 | SPX | US | 4,000 | 2024-10-07 | 2024-10-07 | controlled |
| 58050 | 2023-157B | Falcon Heavy | SPX | US | 4,000 | 2023-10-13 | 2023-10-13 | controlled |
| 61508 | 2024-182B | Falcon Heavy | SPX | US | 4,000 | 2024-10-14 | 2024-10-14 | controlled |
| 39480 | 2013-074B | Fregat | NPOL | RU | 1,050 | 2013-12-19 | 2013-12-19 | controlled |
| 57601 | 2023-118B | Fregat | NPOLO | RU | 1,000 | 2023-08-10 | 2023-08-11 | controlled |
| 40323 | 2014-076E | H-IIA/B | MHI | J | 4,000 | 2014-12-03 | 2014-12-03 | controlled |
| 45919 | 2020-047B | H-IIA/B | MHI | J | 4,000 | 2020-07-19 | 2020-07-20 | controlled |
| 54258 | 2022-156B | SLS (ICPS) | MSFC | US | 3,830 | 2022-11-16 | 2022-11-16 | controlled |
| 41876 | 2016-073B | Vega | AE | F | 660 | 2016-12-05 | 2016-12-05 | controlled |
| 42064 | 2017-013B | Vega | AESP | F | 660 | 2017-03-07 | 2017-03-07 | controlled |
| 41468 | 2016-026E | Volga | RVSNR | RU | 1,120 | 2016-04-28 | 2016-04-28 | controlled |
| 42799 | 2017-037B | Volga | RVSNR | RU | 1,120 | 2017-06-23 | 2017-06-24 | controlled |
| 44798 | 2019-079B | Volga | RVSNR | RU | 1,120 | 2019-11-25 | 2019-11-26 | controlled |
| 54112 | 2022-137D | Volga | RVSNR | RU | 1,120 | 2022-10-21 | 2022-10-22 | controlled |
| 41929 | 2015-019C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2015-03-30 | 2015-04-01 | controlled |
| 41624 | 2016-042A | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2016-06-25 | 2016-06-27 | controlled |

#### Still-in-orbit — 456 bodies

| NORAD | COSPAR (Piece) | Vehicle family | Operator (Owner) | Launch state | Dry mass kg (GCAT DryMass) | Launch date | Reentry date / status | Label |
|---|---|---|---|---|---:|---|---|---|
| 58501 | 2023-188B | ADD test vehicle (KR) | ADD | KR | 100 | 2023-12-04 | still in orbit | still-in-orbit |
| 39080 | 2013-006C | Ariane 5 | AE | F | 5,000 | 2013-02-07 | still in orbit | still-in-orbit |
| 39235 | 2013-044C | Ariane 5 | AE | F | 5,000 | 2013-08-29 | still in orbit | still-in-orbit |
| 39510 | 2014-006C | Ariane 5 | AE | F | 5,000 | 2014-02-06 | still in orbit | still-in-orbit |
| 39618 | 2014-011C | Ariane 5 | AE | F | 5,000 | 2014-03-22 | still in orbit | still-in-orbit |
| 40148 | 2014-054C | Ariane 5 | AE | F | 5,000 | 2014-09-11 | still in orbit | still-in-orbit |
| 40273 | 2014-062C | Ariane 5 | AE | F | 5,000 | 2014-10-16 | still in orbit | still-in-orbit |
| 40334 | 2014-078C | Ariane 5 | AE | F | 5,000 | 2014-12-06 | still in orbit | still-in-orbit |
| 40615 | 2015-022C | Ariane 5 | AE | F | 5,000 | 2015-04-26 | still in orbit | still-in-orbit |
| 40665 | 2015-026C | Ariane 5 | AE | F | 5,000 | 2015-05-27 | still in orbit | still-in-orbit |
| 40734 | 2015-034C | Ariane 5 | AE | F | 5,000 | 2015-07-15 | still in orbit | still-in-orbit |
| 40876 | 2015-039C | Ariane 5 | AE | F | 5,000 | 2015-08-20 | still in orbit | still-in-orbit |
| 40942 | 2015-054C | Ariane 5 | AE | F | 5,000 | 2015-09-30 | still in orbit | still-in-orbit |
| 41030 | 2015-065C | Ariane 5 | AE | F | 5,000 | 2015-11-10 | still in orbit | still-in-orbit |
| 41309 | 2016-004B | Ariane 5 | AE | F | 5,000 | 2016-01-27 | still in orbit | still-in-orbit |
| 41383 | 2016-014B | Ariane 5 | AE | F | 5,000 | 2016-03-09 | still in orbit | still-in-orbit |
| 41593 | 2016-039C | Ariane 5 | AE | F | 5,000 | 2016-06-18 | still in orbit | still-in-orbit |
| 41749 | 2016-053C | Ariane 5 | AE | F | 5,000 | 2016-08-24 | still in orbit | still-in-orbit |
| 41795 | 2016-060C | Ariane 5 | AE | F | 5,000 | 2016-10-05 | still in orbit | still-in-orbit |
| 41863 | 2016-069E | Ariane 5 | AE | F | 3,057 | 2016-11-17 | still in orbit | still-in-orbit |
| 41905 | 2016-082C | Ariane 5 | AE | F | 5,000 | 2016-12-21 | still in orbit | still-in-orbit |
| 41946 | 2017-007C | Ariane 5 | AE | F | 5,000 | 2017-02-14 | still in orbit | still-in-orbit |
| 42693 | 2017-023C | Ariane 5 | AESP | F | 5,000 | 2017-05-04 | still in orbit | still-in-orbit |
| 42742 | 2017-029C | Ariane 5 | AESP | F | 5,000 | 2017-06-01 | still in orbit | still-in-orbit |
| 42816 | 2017-040C | Ariane 5 | AESP | F | 5,000 | 2017-06-28 | still in orbit | still-in-orbit |
| 42952 | 2017-059C | Ariane 5 | AESP | F | 5,000 | 2017-09-29 | still in orbit | still-in-orbit |
| 43059 | 2017-079E | Ariane 5 | AESP | F | 3,300 | 2017-12-12 | still in orbit | still-in-orbit |
| 43176 | 2018-012C | Ariane 5 | AESP | F | 5,000 | 2018-01-25 | still in orbit | still-in-orbit |
| 43273 | 2018-033C | Ariane 5 | AESP | F | 5,000 | 2018-04-05 | still in orbit | still-in-orbit |
| 43568 | 2018-060E | Ariane 5 | AESP | F | 3,300 | 2018-07-25 | still in orbit | still-in-orbit |
| 43634 | 2018-074C | Ariane 5 | AESP | F | 5,000 | 2018-09-25 | still in orbit | still-in-orbit |
| 43825 | 2018-100C | Ariane 5 | AESP | F | 5,000 | 2018-12-04 | still in orbit | still-in-orbit |
| 44335 | 2019-034C | Ariane 5 | AESP | F | 5,000 | 2019-06-20 | still in orbit | still-in-orbit |
| 44477 | 2019-049C | Ariane 5 | AESP | F | 5,000 | 2019-08-06 | still in orbit | still-in-orbit |
| 44802 | 2019-080C | Ariane 5 | AESP | F | 5,000 | 2019-11-26 | still in orbit | still-in-orbit |
| 45029 | 2020-005D | Ariane 5 | AESP | F | 5,000 | 2020-01-16 | still in orbit | still-in-orbit |
| 45248 | 2020-013D | Ariane 5 | AESP | F | 5,000 | 2020-02-18 | still in orbit | still-in-orbit |
| 46116 | 2020-056E | Ariane 5 | AESP | F | 5,000 | 2020-08-15 | still in orbit | still-in-orbit |
| 49058 | 2021-069D | Ariane 5 | AESP | F | 5,000 | 2021-07-30 | still in orbit | still-in-orbit |
| 49335 | 2021-095D | Ariane 5 | AESP | F | 5,000 | 2021-10-24 | still in orbit | still-in-orbit |
| 52906 | 2022-067D | Ariane 5 | AESP | F | 5,000 | 2022-06-22 | still in orbit | still-in-orbit |
| 53766 | 2022-110B | Ariane 5 | AESP | F | 5,000 | 2022-09-07 | still in orbit | still-in-orbit |
| 54745 | 2022-170E | Ariane 5 | AESP | F | 5,000 | 2022-12-13 | still in orbit | still-in-orbit |
| 57216 | 2023-093D | Ariane 5 | AESP | F | 5,000 | 2023-07-05 | still in orbit | still-in-orbit |
| 39238 | 2013-045B | Blok DM (Proton/Zenit) | SIS | RU | 2,540 | 2013-08-31 | still in orbit | still-in-orbit |
| 39774 | 2014-030B | Blok DM (Proton/Zenit) | ELUS | US | 3,070 | 2014-05-26 | still in orbit | still-in-orbit |
| 40896 | 2015-048B | Blok DM (Proton/Zenit) | VVKOV | RU | 2,440 | 2015-09-14 | still in orbit | still-in-orbit |
| 44904 | 2019-095B | Blok DM (Proton/Zenit) | VVKOV | RU | 2,440 | 2019-12-24 | still in orbit | still-in-orbit |
| 54034 | 2022-131B | Blok DM (Proton/Zenit) | VVKOV | RU | 2,440 | 2022-10-12 | still in orbit | still-in-orbit |
| 55507 | 2023-016B | Blok DM (Proton/Zenit) | VVKOV | RU | 2,440 | 2023-02-05 | still in orbit | still-in-orbit |
| 39060 | 2013-001D | Briz-KM | VVKO | RU | 2,370 | 2013-01-15 | still in orbit | still-in-orbit |
| 39252 | 2013-048D | Briz-KM | VVKO | RU | 2,370 | 2013-09-11 | still in orbit | still-in-orbit |
| 39486 | 2013-076D | Briz-KM | VVKO | RU | 2,370 | 2013-12-25 | still in orbit | still-in-orbit |
| 39764 | 2014-028D | Briz-KM | VVKO | RU | 2,370 | 2014-05-23 | still in orbit | still-in-orbit |
| 40064 | 2014-036D | Briz-KM | VVKO | RU | 2,370 | 2014-07-03 | still in orbit | still-in-orbit |
| 40556 | 2015-020E | Briz-KM | VVKOV | RU | 2,370 | 2015-03-31 | still in orbit | still-in-orbit |
| 40923 | 2015-050D | Briz-KM | VVKOV | RU | 2,370 | 2015-09-23 | still in orbit | still-in-orbit |
| 41336 | 2016-011B | Briz-KM | EUROK | RU | 2,370 | 2016-02-16 | still in orbit | still-in-orbit |
| 41580 | 2016-034B | Briz-KM | VVKOV | RU | 2,370 | 2016-06-04 | still in orbit | still-in-orbit |
| 42970 | 2017-064B | Briz-KM | EUROK | RU | 2,370 | 2017-10-13 | still in orbit | still-in-orbit |
| 43438 | 2018-039B | Briz-KM | EUROK | RU | 2,370 | 2018-04-25 | still in orbit | still-in-orbit |
| 43754 | 2018-097D | Briz-KM | VVKOV | RU | 2,370 | 2018-11-30 | still in orbit | still-in-orbit |
| 44518 | 2019-057B | Briz-KM | VVKOV | RU | 2,370 | 2019-08-30 | still in orbit | still-in-orbit |
| 39123 | 2013-012B | Briz-M | KHRR | RU | 1,600 | 2013-03-26 | still in orbit | still-in-orbit |
| 39128 | 2013-014B | Briz-M | KHRR | RU | 1,600 | 2013-04-15 | still in orbit | still-in-orbit |
| 39164 | 2013-022B | Briz-M | KHRR | RU | 1,600 | 2013-05-14 | still in orbit | still-in-orbit |
| 39173 | 2013-026B | Briz-M | KHRR | RU | 1,600 | 2013-06-03 | still in orbit | still-in-orbit |
| 39286 | 2013-056B | Briz-M | KHRR | RU | 1,600 | 2013-09-29 | still in orbit | still-in-orbit |
| 39361 | 2013-058B | Briz-M | KHRR | RU | 1,600 | 2013-10-25 | still in orbit | still-in-orbit |
| 39376 | 2013-062B | Briz-M | KHRR | RU | 1,600 | 2013-11-11 | still in orbit | still-in-orbit |
| 39494 | 2013-073C | Briz-M | KHRR | RU | 1,600 | 2013-12-08 | still in orbit | still-in-orbit |
| 39488 | 2013-077B | Briz-M | KHRR | RU | 1,600 | 2013-12-26 | still in orbit | still-in-orbit |
| 39523 | 2014-007B | Briz-M | KHRR | RU | 1,600 | 2014-02-14 | still in orbit | still-in-orbit |
| 39614 | 2014-010C | Briz-M | KHRO | RU | 1,600 | 2014-03-15 | still in orbit | still-in-orbit |
| 39729 | 2014-023C | Briz-M | KHRO | RU | 1,600 | 2014-04-28 | still in orbit | still-in-orbit |
| 40259 | 2014-058B | Briz-M | KHRO | RU | 1,600 | 2014-09-27 | still in orbit | still-in-orbit |
| 40278 | 2014-064B | Briz-M | KHRO | RU | 1,600 | 2014-10-21 | still in orbit | still-in-orbit |
| 40346 | 2014-082B | Briz-M | KHRO | RU | 1,600 | 2014-12-15 | still in orbit | still-in-orbit |
| 40365 | 2014-089B | Briz-M | KHRO | RU | 1,600 | 2014-12-27 | still in orbit | still-in-orbit |
| 40385 | 2015-005B | Briz-M | KHRO | RU | 1,600 | 2015-02-01 | still in orbit | still-in-orbit |
| 40506 | 2015-012B | Briz-M | KHRO | RU | 1,600 | 2015-03-18 | still in orbit | still-in-orbit |
| 40883 | 2015-042B | Briz-M | KHRO | RU | 1,600 | 2015-08-28 | still in orbit | still-in-orbit |
| 40985 | 2015-060B | Briz-M | KHRO | RU | 1,600 | 2015-10-16 | still in orbit | still-in-orbit |
| 41122 | 2015-075B | Briz-M | KHRO | RU | 1,600 | 2015-12-13 | still in orbit | still-in-orbit |
| 41192 | 2015-082B | Briz-M | KHRO | RU | 1,600 | 2015-12-24 | still in orbit | still-in-orbit |
| 41311 | 2016-005B | Briz-M | KHRO | RU | 1,600 | 2016-01-29 | still in orbit | still-in-orbit |
| 41582 | 2016-035B | Briz-M | KHRO | RU | 1,600 | 2016-06-09 | still in orbit | still-in-orbit |
| 42750 | 2017-032B | Briz-M | KHRO | RU | 1,600 | 2017-06-08 | still in orbit | still-in-orbit |
| 42909 | 2017-046C | Briz-M | KHRO | RU | 1,600 | 2017-08-16 | still in orbit | still-in-orbit |
| 42935 | 2017-053B | Briz-M | KHRO | RU | 1,600 | 2017-09-11 | still in orbit | still-in-orbit |
| 42943 | 2017-057B | Briz-M | KHRO | RU | 1,600 | 2017-09-28 | still in orbit | still-in-orbit |
| 43433 | 2018-037B | Briz-M | KHRO | RU | 1,600 | 2018-04-18 | still in orbit | still-in-orbit |
| 43868 | 2018-107B | Briz-M | KHRO | RU | 1,600 | 2018-12-21 | still in orbit | still-in-orbit |
| 44308 | 2019-031B | Briz-M | KHRO | RU | 1,600 | 2019-05-30 | still in orbit | still-in-orbit |
| 44458 | 2019-048B | Briz-M | KHRO | RU | 1,600 | 2019-08-05 | still in orbit | still-in-orbit |
| 44626 | 2019-067C | Briz-M | KHRO | RU | 1,600 | 2019-10-09 | still in orbit | still-in-orbit |
| 45987 | 2020-053C | Briz-M | KHRO | RU | 1,600 | 2020-07-30 | still in orbit | still-in-orbit |
| 50003 | 2021-123C | Briz-M | KHRO | RU | 1,600 | 2021-12-13 | still in orbit | still-in-orbit |
| 55842 | 2023-031B | Briz-M | KHRO | RU | 1,600 | 2023-03-12 | still in orbit | still-in-orbit |
| 43161 | 2018-008G | CZ-11 | CASC | CN | 500 | 2018-01-19 | still in orbit | still-in-orbit |
| 43872 | 2018-108B | CZ-11 | CASC | CN | 500 | 2018-12-21 | still in orbit | still-in-orbit |
| 62187 | 2024-226C | CZ-12 | CNSA | CN | 6,000 | 2024-11-30 | still in orbit | still-in-orbit |
| 39203 | 2013-035B | CZ-2C | CASC | CN | 3,800 | 2013-07-15 | still in orbit | still-in-orbit |
| 39625 | 2014-014B | CZ-2C | CASC | CN | 3,800 | 2014-03-31 | still in orbit | still-in-orbit |
| 40262 | 2014-059B | CZ-2C | CASC | CN | 3,800 | 2014-09-28 | still in orbit | still-in-orbit |
| 40287 | 2014-066B | CZ-2C | CASC | CN | 3,800 | 2014-10-27 | still in orbit | still-in-orbit |
| 42948 | 2017-058D | CZ-2C | CASC | CN | 3,800 | 2017-09-29 | still in orbit | still-in-orbit |
| 43084 | 2017-085D | CZ-2C | CASC | CN | 3,800 | 2017-12-25 | still in orbit | still-in-orbit |
| 43610 | 2018-068B | CZ-2C | CASC | CN | 3,800 | 2018-09-07 | still in orbit | still-in-orbit |
| 45722 | 2020-036B | CZ-2C | CASC | CN | 3,800 | 2020-06-10 | still in orbit | still-in-orbit |
| 48427 | 2021-039E | CZ-2C | CASC | CN | 3,800 | 2021-05-06 | still in orbit | still-in-orbit |
| 48862 | 2021-055C | CZ-2C | CASC | CN | 3,800 | 2021-06-18 | still in orbit | still-in-orbit |
| 51953 | 2022-023H | CZ-2C | CASC | CN | 3,800 | 2022-03-05 | still in orbit | still-in-orbit |
| 52794 | 2022-058K | CZ-2C | CASC | CN | 3,800 | 2022-06-02 | still in orbit | still-in-orbit |
| 54039 | 2022-132E | CZ-2C | CASC | CN | 3,800 | 2022-10-12 | still in orbit | still-in-orbit |
| 55846 | 2023-032C | CZ-2C | CASC | CN | 3,800 | 2023-03-13 | still in orbit | still-in-orbit |
| 58499 | 2023-187D | CZ-2C | CASC | CN | 3,800 | 2023-12-04 | still in orbit | still-in-orbit |
| 58754 | 2024-007B | CZ-2C | CASC | CN | 3,800 | 2024-01-09 | still in orbit | still-in-orbit |
| 58916 | 2024-023M | CZ-2C | CASC | CN | 3,800 | 2024-02-02 | still in orbit | still-in-orbit |
| 61873 | 2024-203E | CZ-2C | CASC | CN | 4,006 | 2024-11-09 | still in orbit | still-in-orbit |
| 62078 | 2024-218A | CZ-2C | CASC | CN | 3,800 | 2024-11-24 | still in orbit | still-in-orbit |
| 39154 | 2013-018E | CZ-2D | CASC | CN | 4,006 | 2013-04-26 | still in orbit | still-in-orbit |
| 41858 | 2016-068B | CZ-2D | CNSA | CN | 4,006 | 2016-11-11 | still in orbit | still-in-orbit |
| 44548 | 2019-063B | CZ-2D | CNSA | CN | 4,006 | 2019-09-25 | still in orbit | still-in-orbit |
| 51103 | 2022-004B | CZ-2D | CASC | CN | 4,006 | 2022-01-17 | still in orbit | still-in-orbit |
| 53878 | 2022-115B | CZ-2D | CNSA | CN | 4,006 | 2022-09-20 | still in orbit | still-in-orbit |
| 54030 | 2022-129B | CZ-2D | CASC | CN | 4,006 | 2022-10-08 | still in orbit | still-in-orbit |
| 54215 | 2022-142B | CZ-2D | CASC | CN | 4,006 | 2022-10-29 | still in orbit | still-in-orbit |
| 54641 | 2022-165B | CZ-2D | CNSA | CN | 4,006 | 2022-12-08 | still in orbit | still-in-orbit |
| 58074 | 2023-159B | CZ-2D | CNSA | CN | 4,006 | 2023-10-15 | still in orbit | still-in-orbit |
| 59396 | 2024-063B | CZ-2D | CASC | CN | 4,006 | 2024-04-02 | still in orbit | still-in-orbit |
| 40368 | 2014-090B | CZ-3A | CASC | CN | 2,800 | 2014-12-31 | still in orbit | still-in-orbit |
| 41435 | 2016-021B | CZ-3A | CASC | CN | 2,800 | 2016-03-29 | still in orbit | still-in-orbit |
| 43492 | 2018-050B | CZ-3A | CASC | CN | 2,800 | 2018-06-05 | still in orbit | still-in-orbit |
| 39158 | 2013-020B | CZ-3B | CASC | CN | 2,800 | 2013-05-01 | still in orbit | still-in-orbit |
| 41022 | 2015-063B | CZ-3B | CASC | CN | 2,800 | 2015-11-03 | still in orbit | still-in-orbit |
| 42663 | 2017-018B | CZ-3B | CASC | CN | 2,800 | 2017-04-12 | still in orbit | still-in-orbit |
| 43110 | 2018-003D | CZ-3B | CASC | CN | 2,800 | 2018-01-11 | still in orbit | still-in-orbit |
| 43247 | 2018-029C | CZ-3B | CASC | CN | 2,800 | 2018-03-29 | still in orbit | still-in-orbit |
| 43649 | 2018-078C | CZ-3B | CASC | CN | 2,800 | 2018-10-15 | still in orbit | still-in-orbit |
| 44077 | 2019-017B | CZ-3B | CASC | CN | 2,800 | 2019-03-31 | still in orbit | still-in-orbit |
| 44205 | 2019-023B | CZ-3B | CASC | CN | 2,800 | 2019-04-20 | still in orbit | still-in-orbit |
| 44796 | 2019-078D | CZ-3B | CASC | CN | 2,800 | 2019-11-23 | still in orbit | still-in-orbit |
| 45808 | 2020-040B | CZ-3B | CASC | CN | 2,800 | 2020-06-23 | still in orbit | still-in-orbit |
| 45864 | 2020-045B | CZ-3B | CASC | CN | 2,800 | 2020-07-09 | still in orbit | still-in-orbit |
| 49331 | 2021-094B | CZ-3B | CASC | CN | 2,800 | 2021-10-24 | still in orbit | still-in-orbit |
| 52256 | 2022-038B | CZ-3B | CASC | CN | 2,800 | 2022-04-15 | still in orbit | still-in-orbit |
| 55687 | 2023-023B | CZ-3B | CASC | CN | 2,800 | 2023-02-23 | still in orbit | still-in-orbit |
| 55913 | 2023-036B | CZ-3B | CASC | CN | 2,800 | 2023-03-17 | still in orbit | still-in-orbit |
| 56565 | 2023-066B | CZ-3B | CASC | CN | 2,800 | 2023-05-17 | still in orbit | still-in-orbit |
| 58657 | 2023-207D | CZ-3B | CASC | CN | 2,800 | 2023-12-26 | still in orbit | still-in-orbit |
| 59070 | 2024-040B | CZ-3B | CASC | CN | 2,800 | 2024-02-29 | still in orbit | still-in-orbit |
| 59707 | 2024-087C | CZ-3B | CASC | CN | 2,800 | 2024-05-09 | still in orbit | still-in-orbit |
| 59916 | 2024-104B | CZ-3B | CASC | CN | 2,800 | 2024-05-30 | still in orbit | still-in-orbit |
| 61504 | 2024-181B | CZ-3B | CASC | CN | 2,800 | 2024-10-10 | still in orbit | still-in-orbit |
| 62375 | 2024-246B | CZ-3B | CASC | CN | 2,800 | 2024-12-20 | still in orbit | still-in-orbit |
| 41587 | 2016-037B | CZ-3C | CASC | CN | 2,800 | 2016-06-12 | still in orbit | still-in-orbit |
| 41870 | 2016-072B | CZ-3C | CASC | CN | 2,800 | 2016-11-22 | still in orbit | still-in-orbit |
| 43875 | 2018-110B | CZ-3C | CASC | CN | 2,800 | 2018-12-24 | still in orbit | still-in-orbit |
| 44232 | 2019-027B | CZ-3C | CASC | CN | 2,800 | 2019-05-17 | still in orbit | still-in-orbit |
| 40337 | 2014-079B | CZ-4B | CNSA | CN | 1,000 | 2014-12-07 | still in orbit | still-in-orbit |
| 44531 | 2019-059D | CZ-4B | CNSA | CN | 1,000 | 2019-09-12 | still in orbit | still-in-orbit |
| 46470 | 2020-066B | CZ-4B | CNSA | CN | 1,000 | 2020-09-21 | still in orbit | still-in-orbit |
| 48158 | 2021-028B | CZ-4B | CNSA | CN | 1,000 | 2021-04-08 | still in orbit | still-in-orbit |
| 48624 | 2021-043D | CZ-4B | CNSA | CN | 1,000 | 2021-05-19 | still in orbit | still-in-orbit |
| 61938 | 2024-208C | CZ-4B | CNSA | CN | 1,000 | 2024-11-13 | still in orbit | still-in-orbit |
| 39211 | 2013-037D | CZ-4C | CNSA | CN | 1,000 | 2013-07-19 | still in orbit | still-in-orbit |
| 39242 | 2013-046D | CZ-4C | CNSA | CN | 1,000 | 2013-09-01 | still in orbit | still-in-orbit |
| 39261 | 2013-052B | CZ-4C | CNSA | CN | 1,000 | 2013-09-23 | still in orbit | still-in-orbit |
| 39411 | 2013-065B | CZ-4C | CNSA | CN | 1,000 | 2013-11-20 | still in orbit | still-in-orbit |
| 40112 | 2014-047D | CZ-4C | CNSA | CN | 1,000 | 2014-08-09 | still in orbit | still-in-orbit |
| 40276 | 2014-063B | CZ-4C | CNSA | CN | 1,000 | 2014-10-20 | still in orbit | still-in-orbit |
| 40341 | 2014-080D | CZ-4C | CNSA | CN | 1,000 | 2014-12-10 | still in orbit | still-in-orbit |
| 40879 | 2015-040B | CZ-4C | CNSA | CN | 1,000 | 2015-08-27 | still in orbit | still-in-orbit |
| 41039 | 2015-069B | CZ-4C | CNSA | CN | 1,000 | 2015-11-26 | still in orbit | still-in-orbit |
| 41728 | 2016-049B | CZ-4C | CNSA | CN | 1,000 | 2016-08-09 | still in orbit | still-in-orbit |
| 43264 | 2018-031F | CZ-4C | CNSA | CN | 1,000 | 2018-03-31 | still in orbit | still-in-orbit |
| 43278 | 2018-034D | CZ-4C | CNSA | CN | 1,000 | 2018-04-10 | still in orbit | still-in-orbit |
| 43462 | 2018-043B | CZ-4C | CNSA | CN | 1,000 | 2018-05-08 | still in orbit | still-in-orbit |
| 47304 | 2020-103C | CZ-4C | CNSA | CN | 1,000 | 2020-12-27 | still in orbit | still-in-orbit |
| 47537 | 2021-007F | CZ-4C | CNSA | CN | 1,000 | 2021-01-29 | still in orbit | still-in-orbit |
| 47696 | 2021-014F | CZ-4C | CNSA | CN | 1,000 | 2021-02-24 | still in orbit | still-in-orbit |
| 47858 | 2021-020E | CZ-4C | CNSA | CN | 1,000 | 2021-03-13 | still in orbit | still-in-orbit |
| 48080 | 2021-026B | CZ-4C | CNSA | CN | 1,000 | 2021-03-30 | still in orbit | still-in-orbit |
| 48341 | 2021-037B | CZ-4C | CNSA | CN | 1,000 | 2021-04-30 | still in orbit | still-in-orbit |
| 49010 | 2021-062C | CZ-4C | CNSA | CN | 1,000 | 2021-07-04 | still in orbit | still-in-orbit |
| 49123 | 2021-079B | CZ-4C | CNSA | CN | 1,000 | 2021-09-07 | still in orbit | still-in-orbit |
| 49496 | 2021-109B | CZ-4C | CNSA | CN | 1,000 | 2021-11-22 | still in orbit | still-in-orbit |
| 50467 | 2021-131C | CZ-4C | CNSA | CN | 1,000 | 2021-12-26 | still in orbit | still-in-orbit |
| 52201 | 2022-035B | CZ-4C | CNSA | CN | 1,000 | 2022-04-06 | still in orbit | still-in-orbit |
| 52258 | 2022-039B | CZ-4C | CNSA | CN | 1,000 | 2022-04-15 | still in orbit | still-in-orbit |
| 52913 | 2022-069B | CZ-4C | CNSA | CN | 1,000 | 2022-06-27 | still in orbit | still-in-orbit |
| 53699 | 2022-106B | CZ-4C | CNSA | CN | 1,000 | 2022-09-02 | still in orbit | still-in-orbit |
| 54250 | 2022-154B | CZ-4C | CNSA | CN | 1,000 | 2022-11-15 | still in orbit | still-in-orbit |
| 54701 | 2022-169C | CZ-4C | CNSA | CN | 1,000 | 2022-12-12 | still in orbit | still-in-orbit |
| 55838 | 2023-030C | CZ-4C | CNSA | CN | 1,000 | 2023-03-09 | still in orbit | still-in-orbit |
| 56158 | 2023-048B | CZ-4C | CNSA | CN | 1,000 | 2023-03-31 | still in orbit | still-in-orbit |
| 57491 | 2023-111B | CZ-4C | CNSA | CN | 1,000 | 2023-08-03 | still in orbit | still-in-orbit |
| 57655 | 2023-123B | CZ-4C | CNSA | CN | 1,000 | 2023-08-20 | still in orbit | still-in-orbit |
| 57798 | 2023-136B | CZ-4C | CNSA | CN | 1,000 | 2023-09-06 | still in orbit | still-in-orbit |
| 57959 | 2023-149B | CZ-4C | CNSA | CN | 1,000 | 2023-09-26 | still in orbit | still-in-orbit |
| 59729 | 2024-089B | CZ-4C | CNSA | CN | 1,000 | 2024-05-11 | still in orbit | still-in-orbit |
| 61572 | 2024-186B | CZ-4C | CNSA | CN | 1,000 | 2024-10-15 | still in orbit | still-in-orbit |
| 58583 | 2023-197B | CZ-5 | CNSA | CN | 5,100 | 2023-12-15 | still in orbit | still-in-orbit |
| 59021 | 2024-037B | CZ-5 | CNSA | CN | 5,100 | 2024-02-23 | still in orbit | still-in-orbit |
| 44784 | 2019-076F | CZ-6 | CNSA | CN | 1,000 | 2019-11-13 | still in orbit | still-in-orbit |
| 49023 | 2021-064F | CZ-6 | CNSA | CN | 1,000 | 2021-07-09 | still in orbit | still-in-orbit |
| 49061 | 2021-070C | CZ-6 | CNSA | CN | 1,000 | 2021-08-04 | still in orbit | still-in-orbit |
| 52152 | 2022-031C | CZ-6A | CNSA | CN | 6,000 | 2022-03-29 | still in orbit | still-in-orbit |
| 54236 | 2022-151B | CZ-6A | CNSA | CN | 6,000 | 2022-11-11 | still in orbit | still-in-orbit |
| 57831 | 2023-139B | CZ-6A | CNSA | CN | 6,000 | 2023-09-10 | still in orbit | still-in-orbit |
| 58200 | 2023-168B | CZ-6A | CNSA | CN | 6,000 | 2023-10-31 | still in orbit | still-in-orbit |
| 59344 | 2024-058B | CZ-6A | CNSA | CN | 6,000 | 2024-03-26 | still in orbit | still-in-orbit |
| 60214 | 2024-126D | CZ-6A | CNSA | CN | 6,000 | 2024-07-04 | still in orbit | still-in-orbit |
| 60397 | 2024-140U | CZ-6A | CNSA | CN | 6,000 | 2024-08-06 | still in orbit | still-in-orbit |
| 61570 | 2024-185U | CZ-6A | CNSA | CN | 6,000 | 2024-10-15 | still in orbit | still-in-orbit |
| 62237 | 2024-232A | CZ-6A | CNSA | CN | 6,000 | 2024-12-05 | still in orbit | still-in-orbit |
| 55132 | 2023-002B | CZ-7A | CASC | CN | 2,800 | 2023-01-08 | still in orbit | still-in-orbit |
| 39071 | 2013-004B | Centaur | ULAL | US | 2,020 | 2013-01-31 | still in orbit | still-in-orbit |
| 39167 | 2013-023B | Centaur | ULAL | US | 2,020 | 2013-05-15 | still in orbit | still-in-orbit |
| 39207 | 2013-036B | Centaur | LMSSD | US | 2,020 | 2013-07-19 | still in orbit | still-in-orbit |
| 39505 | 2014-004B | Centaur | ULAL | US | 2,020 | 2014-01-24 | still in orbit | still-in-orbit |
| 39653 | 2014-020B | Centaur | ULAL | US | 2,020 | 2014-04-10 | still in orbit | still-in-orbit |
| 40106 | 2014-045B | Centaur | ULAL | US | 2,020 | 2014-08-02 | still in orbit | still-in-orbit |
| 40209 | 2014-055B | Centaur | ULAL | US | 2,020 | 2014-09-17 | still in orbit | still-in-orbit |
| 40295 | 2014-068B | Centaur | ULAL | US | 2,020 | 2014-10-29 | still in orbit | still-in-orbit |
| 40375 | 2015-002B | Centaur | LMSSD | US | 2,020 | 2015-01-21 | still in orbit | still-in-orbit |
| 40731 | 2015-033B | Centaur | ULAL | US | 2,020 | 2015-07-15 | still in orbit | still-in-orbit |
| 40888 | 2015-044B | Centaur | LMSSD | US | 2,020 | 2015-09-02 | still in orbit | still-in-orbit |
| 40947 | 2015-056B | Centaur | ULAL | US | 2,020 | 2015-10-02 | still in orbit | still-in-orbit |
| 41020 | 2015-062B | Centaur | ULAL | US | 2,020 | 2015-10-31 | still in orbit | still-in-orbit |
| 41329 | 2016-007B | Centaur | ULAL | US | 2,020 | 2016-02-05 | still in orbit | still-in-orbit |
| 41623 | 2016-041B | Centaur | LMSSD | US | 2,020 | 2016-06-24 | still in orbit | still-in-orbit |
| 41867 | 2016-071B | Centaur | ULAL | US | 2,020 | 2016-11-19 | still in orbit | still-in-orbit |
| 42916 | 2017-047B | Centaur | ULAL | US | 2,020 | 2017-08-18 | still in orbit | still-in-orbit |
| 43227 | 2018-022B | Centaur | ULAL | US | 2,020 | 2018-03-01 | still in orbit | still-in-orbit |
| 43341 | 2018-036C | Centaur | LMSSD | US | 2,020 | 2018-04-14 | still in orbit | still-in-orbit |
| 43652 | 2018-079B | Centaur | ULAL | US | 2,020 | 2018-10-17 | still in orbit | still-in-orbit |
| 44483 | 2019-051C | Centaur | ULAL | US | 2,020 | 2019-08-08 | still in orbit | still-in-orbit |
| 45466 | 2020-022C | Centaur | ULAL | US | 2,020 | 2020-03-26 | still in orbit | still-in-orbit |
| 46919 | 2020-083B | Centaur | ULAL | US | 2,020 | 2020-11-13 | still in orbit | still-in-orbit |
| 49819 | 2021-118C | Centaur | ULAL | US | 2,020 | 2021-12-07 | still in orbit | still-in-orbit |
| 51282 | 2022-006C | Centaur | LMSSD | US | 2,020 | 2022-01-21 | still in orbit | still-in-orbit |
| 51851 | 2022-021B | Centaur | LMSSD | US | 2,020 | 2022-03-01 | still in orbit | still-in-orbit |
| 52942 | 2022-073C | Centaur | ULAD | US | 2,020 | 2022-07-01 | still in orbit | still-in-orbit |
| 53356 | 2022-092B | Centaur | ULAL | US | 2,020 | 2022-08-04 | still in orbit | still-in-orbit |
| 53962 | 2022-123C | Centaur | ULAL | US | 2,020 | 2022-10-04 | still in orbit | still-in-orbit |
| 57839 | 2023-140D | Centaur | ULAL | US | 2,020 | 2023-09-10 | still in orbit | still-in-orbit |
| 60325 | 2024-134D | Centaur | ULAL | US | 2,020 | 2024-07-30 | still in orbit | still-in-orbit |
| 58401 | 2023-179B | DPRK (Unha/Chollima) | KP | KP | 50 | 2023-11-21 | still in orbit | still-in-orbit |
| 39169 | 2013-024B | Delta | ULAB | US | 3,450 | 2013-05-25 | still in orbit | still-in-orbit |
| 39534 | 2014-008B | Delta | ULAB | US | 2,850 | 2014-02-21 | still in orbit | still-in-orbit |
| 39742 | 2014-026B | Delta | ULAB | US | 2,850 | 2014-05-17 | still in orbit | still-in-orbit |
| 40060 | 2014-035B | Delta | BOHB | US | 924 | 2014-07-02 | still in orbit | still-in-orbit |
| 40102 | 2014-043D | Delta | ULAB | US | 2,850 | 2014-07-28 | still in orbit | still-in-orbit |
| 40535 | 2015-013B | Delta | ULAB | US | 2,850 | 2015-03-25 | still in orbit | still-in-orbit |
| 41585 | 2016-036B | Delta | ULAB | US | 3,450 | 2016-06-11 | still in orbit | still-in-orbit |
| 41746 | 2016-052C | Delta | ULAB | US | 2,850 | 2016-08-19 | still in orbit | still-in-orbit |
| 47238 | 2020-095B | Delta | ULAB | US | 3,450 | 2020-12-11 | still in orbit | still-in-orbit |
| 57100 | 2023-089B | Delta | ULAB | US | 3,450 | 2023-06-22 | still in orbit | still-in-orbit |
| 59454 | 2024-067B | Delta | ULAB | US | 3,450 | 2024-04-09 | still in orbit | still-in-orbit |
| 39228 | 2013-042B | Dnepr | KTRAS | RU | 1,000 | 2013-08-22 | still in orbit | still-in-orbit |
| 39448 | 2013-066AJ | Dnepr | KTRAS | RU | 1,000 | 2013-11-21 | still in orbit | still-in-orbit |
| 40047 | 2014-033AP | Dnepr | KTRAS | RU | 1,000 | 2014-06-19 | still in orbit | still-in-orbit |
| 40303 | 2014-070F | Dnepr | KTRAS | RU | 1,000 | 2014-11-06 | still in orbit | still-in-orbit |
| 40541 | 2015-014C | Dnepr | KTRAS | RU | 1,000 | 2015-03-25 | still in orbit | still-in-orbit |
| 44636 | 2019-069C | Electron | RLABN | NZ | 40 | 2019-10-17 | still in orbit | still-in-orbit |
| 45728 | 2020-037F | Electron | RLABN | NZ | 50 | 2020-06-13 | still in orbit | still-in-orbit |
| 47347 | 2021-004B | Electron | RLABN | NZ | 40 | 2021-01-20 | still in orbit | still-in-orbit |
| 53104 | 2022-079C | Electron | RLABN | NZ | 40 | 2022-07-13 | still in orbit | still-in-orbit |
| 53354 | 2022-091C | Electron | RLABN | NZ | 40 | 2022-08-04 | still in orbit | still-in-orbit |
| 53817 | 2022-113C | Electron | RLABN | NZ | 40 | 2022-09-15 | still in orbit | still-in-orbit |
| 54024 | 2022-127B | Electron | RLABN | NZ | 40 | 2022-10-07 | still in orbit | still-in-orbit |
| 54228 | 2022-147B | Electron | RLABN | NZ | 40 | 2022-11-04 | still in orbit | still-in-orbit |
| 55908 | 2023-035A | Electron | RLABN | NZ | 40 | 2023-03-16 | still in orbit | still-in-orbit |
| 57393 | 2023-100H | Electron | RLABN | NZ | 40 | 2023-07-18 | still in orbit | still-in-orbit |
| 57694 | 2023-126B | Electron | RLABN | NZ | 40 | 2023-08-23 | still in orbit | still-in-orbit |
| 58579 | 2023-196B | Electron | RLABN | NZ | 42 | 2023-12-15 | still in orbit | still-in-orbit |
| 58901 | 2024-022C | Electron | RLABN | NZ | 43 | 2024-01-31 | still in orbit | still-in-orbit |
| 58993 | 2024-034B | Electron | RLABN | NZ | 43 | 2024-02-18 | still in orbit | still-in-orbit |
| 59225 | 2024-047B | Electron | RLABN | NZ | 40 | 2024-03-12 | still in orbit | still-in-orbit |
| 59292 | 2024-053E | Electron | RLABN | NZ | 40 | 2024-03-21 | still in orbit | still-in-orbit |
| 59590 | 2024-077D | Electron | RLABN | NZ | 50 | 2024-04-23 | still in orbit | still-in-orbit |
| 60085 | 2024-114G | Electron | RLABN | NZ | 50 | 2024-06-20 | still in orbit | still-in-orbit |
| 60420 | 2024-142B | Electron | RLABN | NZ | 50 | 2024-08-11 | still in orbit | still-in-orbit |
| 61226 | 2024-172G | Electron | RLABN | NZ | 50 | 2024-09-20 | still in orbit | still-in-orbit |
| 62086 | 2024-219F | Electron | RLABN | NZ | 50 | 2024-11-25 | still in orbit | still-in-orbit |
| 62407 | 2024-248B | Electron | RLABN | NZ | 50 | 2024-12-21 | still in orbit | still-in-orbit |
| 39254 | 2013-049B | Epsilon | ISASJ | J | 185 | 2013-09-14 | still in orbit | still-in-orbit |
| 39255 | 2013-049C | Epsilon | ISASJ | J | 800 | 2013-09-14 | still in orbit | still-in-orbit |
| 41897 | 2016-080B | Epsilon | ISASJ | J | 400 | 2016-12-20 | still in orbit | still-in-orbit |
| 49404 | 2021-102K | Epsilon | ISASJ | J | 185 | 2021-11-09 | still in orbit | still-in-orbit |
| 40618 | 2015-023B | Falcon 9 | SPX | US | 4,000 | 2015-04-27 | still in orbit | still-in-orbit |
| 41381 | 2016-013B | Falcon 9 | SPX | US | 4,000 | 2016-03-04 | still in orbit | still-in-orbit |
| 41590 | 2016-038C | Falcon 9 | SPX | US | 4,000 | 2016-06-15 | still in orbit | still-in-orbit |
| 42433 | 2017-017B | Falcon 9 | SPX | US | 4,000 | 2017-03-30 | still in orbit | still-in-orbit |
| 42819 | 2017-041B | Falcon 9 | SPX | US | 4,000 | 2017-07-05 | still in orbit | still-in-orbit |
| 42968 | 2017-063B | Falcon 9 | SPX | US | 4,000 | 2017-10-11 | still in orbit | still-in-orbit |
| 43179 | 2018-013B | Falcon 9 | SPX | US | 4,000 | 2018-01-31 | still in orbit | still-in-orbit |
| 43464 | 2018-044B | Falcon 9 | SPX | US | 4,000 | 2018-05-11 | still in orbit | still-in-orbit |
| 43563 | 2018-059B | Falcon 9 | SPX | US | 4,000 | 2018-07-22 | still in orbit | still-in-orbit |
| 43612 | 2018-069B | Falcon 9 | SPX | US | 4,000 | 2018-09-10 | still in orbit | still-in-orbit |
| 44480 | 2019-050B | Falcon 9 | SPX | US | 4,000 | 2019-08-06 | still in orbit | still-in-orbit |
| 44869 | 2019-091B | Falcon 9 | SPX | US | 4,000 | 2019-12-17 | still in orbit | still-in-orbit |
| 47241 | 2020-096B | Falcon 9 | SPX | US | 4,000 | 2020-12-13 | still in orbit | still-in-orbit |
| 47307 | 2021-001B | Falcon 9 | SPX | US | 4,000 | 2021-01-08 | still in orbit | still-in-orbit |
| 48839 | 2021-049B | Falcon 9 | SPX | US | 4,000 | 2021-06-06 | still in orbit | still-in-orbit |
| 52818 | 2022-061B | Falcon 9 | SPX | US | 4,000 | 2022-06-08 | still in orbit | still-in-orbit |
| 52934 | 2022-071B | Falcon 9 | SPX | US | 4,000 | 2022-06-29 | still in orbit | still-in-orbit |
| 54028 | 2022-128C | Falcon 9 | SPX | US | 4,000 | 2022-10-08 | still in orbit | still-in-orbit |
| 54049 | 2022-134B | Falcon 9 | SPX | US | 4,000 | 2022-10-15 | still in orbit | still-in-orbit |
| 54226 | 2022-146B | Falcon 9 | SPX | US | 4,000 | 2022-11-03 | still in orbit | still-in-orbit |
| 54260 | 2022-157B | Falcon 9 | SPX | US | 4,000 | 2022-11-23 | still in orbit | still-in-orbit |
| 54757 | 2022-174C | Falcon 9 | SPX | US | 4,000 | 2022-12-16 | still in orbit | still-in-orbit |
| 55684 | 2023-022B | Falcon 9 | SPX | US | 4,000 | 2023-02-18 | still in orbit | still-in-orbit |
| 55972 | 2023-038C | Falcon 9 | SPX | US | 4,000 | 2023-03-17 | still in orbit | still-in-orbit |
| 56175 | 2023-052B | Falcon 9 | SPX | US | 4,000 | 2023-04-07 | still in orbit | still-in-orbit |
| 56369 | 2023-059C | Falcon 9 | SPX | US | 4,000 | 2023-04-28 | still in orbit | still-in-orbit |
| 57046 | 2023-086B | Falcon 9 | SPX | US | 4,000 | 2023-06-18 | still in orbit | still-in-orbit |
| 58348 | 2023-175C | Falcon 9 | SPX | US | 4,000 | 2023-11-12 | still in orbit | still-in-orbit |
| 58699 | 2024-003B | Falcon 9 | SPX | US | 4,000 | 2024-01-03 | still in orbit | still-in-orbit |
| 58996 | 2024-035B | Falcon 9 | SPX | US | 4,000 | 2024-02-20 | still in orbit | still-in-orbit |
| 59599 | 2024-079B | Falcon 9 | SPX | US | 4,000 | 2024-04-28 | still in orbit | still-in-orbit |
| 60087 | 2024-115B | Falcon 9 | SPX | US | 4,000 | 2024-06-20 | still in orbit | still-in-orbit |
| 60234 | 2024-127B | Falcon 9 | SPX | US | 4,000 | 2024-07-08 | still in orbit | still-in-orbit |
| 60424 | 2024-143C | Falcon 9 | SPX | US | 4,000 | 2024-08-12 | still in orbit | still-in-orbit |
| 61184 | 2024-167C | Falcon 9 | SPX | US | 4,000 | 2024-09-17 | still in orbit | still-in-orbit |
| 61911 | 2024-206B | Falcon 9 | SPX | US | 4,000 | 2024-11-11 | still in orbit | still-in-orbit |
| 62007 | 2024-212B | Falcon 9 | SPX | US | 4,000 | 2024-11-17 | still in orbit | still-in-orbit |
| 62260 | 2024-234B | Falcon 9 | SPX | US | 4,000 | 2024-12-05 | still in orbit | still-in-orbit |
| 62364 | 2024-244C | Falcon 9 | SPX | US | 4,000 | 2024-12-17 | still in orbit | still-in-orbit |
| 44345 | 2019-036G | Falcon Heavy | SPX | US | 4,000 | 2019-06-25 | still in orbit | still-in-orbit |
| 54221 | 2022-144C | Falcon Heavy | SPX | US | 4,000 | 2022-11-01 | still in orbit | still-in-orbit |
| 55265 | 2023-008C | Falcon Heavy | SPX | US | 4,000 | 2023-01-15 | still in orbit | still-in-orbit |
| 56373 | 2023-060D | Falcon Heavy | SPX | US | 4,000 | 2023-05-01 | still in orbit | still-in-orbit |
| 57480 | 2023-108B | Falcon Heavy | SPX | US | 4,000 | 2023-07-29 | still in orbit | still-in-orbit |
| 60134 | 2024-119B | Falcon Heavy | SPX | US | 4,000 | 2024-06-25 | still in orbit | still-in-orbit |
| 60210 | 2024-125H | Firefly Alpha | FFLY | US | 909 | 2024-07-04 | still in orbit | still-in-orbit |
| 39156 | 2013-019B | Fregat | NPOL | RU | 1,000 | 2013-04-26 | still in orbit | still-in-orbit |
| 39192 | 2013-031E | Fregat | NPOL | RU | 1,050 | 2013-06-25 | still in orbit | still-in-orbit |
| 39621 | 2014-012B | Fregat | NPOLO | RU | 1,000 | 2014-03-23 | still in orbit | still-in-orbit |
| 40002 | 2014-032B | Fregat | NPOLO | RU | 1,000 | 2014-06-14 | still in orbit | still-in-orbit |
| 40083 | 2014-038E | Fregat | NPOLO | RU | 1,050 | 2014-07-10 | still in orbit | still-in-orbit |
| 40130 | 2014-050C | Fregat | NPOLO | RU | 1,050 | 2014-08-22 | still in orbit | still-in-orbit |
| 40297 | 2014-069B | Fregat | NPOLO | RU | 1,000 | 2014-10-30 | still in orbit | still-in-orbit |
| 40316 | 2014-075B | Fregat | NPOLO | RU | 1,000 | 2014-11-30 | still in orbit | still-in-orbit |
| 40352 | 2014-083E | Fregat | NPOLO | RU | 1,050 | 2014-12-18 | still in orbit | still-in-orbit |
| 40546 | 2015-017C | Fregat | NPOLO | RU | 1,050 | 2015-03-27 | still in orbit | still-in-orbit |
| 40891 | 2015-045C | Fregat | NPOLO | RU | 1,050 | 2015-09-11 | still in orbit | still-in-orbit |
| 41033 | 2015-066B | Fregat | NPOLO | RU | 1,000 | 2015-11-17 | still in orbit | still-in-orbit |
| 41106 | 2015-074B | Fregat | NPOLO | RU | 1,000 | 2015-12-11 | still in orbit | still-in-orbit |
| 41176 | 2015-079C | Fregat | NPOLO | RU | 1,050 | 2015-12-17 | still in orbit | still-in-orbit |
| 41331 | 2016-008B | Fregat | NPOLO | RU | 1,000 | 2016-02-07 | still in orbit | still-in-orbit |
| 41551 | 2016-030C | Fregat | NPOLO | RU | 1,050 | 2016-05-24 | still in orbit | still-in-orbit |
| 41555 | 2016-032B | Fregat | NPOLO | RU | 1,000 | 2016-05-29 | still in orbit | still-in-orbit |
| 42710 | 2017-026B | Fregat | NPOLO | RU | 1,000 | 2017-05-18 | still in orbit | still-in-orbit |
| 42720 | 2017-027B | Fregat | NPOLO | RU | 1,000 | 2017-05-25 | still in orbit | still-in-orbit |
| 42940 | 2017-055B | Fregat | NPOLO | RU | 1,000 | 2017-09-22 | still in orbit | still-in-orbit |
| 43088 | 2017-086B | Fregat | NPOLO | RU | 1,000 | 2017-12-26 | still in orbit | still-in-orbit |
| 43235 | 2018-024E | Fregat | NPOLO | RU | 1,050 | 2018-03-09 | still in orbit | still-in-orbit |
| 43509 | 2018-053B | Fregat | NPOLO | RU | 1,000 | 2018-06-16 | still in orbit | still-in-orbit |
| 43688 | 2018-086B | Fregat | NPOLO | RU | 1,000 | 2018-11-03 | still in orbit | still-in-orbit |
| 44116 | 2019-020E | Fregat | NPOLO | RU | 1,050 | 2019-04-04 | still in orbit | still-in-orbit |
| 44300 | 2019-030B | Fregat | NPOLO | RU | 1,000 | 2019-05-27 | still in orbit | still-in-orbit |
| 44454 | 2019-046B | Fregat | NPOLO | RU | 1,000 | 2019-07-30 | still in orbit | still-in-orbit |
| 44553 | 2019-065B | Fregat | NPOLO | RU | 1,000 | 2019-09-26 | still in orbit | still-in-orbit |
| 44851 | 2019-088B | Fregat | NPOLO | RU | 1,000 | 2019-12-11 | still in orbit | still-in-orbit |
| 45255 | 2020-015B | Fregat | NPOLO | RU | 1,000 | 2020-02-20 | still in orbit | still-in-orbit |
| 45359 | 2020-018B | Fregat | NPOLO | RU | 1,000 | 2020-03-16 | still in orbit | still-in-orbit |
| 45609 | 2020-031B | Fregat | NPOLO | RU | 1,000 | 2020-05-22 | still in orbit | still-in-orbit |
| 46806 | 2020-075B | Fregat | NPOLO | RU | 1,000 | 2020-10-25 | still in orbit | still-in-orbit |
| 47720 | 2021-016B | Fregat | NPOLO | RU | 1,000 | 2021-02-28 | still in orbit | still-in-orbit |
| 49504 | 2021-113B | Fregat | NPOLO | RU | 1,000 | 2021-11-25 | still in orbit | still-in-orbit |
| 49811 | 2021-116C | Fregat | NPOLO | RU | 1,050 | 2021-12-05 | still in orbit | still-in-orbit |
| 52146 | 2022-030B | Fregat | NPOLO | RU | 1,000 | 2022-03-22 | still in orbit | still-in-orbit |
| 52985 | 2022-075B | Fregat | NPOLO | RU | 1,000 | 2022-07-07 | still in orbit | still-in-orbit |
| 54032 | 2022-130B | Fregat | NPOLO | RU | 1,000 | 2022-10-10 | still in orbit | still-in-orbit |
| 54154 | 2022-139E | Fregat | NPOL | RU | 1,000 | 2022-10-22 | still in orbit | still-in-orbit |
| 54224 | 2022-145B | Fregat | NPOLO | RU | 1,000 | 2022-11-02 | still in orbit | still-in-orbit |
| 54378 | 2022-161B | Fregat | NPOLO | RU | 1,000 | 2022-11-28 | still in orbit | still-in-orbit |
| 57518 | 2023-114B | Fregat | NPOLO | RU | 1,000 | 2023-08-07 | still in orbit | still-in-orbit |
| 58585 | 2023-198B | Fregat | NPOLO | RU | 1,000 | 2023-12-16 | still in orbit | still-in-orbit |
| 59073 | 2024-039W | Fregat | NPOL | RU | 1,000 | 2024-02-29 | still in orbit | still-in-orbit |
| 56760 | 2023-076B | GSLV | ISRO | IN | 2,630 | 2023-05-29 | still in orbit | still-in-orbit |
| 58991 | 2024-033B | GSLV | ISRO | IN | 2,630 | 2024-02-17 | still in orbit | still-in-orbit |
| 39771 | 2014-029F | H-IIA/B | MHI | J | 4,000 | 2014-05-24 | still in orbit | still-in-orbit |
| 40268 | 2014-060B | H-IIA/B | MHI | J | 4,000 | 2014-10-07 | still in orbit | still-in-orbit |
| 41037 | 2015-068B | H-IIA/B | MHI | J | 4,000 | 2015-11-24 | still in orbit | still-in-orbit |
| 41341 | 2016-012E | H-IIA/B | MHI | J | 4,000 | 2016-02-17 | still in orbit | still-in-orbit |
| 41837 | 2016-064B | H-IIA/B | MHI | J | 4,000 | 2016-11-02 | still in orbit | still-in-orbit |
| 41941 | 2017-005B | H-IIA/B | MHI | J | 4,000 | 2017-01-24 | still in orbit | still-in-orbit |
| 42739 | 2017-028B | H-IIA/B | MHI | J | 4,000 | 2017-06-01 | still in orbit | still-in-orbit |
| 42918 | 2017-048B | H-IIA/B | MHI | J | 4,000 | 2017-08-19 | still in orbit | still-in-orbit |
| 42966 | 2017-062B | H-IIA/B | MHI | J | 4,000 | 2017-10-09 | still in orbit | still-in-orbit |
| 43682 | 2018-084L | H-IIA/B | MHI | J | 4,000 | 2018-10-29 | still in orbit | still-in-orbit |
| 49337 | 2021-096B | H-IIA/B | MHI | J | 4,000 | 2021-10-26 | still in orbit | still-in-orbit |
| 58818 | 2024-015B | Iranian (Simorgh/Safir/Qased/Qaem) | IRGC | IR | 200 | 2024-01-20 | still in orbit | still-in-orbit |
| 58851 | 2024-018C | Iranian (Simorgh/Safir/Qased/Qaem) | IRSA | IR | 1,500 | 2024-01-28 | still in orbit | still-in-orbit |
| 61071 | 2024-165A | Iranian (Simorgh/Safir/Qased/Qaem) | IRGC | IR | 200 | 2024-09-14 | still in orbit | still-in-orbit |
| 58507 | 2023-190C | Jielong | CZHJ | CN | 500 | 2023-12-05 | still in orbit | still-in-orbit |
| 52896 | 2022-065C | KSLV | KARI | KR | 1,250 | 2022-06-21 | still in orbit | still-in-orbit |
| 56750 | 2023-072H | KSLV | KARI | KR | 1,250 | 2023-05-25 | still in orbit | still-in-orbit |
| 54149 | 2022-138AN | LVM3 (GSLV Mk III) | NSIL/ISRO | IN | 4,400 | 2022-10-22 | still in orbit | still-in-orbit |
| 42925 | 2017-050E | Minotaur | OATKC | US | 203 | 2017-08-26 | still in orbit | still-in-orbit |
| 45877 | 2020-046E | Minotaur | SMC | US | 500 | 2020-07-15 | still in orbit | still-in-orbit |
| 48849 | 2021-052D | Minotaur | NGISC | US | 410 | 2021-06-15 | still in orbit | still-in-orbit |
| 39093 | 2013-009H | PSLV | ISRO | IN | 920 | 2013-02-25 | still in orbit | still-in-orbit |
| 39200 | 2013-034B | PSLV | ISRO | IN | 920 | 2013-07-01 | still in orbit | still-in-orbit |
| 39371 | 2013-060B | PSLV | ISRO | IN | 920 | 2013-11-05 | still in orbit | still-in-orbit |
| 39636 | 2014-017B | PSLV | ISRO | IN | 920 | 2014-04-04 | still in orbit | still-in-orbit |
| 40058 | 2014-034F | PSLV | ISRO | IN | 920 | 2014-06-30 | still in orbit | still-in-orbit |
| 40270 | 2014-061B | PSLV | ISRO | IN | 920 | 2014-10-15 | still in orbit | still-in-orbit |
| 40548 | 2015-018B | PSLV | ISRO | IN | 920 | 2015-03-28 | still in orbit | still-in-orbit |
| 40720 | 2015-032F | PSLV | ISRO | IN | 920 | 2015-07-10 | still in orbit | still-in-orbit |
| 40937 | 2015-052H | PSLV | ISRO | IN | 920 | 2015-09-28 | still in orbit | still-in-orbit |
| 41242 | 2016-003B | PSLV | ISRO | IN | 920 | 2016-01-20 | still in orbit | still-in-orbit |
| 41385 | 2016-015B | PSLV | ISRO | IN | 920 | 2016-03-10 | still in orbit | still-in-orbit |
| 41470 | 2016-027B | PSLV | ISRO | IN | 920 | 2016-04-28 | still in orbit | still-in-orbit |
| 41791 | 2016-059J | PSLV | ISRO | IN | 920 | 2016-09-26 | still in orbit | still-in-orbit |
| 41878 | 2016-074B | PSLV | ISRO | IN | 920 | 2016-12-07 | still in orbit | still-in-orbit |
| 43287 | 2018-035B | PSLV | ISRO | IN | 920 | 2018-04-11 | still in orbit | still-in-orbit |
| 43620 | 2018-071C | PSLV | ISRO | IN | 920 | 2018-09-16 | still in orbit | still-in-orbit |
| 44805 | 2019-081B | PSLV | ISRO | IN | 920 | 2019-11-27 | still in orbit | still-in-orbit |
| 44862 | 2019-089L | PSLV | ISRO | IN | 920 | 2019-12-11 | still in orbit | still-in-orbit |
| 46915 | 2020-081L | PSLV | ISRO | IN | 920 | 2020-11-07 | still in orbit | still-in-orbit |
| 47257 | 2020-099B | PSLV | ISRO | IN | 920 | 2020-12-17 | still in orbit | still-in-orbit |
| 47700 | 2021-015B | PSLV | ISRO/NSIL | IN | 920 | 2021-02-28 | still in orbit | still-in-orbit |
| 51659 | 2022-013D | PSLV | ISRO | IN | 920 | 2022-02-14 | still in orbit | still-in-orbit |
| 54362 | 2022-158B | PSLV | ISRO | IN | 920 | 2022-11-26 | still in orbit | still-in-orbit |
| 57755 | 2023-132B | PSLV | ISRO | IN | 920 | 2023-09-02 | still in orbit | still-in-orbit |
| 62257 | 2024-233B | PSLV | ISRO | IN | 920 | 2024-12-05 | still in orbit | still-in-orbit |
| 39198 | 2013-033B | Pegasus | OSCC | US | 202 | 2013-06-28 | still in orbit | still-in-orbit |
| 41892 | 2016-078J | Pegasus | OATKC | US | 202 | 2016-12-15 | still in orbit | still-in-orbit |
| 44629 | 2019-068B | Pegasus | NGISC | US | 202 | 2019-10-11 | still in orbit | still-in-orbit |
| 39679 | 2014-021B | Soyuz (Blok-I) | VVKO | RU | 2,350 | 2014-04-16 | still in orbit | still-in-orbit |
| 40698 | 2015-028B | Vega | AE | F | 660 | 2015-06-23 | still in orbit | still-in-orbit |
| 49467 | 2021-105D | Vega | AESP | F | 660 | 2021-11-16 | still in orbit | still-in-orbit |
| 53109 | 2022-080E | Vega | ESA | I-ESA | 660 | 2022-07-13 | still in orbit | still-in-orbit |
| 40751 | 2015-037D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2015-07-25 | still in orbit | still-in-orbit |
| 41316 | 2016-006B | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2016-02-01 | still in orbit | still-in-orbit |
| 41840 | 2016-065C | Yuanzheng (YZ kick stage) | CNSA | CN | 2,000 | 2016-11-03 | still in orbit | still-in-orbit |
| 43003 | 2017-069C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2017-11-05 | still in orbit | still-in-orbit |
| 43109 | 2018-003C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-01-11 | still in orbit | still-in-orbit |
| 43210 | 2018-018D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-02-12 | still in orbit | still-in-orbit |
| 43248 | 2018-029D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-03-29 | still in orbit | still-in-orbit |
| 43584 | 2018-062D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-07-29 | still in orbit | still-in-orbit |
| 43605 | 2018-067D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-08-24 | still in orbit | still-in-orbit |
| 43625 | 2018-072D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-09-19 | still in orbit | still-in-orbit |
| 43650 | 2018-078D | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-10-15 | still in orbit | still-in-orbit |
| 43708 | 2018-093C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2018-11-18 | still in orbit | still-in-orbit |
| 44544 | 2019-061C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2019-09-22 | still in orbit | still-in-orbit |
| 44795 | 2019-078C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2019-11-23 | still in orbit | still-in-orbit |
| 44866 | 2019-090C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2019-12-16 | still in orbit | still-in-orbit |
| 58656 | 2023-207C | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2023-12-26 | still in orbit | still-in-orbit |
| 60326 | 2024-048E | Yuanzheng (YZ kick stage) | CASC | CN | 2,500 | 2024-03-13 | still in orbit | still-in-orbit |
| 61185 | 2024-168A | Yuanzheng (YZ kick stage) | CASC | CN | 2,075 | 2024-09-19 | still in orbit | still-in-orbit |

---

## 4. Secondary census — per-vehicle-family aggregation

Every one of the 1,073 bodies above is also counted in this family roll-up (sorted by uncontrolled-body count). This is a *summary view of §3*, not a substitute for it. "Modal dry mass" is the most common GCAT `DryMass` value within the family (per-body values are in §3). All labels by the §2 rule.

| Vehicle family | Launch state(s) | Modal dry mass (kg) | Total | Uncontrolled | Controlled | Still-in-orbit |
|---|---|---:|---:|---:|---:|---:|
| Soyuz (Blok-I) | RU | 2,350 | 120 | 119 | 0 | 1 |
| Electron | NZ | 250 | 97 | 75 | 0 | 22 |
| CZ-3B | CN | 2,800 | 77 | 53 | 2 | 22 |
| Falcon 9 | US | 4,000 | 86 | 35 | 12 | 39 |
| Kuaizhou/KT | CN | 50 | 27 | 27 | 0 | 0 |
| CZ-4B | CN | 1,000 | 32 | 26 | 0 | 6 |
| CZ-2C | CN | 3,800 | 39 | 20 | 0 | 19 |
| CZ-2D | CN | 4,006 | 28 | 18 | 0 | 10 |
| Antares | US | 1,220 | 17 | 17 | 0 | 0 |
| H-IIA/B | J | 4,000 | 28 | 15 | 2 | 11 |
| CZ-2F | CN | 5,500 | 14 | 14 | 0 | 0 |
| CZ-11 | CN | 500 | 14 | 12 | 0 | 2 |
| GSLV | IN | 2,500 | 12 | 10 | 0 | 2 |
| CZ-7 | CN | 6,000 | 9 | 9 | 0 | 0 |
| PSLV | IN | 920 | 32 | 7 | 0 | 25 |
| CZ-7A | CN | 2,800 | 7 | 6 | 0 | 1 |
| Centaur | US | 2,020 | 48 | 5 | 12 | 31 |
| Epsilon | J | 185 | 9 | 5 | 0 | 4 |
| Iranian (Simorgh/Safir/Qased/Qaem) | IR | 100 | 8 | 5 | 0 | 3 |
| CZ-6 | CN | 1,000 | 8 | 5 | 0 | 3 |
| Lijian-1/Kinetica | CN | 500 | 5 | 5 | 0 | 0 |
| Gravity-1 | CN | 150 | 5 | 5 | 0 | 0 |
| CZ-4C | CN | 1,000 | 42 | 4 | 1 | 37 |
| Yuanzheng (YZ kick stage) | CN | 2,075 | 24 | 4 | 2 | 18 |
| Shavit | IL | 100 | 4 | 4 | 0 | 0 |
| CZ-5B | CN | 21,600 | 4 | 4 | 0 | 0 |
| LauncherOne | US | 200 | 4 | 4 | 0 | 0 |
| SSLV | IN | 400 | 4 | 4 | 0 | 0 |
| CZ-3C | CN | 2,800 | 8 | 3 | 1 | 4 |
| Minotaur | US | 140 | 6 | 3 | 0 | 3 |
| Jielong | CN | 500 | 4 | 3 | 0 | 1 |
| Ariane 5 | F | 5,000 | 49 | 2 | 4 | 43 |
| Delta | US | 3,450 | 18 | 2 | 5 | 11 |
| CZ-5 | CN | 5,100 | 7 | 2 | 3 | 2 |
| Volga | RU | 1,120 | 6 | 2 | 4 | 0 |
| CZ-8 | CN | 2,800 | 3 | 2 | 1 | 0 |
| Firefly Alpha | US | 909 | 3 | 2 | 0 | 1 |
| Strela | RU | 725 | 2 | 2 | 0 | 0 |
| Zenit | RU | 9,300 | 2 | 2 | 0 | 0 |
| CN commercial small (SMA/YL/OS-M) | CN | 550 | 2 | 2 | 0 | 0 |
| Zhuque | CN | 5,000 | 2 | 2 | 0 | 0 |
| Fregat | RU | 1,000 | 48 | 1 | 2 | 45 |
| Briz-KM | RU | 2,370 | 14 | 1 | 0 | 13 |
| Falcon Heavy | US | 4,000 | 9 | 1 | 2 | 6 |
| Vega | F/I-ESA | 660 | 6 | 1 | 2 | 3 |
| Pegasus | US | 202 | 4 | 1 | 0 | 3 |
| CZ-3A | CN | 2,800 | 4 | 1 | 0 | 3 |
| KSLV | KR | 1,250 | 3 | 1 | 0 | 2 |
| DPRK (Unha/Chollima) | KP | 50 | 2 | 1 | 0 | 1 |
| LVM3 (GSLV Mk III) | IN | 4,400 | 2 | 1 | 0 | 1 |
| SS-520 | J | 10 | 1 | 1 | 0 | 0 |
| Proton-M | RU | 4,185 | 1 | 1 | 0 | 0 |
| Hyperbola-1 | CN | 200 | 1 | 1 | 0 | 0 |
| H3 | J | 2,500 | 1 | 1 | 0 | 0 |
| Briz-M | RU | 1,600 | 37 | 0 | 1 | 36 |
| CZ-6A | CN | 6,000 | 9 | 0 | 0 | 9 |
| Blok DM (Proton/Zenit) | RU/US | 2,440 | 7 | 0 | 1 | 6 |
| Dnepr | RU | 1,000 | 5 | 0 | 0 | 5 |
| SLS (ICPS) | US | 3,830 | 1 | 0 | 1 | 0 |
| ADD test vehicle (KR) | KR | 100 | 1 | 0 | 0 | 1 |
| CZ-12 | CN | 6,000 | 1 | 0 | 0 | 1 |

**Findings worth flagging.** (1) **China dominates uncontrolled bodies by count and by mass** — 228 of 559 uncontrolled bodies and ~630 t of ~1,262 t total uncontrolled dry mass, with the single heaviest contributor by far being the **CZ-5B core at 21,600 kg/body**. (2) **CZ-6A second stages (6,000 kg each) are a building still-in-orbit hazard:** 9 of 9 are stranded at high LEO with no disposal capability — future uncontrolled reentries (M1's "future uncontrolled" long-horizon category). (3) Controlled disposal is still concentrated in a few Western families: of 58 controlled bodies, 12 are Centaur, 12 Falcon 9 second stages, 5 Delta, 4 Ariane 5, 4 Volga — i.e. controlled deorbit is the exception, not the norm.

---

## 5. Coverage note — total population reconciliation (included + excluded = total)

**Catalog total for the window (the M2 "total population count").** GCAT `satcat.tsv` contains **1,073** orbital rocket-body objects (`Type` = `R[0-9]`) with launch date in 2013–2024. This is the inventory's population, and **all 1,073 appear as individual rows in §3.**

| Category | Count | Treatment |
|---|---:|---|
| **Included rows — all classified, all shown in §3** | **1,073** | every orbital rocket body in the window, one row each, labelled |
| — uncontrolled (status `R`) | 559 | included, labelled uncontrolled |
| — controlled (status `D`/`DSO`) | 58 | included, labelled controlled (compliance baseline) |
| — still-in-orbit (status `O`) | 456 | included, labelled still-in-orbit (future-hazard subset, e.g. CZ-6A) |
| **Excluded by the M1 unit-of-analysis definition** | (not part of the 1,073) | not rocket bodies / outside unit of analysis |
| — payloads / satellites (`Type P*`) | excluded | M1 excludes payloads (separate accountability question) |
| — debris / fragments (`Type D*`) | excluded | M1 excludes mission / fragmentation debris |
| — components / adapters (`Type C*`) | excluded | M1 excludes non-stage hardware |
| — suborbital sounding rockets (GCAT `rcat.tsv`) | excluded | M1 excludes suborbital stages (never reached orbit) |
| **Total population (window) = included** | **1,073** | **559 + 58 + 456 = 1,073 ✓** |

So **included (1,073) = total population (1,073)**, with zero rocket bodies dropped. The "excluded" lines are the *object classes* removed by the M1 unit-of-analysis definition (payloads, debris, components, suborbital), which are outside the rocket-body population by construction. No rocket-body row in the window is omitted, and no row required the M1 default-uncontrolled fallback (§2).

**Sub-window cross-checks (for M3, per M1 §D).** Within 2013–2024, uncontrolled reentries by launch year rise from ~30/yr (2013–2014) to **71 (2023) and 69 (2024)**, consistent with the post-2019 launch-rate surge M1 flagged. (Counts derivable from §3 by launch-date year.)

---

## 6. Independent published sanity checks on inventory scale

1. **Share of reentered stages that are uncontrolled.** This inventory: **90.6%** of bodies that have left orbit (559 of 617 reentered) were uncontrolled. Comparators: **Byers, Wright & Boley 2022** report ~**70%** of historic rocket-body deorbits uncontrolled under a 7-day cutoff (arXiv:2210.02188 §4; the abstract notes >60% of 2020 launches, 72% in 2022 — confirmed); **Pardini & Anselmo 2024** report ~**80%** of orbital-stage uncontrolled reentries *exceeded the 1-in-10,000 casualty threshold* in 2021 (https://www.sciencedirect.com/science/article/pii/S2468896724000077); the CNR summary cites **84%** over 2010–2022 (https://www.cnr.it/en/focus/074-60/...). *Reconciliation (per M1):* the 84%/80% are *threshold-exceedance* shares (an M3 comparator), not a controlled/uncontrolled split. My 90.6% sits above Byers' ~70% because GCAT `Status R` counts every very-low-orbit naturally-decaying stage as uncontrolled (a stricter, physically-correct denominator than a span-only proxy) and because controlled deorbit is still rare outside Falcon 9 / Centaur / Ariane-5 / CZ-5. The order of magnitude agrees: the large majority of stages reenter uncontrolled.

2. **Annual abandoned-rocket-body count.** This inventory: of 120 rocket bodies launched in 2023, **115 were left uncontrolled-or-in-orbit** (status `R` or `O`; 5 controlled disposal). Independent figure: *Scientific Reports* 14 (2024), "Airspace closures due to reentering space objects," states **128 rocket bodies were abandoned in orbit from 2023 launches** (https://www.nature.com/articles/s41598-024-84001-2). The ~10% gap reflects their reentry-year/definition vs my launch-year GCAT snapshot; the scale matches.

3. **Attribution by launching state (count and dry mass).** Uncontrolled bodies 2013–2024: China **228** (≈630 t), Russia **128** (≈311 t), New Zealand 75 (≈14 t, tiny Electron kick stages), USA 70 (≈184 t), Japan 22 (≈64 t), India 22 (≈45 t). By dry mass the uncontrolled split is **CN ~50% / RU ~25% / US ~15%**. Comparator: Pardini & Anselmo 2024 report a **62% Chinese / 18% Russian-Soviet / 14% American** split of *casualty risk*. Ordering matches exactly (China ≫ Russia > USA); the mass-share (50/25/15) vs risk-share (62/18/14) divergence is expected — risk weights heavy, large-casualty-area bodies (the 21.6 t CZ-5B cores) more than proportionally. Converting this mass/count attribution into the 62/18/14 risk attribution is the M3 step.

---

## Limitations & counter-evidence

1. **The control label rides on GCAT's `Status` coding.** Mapping `R`→uncontrolled and `D`/`DSO`→controlled assumes GCAT correctly distinguishes natural decay from commanded burns. For well-documented Western stages (Falcon 9, Centaur, Ariane-5) this is reliable; for some Chinese/Russian stages the `R` vs `DSO` call is McDowell's expert inference, not an operator declaration, and could be wrong in individual rows. Mitigation: §2 documents the agreement with the M1 ≥7-day proxy (445/559) and the 114 short-span exceptions are independently defensible low-perigee natural decays.

2. **The 90.6% uncontrolled fraction is higher than the literature's ~70–80%, by construction.** Status `R` counts naturally-short-lived very-low-orbit stages (Soyuz Blok-I, some Electron/Kuaizhou) as uncontrolled, a stricter denominator than Byers' span-only definition. A reader could argue a stage that decays in 2 days deposits negligible casualty risk and should not inflate the headline. Counter: M1's posture is risk-inclusive and the M3 casualty model *weights* each body by mass/casualty-area, so these tiny short-lived stages contribute almost nothing to risk even while counted — the count and the risk are different ledgers (§6 keeps them separate).

3. **Mass is dry mass from a single source, and is not surviving/reentry mass.** Every mass cell is GCAT `DryMass`. GCAT populated all 1,073 rows (better than M1 feared), but its values for older/foreign stages are themselves estimates (good to ~10–20%; ranking robust). Critically, **dry mass is not the quantity M3 needs** — reentry *surviving mass* and *casualty area* require fragment demise simulation absent from any open catalog (M1 Limitation 2), so no per-row reentry-mass column exists; this is stated rather than faked.

4. **Family attribution is regex-derived from GCAT `Name`.** The §4 family roll-up and the §3 "Vehicle family" column are assigned by pattern-matching the GCAT `Name` string. This is reliable for named vehicles (CZ-5B, Falcon 9, Electron) but a handful of mixed buckets (e.g. "CN commercial small," "Iranian (Simorgh/Safir/Qased/Qaem)") group genuinely different stages; the per-row NORAD/COSPAR/Name lets a reviewer disaggregate. No body is dropped or double-counted (§5 reconciles to 1,073).

5. **Snapshot dependence.** GCAT is a living catalog (this snapshot 2026-06-26). Late reentries of bodies still listed `O` will shift the uncontrolled/still-in-orbit split over time (the 456 in-orbit bodies are future reentries, most uncontrolled — e.g. CZ-6A). A re-run on a later GCAT will move counts by a few percent; the structural conclusions (China-dominated, CZ-5B the single heaviest hazard, controlled deorbit still rare) will not.

6. **Counter-evidence on harm (carried from M1).** No confirmed human casualty has resulted from any of these 559 uncontrolled reentries (Byers et al. 2022 note no such event was reported). The case is *expected* risk against a published threshold, not a realised body count — a fair counterpoint that M3 must engage rather than assume away.

---

## Source list (dated)

- **GCAT — General Catalog of Artificial Space Objects** (J. McDowell), `tsv/cat/satcat.tsv`, snapshot 2026-06-26 (header "Updated 2026 Jun 26 1346:41"). https://planet4589.org/space/gcat/ ; status-field definitions https://planet4589.org/space/gcat/web/intro/phases.html . CC-BY. — inventory spine for all §3 columns: NORAD (`Satcat`), COSPAR (`Piece`), `Type`, `Name`, operator (`Owner`), launch state (`State`), dry mass (`DryMass`), launch date (`LDate`), decay date (`DDate`), `Status`, `Perigee`, `Inc`.
- **M1 — Methodology and Source Register** (this problem), `artifacts/2026-06-26-m1-methodology-source-register.md`. — classification rule, ≥7-day proxy, unit of analysis, study window, data-source register, casualty model (for M3).
- Byers, Wright & Boley, "Unnecessary risks created by uncontrolled rocket reentries," *Nature Astronomy* 6, 1093–1097 (2022). DOI 10.1038/s41550-022-01718-8; arXiv:2210.02188. — ~70% uncontrolled fraction; ≥7-day rule.
- Pardini & Anselmo, "The risk of casualties from the uncontrolled re-entry of spacecraft and orbital stages," *J. Space Safety Engineering* 11(2):181–191 (2024). https://www.sciencedirect.com/science/article/pii/S2468896724000077 . — ~80% (2021) exceeding 1-in-10,000; 62%/18%/14% CN/RU/US risk split.
- CNR research focus summarising Pardini & Anselmo. https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites . — 84% (2010–2022) exceeding threshold.
- "Airspace closures due to reentering space objects," *Scientific Reports* 14 (2024), s41598-024-84001-2. https://www.nature.com/articles/s41598-024-84001-2 . — 128 rocket bodies abandoned in orbit from 2023 launches (scale sanity check).

*Reproducibility: the §3 table was generated by re-downloading GCAT `satcat.tsv` (2026-06-26) and applying the §1 filter (`Type` = `R[0-9]`, `LDate` 2013–2024) and the §2 `Status`→label map. Filter yields 1,073 rows (559 R / 15 D + 43 DSO / 456 O). All scratchpad intermediates are ephemeral; this artifact's §3 table is the durable record.*
