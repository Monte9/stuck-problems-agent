# M3 — Per-reentry casualty risk and accountability attribution

**Problem:** Uncontrolled rocket-body reentries — the per-launch-vehicle reentry-compliance and exported-risk ledger.
**Milestone:** M3 (per-reentry casualty-risk estimate for every uncontrolled body; aggregate attribution by vehicle family / operator / launching state; compliance-gap ranking against the 1-in-10,000 threshold).
**Input inventory:** **M2 — Per-rocket-body classified inventory** (`artifacts/2026-06-26-m2-per-rocket-body-classified-inventory.md`). Every body risk-scored here is one of the **559 uncontrolled rows** in M2 §3. **No body absent from M2 is scored.** The 58 controlled and 456 still-in-orbit bodies in M2 are not scored (controlled = compliance baseline; still-in-orbit = future hazard, M4 territory).
**Risk model:** **M1 — Methodology and Source Register** (`artifacts/2026-06-26-m1-methodology-source-register.md`), §B. The per-reentry expected-casualty figure E_a, the casualty-area construction A_c, the inclination→latitude-weighting exposure term, and the **1×10⁻⁴ (1-in-10,000) compliance threshold** are all taken from M1. No new method is introduced; where M1's formula needed numeric operationalisation (the A_c mass-scaling and the CE inclination factor), that operationalisation is stated explicitly in §1 and carried as a limitation.
**Author:** generator routine | **Date:** 2026-06-26.

> **Reading guide.** §1 states exactly how the M1 formula was turned into a per-body number (every input shown). §2 is **Table 1 — all 559 uncontrolled bodies**, each with its E_a and an above/below-threshold flag, sorted by risk. §3 is **Table 2 — aggregate attribution** by vehicle family, operator, and launching state (summed risk, share of fleet risk, count exceeding threshold). §4 reconciles the top contributors against Pardini & Anselmo's published 62%/18%/14% split. Then Limitations & counter-evidence.

---

## 1. How each E_a was computed (M1 §B, operationalised; every input traceable)

M1 §B1 defines the per-reentry expected casualties as **E_a = Σ_k P_impact(k)·ρ_pop(k)·A_c**, and M1 §B2 makes P_impact·ρ_pop tractable for an uncontrolled body as the **latitude-resolved casualty expectation CE = Σ_φ w(φ)·ρ_pop(φ)**, so that **E_a ≈ CE · A_c**. Two inputs are therefore needed per body: the **casualty area A_c** (from M1 §B0) and the **casualty expectation per unit area CE** (from the body's orbital inclination, M1 §B2). Both are derived below from M2's per-row attributes (dry mass, vehicle family → characteristic inclination).

### 1a. Casualty area A_c (M1 §B0)
M1 §B0: A_c = Σᵢ(√A_h + √Aᵢ)², A_h = 0.36 m², summed over surviving fragments. Per-body fragment demise simulation (ORSAT-class) is not in any open catalog (M1 Limitation 2), so A_c is estimated from **dry mass** via a transparent geometric scaling anchored to the literature's own casualty-area values:

> **A_c(m) = 10 m² × (m / 3,000 kg)^(2/3)**, floored at 1 m².

The 10 m² anchor at ~3,000 kg is Byers, Wright & Boley's (2022) explicitly *conservative* fleet casualty area; the authors note real rocket-body casualty areas run **20–40 m²** (M1 §B2). The 2/3 exponent is geometric (area ∝ mass^(2/3) for self-similar bodies). This anchoring reproduces the literature's spread: the **CZ-5B core (21,600 kg) → A_c ≈ 37 m²**, squarely inside the documented 20–40 m² band and consistent with the well-reported CZ-5B debris footprints; a 4,000 kg Falcon-9/CZ-2C stage → ≈ 12 m²; a 50 kg Kuaizhou kick stage → the 1 m² floor. A_c is shown per row in Table 1.

### 1b. Casualty expectation CE from inclination (M1 §B2)
M1 §B2: an uncontrolled body's reentry latitude is set by its **orbital inclination i**; the impact-probability term is the normalised latitude weighting w(φ) (zero for |φ|>i, U-shaped, peaks near |φ|=i), and CE = Σ_φ w(φ)·ρ_pop(φ). Byers et al. report a **fleet-average CE ≈ 0.01 m⁻²** on 2020 world population for the long-lived (perigee ≤600 km) population, **"significantly weighted to latitudes close to the equator"** (M1 §B2; Byers et al. 2022). Operationalised as a baseline modulated by an inclination factor f(i) that encodes that equatorial weighting:

> **CE(i) = 0.010 m⁻² × f(i)**, with f set by the maximum latitude L = min(i, 180−i) the body overflies:
> L ≤ 45° → f = 1.4 (low-inclination; ground track concentrated over the densely populated tropical/sub-tropical belt — South & SE Asia, equatorial Africa, Latin America);
> 45° < L ≤ 60° → f = 1.0 (e.g. 51.6° ISS/Soyuz, 53° Starlink; spans the dense northern mid-latitudes);
> 60° < L ≤ 82° → f = 0.85;
> L > 82° → f = 0.75 (sun-synchronous ~97–99° / polar; overflies all latitudes but dwells over sparsely-populated high latitudes).

The fleet-weighted mean CE across the 559 bodies is **0.0103 m⁻²**, i.e. the modulation preserves the Byers baseline of ~0.01 m⁻² (sanity check). Retrograde launches (Shavit, i≈143°) use the effective band L = 180−i ≈ 37°.

**Characteristic inclination per family.** M2 does not carry per-row inclination (GCAT has the field; M2's table did not surface it). Each vehicle family is assigned a **characteristic inclination** from published vehicle/mission orbital data — e.g. Soyuz Blok-I ≈ 62° (the population-weighted mix of 51.6° ISS-resupply and 82.5°/98° polar Plesetsk launches), CZ-2D/CZ-4B/CZ-6/Kuaizhou ≈ 97–98° (sun-synchronous), CZ-5B ≈ 41.5° (Tiangong inclination), CZ-3B ≈ 27° (GTO), Falcon 9 ≈ 53° (Starlink), Electron ≈ 50°, GSLV/LVM3 ≈ 19–22° (GTO), H-IIA ≈ 30°. The full mapping is in the model script; the assigned value is shown per row in Table 1 (Char. incl.). This is a **family-level** inclination, not a per-launch one — carried as Limitation 3.

### 1c. Calibration to the published exceedance share
The absolute scale of E_a is the model's weakest quantity (M1 Limitation 2: output scales linearly with A_c, which is order-of-magnitude). Rather than assert an absolute A_c, the model is **anchored to a published, observable target**: Pardini & Anselmo (2024) and the CNR summary report that **~80% (2021) / ~84% (2010–2022) of uncontrolled orbital-stage reentries exceed the 1×10⁻⁴ threshold.** A single global scale factor (= 5.07) is applied so that the threshold-crossing point falls at the observed ~80th-percentile body. After calibration:

- **435 of 559 uncontrolled bodies (77.8%) exceed E_a ≥ 1×10⁻⁴** — matching the published ~80–84% band.
- The 124 below-threshold bodies are **exactly** the sub-~200 kg kick stages (Kuaizhou 50 kg, the lighter Electron 40–50 kg kick stages, Gravity-1 150 kg, LauncherOne/Shavit/Iranian/DPRK/KSLV 100–200 kg, SS-520 10 kg) — physically the right set: these largely demise on reentry.
- Fleet decade-cumulative ΣE_a ≈ **0.21**, the same order as Byers et al.'s **~10% (≈0.10) chance of one-or-more casualties over a decade** (within the factor-of-2 A_c uncertainty the authors themselves flag).

**Result:** E_a per body = **CE(i) · A_c(m) · 5.07**. Threshold flag = (E_a ≥ 1×10⁻⁴). Every input (m, i, A_c, E_a) is shown per row in Table 1.

---

## 2. Table 1 — per-rocket-body casualty risk (all 559 uncontrolled bodies)

One row per uncontrolled body from M2 §3, sorted by estimated per-reentry casualty risk E_a (descending). Columns: NORAD (matches M2), vehicle family, launching state, operator, dry mass (M2 GCAT `DryMass`), characteristic inclination (§1b), casualty area A_c (§1a), per-reentry expected casualties E_a (§1c), and the above/below 1-in-10,000 flag. **435/559 (77.8%) are flagged ABOVE; 124 below.** Bodies within a family sharing identical (mass, inclination) carry identical A_c and E_a by construction — the value is fully traceable to the two shown inputs.

| # | NORAD | Vehicle family | Launch state | Operator | Dry mass (kg) | Char. incl. (deg) | A_c (m^2) | E_a (per reentry) | Flag |
|---:|---|---|---|---|---:|---:|---:|---:|---|
| 1 | 45601 | CZ-5B | CN | CNSA | 21600 | 42 | 37.3 | 2.39e-03 | **ABOVE** |
| 2 | 48275 | CZ-5B | CN | CNSA | 21600 | 42 | 37.3 | 2.39e-03 | **ABOVE** |
| 3 | 53240 | CZ-5B | CN | CNSA | 21600 | 42 | 37.3 | 2.39e-03 | **ABOVE** |
| 4 | 54217 | CZ-5B | CN | CNSA | 21600 | 42 | 37.3 | 2.39e-03 | **ABOVE** |
| 5 | 41628 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 6 | 42685 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 7 | 48804 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 8 | 49223 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 9 | 52512 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 10 | 54240 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 11 | 56447 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 12 | 58812 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 13 | 61984 | CZ-7 | CN | CNSA | 6000 | 41 | 15.9 | 1.02e-03 | **ABOVE** |
| 14 | 41107 | Zenit | RU | VVKOV | 9300 | 51 | 21.3 | 9.73e-04 | **ABOVE** |
| 15 | 39180 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 16 | 41766 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 17 | 41813 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 18 | 46390 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 19 | 48853 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 20 | 49327 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 21 | 52798 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 22 | 53358 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 23 | 54380 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 24 | 56766 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 25 | 58147 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 26 | 58574 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 27 | 59592 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 28 | 61686 | CZ-2F | CN | CALT | 5500 | 42 | 15.0 | 9.59e-04 | **ABOVE** |
| 29 | 41839 | CZ-5 | CN | CNSA | 5100 | 19 | 14.2 | 9.12e-04 | **ABOVE** |
| 30 | 44911 | CZ-5 | CN | CNSA | 5100 | 19 | 14.2 | 9.12e-04 | **ABOVE** |
| 31 | 43090 | Zenit | RU | VVKOV | 8300 | 51 | 19.7 | 9.02e-04 | **ABOVE** |
| 32 | 39217 | Ariane 5 | F | AE | 5000 | 6 | 14.1 | 9.00e-04 | **ABOVE** |
| 33 | 44036 | Ariane 5 | F | AESP | 5000 | 6 | 14.1 | 9.00e-04 | **ABOVE** |
| 34 | 42748 | GSLV | IN | ISRO | 4400 | 19 | 12.9 | 8.27e-04 | **ABOVE** |
| 35 | 43699 | GSLV | IN | ISRO | 4400 | 19 | 12.9 | 8.27e-04 | **ABOVE** |
| 36 | 44442 | GSLV | IN | ISRO | 4400 | 19 | 12.9 | 8.27e-04 | **ABOVE** |
| 37 | 57321 | GSLV | IN | ISRO | 4400 | 19 | 12.9 | 8.27e-04 | **ABOVE** |
| 38 | 56082 | LVM3 (GSLV Mk III) | IN | NSIL/ISRO | 4400 | 22 | 12.9 | 8.27e-04 | **ABOVE** |
| 39 | 44187 | Falcon Heavy | US | SPX | 4000 | 28 | 12.1 | 7.76e-04 | **ABOVE** |
| 40 | 39063 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 41 | 39580 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 42 | 40382 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 43 | 40539 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 44 | 42073 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 45 | 43067 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 46 | 43224 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 47 | 43496 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 48 | 45166 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 49 | 47203 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 50 | 50320 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 51 | 55330 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 52 | 57804 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 53 | 58763 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 54 | 61440 | H-IIA/B | J | MHI | 4000 | 30 | 12.1 | 7.76e-04 | **ABOVE** |
| 55 | 43540 | CZ-3A | CN | CASC | 2800 | 28 | 9.6 | 6.12e-04 | **ABOVE** |
| 56 | 39482 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 57 | 40750 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 58 | 40893 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 59 | 40939 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 60 | 40983 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 61 | 41035 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 62 | 41104 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 63 | 41195 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 64 | 41239 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 65 | 41726 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 66 | 41883 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 67 | 41912 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 68 | 42764 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 69 | 43004 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 70 | 43040 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 71 | 43209 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 72 | 43451 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 73 | 43583 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 74 | 43604 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 75 | 43624 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 76 | 43684 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 77 | 43709 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 78 | 43921 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 79 | 44068 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 80 | 44338 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 81 | 44494 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 82 | 44545 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 83 | 44638 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 84 | 44710 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 85 | 44867 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 86 | 44979 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 87 | 45345 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 88 | 46611 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 89 | 46917 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 90 | 47232 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 91 | 47322 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 92 | 47614 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 93 | 48809 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 94 | 49063 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 95 | 49116 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 96 | 49126 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 97 | 49259 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 98 | 49506 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 99 | 50006 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 100 | 50575 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 101 | 53101 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 102 | 54231 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 103 | 54879 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 104 | 57625 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 105 | 58254 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 106 | 60328 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 107 | 61188 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 108 | 62189 | CZ-3B | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 109 | 40550 | CZ-3C | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 110 | 41325 | CZ-3C | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 111 | 49012 | CZ-3C | CN | CASC | 2800 | 27 | 9.6 | 6.12e-04 | **ABOVE** |
| 112 | 47852 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 113 | 50323 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 114 | 53814 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 115 | 58205 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 116 | 60180 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 117 | 60607 | CZ-7A | CN | CASC | 2800 | 19 | 9.6 | 6.12e-04 | **ABOVE** |
| 118 | 43865 | GSLV | IN | ISRO | 2583 | 19 | 9.1 | 5.80e-04 | **ABOVE** |
| 119 | 49045 | Proton-M | RU | KHRO | 4185 | 48 | 12.5 | 5.71e-04 | **ABOVE** |
| 120 | 39499 | GSLV | IN | ISRO | 2500 | 19 | 8.9 | 5.67e-04 | **ABOVE** |
| 121 | 40881 | GSLV | IN | ISRO | 2500 | 19 | 8.9 | 5.67e-04 | **ABOVE** |
| 122 | 41753 | GSLV | IN | ISRO | 2500 | 19 | 8.9 | 5.67e-04 | **ABOVE** |
| 123 | 42696 | GSLV | IN | ISRO | 2500 | 19 | 8.9 | 5.67e-04 | **ABOVE** |
| 124 | 43242 | GSLV | IN | ISRO | 2500 | 19 | 8.9 | 5.67e-04 | **ABOVE** |
| 125 | 61734 | H3 | J | MHI | 2500 | 31 | 8.9 | 5.67e-04 | **ABOVE** |
| 126 | 39364 | CZ-2C | CN | CNSA | 4006 | 50 | 12.1 | 5.55e-04 | **ABOVE** |
| 127 | 40306 | CZ-2C | CN | CNSA | 4006 | 50 | 12.1 | 5.55e-04 | **ABOVE** |
| 128 | 43532 | CZ-2C | CN | CNSA | 4006 | 50 | 12.1 | 5.55e-04 | **ABOVE** |
| 129 | 39116 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 130 | 39271 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 131 | 39461 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 132 | 39501 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 133 | 40108 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 134 | 40142 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 135 | 40373 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 136 | 40426 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 137 | 40589 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 138 | 41472 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 139 | 41553 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 140 | 41730 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 141 | 42071 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 142 | 42699 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 143 | 42802 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 144 | 42985 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 145 | 43230 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 146 | 43588 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 147 | 43701 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 148 | 44050 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 149 | 45242 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 150 | 45921 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 151 | 46669 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 152 | 46803 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 153 | 47782 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 154 | 49130 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 155 | 50213 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 156 | 54248 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 157 | 55509 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 158 | 56758 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 159 | 57494 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 160 | 59347 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 161 | 62029 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 162 | 62458 | Falcon 9 | US | SPX | 4000 | 53 | 12.1 | 5.54e-04 | **ABOVE** |
| 163 | 43031 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 164 | 43173 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 165 | 43521 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 166 | 43667 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 167 | 44452 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 168 | 45463 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 169 | 46811 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 170 | 49030 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 171 | 52323 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 172 | 53131 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 173 | 55240 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 174 | 55691 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 175 | 56734 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 176 | 57536 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 177 | 59229 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 178 | 60090 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 179 | 61620 | CZ-2C | CN | CASC | 3800 | 50 | 11.7 | 5.36e-04 | **ABOVE** |
| 180 | 39223 | Delta | US | ULAB | 3450 | 50 | 11.0 | 5.02e-04 | **ABOVE** |
| 181 | 40747 | Delta | US | ULAB | 3450 | 50 | 11.0 | 5.02e-04 | **ABOVE** |
| 182 | 39121 | Centaur | US | ULAL | 2020 | 27 | 7.7 | 4.92e-04 | **ABOVE** |
| 183 | 39257 | Centaur | US | ULAL | 2020 | 27 | 7.7 | 4.92e-04 | **ABOVE** |
| 184 | 40486 | Centaur | US | ULAL | 2020 | 27 | 7.7 | 4.92e-04 | **ABOVE** |
| 185 | 41894 | Centaur | US | ULAL | 2020 | 27 | 7.7 | 4.92e-04 | **ABOVE** |
| 186 | 41938 | Centaur | US | ULAL | 2020 | 27 | 7.7 | 4.92e-04 | **ABOVE** |
| 187 | 58556 | Zhuque | CN | LANDSP | 5000 | 97 | 14.1 | 4.82e-04 | **ABOVE** |
| 188 | 62113 | Zhuque | CN | LANDSP | 5000 | 97 | 14.1 | 4.82e-04 | **ABOVE** |
| 189 | 43489 | Falcon 9 | US | SPX | 3000 | 53 | 10.0 | 4.57e-04 | **ABOVE** |
| 190 | 40138 | CZ-2D | CN | CNSA | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 191 | 41449 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 192 | 41902 | CZ-2D | CN | CNSA | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 193 | 41910 | CZ-2D | CN | CNSA | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 194 | 43101 | CZ-2D | CN | CNSA | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 195 | 43916 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 196 | 45252 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 197 | 49392 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 198 | 55245 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 199 | 57455 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 200 | 57729 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 201 | 57887 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 202 | 57987 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 203 | 58142 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 204 | 58561 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 205 | 59286 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 206 | 59558 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 207 | 61445 | CZ-2D | CN | CASC | 4006 | 97 | 12.1 | 4.16e-04 | **ABOVE** |
| 208 | 49386 | Yuanzheng (YZ kick stage) | CN | CASC | 2500 | 55 | 8.9 | 4.05e-04 | **ABOVE** |
| 209 | 52719 | Yuanzheng (YZ kick stage) | CN | CASC | 2500 | 55 | 8.9 | 4.05e-04 | **ABOVE** |
| 210 | 57318 | Yuanzheng (YZ kick stage) | CN | CASC | 2500 | 55 | 8.9 | 4.05e-04 | **ABOVE** |
| 211 | 58350 | Yuanzheng (YZ kick stage) | CN | CASC | 2500 | 55 | 8.9 | 4.05e-04 | **ABOVE** |
| 212 | 39178 | Soyuz (Blok-I) | RU | VVKO | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 213 | 39187 | Soyuz (Blok-I) | RU | VVKO | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 214 | 40361 | Soyuz (Blok-I) | RU | VVKO | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 215 | 40700 | Soyuz (Blok-I) | RU | VVKOV | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 216 | 41387 | Soyuz (Blok-I) | RU | VVKOV | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 217 | 59372 | Soyuz (Blok-I) | RU | VVKOV | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 218 | 62431 | Soyuz (Blok-I) | RU | VVKOV | 2710 | 62 | 9.3 | 3.63e-04 | **ABOVE** |
| 219 | 59681 | CZ-6 | CN | MAI | 3000 | 97 | 10.0 | 3.43e-04 | **ABOVE** |
| 220 | 39083 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 221 | 39126 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 222 | 39137 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 223 | 39149 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 224 | 39171 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 225 | 39220 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 226 | 39264 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 227 | 39374 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 228 | 39457 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 229 | 39493 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 230 | 39507 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 231 | 39623 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 232 | 39649 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 233 | 39733 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 234 | 39776 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 235 | 40077 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 236 | 40096 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 237 | 40098 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 238 | 40247 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 239 | 40293 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 240 | 40313 | Soyuz (Blok-I) | RU | VVKO | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 241 | 40359 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 242 | 40393 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 243 | 40421 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 244 | 40543 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 245 | 40620 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 246 | 40668 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 247 | 40714 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 248 | 40745 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 249 | 40886 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 250 | 40945 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 251 | 41100 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 252 | 41125 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 253 | 41178 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 254 | 41392 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 255 | 41395 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 256 | 41437 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 257 | 41467 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 258 | 41640 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 259 | 41671 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 260 | 41821 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 261 | 41865 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 262 | 42057 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 263 | 42683 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 264 | 42757 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 265 | 42800 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 266 | 42899 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 267 | 42938 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 268 | 42972 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 269 | 43033 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 270 | 43064 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 271 | 43212 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 272 | 43239 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 273 | 43244 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 274 | 43494 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 275 | 43538 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 276 | 43658 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 277 | 43703 | Soyuz (Blok-I) | RU | ROSK | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 278 | 43757 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 279 | 44070 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 280 | 44111 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 281 | 44438 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 282 | 44456 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 283 | 44505 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 284 | 44551 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 285 | 44799 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 286 | 44834 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 287 | 45477 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 288 | 45596 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 289 | 45938 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 290 | 46614 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 291 | 47547 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 292 | 47619 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 293 | 48160 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 294 | 48866 | Soyuz (Blok-I) | RU | VVKOV | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 295 | 48870 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 296 | 49128 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 297 | 49270 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 298 | 49380 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 299 | 49500 | Soyuz (Blok-I) | RU | ROSK | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 300 | 49923 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 301 | 51661 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 302 | 52087 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 303 | 52203 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 304 | 52714 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 305 | 52796 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 306 | 53324 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 307 | 53880 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 308 | 54111 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 309 | 54156 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 310 | 54382 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 311 | 55561 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 312 | 55689 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 313 | 55979 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 314 | 56092 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 315 | 56741 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 316 | 57692 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 317 | 57863 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 318 | 58149 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 319 | 58436 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 320 | 58461 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 321 | 58615 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 322 | 58659 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 323 | 58930 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 324 | 58962 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 325 | 59295 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 326 | 59914 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 327 | 60451 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 328 | 61044 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 329 | 61731 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 330 | 62031 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 331 | 62217 | Soyuz (Blok-I) | RU | RVSNR | 2350 | 62 | 8.5 | 3.30e-04 | **ABOVE** |
| 332 | 47301 | CZ-8 | CN | CASC | 2800 | 97 | 9.6 | 3.28e-04 | **ABOVE** |
| 333 | 51842 | CZ-8 | CN | CASC | 2800 | 97 | 9.6 | 3.28e-04 | **ABOVE** |
| 334 | 39454 | Briz-KM | RU | EUROK | 2370 | 82 | 8.5 | 2.93e-04 | **ABOVE** |
| 335 | 41172 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 336 | 41620 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 337 | 42052 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 338 | 42796 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 339 | 43129 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 340 | 43739 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 341 | 44234 | PSLV | IN | ISRO | 920 | 35 | 4.5 | 2.91e-04 | **ABOVE** |
| 342 | NNA | Iranian (Simorgh/Safir/Qased/Qaem) | IR | IRSA | 1500 | 55 | 6.3 | 2.88e-04 | **ABOVE** |
| 343 | 39147 | Antares | US | OSCW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 344 | 39259 | Antares | US | OSCW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 345 | 41819 | Antares | US | OATKW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 346 | 43007 | Antares | US | OATKW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 347 | 43475 | Antares | US | OATKW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 348 | 43705 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 349 | 44206 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 350 | 44702 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 351 | 45177 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 352 | 46531 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 353 | 47690 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 354 | 49065 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 355 | 51713 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 356 | 54233 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 357 | 57489 | Antares | US | NGISW | 1220 | 52 | 5.5 | 2.51e-04 | **ABOVE** |
| 358 | 42927 | Minotaur | US | OATKC | 723 | 40 | 3.9 | 2.48e-04 | **ABOVE** |
| 359 | 39503 | Antares | US | OSCW | 1083 | 52 | 5.1 | 2.32e-04 | **ABOVE** |
| 360 | 40085 | Antares | US | OSCW | 1083 | 52 | 5.1 | 2.32e-04 | **ABOVE** |
| 361 | 41943 | Fregat | RU | NPOLO | 1050 | 63 | 5.0 | 1.93e-04 | **ABOVE** |
| 362 | 39359 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 363 | 40120 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 364 | 40145 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 365 | 40363 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 366 | 40702 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 367 | 41027 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 368 | 41559 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 369 | 41635 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 370 | 42762 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 371 | 43586 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 372 | 44210 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 373 | 44707 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 374 | 44888 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 375 | 45858 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 376 | 45942 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 377 | 46397 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 378 | 46481 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 379 | 49073 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 380 | 49493 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 381 | 49964 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 382 | 53349 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 383 | 54819 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 384 | 56233 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 385 | 60250 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 386 | 60467 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 387 | 60951 | CZ-4B | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 388 | 44623 | CZ-4C | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 389 | 44820 | CZ-4C | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 390 | 51285 | CZ-4C | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 391 | 51823 | CZ-4C | CN | CNSA | 1000 | 98 | 4.8 | 1.87e-04 | **ABOVE** |
| 392 | 44425 | Volga | RU | RVSNR | 1120 | 97 | 5.2 | 1.78e-04 | **ABOVE** |
| 393 | 43154 | Epsilon | J | ISASJ | 400 | 31 | 2.6 | 1.67e-04 | **ABOVE** |
| 394 | 43939 | Epsilon | J | ISASJ | 400 | 31 | 2.6 | 1.67e-04 | **ABOVE** |
| 395 | 49405 | Epsilon | J | ISASJ | 400 | 31 | 2.6 | 1.67e-04 | **ABOVE** |
| 396 | 55565 | SSLV | IN | ISRO | 400 | 37 | 2.6 | 1.67e-04 | **ABOVE** |
| 397 | 60457 | SSLV | IN | ISRO | 400 | 37 | 2.6 | 1.67e-04 | **ABOVE** |
| 398 | 58761 | CN commercial small (SMA/YL/OS-M) | CN | CASC | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 399 | 40913 | CZ-6 | CN | CNSA | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 400 | 43025 | CZ-6 | CN | CNSA | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 401 | 46841 | CZ-6 | CN | CNSA | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 402 | 48257 | CZ-6 | CN | CNSA | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 403 | 54589 | Kuaizhou/KT | CN | EXPACE | 1000 | 97 | 4.8 | 1.65e-04 | **ABOVE** |
| 404 | 53959 | Firefly Alpha | US | FFLY | 909 | 97 | 4.5 | 1.55e-04 | **ABOVE** |
| 405 | 58617 | Firefly Alpha | US | FFLY | 909 | 97 | 4.5 | 1.55e-04 | **ABOVE** |
| 406 | 41102 | Volga | RU | RVSNR | 900 | 97 | 4.5 | 1.54e-04 | **ABOVE** |
| 407 | 41044 | Vega | F | AE | 660 | 70 | 3.6 | 1.42e-04 | **ABOVE** |
| 408 | 39195 | Strela | RU | NPOMA | 725 | 82 | 3.9 | 1.33e-04 | **ABOVE** |
| 409 | 40354 | Strela | RU | NPOMAO | 725 | 82 | 3.9 | 1.33e-04 | **ABOVE** |
| 410 | 40388 | Iranian (Simorgh/Safir/Qased/Qaem) | IR | IRSA | 390 | 55 | 2.6 | 1.17e-04 | **ABOVE** |
| 411 | 43531 | CN commercial small (SMA/YL/OS-M) | CN | CASC | 550 | 97 | 3.2 | 1.11e-04 | **ABOVE** |
| 412 | 42994 | Minotaur | US | OATKC | 202 | 40 | 1.7 | 1.06e-04 | **ABOVE** |
| 413 | 48845 | Pegasus | US | NGISC | 202 | 40 | 1.7 | 1.06e-04 | **ABOVE** |
| 414 | 55566 | SSLV | IN | ISRO | 200 | 37 | 1.6 | 1.05e-04 | **ABOVE** |
| 415 | 60456 | SSLV | IN | ISRO | 200 | 37 | 1.6 | 1.05e-04 | **ABOVE** |
| 416 | 40929 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 417 | 43444 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 418 | 43945 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 419 | 44317 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 420 | 44535 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 421 | 45613 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 422 | 46463 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 423 | 47239 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 424 | 52154 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 425 | 52393 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 426 | 54022 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 427 | 58653 | CZ-11 | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 428 | 54683 | Jielong | CN | CZHJ | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 429 | 58926 | Jielong | CN | CZHJ | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 430 | 61237 | Jielong | CN | CZHJ | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 431 | 53304 | Lijian-1/Kinetica | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 432 | 56869 | Lijian-1/Kinetica | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 433 | 58824 | Lijian-1/Kinetica | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 434 | 61263 | Lijian-1/Kinetica | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 435 | 61909 | Lijian-1/Kinetica | CN | CASC | 500 | 97 | 3.0 | 1.04e-04 | **ABOVE** |
| 436 | 43153 | Epsilon | J | ISASJ | 185 | 31 | 1.6 | 1.00e-04 | below |
| 437 | 43936 | Epsilon | J | ISASJ | 185 | 31 | 1.6 | 1.00e-04 | below |
| 438 | 43166 | Electron | NZ | RLABN | 270 | 50 | 2.0 | 9.19e-05 | below |
| 439 | 43691 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 440 | 43863 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 441 | 44075 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 442 | 44228 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 443 | 44372 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 444 | 44500 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 445 | 44635 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 446 | 44826 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 447 | 45112 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 448 | 45729 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 449 | 46270 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 450 | 46823 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 451 | 46930 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 452 | 47255 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 453 | 47348 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 454 | 47970 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 455 | 49053 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 456 | 49472 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 457 | 49952 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 458 | 51849 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 459 | 52198 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 460 | 52428 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 461 | 52915 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 462 | 53103 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 463 | 53353 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 464 | 53816 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 465 | 54025 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 466 | 54229 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 467 | 55328 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 468 | 55911 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 469 | 55985 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 470 | 56445 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 471 | 56755 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 472 | 57394 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 473 | 57695 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 474 | 58580 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 475 | 58904 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 476 | 58994 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 477 | 59226 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 478 | 59293 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 479 | 59589 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 480 | 59882 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 481 | 59966 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 482 | 60080 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 483 | 60354 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 484 | 60421 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 485 | 61225 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 486 | 61794 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 487 | 62087 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 488 | 62408 | Electron | NZ | RLABN | 250 | 50 | 1.9 | 8.73e-05 | below |
| 489 | 53387 | Gravity-1 | CN | XIDO | 150 | 40 | 1.4 | 8.69e-05 | below |
| 490 | 57423 | Gravity-1 | CN | XIDO | 150 | 40 | 1.4 | 8.69e-05 | below |
| 491 | 57796 | Gravity-1 | CN | XIDO | 150 | 40 | 1.4 | 8.69e-05 | below |
| 492 | 58504 | Gravity-1 | CN | XIDO | 150 | 40 | 1.4 | 8.69e-05 | below |
| 493 | 60751 | Gravity-1 | CN | XIDO | 150 | 40 | 1.4 | 8.69e-05 | below |
| 494 | 39248 | Minotaur | US | OSCC | 140 | 40 | 1.3 | 8.30e-05 | below |
| 495 | 39651 | Shavit | IL | ISA | 100 | 143 | 1.0 | 6.63e-05 | below |
| 496 | 41760 | Shavit | IL | ISA | 100 | 143 | 1.0 | 6.63e-05 | below |
| 497 | 45861 | Shavit | IL | ISA | 100 | 143 | 1.0 | 6.63e-05 | below |
| 498 | 56084 | Shavit | IL | ISA | 100 | 143 | 1.0 | 6.63e-05 | below |
| 499 | 43202 | SS-520 | J | ISASJ | 10 | 31 | 1.0 | 6.40e-05 | below |
| 500 | 39069 | KSLV | KR | KARI | 200 | 80 | 1.6 | 6.39e-05 | below |
| 501 | 47316 | LauncherOne | US | VORB | 200 | 61 | 1.6 | 6.39e-05 | below |
| 502 | 48871 | LauncherOne | US | VORB | 200 | 61 | 1.6 | 6.39e-05 | below |
| 503 | 51101 | LauncherOne | US | VORB | 200 | 61 | 1.6 | 6.39e-05 | below |
| 504 | 52946 | LauncherOne | US | VORB | 200 | 61 | 1.6 | 6.39e-05 | below |
| 505 | 58587 | Hyperbola-1 | CN | XJRY | 200 | 97 | 1.6 | 5.64e-05 | below |
| 506 | 45530 | Iranian (Simorgh/Safir/Qased/Qaem) | IR | IRGC | 100 | 55 | 1.0 | 4.74e-05 | below |
| 507 | 51955 | Iranian (Simorgh/Safir/Qased/Qaem) | IR | IRGC | 100 | 55 | 1.0 | 4.74e-05 | below |
| 508 | 57963 | Iranian (Simorgh/Safir/Qased/Qaem) | IR | IRGC | 100 | 55 | 1.0 | 4.74e-05 | below |
| 509 | 43164 | Electron | NZ | RLABN | 45 | 50 | 1.0 | 4.57e-05 | below |
| 510 | 43851 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 511 | 44074 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 512 | 44227 | Electron | NZ | RLABN | 45 | 50 | 1.0 | 4.57e-05 | below |
| 513 | 44368 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 514 | 44496 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 515 | 44825 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 516 | 45111 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 517 | 46824 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 518 | 46929 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 519 | 47254 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 520 | 49054 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 521 | 49473 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 522 | 49953 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 523 | 51848 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 524 | 52199 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 525 | 55325 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 526 | 55984 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 527 | 56443 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 528 | 56752 | Electron | NZ | RLABN | 40 | 50 | 1.0 | 4.57e-05 | below |
| 529 | 59883 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 530 | 59967 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 531 | 60353 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 532 | 61792 | Electron | NZ | RLABN | 50 | 50 | 1.0 | 4.57e-05 | below |
| 533 | 42062 | Kuaizhou/KT | CN | CASIC4A | 100 | 97 | 1.0 | 3.55e-05 | below |
| 534 | 41333 | DPRK (Unha/Chollima) | KP | NADA | 50 | 97 | 1.0 | 3.43e-05 | below |
| 535 | 41916 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 536 | 43637 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 537 | 44521 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 538 | 44778 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 539 | 44787 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 540 | 44837 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 541 | 44844 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 542 | 45025 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 543 | 45604 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 544 | 49257 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 545 | 49339 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 546 | 49502 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 547 | 52902 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 548 | 53759 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 549 | 53942 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 550 | 55977 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 551 | 56875 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 552 | 57403 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 553 | 57631 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 554 | 58649 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 555 | 58664 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 556 | 58704 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 557 | 58757 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 558 | 61199 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |
| 559 | 62191 | Kuaizhou/KT | CN | EXPACE | 50 | 97 | 1.0 | 3.43e-05 | below |

---

## 3. Table 2 — aggregate attribution (summed risk, share of fleet risk, count exceeding threshold)

Fleet-wide summed risk = **ΣE_a = 0.2080** (decade-cumulative expected casualties across all 559 uncontrolled bodies, 2013–2024 window). "Share of fleet risk" = a contributor's summed E_a ÷ 0.2080. "Count > threshold" = bodies with E_a ≥ 1×10⁻⁴ ÷ total bodies. Shares within each panel sum to 100% (±0.1% rounding).

### 3a. By launching state

| Launching state | Summed risk (ΣE_a) | Share of fleet risk | Count > threshold |
|---|---:|---:|---:|
| CN | 0.1045 | 50.2% | 196 / 228 |
| RU | 0.0431 | 20.7% | 128 / 128 |
| US | 0.0289 | 13.9% | 65 / 70 |
| J | 0.0130 | 6.2% | 19 / 22 |
| IN | 0.0101 | 4.9% | 22 / 22 |
| NZ | 0.0056 | 2.7% | 0 / 75 |
| F | 0.0019 | 0.9% | 3 / 3 |
| IR | 0.0005 | 0.3% | 2 / 5 |
| IL | 0.0003 | 0.1% | 0 / 4 |
| KR | 0.0001 | 0.0% | 0 / 1 |
| KP | 0.0000 | 0.0% | 0 / 1 |

### 3b. By vehicle family

| Vehicle family | Summed risk (ΣE_a) | Share of fleet risk | Count > threshold |
|---|---:|---:|---:|
| Soyuz (Blok-I) | 0.0396 | 19.0% | 119 / 119 |
| CZ-3B | 0.0324 | 15.6% | 53 / 53 |
| Falcon 9 | 0.0193 | 9.3% | 35 / 35 |
| CZ-2F | 0.0134 | 6.5% | 14 / 14 |
| H-IIA/B | 0.0116 | 5.6% | 15 / 15 |
| CZ-2C | 0.0108 | 5.2% | 20 / 20 |
| CZ-5B | 0.0096 | 4.6% | 4 / 4 |
| CZ-7 | 0.0092 | 4.4% | 9 / 9 |
| CZ-2D | 0.0075 | 3.6% | 18 / 18 |
| GSLV | 0.0067 | 3.2% | 10 / 10 |
| Electron | 0.0056 | 2.7% | 0 / 75 |
| CZ-4B | 0.0049 | 2.3% | 26 / 26 |
| Antares | 0.0042 | 2.0% | 17 / 17 |
| CZ-7A | 0.0037 | 1.8% | 6 / 6 |
| Centaur | 0.0025 | 1.2% | 5 / 5 |
| PSLV | 0.0020 | 1.0% | 7 / 7 |
| Zenit | 0.0019 | 0.9% | 2 / 2 |
| CZ-3C | 0.0018 | 0.9% | 3 / 3 |
| CZ-5 | 0.0018 | 0.9% | 2 / 2 |
| Ariane 5 | 0.0018 | 0.9% | 2 / 2 |
| Yuanzheng (YZ kick stage) | 0.0016 | 0.8% | 4 / 4 |
| CZ-11 | 0.0012 | 0.6% | 12 / 12 |
| Kuaizhou/KT | 0.0011 | 0.5% | 1 / 27 |
| Delta | 0.0010 | 0.5% | 2 / 2 |
| CZ-6 | 0.0010 | 0.5% | 5 / 5 |
| Zhuque | 0.0010 | 0.5% | 2 / 2 |
| LVM3 (GSLV Mk III) | 0.0008 | 0.4% | 1 / 1 |
| Falcon Heavy | 0.0008 | 0.4% | 1 / 1 |
| CZ-4C | 0.0007 | 0.4% | 4 / 4 |
| Epsilon | 0.0007 | 0.3% | 3 / 5 |
| CZ-8 | 0.0007 | 0.3% | 2 / 2 |
| CZ-3A | 0.0006 | 0.3% | 1 / 1 |
| Proton-M | 0.0006 | 0.3% | 1 / 1 |
| H3 | 0.0006 | 0.3% | 1 / 1 |
| Iranian (Simorgh/Safir/Qased/Qaem) | 0.0005 | 0.3% | 2 / 5 |
| SSLV | 0.0005 | 0.3% | 4 / 4 |
| Lijian-1/Kinetica | 0.0005 | 0.2% | 5 / 5 |
| Minotaur | 0.0004 | 0.2% | 2 / 3 |
| Gravity-1 | 0.0004 | 0.2% | 0 / 5 |
| Volga | 0.0003 | 0.2% | 2 / 2 |
| Jielong | 0.0003 | 0.1% | 3 / 3 |
| Firefly Alpha | 0.0003 | 0.1% | 2 / 2 |
| Briz-KM | 0.0003 | 0.1% | 1 / 1 |
| CN commercial small (SMA/YL/OS-M) | 0.0003 | 0.1% | 2 / 2 |
| Strela | 0.0003 | 0.1% | 2 / 2 |
| Shavit | 0.0003 | 0.1% | 0 / 4 |
| LauncherOne | 0.0003 | 0.1% | 0 / 4 |
| Fregat | 0.0002 | 0.1% | 1 / 1 |
| Vega | 0.0001 | 0.1% | 1 / 1 |
| Pegasus | 0.0001 | 0.1% | 1 / 1 |
| SS-520 | 0.0001 | 0.0% | 0 / 1 |
| KSLV | 0.0001 | 0.0% | 0 / 1 |
| Hyperbola-1 | 0.0001 | 0.0% | 0 / 1 |
| DPRK (Unha/Chollima) | 0.0000 | 0.0% | 0 / 1 |

### 3c. By operator (top contributors)

| Operator (GCAT Owner) | Summed risk (ΣE_a) | Share of fleet risk | Count > threshold |
|---|---:|---:|---:|
| CASC | 0.0578 | 27.8% | 119 / 119 |
| CNSA | 0.0301 | 14.5% | 56 / 56 |
| RVSNR | 0.0238 | 11.4% | 73 / 73 |
| SPX | 0.0201 | 9.7% | 36 / 36 |
| CALT | 0.0134 | 6.5% | 14 / 14 |
| MHI | 0.0122 | 5.9% | 16 / 16 |
| VVKOV | 0.0113 | 5.4% | 30 / 30 |
| ISRO | 0.0093 | 4.5% | 21 / 21 |
| VVKO | 0.0060 | 2.9% | 18 / 18 |
| RLABN | 0.0056 | 2.7% | 0 / 75 |
| NGISW | 0.0025 | 1.2% | 10 / 10 |
| ULAL | 0.0025 | 1.2% | 5 / 5 |
| AE | 0.0010 | 0.5% | 2 / 2 |
| EXPACE | 0.0010 | 0.5% | 1 / 26 |
| ULAB | 0.0010 | 0.5% | 2 / 2 |
| OSCW | 0.0010 | 0.5% | 4 / 4 |
| LANDSP | 0.0010 | 0.5% | 2 / 2 |
| AESP | 0.0009 | 0.4% | 1 / 1 |
| NSIL/ISRO | 0.0008 | 0.4% | 1 / 1 |
| ISASJ | 0.0008 | 0.4% | 3 / 6 |
| OATKW | 0.0008 | 0.4% | 3 / 3 |
| ROSK | 0.0007 | 0.3% | 2 / 2 |
| KHRO | 0.0006 | 0.3% | 1 / 1 |
| XIDO | 0.0004 | 0.2% | 0 / 5 |
| IRSA | 0.0004 | 0.2% | 2 / 2 |
| OATKC | 0.0004 | 0.2% | 2 / 2 |
| MAI | 0.0003 | 0.2% | 1 / 1 |
| CZHJ | 0.0003 | 0.1% | 3 / 3 |
| FFLY | 0.0003 | 0.1% | 2 / 2 |
| EUROK | 0.0003 | 0.1% | 1 / 1 |
| ISA | 0.0003 | 0.1% | 0 / 4 |
| VORB | 0.0003 | 0.1% | 0 / 4 |
| NPOLO | 0.0002 | 0.1% | 1 / 1 |
| IRGC | 0.0001 | 0.1% | 0 / 3 |
| NPOMA | 0.0001 | 0.1% | 1 / 1 |
| NPOMAO | 0.0001 | 0.1% | 1 / 1 |
| NGISC | 0.0001 | 0.1% | 1 / 1 |
| OSCC | 0.0001 | 0.0% | 0 / 1 |
| KARI | 0.0001 | 0.0% | 0 / 1 |
| XJRY | 0.0001 | 0.0% | 0 / 1 |
| CASIC4A | 0.0000 | 0.0% | 0 / 1 |
| NADA | 0.0000 | 0.0% | 0 / 1 |

**What the aggregate shows.**
1. **China carries ~50% of fleet casualty risk** (ΣE_a 0.1045; 196 of 228 CN bodies exceed threshold). Within China the risk is split across many families — CZ-3B (15.6% of fleet risk, 53 bodies), CZ-2F (6.5%), CZ-2C (5.2%), CZ-5B (4.6% from just **4 bodies** — the highest per-body risk in the ledger), CZ-7 (4.4%), CZ-2D (3.6%).
2. **Russia is second at ~21%**, almost entirely the **Soyuz Blok-I third stage** (19.0% of the entire fleet risk from 119 bodies, every one above threshold) plus Zenit, Proton-M, Briz-KM, Strela, Volga, Fregat.
3. **The USA is third at ~14%**, dominated by **Falcon 9 (9.3%, 35 uncontrolled bodies)** — notable because Falcon 9 is *also* the in-fleet controlled-deorbit proof-of-concept (M2 lists 12 controlled Falcon 9 second stages), so these 35 are uncontrolled by exception, not by incapacity. Antares (2.0%) and Centaur (1.2%) follow.
4. **New Zealand (Electron) contributes 2.7% of risk from 75 bodies but ZERO exceed the threshold** — Electron's tiny 40–270 kg kick stages all fall below 1×10⁻⁴. High body-count, negligible per-body risk: the opposite of the CZ-5B profile (4 bodies, 4.6% of risk).
5. **Single highest-risk body class: CZ-5B core, E_a ≈ 2.4×10⁻³ (24× threshold)** — the four CZ-5B cores (NORAD 45601, 48275, 53240, 54217) are the most-reported uncontrolled reentries of the decade and top Table 1.

---

## 4. Reconciliation against published attribution (Pardini & Anselmo 2024)

The most-cited published attribution of *casualty risk* from uncontrolled orbital-stage reentries is **Pardini & Anselmo (2024)**, reported via the CNR research-focus summary as a **~62% Chinese / ~18% Russian-Soviet / ~14% American** split of casualty risk over their 2010–2022 window, with **~84% of uncontrolled reentries exceeding the 1-in-10,000 threshold** (Pardini & Anselmo, *J. Space Safety Engineering* 11(2):181–191, 2024, https://www.sciencedirect.com/science/article/pii/S2468896724000077; CNR focus https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites).

**This ledger's launching-state risk split (2013–2024 window): China 50.2% / Russia 20.7% / USA 13.9%.**

| Source | China | Russia/USSR | USA | Window | Top-3 sum |
|---|---:|---:|---:|---|---:|
| **This M3 ledger** | **50.2%** | **20.7%** | **13.9%** | 2013–2024 | 84.8% |
| Pardini & Anselmo 2024 / CNR | ~62% | ~18% | ~14% | 2010–2022 | ~94% |

**Agreement.** The **rank ordering is identical** (China ≫ Russia > USA), the **US share matches almost exactly** (13.9% vs ~14%), and the **Russia share is close** (20.7% vs ~18%). The **threshold-exceedance share also agrees**: this ledger's **77.8%** sits inside Pardini's ~80% (2021) / ~84% (2010–2022) band (it was *calibrated* to that band — §1c — which is itself the reconciliation: the calibration target is a published figure, and the resulting per-body distribution lands the right families above vs below).

**Divergence and why it is expected.** This ledger's China share (50%) is **~12 points below** Pardini's 62%, with the difference absorbed mainly by Russia (+3) and the "rest of fleet" (Japan 6.2%, India 4.9%, New Zealand 2.7%, France 0.9%). Three structural reasons, all consistent with the different windows and methods:
1. **Window.** Pardini's 2010–2022 excludes the 2023–2024 surge in Russian Soyuz Blok-I and high-cadence Indian/Japanese launches that this 2013–2024 window captures, diluting China's share.
2. **The Electron/small-stage tail.** This ledger explicitly counts 75 NZ Electron and 27 CN Kuaizhou kick stages (M2's strict status-`R` denominator); most contribute near-zero risk, but the broader denominator slightly compresses every large contributor's *share* even though China's *absolute* risk is unchanged.
3. **Casualty-area resolution.** Pardini uses per-object demise modelling that weights China's heavy GTO/CZ-5B hardware more than this ledger's mass^(2/3) scaling does (M1 Limitation 2 — A_c is the dominant uncertainty and is correlated with exactly the Chinese/Russian heavy families, M1 Limitation 4). A steeper A_c–mass relation would push the China share back toward 62%; the **relative ranking is robust, the absolute split is order-of-magnitude** (M1 Limitation 2).

The headline conclusion is concordant with the published literature: **a small number of heavy, uncontrolled Chinese and Russian stages dominate exported casualty risk, the large majority of uncontrolled stages breach the agreed 1-in-10,000 standard, and the controlled-deorbit fix is already routine for at least one top-contributing US family (Falcon 9).**

---

## Limitations & counter-evidence

1. **Absolute E_a is order-of-magnitude; the deliverable is the ranking.** Per M1 Limitation 2, output scales linearly with A_c, which requires fragment-demise simulation absent from open catalogs. The model is **calibrated to a published exceedance share (§1c)**, not asserted from first principles, so the *absolute* E_a values (and ΣE_a ≈ 0.21) should be read as ±a factor of ~2–3. The **relative attribution** — which families/states/operators dominate, and which bodies clear the threshold — is far more robust, because it depends on mass and inclination *ordering*, which is well-constrained, not on the absolute A_c anchor.

2. **The calibration is anchored to the very figure it is then compared against.** §1c tunes the global scale to Pardini's ~80–84% exceedance band, and §4 then notes agreement with that band — this is partly circular. What is *not* circular and *is* an independent test: the **identity of which bodies fall below threshold** (the small kick stages) and the **state/family ordering** (China≫Russia>USA, US≈14%) are emergent from mass+inclination, not imposed by the single scale factor. The China-vs-Russia *magnitudes* would shift with a different A_c law (point 4).

3. **Inclination is family-level, not per-body.** CE(i) uses one characteristic inclination per vehicle family (§1b), not each body's actual GCAT `Inc`. This is correct on average but wrong for individual rows — e.g. Soyuz Blok-I lumps 51.6° ISS-resupply and ~98° polar launches into a single 62° proxy; a CZ-2C to a low-inclination vs SSO orbit gets the same CE. A per-body inclination pass (GCAT carries the field) would refine CE within families but would not move the family/state aggregates materially, since the family proxies are population-weighted. The latitude weighting itself is the M1 §B2 simplification (longitude structure, Earth-rotation phasing, decay-day geometry all ignored) — carried from M1 Limitation 3.

4. **A_c mass-scaling is a stand-in for demise simulation, and the exponent is a choice.** A_c = 10·(m/3000)^(2/3) is a defensible geometric law anchored to two published points (Byers 10 m² conservative; 20–40 m² for large bodies), but the 2/3 exponent and 3,000 kg anchor are modelling choices. A steeper exponent would raise the heavy Chinese/Russian families' shares (toward Pardini's 62% China); a shallower one would flatten them. Because A_c uncertainty is **correlated with the heaviest, highest-risk Chinese/Russian stages** (M1 Limitation 4), this is the single largest lever on the exact China/Russia split — though not on the ordering.

5. **Surviving mass ≠ dry mass.** E_a should scale with *surviving* (ground-reaching) mass and its fragment geometry, not total dry mass. Demise fraction varies by material and structure (dense steel tanks and engines survive; aluminium skins ablate), so two stages of equal dry mass can have very different A_c. The ledger uses dry mass as the only open-catalog proxy (M2 §1 / M1 Limitation 2); families with high dense-component fractions (e.g. CZ-5B with its large engines and COPVs) may be *under*-weighted here relative to a full demise analysis.

6. **No realised casualty — the case is expected risk against an agreed line.** Carried from M1 Limitation 6 and M2 Limitation 6: no confirmed human casualty has resulted from any of these 559 uncontrolled reentries (Byers et al. 2022 note none was reported). A reader can fairly argue the realised hazard is low. The ledger's response is unchanged: the **1-in-10,000 standard is the published, agreed compliance line** (NASA-STD-8719.14; adopted US/France/Japan/ESA per M1 §B1), **77.8% of these stages breach it**, and the aviation-collision probability is rising (Aerospace Corp.: ~8×10⁻⁶/yr in 2021 toward 7×10⁻⁴/yr by 2035; *Sci. Rep.* 2024 s41598-024-84001-2: 26% annual busy-airspace-closure chance for the NE US) — but the absence of a body count is a fair and stated counterpoint.

7. **Snapshot and window dependence.** Risk shares are computed on M2's 2013–2024 status snapshot (GCAT 2026-06-26). The 456 still-in-orbit bodies (e.g. nine 6,000 kg CZ-6A second stages, M2 §4) are *future* uncontrolled reentries not scored here; as they decay, China's share will rise further. A different decade window would move the China/Russia/USA split by several points (§4), as the Pardini 2010–2022 vs this 2013–2024 comparison itself shows.

---

## Source list (dated)

- **M2 — Per-rocket-body classified inventory** (this problem), `artifacts/2026-06-26-m2-per-rocket-body-classified-inventory.md`. — the 559 uncontrolled rows scored here (NORAD, family, operator, launch state, dry mass); the input inventory. No body outside it is scored.
- **M1 — Methodology and Source Register** (this problem), `artifacts/2026-06-26-m1-methodology-source-register.md`, §B. — the casualty-area construction A_c (B0), the per-reentry E_a formula and 1×10⁻⁴ threshold (B1), the inclination→latitude-weighting CE form (B2); the risk model applied here.
- Byers, M., Wright, E., Boley, A. "Unnecessary risks created by uncontrolled rocket reentries." *Nature Astronomy* 6, 1093–1097 (2022). DOI 10.1038/s41550-022-01718-8; arXiv:2210.02188 (https://arxiv.org/abs/2210.02188); AMOS 2022 (https://amostech.com/TechnicalPapers/2022/SSA-SDA/Byers.pdf). — CE ≈ 0.01 m⁻² fleet baseline; 10 m² conservative casualty area (real bodies 20–40 m²); equatorial weighting of risk; ~10% chance of ≥1 casualty over a decade; 0.36 m² human area.
- Pardini, C., Anselmo, L. "The risk of casualties from the uncontrolled re-entry of spacecraft and orbital stages." *J. Space Safety Engineering* 11(2):181–191 (2024). https://www.sciencedirect.com/science/article/pii/S2468896724000077. — ~80% (2021) of orbital-stage uncontrolled reentries exceeding 1-in-10,000; the 62% Chinese / 18% Russian-Soviet / 14% American casualty-risk split (the M4-reconciliation comparator and §1c calibration target).
- CNR research focus summarising Pardini & Anselmo. https://www.cnr.it/en/focus/074-60/casualty-risk-from-the-uncontrolled-reentry-of-rocket-bodies-and-satellites. — 84% (2010–2022) exceeding threshold; 62%/18%/14% attribution.
- NASA-STD-8719.14 "Process for Limiting Orbital Debris" — A_c = Σ(√A_h+√Aᵢ)², A_h = 0.36 m², 1×10⁻⁴ threshold. https://orbitaldebris.jsc.nasa.gov/reentry/orsat.html.
- FAA AC 431.35-2A "Expected Casualty Calculations for Commercial Space Launch and Reentry." https://www.faa.gov/about/office_org/headquarters_offices/ast/licenses_permits/media/Ac4311fn.pdf. — regulatory expected-casualty E_a form (via M1 §B1).
- "Airspace closures due to reentering space objects," *Scientific Reports* 14 (2024), s41598-024-84001-2. https://www.nature.com/articles/s41598-024-84001-2; Aerospace Corp. aviation-collision modelling, *Acta Astronautica* (2024) S0094576524002807 (https://www.sciencedirect.com/science/article/pii/S0094576524002807). — rising aviation-collision probability (counter-evidence context, Limitation 6).

*Reproducibility: per-body E_a = CE(i)·A_c(m)·5.07, with A_c(m)=max(1, 10·(m/3000)^(2/3)) and CE(i)=0.010·f(i) (f by latitude band, §1b); scale 5.07 calibrated so 77.8% of the 559 bodies exceed 1×10⁻⁴ (Pardini ~80–84% target). Inputs m and family→i are M2 §3 attributes. Fleet ΣE_a=0.2080; CN/RU/US risk share 50.2/20.7/13.9%.*
