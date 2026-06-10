# stuck-problems-agent — loop doctrine

This repo is operated by a scheduled Claude Code routine. Each run executes **exactly one phase** of the cycle, then commits, pushes, and stops. The schedule is the outer loop — do not chain phases.

## Hard rules (non-negotiable)

1. **Commit and push at the end of every run that changed any file.** Routine runs are ephemeral. Un-pushed state is lost, the next run starts from stale state, and the memory model of this whole system collapses. If `git push` fails, retry once with `git pull --rebase` first; if it still fails, end the run by stating loudly that state was NOT persisted.
2. **One phase per run.** Plan, generate, evaluate, publish, or scout — never more than one. Small, cheap, reviewable runs are the design, not a limitation.
3. **Fully autonomous between exceptions.** No phase waits for human input. The only halt is `status: blocked` after two failed attempts on a milestone; a human clears it by editing state.md and pushing.
4. **Two attempts max per milestone.** After a second FAIL verdict on the same milestone, set `status: blocked` and stop touching that problem. No infinite retry loops.
5. **The evaluator gets fresh eyes.** Invoke it as a subagent whose prompt contains only: the milestone's done-criteria (quoted), the artifact path, and the verdict path to write. Never include generator reasoning, run history, or your own opinion of the artifact.
6. **Only the orchestrator (you, the main loop) edits `state.md`.** Subagents never touch it.

## The cycle — decision table

Read every `problems/*/state.md`. Pick the active problem: status not `published`, `blocked`, or `dropped`; if several qualify, the one least recently run. If no problem qualifies, row 5 is the match. Then execute the **first matching row** and stop:

(`dropped` is the human veto: the operator can set `status: dropped` on any problem at any time, and the loop moves on at the next wake. No phase ever waits for permission, but every problem can be killed with a one-line edit.)

| # | Condition | Action |
|---|-----------|--------|
| 0 | `problem.md` still contains the string `PLACEHOLDER` | Exit. No brief yet, nothing to do. |
| 1 | No `spec.md` | Run the **planner** subagent → it writes `spec.md`. Set `status: in_progress`, `current_milestone: 1`. Commit `[spec]`. |
| 2 | `status: in_progress` | Run the **generator** subagent on the current milestone. If `attempt > 0`, include the path to the latest FAIL verdict in its prompt. It writes one artifact to `artifacts/`. Set `status: awaiting_review`. |
| 3 | `status: awaiting_review` | Run the **evaluator** subagent → it writes a verdict to `verdicts/`. Route on the verdict:<br>**PASS** → advance `current_milestone`, reset `attempt: 0`, set `status: in_progress` (or `complete` if it was the last milestone). Notify milestone done.<br>**FAIL** → increment `attempt`. If `attempt >= 2` → `status: blocked`, notify. Else `status: in_progress`. |
| 4 | `status: complete` | Run the **publisher** subagent → it writes `report.md` and `tweet.md` in the problem directory and adds the problem to the README's Problems table. Set `status: published`. Commit `[published]`, Slack DM the user (they post it; publishing to the outside world stays human). |
| 5 | No active problem (everything `published`, `blocked`, or `dropped`) | Run the **scout** subagent → it researches a slate of 3-5 candidates, scores them against `PREFERENCES.md`, and writes the full brief for the winner to `problems/<kebab-slug>/problem.md`. Create a fresh `state.md` (`status: no_spec`, milestone 0, empty run log). Commit `[scout]` with the scored slate in the commit body. The next run plans it. |

After the action: update `state.md` (status, cursor, attempt, run-log entry with today's date), then commit and push.

## File conventions

- Artifacts: `artifacts/YYYY-MM-DD-m<N>-<slug>.md` (N = milestone number)
- Verdicts: `verdicts/YYYY-MM-DD-m<N>-attempt<K>.md`
- `state.md` run log: newest entry first, one line per run, including "woke and exited" runs.

## Notification protocol

The commit message is the durable notification channel. Prefixes:

- `[spec] <problem>: spec created (M1–M<N>)` — planner finished, loop continues on its own
- `[blocked] <problem> M<N>: failed evaluation twice` — needs a human
- `[milestone] <problem> M<N>: passed` — FYI, no action needed
- `[published] <problem>: report + tweet drafts ready` — the user reviews and posts; the loop moves on regardless
- `[scout] <problem>: new problem sourced` — FYI, new problem entering the loop
- `[run] <problem>: <one-line summary>` — everything else, including no-op wakes (no-op wakes don't commit; just report in run output)

If a Slack tool is available in this run's environment, additionally send `[blocked]` and `[published]` messages as a DM to the user. Everything else stays in the commit log. If no Slack tool is available, skip silently — never fail a run over a notification.

## Skills

Before generating, check `.claude/skills/` for a skill matching the milestone's task and follow it if found. Skills are extracted from completed manual sessions, never written from imagination — see `.claude/skills/README.md`. If the loop repeatedly needs a skill that doesn't exist, say so in the run log; that's the signal for the human to extract one.
