---
name: superpowers-harness-adi
description: Use when a developer wants to drive a complex project or large feature with a controlled superpowers workflow, especially when they mention sh-start, sh-pack, sh-run, or sh-recover, or they need bounded scoping, execution-package creation, controlled implementation, or project recovery.
---

# Superpowers Harness ADI

Treat this skill as a workflow entry layer on top of superpowers.

Its job is to:

1. reduce repeated prompt writing
2. give the developer a stable default workflow
3. keep the human in charge of goals, boundaries, route choices, and recovery

## Core Rule

Never enter the actual workflow until the active entry passes input check.

If key information is missing:

1. say which fields are missing
2. return the matching template from `templates/`
3. stop and wait for the user to fill it

Read `references/input-checks.md` before choosing how to handle missing information.

## Entry Map

| Entry | Use for | Internal route |
| --- | --- | --- |
| `sh-start` | new project start; large feature start on an existing project | `brainstorming` -> user decision -> `writing-plans` |
| `sh-pack` | turning an approved direction into one current execution package | `writing-plans` |
| `sh-run` | implementing an already-written execution package | `executing-plans` |
| `sh-recover` | regaining control after project drift or narrative drift | `brainstorming` -> optional `writing-plans` |

## Step 1: Identify the Entry

Map the user's wording to the nearest entry.

Examples:

- "start this project" -> `sh-start`
- "plan this large feature" -> `sh-start`
- "create the current execution package" -> `sh-pack`
- "start implementation" -> `sh-run`
- "this project has drifted" -> `sh-recover`

If the user explicitly names an entry, trust it unless it is clearly impossible.

## Step 2: Run Input Check

Read `references/input-checks.md`.

Rules:

1. If only one small detail is missing, ask for that one detail.
2. If multiple key fields are missing, return the matching template from `templates/`.
3. If `sh-run` lacks a current execution package or equivalent information, do not continue. Tell the user to fill the `sh-run` template or go back to `sh-pack`.

## Step 3: Execute the Right Route

### `sh-start`

Use `superpowers:brainstorming` first.

Focus on:

1. what problem this work actually solves
2. current MVP
3. explicit non-goals
4. key risks and route options
5. what the human must decide

Do not jump into implementation or heavy PRD.

After the user leaves a decision record, switch to `superpowers:writing-plans` and write one concise main document for the project or feature.

Required output shape:

1. one-sentence goal
2. current MVP
3. explicit non-goals
4. recommended route
5. human decision points
6. concise main document

### `sh-pack`

Use `superpowers:writing-plans`.

Build one current execution package only.

Required package sections:

1. target result
2. why now
3. explicit non-goals
4. task list
5. dependencies
6. acceptance criteria
7. stop lines
8. drift risks

Do not grow extra stages or future packages by default.

### `sh-run`

Use `superpowers:executing-plans`.

Before execution:

1. confirm the execution package exists
2. restate current goal
3. restate explicit non-goals
4. restate stop conditions

During execution:

1. stay inside the current package
2. stop if the work becomes a scope change
3. stop if the route needs to change
4. stop if key structure changes are required

Execution report must include:

1. completed work
2. unresolved risks
3. hard parts
4. trade-offs
5. human decisions needed
6. learning summary

### `sh-recover`

Use `superpowers:brainstorming` to re-establish control.

Read the current evidence first:

1. code and real artifacts
2. current truth documents
3. execution documents
4. legacy or archive materials only when needed

Focus on:

1. what the current mainline really is
2. what drifted
3. what should stop
4. what remains current vs execution vs legacy
5. whether the main document or current execution package must be rewritten

If a rewritten current truth or execution package is needed, switch to `superpowers:writing-plans`.

## Human Control Points

The human must approve or record decisions for:

1. one-sentence goal
2. MVP boundary
3. explicit non-goals
4. route choice
5. current execution package boundary
6. any scope, route, or structure change discovered during execution

Never let the skill silently absorb these choices.

## Guardrails

1. Do not expand the project for completeness.
2. Do not generate heavy PRDs by default.
3. Do not create extra stages unless the current line truly changed.
4. Do not let `sh-run` start without stop lines.
5. Prefer outputs written for the project lead, not just the executor.

## Output Contract

Read `references/output-contracts.md` when composing the final response for an entry.
