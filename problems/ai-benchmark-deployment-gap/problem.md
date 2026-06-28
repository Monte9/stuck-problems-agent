# Problem: the AI-benchmark-to-deployment gap (the leaderboards that price frontier AI overstate what gets deployed)

> Intake brief from the scout routine, 2026-06-28. Category: AI (frontier, operator's #1 lane).
> Shape: the teardown — a hyped capability claim the evidence does not support. The win is deflating an inflated number that a named buyer is about to write into a procurement standard, not starting a fix.

## (a) The problem, in plain language

Public benchmarks — SWE-bench, GPQA, MMLU, the math sets — are the currency that prices frontier AI. Vendors report them in launch posts, investors underwrite valuations on them, and federal buyers are now wiring them into procurement. The claim under audit: those headline scores systematically overstate what the same model does on real, unseen work, and nobody has published a defensible, per-benchmark estimate of the size of that overstatement.

The stakes are large and concrete. The U.S. General Services Administration and NIST's Center for AI Standards and Innovation (CAISI) signed an MOU in March 2026 to "select and interpret benchmarks" for federal AI procurement through the USAi platform ([NIST, 2026](https://www.nist.gov/news-events/news/2026/03/caisi-signs-mou-gsa-boost-ai-evaluation-science-federal-procurement-through)), and NIST itself concedes "well-defined, universal AI tests do not exist yet" ([FedScoop, 2026](https://fedscoop.com/gsa-nist-evaluate-ai-before-agency-deployments-caisi/)). Meanwhile MIT's NANDA initiative found [95% of enterprise GenAI pilots deliver no measurable P&L impact](https://fortune.com/2025/08/18/mit-report-95-percent-generative-ai-pilots-at-companies-failing-cfo/), and Gartner projects [over 40% of agentic-AI projects cancelled by end-2027](https://fortune.com/2025/08/18/mit-report-95-percent-generative-ai-pilots-at-companies-failing-cfo/). Billions in procurement and capex are being allocated against numbers whose deployment validity is unquantified.

## (b) State of the art

The gap is documented in fragments, never assembled. On private, previously-unseen codebases, Claude Opus 4.1 drops from 22.7% to 17.8% and GPT-5 from 23.1% to 14.9% ([SWE-Bench Pro](https://arxiv.org/pdf/2509.16941)); GPT-5.2 falls from 72.8% on SWE-bench Verified to 22.9% on the longer-horizon SWE-EVO ([SWE-EVO, 2025](https://arxiv.org/html/2512.18470v6)). OpenAI itself stopped reporting SWE-bench Verified, finding 59.4% of hard tasks had flawed tests ([OpenAI, 2026](https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/)). Removing contaminated items from GSM8K cut some models' accuracy up to 13% ([contamination survey](https://arxiv.org/html/2601.04301)); audits find leakage of 1-45% across QA benchmarks. PR-acceptance rates run 50-60% below SWE-bench scores ([Presenc, 2026](https://presenc.ai/research/coding-agent-benchmarks-2026)). Each is a single data point; no one has built the cross-benchmark ledger that turns them into a usable reliability discount.

## (c) Why it is stuck/unanswered

Incentives all point toward the inflated number. Vendors pick the scaffold and split that flatter them; investors want the score to rise; conference leaderboards reward saturation. The skeptical work is scattered across arXiv preprints in incompatible formats, and the buyer who most needs the synthesis — CAISI/GSA — is standing up its methodology right now without it. This is a teardown, not a fix: the contribution is the documented inversion, not a new benchmark.

## (d) The AI-agent wedge

A model running unsupervised can build the missing artifact: a reproducible, per-benchmark **deployment-validity ledger**. Ingest published vendor scores, independent re-runs, contamination audits, and private-holdout results; for each major benchmark estimate (i) the contamination/recall fraction, (ii) the controlled score drop from public-to-private and short-to-long-horizon variants, and (iii) the implied "procurement discount" — the haircut a buyer should apply to a headline score before trusting it. Output: a ranked table of which benchmarks survive contamination and which are functionally noise, with a falsifiable discount range per model family. That is precisely the document CAISI says does not exist.

## (e) Who is closest

CAISI/NIST and GSA (the buyers writing the federal eval standard, March-May 2026 [pre-deployment agreements](https://www.nist.gov/news-events/news/2026/03/caisi-signs-mou-gsa-boost-ai-evaluation-science-federal-procurement-through) with five labs); LiveBench / LiveCodeBench / FrontierMath teams (contamination-resistant designs); academic contamination auditors ([arXiv 2601.04301](https://arxiv.org/html/2601.04301)); and Epoch AI / Scale (SWE-Bench Pro leaderboard). Each holds a piece; none has published the synthesized procurement-grade discount.
