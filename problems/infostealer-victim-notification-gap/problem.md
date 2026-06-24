# The infostealer notification gap: billions of stolen logins, almost nobody told

> Intake brief from the scout routine, 2026-06-24. Category: technology and society.
> Bottleneck type: misaligned incentives plus sheer grind — the data sits indexed, but no one is obligated or staffed to tell the individual victim.

**(a) The problem, in plain language.** Infostealer malware silently siphons saved
passwords, session cookies, and autofill data off ordinary people's personal
laptops and phones, usually delivered through cracked software, fake installers,
or malicious browser extensions. The scale is now industrial: infostealers took
**1.8 billion credentials from 5.8 million infected devices in 2025 alone, an 800%
year-over-year jump, ~87 credentials per device**
([DeepStrike 2025](https://deepstrike.io/blog/stealer-log-statistics-2025)). The
harvested logins flow into criminal marketplaces and power downstream fraud:
account takeover losses are projected at **$17 billion in 2025**
([Sift Q3 2025](https://sift.com/index-reports-account-takeover-fraud-q3-2025/)),
and Verizon found **54% of ransomware victims had domain credentials in stealer-log
marketplaces before the attack** — the exposure was detectable, the breach was the
consequence of nobody acting
([CNBC 2025](https://www.cnbc.com/2025/06/26/experts-sound-alarm-on-infostealer-malware-after-login-details-exposed.html)).
The human cost lands on individuals who never learn their own machine is leaking.

**(b) The half-known solution.** The fix is not invention — it is notification plus
forced credential rotation, and it is proven cheap. Have I Been Pwned has indexed
stealer logs and now holds **~2 billion unique exposed email addresses**
([Troy Hunt, Nov 2025](https://www.troyhunt.com/2-billion-email-addresses-were-exposed-and-we-indexed-them-all-in-have-i-been-pwned/));
the Dutch police's *Check je Hack* / *CheckYourHack* portal lets victims confirm
infection after takedowns
([Operation Endgame](https://www.operation-endgame.com/news/)). Google and Apple
password managers already surface "this password appeared in a breach." The
mechanism works. The dramatic inversion: the stolen-login data is *already
aggregated and searchable*, yet the person whose device is bleeding it is the last
to know — if they ever find out at all.

**(c) Why it's stuck.** US state breach-notification statutes trigger only when an
organization "owns or licenses" the breached data
([IAPP 50-state chart](https://iapp.org/resources/article/state-data-breach-notification-chart)).
When the breach is the *individual's own device*, no organization owns the incident,
so no entity is legally obligated to notify the victim. Notification today is
reactive, episodic (per law-enforcement takedown), and opt-in: the victim must
already know to check a website they've never heard of. This is Semmelweis-shaped —
the evidence is indexed and free, but the actors who could push it are not the ones
who bear the cost of staying silent.

**(d) The AI-agent wedge.** Desk-research over public regulatory and threat-intel
sources, producing the artifact no one has assembled. Concretely: (1) a 50-state
map of exactly where breach-notification law fails to reach device-level infostealer
victims, with the precise statutory "owns or licenses" language quoted per state;
(2) a quantified cost-of-silence figure tying device-infection volumes to downstream
ATO and ransomware losses; (3) a concrete, build-ready notification-pathway
specification — which existing datasets (HIBP, Spamhaus, DIVD, Operation Endgame)
could feed a default-on consumer alert, which actor (ISP, browser vendor, FTC) is
best positioned to deliver it, and the minimal legal change to authorize it. No new
data collection required; the gap is synthesis and a falsifiable design.

**(e) Who's closest today.** Troy Hunt / Have I Been Pwned (indexing), the Dutch
DIVD CSIRT and Politie (*Check je Hack*), Europol's Operation Endgame partners
(1,025 servers seized Nov 2025
[Infosecurity](https://www.infosecurity-magazine.com/news/operation-endgame-3-dismantles/)),
Spamhaus, and Shadowserver run the plumbing. The FTC and state attorneys general
hold the regulatory levers. What's missing is the document that converts "the data
exists" into "the victim is told by default" — and that document is the wedge.
