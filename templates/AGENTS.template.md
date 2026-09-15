# AGENTS.md — <PROJECT_NAME>

This project follows the global AI development workflow:

`https://github.com/zcssr1998-art/AI-Development-Rules/blob/main/GLOBAL_AI_RULES.md`

Read the global rules as the cross-project baseline. This file contains only **project-specific overrides, constraints, commands, and acceptance gates**.

## Rule precedence

`explicit current user instruction > this project AGENTS.md > GLOBAL_AI_RULES.md > agent defaults`

## New-session read order

1. `AGENTS.md`
2. global `GLOBAL_AI_RULES.md`
3. `CURRENT_TASK.md` or equivalent, if present
4. current branch / HEAD / `git status` / relevant diff
5. only the files needed for the current task

Do not paste the global rulebook or a repo-resident taskbook into chat again.

## Project identity

- Product: <WHAT_THIS_PROJECT_IS>
- Primary stack: <STACK>
- Canonical runtime/platform: <RUNTIME>

## Project-specific constraints

- <CONSTRAINT_1>
- <CONSTRAINT_2>

## Verification commands / gates

```text
<TEST_COMMAND>
<BUILD_COMMAND>
<SMOKE_COMMAND>
```

## Stable foundations / do-not-rewrite list

- <SYSTEM_OR_FILE>

## Project-specific definition of done

- <RUNTIME_OR_PRODUCT_GATE>

## Security / repository notes

- Never commit secrets or local credentials.
- Preserve unrelated user/remote changes.
- Add only project-specific rules here; cross-project workflow improvements belong in AI-Development-Rules.
