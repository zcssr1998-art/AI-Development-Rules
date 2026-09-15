# Global AI Development Rules

Canonical cross-project rules for AI-assisted development.

## 0. Core operating model

**Repository = development memory; chat = control plane.**

Use chat for goals, decisions, blockers, and concise results. Put durable rules, task specifications, state, test evidence, and detailed logs in the repository when the task is large enough to justify them.

The optimization target is **total repeated understanding per accepted task**, not merely the shortest individual prompt.

## 1. Rule precedence

When instructions conflict, use:

`explicit current user instruction > project-specific AGENTS.md > this global rulebook > agent defaults`

Do not weaken safety, security, authorization, or irreversible-action safeguards.

## 2. Scale the process to the task

Before acting, classify the work.

- **Small/isolated:** locate → change → focused verify → report. Do not create taskbooks, handoff files, new frameworks, or long plans.
- **Medium:** use a compact task specification if it reduces ambiguity; inspect only the affected subsystem.
- **Large/long-lived/cross-system:** use repository-owned task/state/handoff artifacts so another model can resume without reconstructing chat history.

Process ceremony must never cost more than the task itself.

## 3. Define the execution contract before implementation

For non-trivial work, establish:

- objective;
- constraints;
- acceptance criteria;
- allowed/expected scope;
- verification commands or runtime checks;
- important state that must not be redone.

Do not blindly implement a proposed technical route if a materially simpler, safer, cheaper, or more mature route satisfies the same product goal. State the better route and proceed when it does not change the user's product intent.

## 4. Reuse before rebuilding

Before creating a substantial subsystem from scratch:

1. inspect the current repository for an existing implementation or validated pattern;
2. check authoritative documentation when relevant;
3. search mature libraries, frameworks, templates, SDKs, CLIs, or GitHub projects when reuse would materially reduce work;
4. evaluate license, maintenance, dependency cost, security, and compatibility;
5. adapt the smallest proven component that fits.

Preference:

`existing validated project pattern > small mature dependency/pattern > new custom subsystem`

Do not vendor an entire project merely because one small pattern is useful.

## 5. Keep permanent rules separate from temporary tasks

- Stable cross-project rules live here.
- Stable project-specific rules live in the project's `AGENTS.md` or equivalent.
- Temporary requirements and acceptance criteria live in task files.
- Current execution state lives in one compact current-state/handoff artifact when needed.

Do not create multiple files that repeat the same state. If one `CURRENT_TASK.md` already serves as the handoff, do not add another handoff file without a concrete need.

Keep stable rule files stable when possible. Stable prefixes improve prompt-cache reuse and reduce repeated context churn.

## 6. New-session / new-agent startup must be cheap

Default startup order for an adopted project:

1. read local `AGENTS.md`;
2. read this global rulebook only as required by the local pointer/workflow;
3. read the compact current-task/state file if one exists;
4. inspect branch, HEAD, `git status`, and relevant diff;
5. read only the minimum source/docs required for the next step;
6. check for an existing Worker/job/session before creating another.

Do not default to reading the whole repository, every document, full Git history, or old chat transcript.

If a full taskbook already exists in Git, **do not paste its body into chat or another Agent prompt again**. Point to the file.

## 7. Chat should not be a file courier

When GitHub/repository access is available, read and write project artifacts directly.

The user should not be asked to manually copy:

- taskbooks between models;
- Worker summaries back to a reviewer;
- large logs;
- file contents already available in the repository;
- project history that can be recovered from Git/state files.

Use the repository as the shared handoff surface.

## 8. Split responsibilities by cost and capability

Use the least expensive capable path.

- **Strong model / lead:** requirements, architecture, high-risk decisions, hard debugging, integration strategy, final review.
- **Cheaper Worker:** ordinary implementation, repetitive edits, focused fixes, test repair, documentation, deterministic code-search work.
- **Deterministic tools:** test, lint, build, type-check, static analysis, schema validation, probes, exit codes, smoke scripts.

Do not have multiple models independently re-plan the same task. Do not use a high-cost reasoning model for deterministic work that a script or cheaper Worker can perform reliably.

## 9. One coherent task should normally be one Worker job

A Worker task should include the deterministic acceptance criteria known at dispatch time so it does not need to re-read/re-plan the project later.

Prefer:

`one task definition → one resumable Worker job → deterministic verification → diff review`

When a follow-up is genuinely necessary, resume the same session/job if possible and pass only the new failure or missing requirement plus existing state.

A normal Worker startup instruction should be short, e.g.:

`Pull latest state, read AGENTS/current task, execute and verify it, update state, commit/push, return only result/commit/tests/blocker.`

## 10. Resume before restart

A timeout, disconnected chat, UI failure, or missing final message does **not** prove the underlying task failed.

Before re-running long or side-effectful work, inspect:

- existing process/job/session ID;
- current Git state and HEAD;
- partial outputs/artifacts;
- test/build status;
- current task state/checkpoint.

If work can be resumed, resume it. Do not start a duplicate Worker merely because the outer call timed out.

## 11. Deterministic verification decides success

Model prose is not the success condition.

Prefer objective gates such as:

- expected diff exists;
- tests/lint/build/type-check exit 0;
- required smoke/runtime path was actually exercised;
- changed files stay within expected scope;
- no required safety boundary was crossed.

If the task requires subjective judgment that automation cannot establish, mark it explicitly as pending rather than inventing a PASS.

## 12. Stop when acceptance passes

Once required acceptance criteria pass:

- stop model calls;
- do not perform unrelated cleanup;
- do not re-implement a passing Worker solution “for safety”;
- do not run extra broad scans/tests without a reason;
- record optional improvements as later work unless they block current acceptance.

Successful work should not trigger another expensive model call solely to narrate success.

## 13. Context hygiene: high-information evidence only

Prefer targeted context:

- relevant diff/hunks instead of whole unchanged files;
- symbol/path search before recursive reading;
- failed test output instead of all successful test output;
- concise state files instead of prose history recaps.

For logs, provide by default:

- failed command;
- exit code;
- core error/stack;
- relevant surrounding lines;
- necessary `head`/`tail`/filtered output.

Do not feed huge build logs, generated payloads, or entire runtime dumps to a model unless they are actually needed.

## 14. Retry intelligently, not repetitively

One identical retry is acceptable when a transient infrastructure failure is plausible.

After repeated deterministic failure:

`inspect cause → focused repair → retry → safe fallback`

Do not burn tokens repeatedly issuing the same failing operation without new evidence.

## 15. Review the delta, not the entire project

Default review order:

1. `git diff --stat` / changed filenames;
2. target-related diff hunks;
3. deterministic verification result;
4. current task/handoff state;
5. expand to full files or wider architecture only when risk justifies it.

When the user says “review the latest commit/result” or “continue,” retrieve GitHub/repository state directly. Do not ask the user to paste a long Worker report.

## 16. Preserve validated foundations

Do not rewrite stable systems merely for architectural neatness.

Prefer the smallest reversible change that satisfies the requirement. Introduce a new abstraction/framework only when there is a real second use case, demonstrated limitation, or clear maintenance/security benefit.

## 17. Scope discipline

Do not silently expand a focused task into unrelated refactors, extra features, framework migrations, broad cleanup, or speculative architecture.

Fix adjacent issues only when they block the requested acceptance criteria or create a material safety/reliability problem.

## 18. Git and remote durability

For versioned work, preserve unrelated local/remote changes.

- Avoid destructive reset/force-push unless explicitly required and safe.
- Commit coherent verified work.
- Push when the task requires durable remote delivery.
- Verify the remote commit/content when claiming remote completion.

A local success is not a remote success if push/remote verification failed.

## 19. Compact current-state handoff

For medium/large tasks that may span sessions, keep one compact state artifact containing only what is needed to resume:

- current goal;
- branch / last known good commit;
- done/verified items;
- active/recoverable job/session if relevant;
- exact next step;
- `do not redo` items;
- blocker;
- pending human checks if applicable.

Do not paste large logs, diffs, source files, or the whole taskbook into the state file.

## 20. Unattended execution

When the user explicitly asks for unattended/remote continuation, continue safe reversible work without routine confirmation.

Do not interrupt for ordinary compile/test failures, focused repair iterations, or routine implementation choices resolved by current requirements.

Interrupt only for a genuine blocker such as:

- credible destructive/data-loss risk;
- unavailable required credentials/signing/authorization/payment;
- irreversible external side effect needing approval;
- unresolved product-defining ambiguity with materially different outcomes;
- hard environment failure after safe fallbacks are exhausted.

Do not claim subjective human validation if no human performed it.

## 21. Zero-question execution budget for clear technical tasks

After a clear goal is given, default to autonomous execution:

`inspect → choose minimal reversible path → implement → verify → diagnose → repair → re-verify → commit/push if required → report`

Routine technical choices should be resolved from the repository, project rules, and tools rather than turned into A/B/C questions for the user.

## 22. Reporting budget

Detailed execution history belongs in Git, task files, test artifacts, and logs.

Default Worker final report:

```text
PASS | FAIL
commit: <sha or none>
tests: <compact result>
blocker: <none or one key blocker>
```

Primary-agent reports may add materially changed behavior, real remaining risk, human-validation status, and remote verification where relevant.

Do not generate a second long natural-language copy of information already present in the diff, commit, task file, or logs.

## 23. Security and secrets

Never commit, paste into task files, or echo in reports:

- API keys;
- passwords;
- access/refresh tokens;
- session cookies;
- signing secrets;
- private credentials.

Use environment variables or approved secret stores. Redact sensitive values in logs and handoffs.

## 24. Global-rule maintenance

This repository is the canonical source for **cross-project** workflow rules.

When a new lesson applies broadly:

- update/merge it here;
- avoid adding a duplicate project-local copy;
- keep project repositories focused on project-specific overrides;
- prefer editing an overlapping rule over endlessly appending new sections.

Do not put project-specific paths, product decisions, commands, or secrets into this global rulebook.

## 25. Token/context efficiency metric

The main waste patterns to eliminate are:

- same requirement explained to several models;
- same repository repeatedly scanned;
- taskbook stored in Git and then pasted into chat anyway;
- same log repeatedly reread;
- successful work repeatedly summarized;
- timed-out but still-running work restarted;
- accepted work followed by unnecessary model calls;
- strong models used for deterministic chores.

A healthy workflow normally has:

`one authoritative task definition → one resumable execution path → deterministic verification → one diff-based final review`

**Final principle:** human sets goals and final product decisions; strong model designs/reviews; Worker executes; deterministic tools verify; repository remembers.
