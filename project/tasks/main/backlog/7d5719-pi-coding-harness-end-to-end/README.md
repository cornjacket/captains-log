# Task: pi-coding-harness-end-to-end

| Field       | Value                  |
|-------------|------------------------|
| Task-type   | USER-TASK              |
| Status      | backlog             |
| Epic        | main               |
| Tags        | tooling, evaluation               |
| Priority    | —           |
| Created     | 2026-07-27            |
| Completed   | —                      |
| Next-subtask-id | 0000               |

## Goal

Install the **Pi** AI coding harness and drive it end-to-end on one small, real task — not a
tutorial exercise — to see how another harness makes its choices where Claude Code makes different
ones.

- Pi: https://github.com/earendil-works/pi (docs: https://pi.dev/)

## Context

Carried on the daily plan since 2026-07-2x without being started; promoted to a task on 2026-07-27
so it stops rolling forward invisibly.

The point is **comparative**, not adoption. Having built a task system, a project-status rollup, and
a generator family around Claude Code's conventions, the interesting question is which of those
conventions are load-bearing and which are just what this harness happens to do. A second harness
run against a real task is the cheapest way to find out — the friction points are the answer.

Worth watching for specifically:

- How the harness scopes context per step, and what it chooses to re-read vs. carry.
- Whether it wants a task/plan artifact of its own, and what shape — this bears directly on the
  agent-consumable task-spec question now owned by `create-ai-builder`.
- Where its permission/approval boundary sits.

## Subtasks

<!-- When a subtask is finished, run complete-task.sh --parent to mark it [x] before moving on. -->
<!-- subtask-list-start -->
<!-- subtask-list-end -->

## Notes

_None._
