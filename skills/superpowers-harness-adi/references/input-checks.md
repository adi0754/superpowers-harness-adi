# Input Checks

## Shared Rule

Always inspect the user's request before routing into the real workflow.

- Missing one lightweight detail: ask for it directly.
- Missing multiple key details: return the matching template and stop.
- For `sh-run`, missing a current execution package is a hard stop.

## `sh-start`

Minimum required input:

1. current project or feature background
2. the problem to solve
3. why now
4. known constraints

If several of these are missing, return `templates/sh-start.md`.

## `sh-pack`

Minimum required input:

1. current main goal
2. what this round should complete
3. explicit non-goals
4. upstream decision record or main document

If several of these are missing, return `templates/sh-pack.md`.

## `sh-run`

Minimum required input:

1. current execution package or equivalent summary
2. current round goal
3. explicit non-goals
4. stop conditions or escalation conditions

If the package is missing, return `templates/sh-run.md` and recommend `sh-pack`.

## `sh-recover`

Minimum required input:

1. current project or feature
2. where drift is happening
3. what the human wants to regain first
4. available evidence

If several of these are missing, return `templates/sh-recover.md`.
