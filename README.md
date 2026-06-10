# stuck-problems-agent

An autonomous research loop for important-but-stuck problems, operated by a scheduled Claude Code routine. The routine is the loop; this repo is the policy, the assets, and the memory.

- **`CLAUDE.md`** — the doctrine: one phase per run, decided by a state-machine table
- **`.claude/agents/`** — planner (brief → spec), generator (one milestone → one artifact), evaluator (fresh-eyes pass/fail)
- **`.claude/skills/`** — the asset library, extracted from successful manual sessions
- **`problems/<name>/`** — `problem.md` (intake), `spec.md` (plan), `state.md` (memory/cursor), `artifacts/`, `verdicts/`

## How a problem flows

1. Scout routine surfaces a brief. Paste it into `problems/<name>/problem.md` and push.
2. Next run: the **planner** writes `spec.md` with milestones and done-criteria, commits `[spec]`. No approval step. The loop continues on its own.
3. Runs alternate **generate → evaluate**, one phase every 4 hours. PASS advances the milestone. FAIL retries once with the critique attached. A second FAIL blocks the problem and DMs you.
4. All milestones pass → `status: complete`. The final artifacts are the deliverable.

## Your jobs (and nothing else)

- **Unblock** — when a commit says `[blocked]`, read the verdict, fix the spec/rubric/state, push.
- **Weekly 15-minute audit** — the quality backstop now that no human reviews specs. Read two randomly chosen **PASS** artifacts. If one makes you wince, the fix goes into the evaluator rubric (versioned in `evaluator.md`). You're auditing the judge, not the work.
- **Extract skills** — when the log shows repeated freeform work, do it once by hand, extract a SKILL.md.

Everything else runs without you. Watch the commit log: `[blocked]` needs you; `[spec]`, `[milestone]`, and `[run]` don't.
