# Task: when-to-run-claude-dangerously

| Field       | Value                  |
|-------------|------------------------|
| Task-type   | USER-SUBTASK           |
| Status      | —                      |
| Epic        | main               |
| Tags        | tooling, security, second-brain               |
| Parent      | dfcb75-investigate-claude-session-managers             |
| Priority    | —           |
| Created     | 2026-07-29            |
| Completed   | —                      |
| Next-subtask-id | 0000               |

## Goal

Work out **when** running Claude with permission checks bypassed is the right call and **how** to do
it without handing an agent unbounded reach — then write the transferable version of that judgment
into the second-brain.

The research has to produce an actual decision rule, not a list of flags. Specifically:

- **What the bypass actually removes.** Which prompts disappear, and what stays enforced regardless.
  The name suggests "all checks off"; the reality is narrower and the difference is the whole point.
- **What contains it instead.** Sandboxing, containers, VMs, throwaway worktrees, network egress
  limits, credential scoping — bypassing approval is only defensible when something *else* is the
  boundary. Establish what the minimum viable container is.
- **The cases where it earns its keep.** Long mechanical sweeps, generated-code loops, CI and cron
  contexts where no human is present to approve — versus the cases where the approval prompt is
  carrying real safety weight (anything touching credentials, remotes, published artifacts, or a
  working tree with uncommitted work).
- **The failure modes.** What goes wrong in practice, and which of those are recoverable. Prompt
  injection reaching a tool call matters more here than anywhere else, since approval was the
  backstop.

Deliverable: a **new** note in the second-brain vault (`resources/`) stating the decision rule and
the containment requirement in repo-independent terms. Searched the vault on 2026-07-29 — nothing
covers this yet (nearest hits were `agent-instruction-placement`, `reviewing-agent-written-code`, and
`scratch-lives-in-gitignored-sandbox`, none on-topic), so this is a new note rather than an edit.
Per the brain's own rule: the lesson goes in the note, and any repo-specific settings or command
lines stay in the repo that uses them, linked as evidence.

## Context

This lands under the session-manager survey because the two questions are the same question. A
manager that runs several Claude sessions in parallel, unattended, is unusable if every session
blocks on approval prompts — so the pressure to bypass checks comes *from* parallelism. Deciding
whether to adopt a session manager therefore requires knowing what the bypass costs and what has to
be true before it's acceptable. Answering it first keeps the survey from quietly assuming the answer.

The connection to [`../../backlog/7d5719-pi-coding-harness-end-to-end/`](../../backlog/7d5719-pi-coding-harness-end-to-end/)
is the permission boundary: that task asks where a different harness draws the line. This one asks
what is on the other side of the line when you cross it deliberately.

## Subtasks

<!-- When a subtask is finished, run complete-task.sh --parent to mark it [x] before moving on. -->
<!-- subtask-list-start -->
<!-- subtask-list-end -->

## Notes

_None._
