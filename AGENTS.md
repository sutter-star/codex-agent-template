# Project Agent Operating Rules

## Project Memory

Before starting a non-trivial task, read:

- `.agent/SPEC.md`
- `.agent/TASKS.md`
- `.agent/PROGRESS.md`

Read `.agent/FINDINGS.md` when the task involves experiments,
previous failures, research findings, or historical technical decisions.

## Source of Truth

Use the following hierarchy:

1. Current source code and Git state
2. Tests and verification results
3. `.agent/SPEC.md`
4. Individual task files under `.agent/tasks/`
5. `.agent/TASKS.md`
6. `.agent/PROGRESS.md`

Do not treat PROGRESS.md alone as proof that a task is complete.

## Development Workflow

For non-trivial work:

1. Understand the current project state.
2. Identify the relevant task.
3. Inspect relevant code before editing.
4. Keep changes scoped to the assigned task.
5. Run appropriate verification.
6. Review the diff.
7. Update project state files.

## Task Completion

A task may be marked DONE only when:

- implementation is complete
- acceptance criteria are satisfied
- relevant tests or verification have passed
- no known blocking issue remains
- project status files are updated

## Task Scope

Do not modify unrelated modules unless required by the task.

If a task requires an architectural change outside its scope,
stop and report the dependency instead of silently expanding scope.

## Subagents

Use subagents for work that can be isolated.

Preferred roles:

- explorer: investigate code and dependencies
- implementer: implement a specific task
- reviewer: independently verify the implementation

Do not create deeply nested agent hierarchies.

Prefer at most 2-4 concurrently active subagents.

## Research Projects

Record durable experimental knowledge in `.agent/FINDINGS.md`.

Include:

- experiment setup
- relevant parameters
- observation
- result
- interpretation
- next action

Do not store raw logs or large outputs in FINDINGS.md.

## Git

Prefer one logical task per commit.

Use task IDs in commit messages when practical.

Example:

`TASK-004 implement LeRobot dataset recorder`