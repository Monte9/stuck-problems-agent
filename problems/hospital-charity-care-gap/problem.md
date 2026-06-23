# Charity care that nonprofit hospitals are legally required to give — and mostly don't

> Intake brief from the scout routine, 2026-06-23. Category: economics and inequality.
> Bottleneck type: misaligned incentives (collecting the bill pays better than waiving it) compounded by application-friction grind, against a federal mandate that has been law since 2014 and is barely enforced.

## The problem, in plain language

Every US nonprofit hospital is legally required to run a written financial assistance
policy (FAP) and give free or discounted care to patients below an income threshold. It
mostly isn't happening. Patients are billed roughly **$14 billion a year for care that
should have been written off** as charity care, and **only about 29% of eligible patients
actually receive the assistance they qualify for** — meaning 71% are billed anyway
([Dollar For, "Bridging the Chasm," 2024](https://dollarfor.org/wp-content/uploads/2024/04/Dollar_For.Bridging_the_Chasm.pdf)).
A national survey found **53% of adults don't know hospital financial assistance even
exists**, and 52% never got told about it by their hospital
([Breez Health, 2024](https://www.prnewswire.com/news-releases/more-than-half-of-americans-are-unaware-of-hospital-financial-assistance-programs-finds-survey-from-breez-health-302005479.html)).

The human cost lands as debt. Americans hold at least **$220 billion in medical debt**;
about 14 million people owe more than $1,000 and 3 million owe more than $10,000
([KFF, 2024](https://www.kff.org/health-costs/the-burden-of-medical-debt-in-the-united-states/)).
People with medical debt cut spending on food and clothing, drain savings, and file for
bankruptcy. A large share of that debt is owed by people who were *entitled to free care
at the moment of treatment* and never got screened for it.

## The half-known solution

The fix is **presumptive eligibility**: instead of forcing a sick patient to find,
complete, and document a means-tested application, the hospital screens automatically
against data it can already see (enrollment in Medicaid/SNAP/WIC, homelessness, public
estimators of household income) and grants assistance without an application. It is proven
and cheap. Dollar For's modeling shows hospitals could cover **every eligible patient with
a 0.7% drop in revenue** ([Dollar For "Bottom Line" report](https://dollarfor.org/press/bottom-line-report-press-release/)).
North Carolina made it mandatory: as of Jan 1 2025 hospitals must auto-qualify Medicaid/
SNAP/WIC/homeless patients, and by Jan 1 2026 must run full presumptive screening with no
application ([NC Health News, 2024](https://www.northcarolinahealthnews.org/2024/08/13/nc-medical-debt-relief-plan-11-hospitalmust-dos-for-hospitals/)).
Vendors already sell the screening tech ([HFMA, 2025](https://www.hfma.org/revenue-cycle/charity-care/hospitals-implement-charity-care-screenings/)).

## Why it's stuck

The Semmelweis pattern: the law (IRC **Section 501(r)**, in force since 2014) and the data
both exist, but adoption doesn't follow. Three reasons. (1) **Incentives invert** — a bill
sent to collections can be sold or recovered; a waived bill is pure forgone revenue, so the
rational hospital under-screens. (2) **Enforcement is near-zero** — the ultimate 501(r)
penalty is revocation of tax-exempt status, a nuclear option the IRS almost never uses; in
2024 it announced audits of just **35 hospital organizations** out of ~2,900
([Nixon Peabody, 2025](https://www.nixonpeabody.com/insights/alerts/2025/03/18/revisiting-section-501r-compliance-in-2025)).
(3) **Friction is the policy** — FAPs are buried, application-only, and written to deter,
so the gap persists by design.

## The AI-agent desk-research wedge

This is unusually tractable for an unsupervised model because the raw material is public
text. Every 501(r) hospital must post its FAP and a Plain Language Summary, and must file
**Form 990 Schedule H** quantifying charity care. An agent can, over hours: (a) pull and
parse FAPs and Plain Language Summaries for a defined set of hospitals; (b) score each on
machine-readable criteria a regulator already cares about (Is presumptive eligibility
offered? Is the income threshold at/above 200% FPL? Is the summary actually plain-language?
Is the form online or application-gated?); (c) cross-reference Schedule H charity-care
spending against the hospital's revenue to flag systems billing far below peers; and (d)
produce a ranked **non-compliance / inaccessibility scorecard** naming specific hospitals.
That scorecard is the missing artifact: state AGs, the IRS TE/GE division, and advocacy
groups can act on a named list, not on an aggregate statistic.

## Who's closest today

**Dollar For** (patient-facing FAP navigation + the best national estimates), the **Lown
Institute** (hospital fair-share scoring), the **CFPB** (2024 medical-debt and FAP
research, though its enforcement footing is now uncertain), and **North Carolina's** HASP
program (the one jurisdiction mandating presumptive eligibility). What none has published
is a comprehensive, hospital-by-hospital, FAP-text-level compliance map — which is exactly
the desk-research artifact this loop can build.
