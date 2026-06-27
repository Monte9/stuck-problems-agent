# When both satellites swerve: the missing rulebook for on-orbit collision avoidance

## (a) The problem in plain language

Low Earth orbit now runs on a coordination system held together by email. When two
active, maneuverable satellites from different operators are predicted to pass
dangerously close, there is no binding rule for which one moves, when, or which way.
Starlink alone performed **144,404 collision-avoidance maneuvers between 1 Dec 2024 and
31 May 2025** — one maneuver every 1.8 minutes across the constellation, ~41 per
satellite per year — and the full-year 2025 figure was roughly **300,000, a 50% jump on
2024**, projected toward **1 million per year by 2027** ([SpaceX semiannual report via
FODNews/KeepTrack, 2026](https://keeptrack.space/x-report/spacex-brief-2026-04-01);
[Euronews, Jan 2026](https://www.euronews.com/next/2026/01/03/spacex-to-lower-thousands-of-starlink-satellites-in-2026-as-collisions-rise-company-says)).
The buried danger: when both operators maneuver independently without coordination, the
maneuvers can **increase** post-maneuver collision probability rather than reduce it —
two cars swerving the same way ([arXiv 2512.09643, *An Orbital House of Cards*, Dec
2025](https://arxiv.org/pdf/2512.09643); [Office of Space Commerce roadmap docs](https://space.commerce.gov/traffic-coordination-system-for-space-tracss/)).

## (b) State of the art / the gap

The capability that exists: conjunction screening. The US **Traffic Coordination System
for Space (TraCSS)** went live with initial capabilities in 2025 and began onboarding
operators and foreign governments in early 2026, issuing conjunction data messages
(CDMs). The capability that does **not** exist: an operator-to-operator deconfliction
layer that decides who maneuvers. That layer is on the TraCSS roadmap but is **not a
production service** ([Office of Space Commerce](https://space.commerce.gov/category/tracss/)).
Today coordination "is done through exchanging emails" — too slow and unscalable per
Secure World Foundation's Ian Christensen ([SpaceNews](https://spacenews.com/in-space-traffic-coordination-the-biggest-challenge-may-be-coordination/)).
Competing rule proposals exist but none is adopted: NASA guidance says transiting craft
yield to on-station craft; SpaceX proposes orbit-raising satellites move around
established ones; academic work shows a "lighter satellite maneuvers" rule is more
fuel-efficient and equitable ([ScienceDirect, norms of behavior, 2023](https://www.sciencedirect.com/science/article/abs/pii/S2468896723001374)).

## (c) Why it is stuck

Not capability — incentives and the absence of a chosen rule. Each operator rationally
prioritizes its own fleet's safety and fuel, so no one yields by default. The
distributional stakes (whose fuel, whose risk) make a rule politically hard, and the
counterintuitive failure mode (coordinated-looking maneuvers that worsen risk) is
poorly quantified, so regulators lack the number that would force a choice. The UN has
been pulled in on coordination disputes at least twice.

## (d) The AI-agent wedge — the missing artifact

A model running unsupervised can build the **first public quantitative comparison of
candidate right-of-way rules** against real conjunction data: take published TLE / CDM
statistics and the *Orbital House of Cards* close-approach rates, simulate the four
proposed rules (transiting-yields, lighter-maneuvers, mass-weighted, status-quo
ad-hoc), and estimate for each: total maneuvers required, fuel burden distribution
across operators, and — the inversion — the rate at which uncoordinated dual maneuvers
*increase* collision probability. The deliverable is a scored rulebook the Office of
Space Commerce could hand to its TraCSS coordination working group: which rule, by how
much, who pays. That is homework nobody has published.

## (e) Who is closest

**Office of Space Commerce / TraCSS** (the named decision-maker for the US rule).
**Kayhan Space**, building an automated bilateral "operative agreement" framework that
negotiates who maneuvers in seconds — but it encodes whatever rule it is given; the rule
itself is undecided. **Secure World Foundation** and the **arXiv "Orbital House of
Cards" authors** (UT Austin / Slingshot-adjacent) are framing the instability. **ESA**
is automating its own avoidance. The gap they all leave open: the costed,
data-grounded comparison that says which rule to adopt.
