---
name: project-orchestrator
description: Manage long-running software and research projects using specification-driven planning, task decomposition, persistent progress files, and Codex subagents. Use when initializing, planning, resuming, executing, or reviewing a multi-step project.
---

# Project Orchestrator

Use this skill for non-trivial multi-step projects.

## Project Files

Use:

- `.agent/SPEC.md`
- `.agent/TASKS.md`
- `.agent/PROGRESS.md`
- `.agent/FINDINGS.md`
- `.agent/tasks/TASK-XXX.md`

These files externalize project state so work can continue across context windows.

# Mode 1: Initialize

Use when:

- the project is new
- SPEC.md is empty
- the user asks to initialize the workflow

Procedure:

1. Inspect the repository.
2. Understand the user's objective.
3. Ask only clarification questions that materially affect architecture or acceptance criteria.
4. Write `.agent/SPEC.md`.
5. Break the project into logical tasks.
6. Create `.agent/tasks/TASK-XXX.md`.
7. Build dependencies in `.agent/TASKS.md`.
8. Set tasks to TODO, READY, or BLOCKED.
9. Initialize `.agent/PROGRESS.md`.

Do not begin major implementation during initialization unless explicitly requested.

# Mode 2: Resume

Use when the user says:

- continue
- resume
- keep working
- continue the project

Procedure:

1. Read `AGENTS.md`.
2. Read `.agent/SPEC.md`.
3. Read `.agent/TASKS.md`.
4. Read `.agent/PROGRESS.md`.
5. Read relevant findings if needed.
6. Inspect current Git status.
7. Compare documented status against actual code and tests.
8. Identify READY tasks.
9. Select the smallest high-value unblocked task.

If documentation conflicts with code or test results, trust code/tests and repair the project state files.

# Mode 3: Execute Task

Before implementation:

1. Read the specific TASK file.
2. Inspect relevant code.
3. Confirm task dependencies are DONE.
4. Determine whether exploration should be delegated to an explorer subagent.

During implementation:

1. Keep scope narrow.
2. Prefer small, reversible changes.
3. Run relevant tests.
4. Do not silently expand architectural scope.

After implementation:

1. Review the diff.
2. Run acceptance verification.
3. Ask a reviewer subagent to independently check the implementation for non-trivial tasks.
4. Mark DONE only if acceptance criteria pass.
5. Update TASKS.md.
6. Update PROGRESS.md.
7. Record durable research findings in FINDINGS.md.

# Mode 4: Parallel Execution

Parallelize only tasks that:

- have no unresolved dependency between them
- do not modify the same critical files
- do not depend on an unstable shared interface

Prefer 2-4 concurrent workers.

Do not parallelize simply because multiple tasks are READY.

# Mode 5: Review


When reviewing a completed task:


## Reviewer Role

The reviewer is an independent verifier.

The reviewer MUST:

- inspect implementation
- compare against requirements
- identify risks
- report findings


The reviewer MUST NOT:

- modify source files
- implement fixes
- silently change task scope
- mark a task complete without verification


---

## Review Checklist


Review from these perspectives:


### 1. Requirement Compliance

Check:

- Does the implementation satisfy the task objective?
- Are all acceptance criteria satisfied?
- Are required outputs produced?


### 2. Test Quality

Check:

- Are tests meaningful?
- Do tests verify actual behavior?
- Are important cases missing?


### 3. Scope Control

Check:

- Did the implementation modify unrelated files?
- Did the implementation introduce unnecessary complexity?
- Did the agent exceed the assigned task?


### 4. Integration Risk

Check:

- Could this break existing modules?
- Are interfaces compatible?
- Are dependencies affected?


### 5. Documentation and State

Check:

- Is TASK file updated?
- Is PROGRESS.md updated?
- Are important technical findings recorded?


---

## Review Output Format


Return:


### Summary

PASS / NEEDS_CHANGES


### Findings

For each issue:


Severity:

HIGH / MEDIUM / LOW


Location:

file or module


Problem:

description


Impact:

why this matters


Recommendation:

suggested action


---

## Completion Rule


A task can become DONE only when:


- implementation passes review
- verification succeeds
- no blocking issue remains

Otherwise:

set status:

CHANGES_REQUIRED

# Task Decomposition Rules

A good task should:

- have one clear outcome
- be independently testable where possible
- fit one logical commit
- have explicit dependencies
- have acceptance criteria
- avoid spanning unrelated subsystems

Avoid tasks such as:

- "finish backend"
- "improve project"
- "fix everything"

Prefer tasks such as:

- "Implement PiperX state adapter"
- "Add LeRobot episode recorder"
- "Add wheel-clearance termination condition"

# State Management

SPEC.md:
What should exist.

TASKS.md:
What is planned and what depends on what.

PROGRESS.md:
A concise current-state summary.

FINDINGS.md:
Durable technical or experimental knowledge.

Git:
What actually changed.

Tests:
Whether the implementation works.

Never use PROGRESS.md as the sole source of truth.

# Context Management

Do not load every historical file by default.

Load only:

- current specification
- current task
- current progress
- relevant findings
- relevant code

This is a context-isolation workflow.

# Failure Handling

If a task fails:

1. Do not mark DONE.
2. Record the blocker.
3. Set BLOCKED if necessary.
4. Record durable technical findings.
5. Create a follow-up task if the failure reveals new work.

Do not repeatedly retry the same approach without incorporating new evidence.