# stuck-problems-agent

An autonomous research loop for important-but-stuck problems, operated by a scheduled Claude Code routine. The routine is the loop; this repo is the policy, the assets, and the memory.

- **`CLAUDE.md`** — the doctrine: one phase per run, decided by a state-machine table
- **`.claude/agents/`** — planner (brief → spec), generator (one milestone → one artifact), evaluator (fresh-eyes pass/fail)
- **`.claude/skills/`** — the asset library, extracted from successful manual sessions
- **`problems/<name>/`** — `problem.md` (intake), `spec.md` (plan), `state.md` (memory/cursor), `artifacts/`, `verdicts/`

## How a problem flows

1. When nothing is active, the loop scouts a new stuck problem itself and writes the brief (`[scout]`). One problem at a time, in sequence. You can also add a brief by hand to `problems/<name>/problem.md`.
2. Next run: the **planner** writes `spec.md` with milestones and done-criteria, commits `[spec]`. No approval step. The loop continues on its own.
3. Runs alternate **generate → evaluate**, one phase per hour. PASS advances the milestone. FAIL retries once with the critique attached. A second FAIL blocks the problem and DMs you.
4. All milestones pass → the **publisher** drafts `report.md` and `tweet.md`, adds the problem to the table below, and DMs you. Publishing to the outside world stays human: you review and post.
5. The problem is `published`; the next wake scouts a fresh one. The loop never idles.

## Your jobs (and nothing else)

- **Post the publications** — when a DM says `[published]`, review `report.md` and `tweet.md`, then post them.
- **Unblock** — when a commit says `[blocked]`, read the verdict, fix the spec/rubric/state, push.
- **Weekly 15-minute audit** — the quality backstop now that no human reviews specs. Read two randomly chosen **PASS** artifacts. If one makes you wince, the fix goes into the evaluator rubric (versioned in `evaluator.md`). You're auditing the judge, not the work. Extract a SKILL.md when the log shows repeated freeform work.

Everything else runs without you. Watch the commit log: `[blocked]` needs you, `[published]` is your cue to post; the rest is the loop talking to itself.

## Problems

| Problem | Status | Result |
|---------|--------|--------|
| [lead-poisoning](problems/lead-poisoning/) | published | Indonesia's top-ranked target already bans informal battery smelting, yet ~5 licensed smelters coexist with 200+ illegal ones and 47% of children near Jakarta recyclers have elevated blood lead; the missing piece is a $150-350k enforcement map. [report](problems/lead-poisoning/report.md) · [final artifact](problems/lead-poisoning/artifacts/2026-06-10-m5-funder-brief.md) |
| [cbt-insomnia-undertreatment](problems/cbt-insomnia-undertreatment/) | published | Untreated chronic insomnia costs ~$92M per 100,000 US adults per year ($17M–$146M), and Medicare's 2025 digital CBT-I coverage is nominal (the device code has no published fee); a five-action payer dossier shows the cheapest fix is a mailed deprescribing package proven to triple hypnotic discontinuation (26.2% vs 7.5%). [report](problems/cbt-insomnia-undertreatment/report.md) · [final artifact](problems/cbt-insomnia-undertreatment/artifacts/2026-06-11-m4-payer-formulary-action-dossier.md) |
