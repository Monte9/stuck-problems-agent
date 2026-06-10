# stuck-problems-agent

An autonomous research loop for important-but-stuck problems, operated by a scheduled Claude Code routine. The routine is the loop; this repo is the policy, the assets, and the memory.

- **`CLAUDE.md`** — the doctrine: one phase per run, decided by a state-machine table
- **`.claude/agents/`** — planner (brief → spec), generator (one milestone → one artifact), evaluator (fresh-eyes pass/fail)
- **`.claude/skills/`** — the asset library, extracted from successful manual sessions
- **`problems/<name>/`** — `problem.md` (intake), `spec.md` (plan), `state.md` (memory/cursor), `artifacts/`, `verdicts/`

## How a problem flows

1. Scout routine surfaces a brief → you paste it into `problems/<name>/problem.md`, push.
2. Next run: **planner** writes `spec.md`, sets `awaiting_spec_approval`, halts. Runs keep waking and exiting until you act.
3. **You approve** by editing one line in `state.md` — `spec_approved: false` → `true` — and pushing. This is the one human gate in the system.
4. Runs alternate **generate → evaluate**, one phase per day. PASS advances the milestone; FAIL retries once with the critique attached; a second FAIL blocks the problem and pings you.
5. All milestones pass → `status: complete`. The final artifacts are the deliverable.

## Your jobs (and nothing else)

- **Approve specs** — a bad spec poisons every downstream run; this gate stays.
- **Unblock** — when a commit says `[blocked]`, read the verdict, fix the spec/rubric/state, push.
- **Weekly 15-minute audit** — read two randomly chosen **PASS** artifacts. If one makes you wince, the fix goes into the evaluator rubric (it's versioned in `evaluator.md`). You're auditing the judge, not the work.
- **Extract skills** — when the log shows repeated freeform work, do it once by hand, extract a SKILL.md.

Everything else runs silent. Watch the commit log: `[needs-approval]` and `[blocked]` need you; `[milestone]` and `[run]` don't.
