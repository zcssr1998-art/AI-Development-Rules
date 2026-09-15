# AI Development Rules

Central, reusable rules for AI-assisted software development across projects.

## Purpose

This repository is the **single source of truth for cross-project development workflow**. Project repositories should keep only project-specific rules, constraints, commands, and acceptance gates in their own `AGENTS.md`.

Core principle:

> **Repository = development memory; chat = control plane.**

The user should not have to repeatedly paste taskbooks, project history, logs, or Worker reports between models.

## Read order for agents

For a project that adopts these rules:

1. Read the project's local `AGENTS.md` first.
2. Read [`GLOBAL_AI_RULES.md`](./GLOBAL_AI_RULES.md) when the local file points here or when cross-project workflow rules are needed.
3. Read the project's compact current-state/task file, if present.
4. Inspect only the relevant Git state, diff, files, and logs required for the current task.

### Rule precedence

When rules conflict:

`explicit current user instruction > project-specific AGENTS.md > GLOBAL_AI_RULES.md > agent defaults`

Safety/security constraints always remain in force.

## Files

- `GLOBAL_AI_RULES.md` — canonical cross-project workflow and Token/context-efficiency rules.
- `templates/AGENTS.template.md` — thin project-level rule entry point.
- `templates/CURRENT_TASK.template.md` — compact resumable state template for medium/large tasks.
- `templates/TASK.template.md` — repository-resident taskbook template.

## Design constraints

- Do not copy the entire global rulebook into every project.
- Do not create process documents for trivial edits.
- Keep global rules stable and merge overlapping rules instead of endlessly appending near-duplicates.
- Keep secrets, credentials, private machine data, and project-confidential details out of this public repository.
- Project-specific rules remain in the project repository.

## Canonical repository

`https://github.com/zcssr1998-art/AI-Development-Rules`
