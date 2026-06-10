# Skills library

Empty by design. Skills are **extracted from completed manual sessions, never written from imagination** — a skill written from a guess is a guess; a skill extracted from a successful run is an asset.

## When to add one

When the run log shows the generator repeatedly doing the same kind of work freeform, or doing it badly: open Claude Code interactively, do the task by hand once, then extract the transcript into a skill here.

## Contract for every SKILL.md

- **Name:** sharp and specific (`source-synthesis`, not `research-helper`)
- **Input:** what it expects from spec.md / prior artifacts
- **Output:** the artifact it must produce, with format
- **Done:** what finished looks like, in checkable terms
- **Quality checklist** at the bottom — the generator must self-verify against it before writing the artifact. This is the substitute for unit tests: every number sourced, counterarguments addressed, nothing stale presented as current.

Layout: `.claude/skills/<skill-name>/SKILL.md`.

Planned first extractions (do NOT pre-write these): `source-synthesis`, `literature-sweep`, `evidence-dossier`.
