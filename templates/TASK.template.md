# Task — <SHORT_NAME>

Use this template only when the task is complex enough to benefit from a repo-resident taskbook.

## Objective

<WHAT_MUST_BE_TRUE_WHEN_DONE>

## Constraints

- <CONSTRAINT>

## Acceptance criteria

- [ ] <DETERMINISTIC_OR_RUNTIME_CHECK>
- [ ] <DETERMINISTIC_OR_RUNTIME_CHECK>

## Allowed / expected scope

- `<PATH_OR_SUBSYSTEM>`

## Do not change unless required

- `<STABLE_SYSTEM_OR_OUT_OF_SCOPE_AREA>`

## Verification

```text
<COMMAND_OR_SMOKE_STEPS>
```

## Existing state / do not redo

- <ALREADY_COMPLETED_WORK>

## Completion protocol

1. Implement the minimum correct change.
2. Run the required verification.
3. Update compact current-state/handoff if this task spans sessions.
4. Commit/push when required by the project workflow.
5. Return only:

```text
PASS | FAIL
commit: <sha or none>
tests: <compact result>
blocker: <none or one key blocker>
```
