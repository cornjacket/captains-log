# Task: investigate-claude-session-managers

| Field       | Value                  |
|-------------|------------------------|
| Task-type   | USER-TASK              |
| Status      | backlog             |
| Epic        | main               |
| Tags        | tooling, evaluation               |
| Priority    | HIGH           |
| Created     | 2026-07-29            |
| Completed   | —                      |
| Next-subtask-id | 0000               |

## Goal

Survey the tools that sit *above* Claude Code and manage its sessions — spawning, parking, resuming,
and running several sessions in parallel across branches or worktrees — and decide whether one of
them earns a place in the daily loop, or whether the gap is better closed by something built here.

What a survey has to answer to be worth anything:

- **What each one actually manages** — process supervision, session/transcript persistence, worktree
  or branch isolation, parallel fan-out, review of what the sessions produced. These are different
  problems wearing the same name.
- **Where session state lives**, and whether resuming a session weeks later still works.
- **Whether it fights the conventions already in place here** — the task system, `daily-plan.md`,
  the project-status commit schema. A manager that owns the plan file or invents its own task
  artifact is a conflict, not a tool.
- **What it costs to leave** — how much of the workflow ends up encoded in the manager itself.

Outcome: a captain's-log entry recording the comparison and the decision, adopt or not.

## Context

Multiple concurrent Claude Code sessions are already the normal working mode across this
portfolio — a repo per session, with the umbrella workspace as the cross-repo dashboard. What is
missing is anything that manages those sessions as a set: which ones are live, what each was doing,
what to resume after a break. That coordination currently lives in the operator's head.

This connects to two open strands rather than standing alone:

- [`7d5719-pi-coding-harness-end-to-end`](../7d5719-pi-coding-harness-end-to-end/) — the same
  question from the harness side: which conventions here are load-bearing and which are just
  Claude Code's shape. A session manager tests the same seam one level up.
- [`cf94ee-claude-desktop-without-per-prompt-reminders`](../cf94ee-claude-desktop-without-per-prompt-reminders/) —
  both are about getting durable context to persist across sessions without re-establishing it by
  hand each time.

## Subtasks

<!-- When a subtask is finished, run complete-task.sh --parent to mark it [x] before moving on. -->
<!-- subtask-list-start -->
<!-- subtask-list-end -->

## Notes

_None._
