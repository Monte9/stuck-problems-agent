# M2 — Per-rocket-body classified inventory

**Problem:** Uncontrolled rocket-body reentries — the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M2 (row-level inventory of abandoned rocket bodies, classified controlled/uncontrolled).
**Input milestone:** M1 — Methodology and Source Register (`artifacts/2026-06-26-m1-methodology-source-register.md`). This artifact uses **only** M1's data sources (GCAT spine, Space-Track/CelesTrak cross-check, DISCOS/family dry-mass references), M1's controlled-vs-uncontrolled classification rule (the six observable signals, the ≥7-day default test, and default-to-uncontrolled for unresolved cases), M1's pinned **2013–2024** study window, and M1's **stage-not-payload** unit of analysis. No new method is introduced; where M1's rule needed a concrete catalog operationalisation, that operationalisation is stated explicitly in §2 below.
**Author:** generator routine | **Date:** 2026-06-26.

---

## 1. How this inventory was built (data + method, both traceable to M1)

**Spine.** The inventory is built from **GCAT** (M1 source 1), file `tsv/cat/satcat.tsv` from https://planet4589.org/space/gcat/ , downloaded 2026-06-26 (catalog header timestamp "Updated 2026 Jun 26 1346:45"). GCAT carries, per object: NORAD/Satcat number, COSPAR/international designator (`Piece`), object `Type`, `Name` (vehicle/stage), launching `State`, `Owner`, `DryMass`, launch date `LDate`, decay date `DDate`, `Status`, orbital inclination `Inc`, and `Perigee`. These are exactly the M2-required attributes.

**Unit of analysis (from M1 §D).** One row per **orbital rocket stage / upper stage** — GCAT `Type` beginning `R` followed by a stage digit (`R1`,`R2`,`R3`,`R4`…). Payloads (`P*`), debris (`D*`), and components/adapters (`C*`) are excluded by M1's rule. Suborbital sounding-rocket entries (GCAT's separate `rcat.tsv`, all `Satcat="NSO"`) are excluded — they never achieved orbit, per M1's exclusion of suborbital stages.

**Window (from M1 §D):** launch date `LDate` in **2013-01-01 … 2024-12-31**.

**Population produced by this filter: 1,073 orbital rocket bodies.** This is the M2 total population for the window (reconciliation in §4).

**Mass source per row.** Dry mass is taken from GCAT's `DryMass` field, which is itself sourced by McDowell from manufacturer/agency spec sheets and cross-referenced to ESA DISCOS (M1 sources 1 and 7). GCAT populated a dry-mass value for **all 1,073** rows in this window (no blank-mass fallback to family estimates was needed for this window — a better coverage outcome than M1 anticipated). Per-row, the mass basis is therefore "GCAT `DryMass`"; family-level cross-checks against published spec masses are noted where they matter (e.g. CZ-5B core 21.6 t; Falcon 9 S2 ~4.0 t).

---

## 2. Control label assignment (M1 rule, operationalised on GCAT `Status`)

M1's rule (M1 §C) classifies each body **controlled**, **uncontrolled**, or **still-in-orbit** from observable, catalog-derivable signals. GCAT's `Status` field is the cleanest single catalog realisation of those signals, and maps to M1's rule as follows:

| GCAT `Status` | Meaning (GCAT phases doc) | M1 signal it realises | M1 label |
|---|---|---|---|
| `R` | Reentered — destroyed in atmosphere after **natural orbital decay** | Signal 6 (random/non-targeted decay) + signal 4 (dwell ≥ threshold for the long-lived majority) | **uncontrolled** |
| `D` | Deorbited — destroyed in atmosphere via **active deorbit maneuver** | Signal 1/3 (operator-declared / propulsive disposal) | **controlled** |
| `DSO` | Disposed to a graveyard/escape/sub-orbital-disposal trajectory via an **active burn** (e.g. Centaur, CZ-5 second stage, Ariane-5 ESC to Point-Nemo or heliocentric disposal) | Signal 2/3 (targeted disposal, restartable stage) | **controlled** |
| `O` | In orbit — not yet reentered | M1 "still-in-orbit" branch | **still-in-orbit** |

*GCAT Status definitions:* https://planet4589.org/space/gcat/web/intro/phases.html (R = "Reentered … after natural orbital decay"; D = "Deorbited … via active deorbit maneuver"; O = "In orbit").

**On the ≥7-day test (M1 signal 4).** M1 adopts a launch-to-reentry span ≥ 7 days as the *proxy* discriminator following Byers et al. 2022. Here the cleaner ground truth — GCAT's `Status R` (natural decay) vs `D`/`DSO` (active burn) — is available directly, so the span is used as a **reported cross-check column, not as the deciding test**. The two agree for the long-lived majority: of the 559 status-`R` (uncontrolled) bodies, **445 (80%) also have span ≥ 7 days**, satisfying both signals. The **114 status-`R` bodies with span < 7 days are still labelled uncontrolled** — and this is the M1-consistent call, not a deviation: status `R` is by definition *natural decay with no burn* (signal 6), and these are very-low-orbit stages (perigee 89–162 km; 82 of the 114 are Soyuz Blok-I third stages inserted into ~170 km orbits) that decay naturally within days. A short span here means "naturally short-lived low-perigee stage," not "commanded deorbit." Treating them as uncontrolled is exactly M1's default-to-uncontrolled posture for the conservative, risk-inclusive ledger.

**Disposal-capability override (M1 signal 5) — the CZ-5B case.** The four Long March 5B core stages (NORAD 45601, 48275, 53240, 54217; 21.6 t each — the largest objects in this inventory and the most-reported uncontrolled reentries of the decade) have spans of 4–10 days. The naive ≥7-day proxy would have mislabelled the span-4 and span-6 cores as "controlled?". M1 signal 5 (no disposal capability) and GCAT `Status R` (natural decay) both override that: the CZ-5B core has no re-ignitable disposal system and reenters uncontrolled. All four are correctly **uncontrolled** under the status-based mapping, with no manual override needed. This is the worked example M1 anticipated when it said signals 1–6 override the bare time test.

**Default-uncontrolled count (M1 transparency requirement).** M1 requires reporting how many rows rest on the default-to-uncontrolled assumption. Here **zero** rows required the genuine "cannot resolve from any signal → default uncontrolled" fallback: every reentered row carries a definite GCAT `Status` (R, D, or DSO). The 114 short-span `R` rows are labelled uncontrolled by *signal 6 (natural decay) actively present*, not by absence of information. This is a stronger evidentiary footing than M1's worst case.

---

## 3. The inventory

### 3a. Aggregate counts (the whole 1,073-body population, classified)

| Class (M1 label) | GCAT status | Count | Share |
|---|---|---|---|
| **Uncontrolled** | `R` (natural decay) | **559** | 52.1% |
| **Controlled** | `D` + `DSO` (active deorbit/disposal) | **58** | 5.4% |
| **Still-in-orbit** | `O` | **456** | 42.5% |
| **Total** | — | **1,073** | 100% |

*Source: GCAT satcat.tsv, filtered as §1–2, 2026-06-26.* Of the **617 bodies that have already left orbit** (R+D+DSO), **559 (90.6%) were uncontrolled** and 58 (9.4%) controlled — see §5 sanity check.

### 3b. Per-vehicle-family inventory (aggregated rows; the primary census)

A full one-row-per-body table of all 1,073 objects is large; per M1/M2 guidance, the census is presented **aggregated by vehicle family** (every body is counted; no body is dropped), with representative individual rows in §3c. Families are sorted by uncontrolled-body count. `Dry mass` is the GCAT modal/representative dry mass for the family's stage (per-body values in the JSON working set; cross-checked to published spec masses). All rows: control label by §2 rule; mass basis = GCAT `DryMass`.

| Vehicle family (stage) | Launch state | Dry mass (kg) | Total | Uncontrolled | Controlled | Still-in-orbit |
|---|---|---:|---:|---:|---:|---:|
| Soyuz Blok-I 3rd stage (Soyuz-2/-U/-FG) | RU | ~2,350 | 120 | 119 | 0 | 1 |
| Electron Curie/kick stage | NZ | ~150 | 97 | 75 | 0 | 22 |
| CZ-3B (Long March 3B) 3rd stage | CN | ~2,800 | 77 | 53 | 2 | 22 |
| Falcon 9 second stage | US | ~4,000 | 86 | 35 | 12 | 39 |
| Kuaizhou (KZ-1A) upper stage | CN | ~90 | 26 | 26 | 0 | 0 |
| CZ-4B (Long March 4B) 3rd stage | CN | ~1,000 | 32 | 26 | 0 | 6 |
| CZ-2C (Long March 2C) 2nd stage | CN | ~3,800 | 39 | 20 | 0 | 19 |
| CZ-2D (Long March 2D) 2nd stage | CN | ~4,000 | 28 | 18 | 0 | 10 |
| Antares (Castor-30/upper) | US | ~1,200 | 17 | 17 | 0 | 0 |
| H-IIA second stage | J | ~4,000 | 28 | 15 | 2 | 11 |
| CZ-2F (Long March 2F) 2nd stage | CN | ~5,500 | 14 | 14 | 0 | 0 |
| CZ-11 (Long March 11) upper | CN | ~500 | 14 | 12 | 0 | 2 |
| GSLV upper stage | IN | ~3,200 | 12 | 10 | 0 | 2 |
| CZ-7 (Long March 7) 2nd stage | CN | ~6,000 | 9 | 9 | 0 | 0 |
| PSLV PS4 upper stage | IN | ~920 | 32 | 7 | 0 | 25 |
| CZ-7A (Long March 7A) upper | CN | ~2,800 | 7 | 6 | 0 | 1 |
| Centaur (Atlas V / Vulcan) | US | ~2,050 | 48 | 5 | 12 | 31 |
| CZ-6 (Long March 6) upper | CN | ~1,250 | 8 | 5 | 0 | 3 |
| Epsilon | J | ~350 | 9 | 5 | 0 | 4 |
| Lijian-1 / Kinetica upper | CN | ~500 | 5 | 5 | 0 | 0 |
| **CZ-5B (Long March 5B) core stage** | CN | **21,600** | 4 | **4** | 0 | 0 |
| CZ-4C (Long March 4C) 3rd stage | CN | ~1,000 | 42 | 4 | 1 | 37 |
| Shavit (Israel) | IL | ~100 | 4 | 4 | 0 | 0 |
| SSLV (India) | IN | ~300 | 4 | 4 | 0 | 0 |
| LauncherOne | US | ~200 | 4 | 4 | 0 | 0 |
| Yuanzheng (CZ kick stage) | CN | ~2,160 | 24 | 4 | 2 | 18 |
| Zenit-2 2nd stage | RU | ~8,800 | 2 | 2 | 0 | 0 |
| Ariane 5 ESC/EPS upper | F | ~5,000 | 49 | 2 | 4 | 43 |
| Briz-M (Proton/Angara) upper | RU | ~1,800 | 51 | 1 | 1 | 49 |
| Fregat (Soyuz) upper stage | RU | ~1,050 | 48 | 1 | 2 | 45 |
| **CZ-6A (Long March 6A) 2nd stage** | CN | **6,000** | 8 | 0 | 0 | **8** |
| *(≈40 further families, ≤3 uncontrolled each: Delta II/IV, Vega, Zhuque, Ceres-1, Hyperbola, Minotaur, Pegasus, Qased/Qaem/Simorgh/Safir (Iran), KSLV-II Nuri, Unha/Chollima (DPRK), Strela, Rokot, Dnepr, H3, Vulcan, etc.)* | mixed | mixed | ~110 | ~52 | ~21 | ~37 |

*Source for every cell: GCAT satcat.tsv (M1 source 1), 2026-06-26. Family dry masses cross-checked to GCAT per-body `DryMass` and to published spec sheets; CZ-5B 21.6 t and Falcon 9 S2 ~4.0 t are widely reported (e.g. McDowell/GCAT; Byers et al. 2022; Pardini & Anselmo 2024).*

**Two findings worth flagging from 3b.** (1) **China dominates uncontrolled bodies by count and mass** — and the single heaviest contributor by far is the CZ-5B core at 21.6 t per body. (2) **CZ-6A second stages (6 t each) are a building still-in-orbit hazard**: 8 of 8 are stranded at 500–810 km perigee (NORAD 52152, 54236, 57831, 58200, 59344, 60214, …), i.e. future uncontrolled reentries with no disposal capability — exactly M1's "future uncontrolled" long-horizon category. The 2022 CZ-6A Y1 stage also fragmented into a large debris cloud (a known event), underscoring the hazard.

### 3c. Representative individual rows (one-per-body, per M2 format)

Identifier (NORAD | COSPAR), family, state, dry mass (kg), launch date, reentry date or status, launch-to-reentry span (days), GCAT status, and control label. Mass basis = GCAT `DryMass`; control basis = GCAT `Status` mapped by §2.

| NORAD | COSPAR | Stage / name | Family | State | Dry mass | Launch | Reentry / status | Span (d) | GCAT status | Label |
|---|---|---|---|---|---:|---|---|---:|---|---|
| 45601 | 2020-027C | CZ-5B Y1 Stage 1 | CZ-5B | CN | 21,600 | 2020-05-05 | 2020-05-11 | 6 | R | uncontrolled |
| 48275 | 2021-035B | CZ-5B Y2 Stage 1 | CZ-5B | CN | 21,600 | 2021-04-29 | 2021-05-09 | 10 | R | uncontrolled |
| 53240 | 2022-085B | CZ-5B Y3 Stage 1 | CZ-5B | CN | 21,600 | 2022-07-24 | 2022-07-30 | 6 | R | uncontrolled |
| 54217 | 2022-143B | CZ-5B Y4 Stage 1 | CZ-5B | CN | 21,600 | 2022-10-31 | 2022-11-04 | 4 | R | uncontrolled |
| 41107 | 2015-074C | Zenit-2 Stage 2 | Zenit | RU | 9,300 | 2015-12-11 | 2016-01-01 | 21 | R | uncontrolled |
| 41628 | 2016-042E | CZ-7 Y1 Stage 2 | CZ-7 | CN | 6,000 | 2016-06-25 | 2016-07-28 | 33 | R | uncontrolled |
| 39180 | 2013-029B | CZ-2F Y10 Stage 2 | CZ-2F | CN | 5,500 | 2013-06-11 | 2013-06-21 | 10 | R | uncontrolled |
| 39217 | 2013-038C | Ariane 5 ESC-A | Ariane 5 | F | 5,000 | 2013-07-25 | 2021-02-10 | 2,757 | R | uncontrolled |
| 39116 | 2013-010B | Falcon 9-005 Stage 2 | Falcon 9 S2 | US | 4,000 | 2013-03-01 | 2013-03-11 | 10 | R | uncontrolled |
| 39271 | 2013-055G | Falcon 9-006 Stage 2 | Falcon 9 S2 | US | 4,000 | 2013-09-29 | 2025-02-08 | 4,150 | R | uncontrolled |
| 39063 | 2013-002C | H-2A F22 Stage 2 | H-IIA S2 | J | 4,000 | 2013-01-27 | 2015-02-04 | 738 | R | uncontrolled |
| 39482 | 2013-075B | CZ-3B Y27 Stage 3 | CZ-3B | CN | 2,800 | 2013-12-20 | 2020-08-31 | 2,446 | R | uncontrolled |
| 39454 | 2013-067D | Briz-KM No. 72524 | Briz-KM | RU | 2,370 | 2013-11-22 | 2022-08-01 | 3,174 | R | uncontrolled |
| 39121 | 2013-011B | Centaur AV-037 | Centaur | US | 2,020 | 2013-03-19 | 2014-11-23 | 614 | R | uncontrolled |
| 41943 | 2017-006B | Fregat-MT No.133-07 | Fregat | RU | 1,050 | 2017-01-28 | 2024-06-25 | 2,705 | R | uncontrolled |
| 41172 | 2015-077G | PSLV-C29 PS4 | PSLV | IN | 920 | 2015-12-16 | 2023-01-16 | 2,588 | R | uncontrolled |
| 39083 | 2013-007B | Soyuz-U Blok-I No.137 | Soyuz Blok-I | RU | 2,350 | 2013-02-11 | 2013-02-13 | 2 | R | uncontrolled |
| 43164 | 2018-010B | Electron-2 Kick Stage | Electron | NZ | 45 | 2018-01-21 | 2023-12-17 | 2,156 | R | uncontrolled |
| **— controlled examples (compliance baseline) —** | | | | | | | | | | |
| 58752 | 2024-006B | Centaur V-001 (Vulcan) | Centaur | US | 5,500 | 2024-01-08 | 2024-01-08 (disposal burn) | 0 | DSO | **controlled** |
| 45936 | 2020-049B | CZ-5 Y4 Stage 2 | CZ-5 | CN | 5,100 | 2020-07-23 | 2020-07-23 (disposal) | 0 | DSO | **controlled** |
| 43654 | 2018-080B | Ariane 5 ESC-A | Ariane 5 | F | 5,000 | 2018-10-20 | 2018-10-20 (Point-Nemo) | 0 | DSO | **controlled** |
| *(Falcon 9 S2 controlled deorbits: 12 of 86 in window, GCAT status D/DSO)* | | Falcon 9 S2 | US | 4,000 | various | various (deorbit burn) | — | D/DSO | **controlled** |
| **— still-in-orbit examples (future hazard) —** | | | | | | | | | | |
| 52152 | 2022-031C | CZ-6A Y1 Stage 2 | CZ-6A | CN | 6,000 | 2022-03-29 | still in orbit (perigee 553 km) | — | O | still-in-orbit |
| 54236 | 2022-151B | CZ-6A Y2 Stage 2 | CZ-6A | CN | 6,000 | 2022-11-11 | still in orbit (perigee 813 km) | — | O | still-in-orbit |

*Every row's mass = GCAT `DryMass`; control label = GCAT `Status` per §2 mapping. GCAT satcat.tsv, 2026-06-26.* Note the two Falcon 9 rows (NORAD 39116 vs 39271): both are uncontrolled status `R`, but 39116 decayed in 10 days from a low LEO orbit while 39271, on a higher-energy orbit, took 11+ years — illustrating why the GCAT status (natural decay) rather than the bare span is the correct discriminator (§2).

---

## 4. Coverage note — total population reconciliation (included + excluded = total)

**Catalog total for the window (the M2 "total population count").** GCAT `satcat.tsv` contains **1,073** orbital rocket-body objects (`Type` = `R[0-9]`) with launch date in 2013–2024. This is the inventory's population.

**Reconciliation (included + excluded = total):**

| Category | Count | Treatment |
|---|---:|---|
| **Included rows — all classified** | **1,073** | every orbital rocket body in the window, labelled |
| — uncontrolled (status `R`) | 559 | included, labelled uncontrolled |
| — controlled (status `D`/`DSO`) | 58 | included, labelled controlled (compliance baseline) |
| — still-in-orbit (status `O`) | 456 | included, labelled still-in-orbit (future-hazard subset, e.g. CZ-6A) |
| **Excluded from this rocket-body ledger (per M1 §D)** | — | not rocket bodies / out of unit-of-analysis |
| — payloads/satellites (`Type P*`) | not counted | M1 excludes payloads (separate accountability question) |
| — debris/fragments (`Type D*`) | not counted | M1 excludes mission/fragmentation debris |
| — components/adapters (`Type C*`) | not counted | M1 excludes non-stage hardware |
| — suborbital sounding rockets (GCAT `rcat.tsv`, `Satcat=NSO`) | not counted | M1 excludes suborbital stages (never reached orbit) |
| **Total population (window) = included** | **1,073** | 559 + 58 + 456 = 1,073 ✓ |

So **included (1,073) = total population (1,073)**, with zero rocket bodies dropped; the "excluded" lines are the *object classes excluded by the M1 unit-of-analysis definition* (payloads, debris, components, suborbital), which are outside the rocket-body population by construction and therefore not part of the 1,073. No rocket-body row in the window is omitted, and **no row required the M1 default-uncontrolled fallback** (§2). Counts are reproducible from the saved working set (`scratchpad/final.json`) and the script `analyze.py`.

**Sub-window cross-checks (for M3 reconciliation, per M1 §D).** Within 2013–2024: uncontrolled reentries per launch-year rise from ~30/yr (2013–2014) to 69–71/yr (2023–2024), consistent with the post-2019 launch-rate surge M1 flagged.

---

## 5. Independent published sanity checks on inventory scale

1. **Share of reentered stages that are uncontrolled.** This inventory: **90.6%** of bodies that have left orbit (559 of 617) were uncontrolled. Published comparators (note the M1 reconciliation flag): Byers, Wright & Boley 2022 state ~**70%** of historic rocket-body deorbits are uncontrolled under a 7-day cutoff (arXiv:2210.02188 §4); Pardini & Anselmo 2024 report ~**80%** of orbital-stage uncontrolled reentries *exceeded the 1-in-10,000 casualty threshold* in 2021 (https://www.sciencedirect.com/science/article/pii/S2468896724000077); the CNR summary of that work cites **84%** exceeding threshold over 2010–2022 (https://www.cnr.it/en/focus/074-60/...). **Reconciliation (per M1):** the 84% and 80% figures are a *threshold-exceedance* share, not a controlled/uncontrolled split — they are an M3 comparator, not an M2 one; M1 explicitly flagged that the headline "84%" traces to the CNR summary while Pardini & Anselmo state ~80% for 2021, and M3 must compare against the ~80%/2021 figure. The directly comparable M2 quantity is the *uncontrolled fraction of reentries*; my 90.6% sits above Byers' ~70% because (a) GCAT's status `R` counts every very-low-orbit naturally-decaying stage (e.g. the 82 Soyuz Blok-I third stages) as uncontrolled — physically correct but a stricter denominator than Byers' span-only proxy — and (b) controlled deorbit (status `D`/`DSO`) is still rare outside Falcon 9 / Centaur / Ariane-5 / CZ-5. The order of magnitude agrees: the large majority of stages reenter uncontrolled.

2. **Annual abandoned-rocket-body count.** This inventory: **115** rocket bodies launched in 2023 were left uncontrolled in orbit (status `R` or `O`; 120 launched, of which 5 did controlled disposal). Independent published figure: *Scientific Reports* 14 (2024), "Airspace closures due to reentering space objects," states **128 rocket bodies were abandoned in 2023** (https://www.nature.com/articles/s41598-024-84001-2). The ~10% gap is consistent with their counting by *reentry-year* and a slightly different rocket-body definition vs. my *launch-year* GCAT snapshot; the scale matches.

3. **Attribution by launching state (count and mass).** Uncontrolled bodies 2013–2024: China **228** (630 t dry mass), Russia **128** (311 t), New Zealand 75 (14 t, almost all tiny Electron kick stages), USA 70 (184 t), Japan 22 (64 t), India 22 (45 t). By dry mass the uncontrolled split is **CN ~50% / RU ~25% / US ~15%**. Published comparator: Pardini & Anselmo 2024 report a **62% Chinese / 18% Russian-Soviet / 14% American** split of *casualty risk* (not raw mass). Agreement in ordering (China ≫ Russia > USA) is exact; the mass-share (50/25/15) vs risk-share (62/18/14) divergence is expected and itself informative — risk weights heavy, large-casualty-area bodies (the 21.6 t CZ-5B cores) more than proportionally, pushing China's *risk* share above its *mass* share. This is precisely the M3 step: apply the M1 casualty model to convert this mass/count attribution into the published 62/18/14 risk attribution.

---

## Limitations & counter-evidence

1. **The control label rides on GCAT's `Status` coding.** Mapping `R`→uncontrolled and `D`/`DSO`→controlled assumes GCAT correctly distinguishes natural decay from commanded burns. For well-documented Western stages (Falcon 9, Centaur, Ariane-5) this is reliable; for some Chinese/Russian stages the `R` vs `DSO` call is McDowell's expert inference, not an operator declaration, and could be wrong in individual rows. Mitigation: the per-row span column lets a reviewer see where status and the M1 ≥7-day proxy disagree (114 short-span `R` rows, §2), and those are independently defensible as low-perigee natural decays.

2. **The 90.6% uncontrolled fraction is higher than the literature's ~70–80%, by construction.** Because status `R` counts naturally-short-lived very-low-orbit stages (Soyuz Blok-I, some Electron/Kuaizhou) as uncontrolled, my denominator is stricter than Byers' span-only definition. A reader could argue a stage that decays in 2 days deposits negligible casualty risk and should not inflate the "uncontrolled" headline. Counter: M1's posture is risk-inclusive and the M3 casualty model will *weight* each body by mass/casualty-area, so these tiny short-lived stages contribute almost nothing to risk even while counted — the count and the risk are different ledgers, and §5 keeps them separate.

3. **Dry mass is a single-source field.** Every mass cell comes from GCAT `DryMass`. While GCAT populated all 1,073 rows (better than M1 feared), GCAT's values for older/foreign stages are themselves estimates, and reentry *casualty area* — the quantity M3 actually needs — is not the same as dry mass and is not in any open catalog (M1 Limitation 2). The family masses in §3b are modal/representative; per-body values vary (e.g. CZ-3B third-stage variants). Absolute masses are good to ~10–20%; the *ranking* is robust.

4. **Family aggregation hides per-body heterogeneity.** §3b reports families, not 1,073 individual rows; a few families (Yuanzheng, "other CN commercial") lump genuinely different stages. The §3c representative rows and the saved JSON working set mitigate this, but a fully expanded one-row-per-body table was deliberately summarised per M2's stated allowance for a justified representative inventory. The selection rule is explicit: **all** bodies are counted in the aggregates; individual rows shown are the highest-mass and most-cited cases plus controlled/in-orbit exemplars.

5. **Snapshot dependence.** GCAT is a living catalog (this snapshot: 2026-06-26). Late reentries of bodies still listed `O` will shift the uncontrolled/still-in-orbit split over time (the 456 in-orbit bodies are future reentries, most uncontrolled — e.g. CZ-6A). A re-run on a later GCAT will move counts by a few percent; the structural conclusions (China-dominated, CZ-5B as the single heaviest hazard, controlled deorbit still rare) will not.

6. **Counter-evidence on harm (carried from M1).** No confirmed human casualty has resulted from any of these 559 uncontrolled reentries (Byers et al. 2022). The case is *expected* risk against a published threshold, not a realised body count — a fair counterpoint that M3 must engage rather than assume away.

---

## Source list (dated)

- **GCAT — General Catalog of Artificial Space Objects** (J. McDowell), `tsv/cat/satcat.tsv`, snapshot 2026-06-26. https://planet4589.org/space/gcat/ ; status-field definitions https://planet4589.org/space/gcat/web/intro/phases.html . CC-BY. — inventory spine: NORAD/COSPAR, type, name, state, dry mass, launch/decay dates, status, inclination, perigee.
- **M1 — Methodology and Source Register** (this problem), `artifacts/2026-06-26-m1-methodology-source-register.md`. — classification rule, ≥7-day proxy, unit of analysis, study window, data-source register, casualty model (for M3).
- Byers, Wright & Boley, "Unnecessary risks created by uncontrolled rocket reentries," *Nature Astronomy* 6, 1093–1097 (2022). DOI 10.1038/s41550-022-01718-8; arXiv:2210.02188. — ~70% uncontrolled fraction; ≥7-day rule.
- Pardini & Anselmo, "The risk of casualties from the uncontrolled re-entry of spacecraft and orbital stages," *J. Space Safety Engineering* 11(2):181–191 (2024). https://www.sciencedirect.com/science/article/pii/S2468896724000077 . — ~80% (2021) exceeding 1-in-10,000; 62%/18%/14% CN/RU/US risk split.
- CNR research focus summarising Pardini & Anselmo. https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites . — 84% (2010–2022) exceeding threshold.
- "Airspace closures due to reentering space objects," *Scientific Reports* 14 (2024), s41598-024-84001-2. https://www.nature.com/articles/s41598-024-84001-2 . — 128 rocket bodies abandoned in 2023 (scale sanity check).

*Working set (reproducible): `scratchpad/final.json` (all 1,073 classified rows) and `scratchpad/analyze.py` (the GCAT parse + classifier).*
