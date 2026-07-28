# Task: claude-desktop-without-per-prompt-reminders

| Field       | Value                  |
|-------------|------------------------|
| Task-type   | USER-TASK              |
| Status      | backlog             |
| Epic        | main               |
| Tags        | tooling, workflow               |
| Priority    | —           |
| Created     | 2026-07-27            |
| Completed   | —                      |
| Next-subtask-id | 0000               |

## Goal

Stop re-typing the same standing instructions into every Claude Desktop chat. Move them into
**global custom instructions** for what should hold everywhere, and use **Projects** to partition
and scope the rest so each chat inherits only the context that its kind of work needs.

## Context

Carried on the daily plan since 2026-07-2x without being started; promoted to a task on 2026-07-27
so it stops rolling forward invisibly.

The friction is concrete: per-prompt reminders are unreliable (easy to forget, easy to drift between
chats) and they burn attention on restating context instead of doing work. Desktop already has the
two mechanisms — the question is the **split**, not whether to use them.

The split to work out:

- **Global** — what is true of every chat regardless of subject: tone, how to disagree, lead with a
  one-line summary, when to ask vs. proceed.
- **Per-Project** — what is true of one body of work: which repo, which conventions, which
  reference material. A Project also scopes its own knowledge, so partitioning keeps unrelated
  context from bleeding across.

This is the same problem the CLAUDE.md kernel solves for Claude Code — global directives at the top,
scoped ones at the repo — so the layering already worked out there is the natural starting point,
including the lesson that the always-on layer should stay small.

## Subtasks

<!-- When a subtask is finished, run complete-task.sh --parent to mark it [x] before moving on. -->
<!-- subtask-list-start -->
<!-- subtask-list-end -->

## Notes

_None._
