# Improving this system

Operating context for a development agent working ON this repo (not running it). The scheduled routine runs the loop hourly on its own; your job is to make it better. Monte prompts from his phone, so keep replies tight, propose concrete diffs, and act on reversible changes instead of asking permission. Where this file and the repo disagree, trust the repo.

**This is a living document. Append dated notes to the log at the bottom as you learn things, decide things, or rule things out.** Future sessions read it cold.

## Orient yourself first

Read in order: `CLAUDE.md` (loop doctrine), `PREFERENCES.md` (problem-selection taste), `.claude/agents/*.md` (the five roles), one recent `problems/*/report.md` (sample output), and `git log --oneline -30`. Each `problems/<slug>/state.md` is that problem's memory. Live state (what is published, what is in flight) lives in `README.md`'s Problems table and the git log; this file does not track it.

## What this system is

A repo a scheduled Claude Code routine points at. No orchestration code. The routine is a bootloader: each hourly run reads `CLAUDE.md`, executes exactly ONE phase of a decision table, commits, pushes, exits. The schedule is the outer loop.

- The repo IS the agent: `CLAUDE.md` = policy, `state.md` = memory, the git log = audit trail.
- Five roles (subagents in `.claude/agents/`): scout (source a new problem) → planner (milestone spec) → generator (one milestone) → evaluator (fresh-eyes pass/fail) → publisher (writes `report.md` + `tweet.md`; posting stays human).
- Lifecycle via `status` in state.md: no_spec → in_progress → awaiting_review → (milestones loop) → complete → published. Plus `blocked` (two failed evals) and `dropped` (human veto, a one-line edit).

## Invariants — do NOT undo these without Monte's explicit say-so

Undoing a deliberate decision while calling it an improvement is the main failure mode.

1. One phase per run. Never chain phases.
2. Fully autonomous. No human approval gate (removed on purpose). Only halt is `blocked`. Do not reintroduce gates.
3. Commit AND push every run that changed a file. Runs are ephemeral; unpushed state is lost. Hard rule #1.
4. Evaluator gets fresh eyes: only done-criteria, artifact path, verdict path. Never the generator's reasoning.
5. Two-attempt cap per milestone, then block.
6. Selection is taste (`PREFERENCES.md`), evaluation is rigor (evaluator rubric). Improve them by editing those files, never by adding a human to the loop.
7. Publishing to the world stays human. Publisher drafts; Monte posts.
8. Start simple. Earn complexity from observed failure, not imagination.

## How to change things safely

- Most improvements are repo edits (`CLAUDE.md`, agent prompts, `PREFERENCES.md`, evaluator rubric). Edit, commit, push. Every run clones fresh, so changes take effect next wake. No deploy step.
- Always `git pull --rebase` before editing; the loop pushes hourly and will conflict.
- Test a doctrine/agent change by pushing it and watching the next commit on `main`.
- Routine CONFIG (model, cron, connectors) is NOT in the repo; it lives in the claude.ai routine, set via its API/UI. If you cannot reach it, propose the change and Monte applies it. Trigger id `trig_01GG9rPWBGukAjkzVurhH69T`.
- Prose you write (reports, tweets, docs): no em-dashes, short sentences, name the evidence, no hype words, no filler. Objectivity is the brand.

## Operational gotchas (every failure here is SILENT)

- If the loop stalls: check the routine's `last_fired_at` and the transcript at claude.ai/code. Failures do NOT surface via the API or commit log.
- A removed/renamed model silently freezes the routine (the Fable 5 takedown did this; model is now `claude-opus-4-8`).
- Pushing needs `allow_unrestricted_git_push: true` and the push branch pinned to `main` in routine config, plus the Claude GitHub App installed on the repo owner's account with this repo in scope.
- Routine UI edits silently reset cron, push branch, and the event uuid.
- Minimum cron interval is 1 hour. `permission_mode` is a valid `session_context` field; reasoning-effort is not exposed.

## Improvement backlog (propose before doing; pick the highest-leverage one)

1. **Shape vs category (top priority).** The scout enforces category variety, but story SHAPE has converged hard on "name a cheap proven fix nobody deploys, hand an official a dossier/scorecard." Decide whether `PREFERENCES.md` should reward shape diversity (an investigation, a forecast, a teardown, a measurement) and draft the edit.
2. **Re-rank the roster from evidence.** The sampling lap is essentially done. Tier categories into P0/P1 by which reports were worth posting vs dropped.
3. **Sharpen `PREFERENCES.md`** from the accumulated accept/drop signal. It is still close to its first draft.
4. **Extract the first skill.** The "treatment-rate league table / cost-of-the-gap model / ranked scorecard" pattern recurs across nearly every problem. A `SKILL.md` would make the generator faster and more consistent. Extract from a successful run, never from imagination.
5. **Evaluator rubric is v1.** The weekly audit (read 2 PASS reports, fix what makes you wince) feeds rubric edits. The rubric is the judge, versioned.

## Notes log

Append below, newest first. One dated entry per decision, ruling-out, or lesson.

- 2026-06-25 — File created. Seven problems published; story-shape convergence (item 1) is the live design question and the agreed top priority. No improvements applied yet.
