# AGENTS.md — AI-Development-Rules

This repository is the canonical source for the user's **cross-project AI development workflow**.

## Source of truth

- `GLOBAL_AI_RULES.md` — canonical global rulebook.
- `templates/` — thin project/task/state templates.
- `README.md` — purpose, adoption model, and precedence.

## Maintenance rules

- Keep this repository project-agnostic.
- Do not add project-specific paths, product decisions, runtime commands, secrets, credentials, or private machine details.
- When a new lesson overlaps an existing rule, edit/merge the existing rule instead of appending a near-duplicate section.
- Optimize for high information density and stable wording so downstream prompt caching remains effective.
- Do not make the global rulebook so procedural that trivial tasks become over-engineered.
- Project-specific overrides belong in each project's local `AGENTS.md`.
- Keep templates thin; they are optional scaffolding, not mandatory ceremony.

## Rule precedence for downstream projects

`explicit current user instruction > project AGENTS.md > GLOBAL_AI_RULES.md > agent defaults`

## Verification before changing the rulebook

Before committing a global-rule change, check that it is truly cross-project and does not contradict an existing rule. Prefer one canonical rule over multiple similar formulations.
