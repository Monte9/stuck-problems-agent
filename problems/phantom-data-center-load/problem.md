# Phantom data-center load: how much of the "AI grid crisis" is real?

## (a) The problem, in plain language

The United States is being told that AI will break the electric grid. Utilities
report tens of gigawatts of new data-center interconnection requests, capacity
auctions have exploded, and ratepayers are paying for it now. PJM's capacity
auction jumped from $2.2 billion for the 2024-25 delivery year to $16.4 billion
for 2027-28; retail prices rose 8.25% nationally year-over-year as of January
2026 and 19.35% in Virginia
([PowerMag, 2026](https://www.powermag.com/phantom-data-centers-didnt-break-the-power-grid-they-proved-it-was-already-broken/)).
The justification for new gas plants, transmission, and these price hikes is a
single forecast: roughly 5.7% annual demand growth through 2030, after two
decades below 1%.

But the request numbers may be largely fictional. CenterPoint's data-center
interconnection requests surged from 1 GW to 25 GW in twelve months. Exelon
states only **22% of its 65-GW pipeline through 2040 is likely to materialize**
([PowerMag, 2026](https://www.powermag.com/phantom-data-centers-didnt-break-the-power-grid-they-proved-it-was-already-broken/)).
A developer can file the same project in multiple utility territories, or
multiple times with one utility, because a queue position is cheap and powered
land is a tradeable asset
([WRI, 2025](https://www.wri.org/insights/us-data-centers-electricity-demand)).
The stakes: if utilities build generation against demand that never appears,
the stranded assets fall on existing customers, not on the data centers that
were never built.

## (b) State of the art

The headline forecasts (FERC, EPRI, grid operators) sum utility-reported
interconnection queues with little de-duplication. The skeptical case is
asserted anecdotally (Exelon's 22%, CenterPoint's 25x) but **nobody has
published a defensible national estimate of the phantom fraction.** The raw
material exists: LBNL's *Queued Up: 2025 Edition* aggregates cleaned queue data
from 50+ grid operators (~97% of US capacity) and finds only 13% of 2000-2019
generation requests ever reached operation; 77% were withdrawn
([LBNL, 2025](https://emp.lbl.gov/publications/queued-2025-edition-characteristics)).
State PUC dockets, utility integrated resource plans, and RTO large-load queues
contain project-level requests that can be cross-matched.

## (c) Why it is stuck/unanswered

Incentives point the wrong way. Utilities earn a regulated return on capital
they build, so over-forecasting demand is profitable, not penalized. Developers
benefit from queue inflation. No actor owns the de-duplicated number, and the
data is fragmented across dozens of jurisdictions with inconsistent formats.
Meanwhile FERC ended the single national interconnection standard in 2026 and
ordered each RTO to write its own large-load rules
([Utility Dive, 2026](https://www.utilitydive.com/news/ferc-doe-data-center-interconnection/823360/)),
so the cost-allocation fight is being decided right now, on contested numbers.

## (d) The AI-agent wedge

A model running unsupervised can build the first **bottom-up reconciliation of
announced vs. real data-center load**: ingest LBNL queue data, RTO large-load
interconnection reports, state IRP filings, and developer announcements;
flag duplicate filings (same parcel/developer across territories), projects
lacking site control or signed offtake, and capacity double-counted between
"announced" and "under construction" (Sightline tracked 12 GW announced vs.
5 GW building for 2026). Output: a defensible phantom-fraction range, by RTO,
with the implied over-build in GW and the ratepayer cost exposure. That is a
falsifiable number nobody has computed.

## (e) Who is closest

LBNL's Berkeley Lab queue team (Joseph Rand, Ryan Wiser) has the cleanest data
but does not isolate phantom data-center load. RMI and the Brattle Group analyze
interconnection reform; WRI and the Southern Environmental Law Center
([SELC, 2025](https://www.selc.org/news/experts-say-data-center-growth-is-speculative/))
argue the growth is speculative but stop short of a national estimate. FERC,
PJM, ERCOT, and state PUCs are the decision-makers who would act on the artifact
within the next year as they write large-load rules and rule on IRP approvals.
