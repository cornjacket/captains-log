# Task: task-devkit-pluggable-subsystems

| Field       | Value                  |
|-------------|------------------------|
| Task-type   | USER-TASK              |
| Status | backlog |
| Epic        | main               |
| Tags        | —               |
| Priority    | —           |
| Created     | 2026-07-24            |
| Completed   | —                      |
| Next-subtask-id | 0006 |

## Goal

Generalize the `second-brain-devkit` generator model into a family of **pluggable markdown
subsystems** — self-contained tooling a *devkit* generates into a target repo for a specific
purpose — with a **task system** as the second instance after the brain.

Sequence it rather than front-loading the framework: use a task system by hand first, extract
`task-devkit` only on the second real need, and factor out shared machinery only on the third
consumer.

## Context

Recorded 2026-07-20, sparked by deciding where to track second-brain *maintenance* tasks (capture
/ verify / write-a-note items, not coding tasks). That landed on a folder in `second-brain/`
**outside** the PARA `vault/`, and the concrete need generalized into a pattern.

**Why the pattern matters.** New subsystem → new `*-devkit` repo that emits into any target. What
makes it safe was validated 2026-07-20: the devkit's `update_brain.py` is **strictly additive** —
it writes only files from its `template/` tree, never deletes unmanaged content, and preserves
user territory (`vault/`, `config/`, `data/`, `CLAUDE.md`). A generated subsystem can be dropped
into a repo without clobbering the user's own content.

**Why the order below is not the source doc's order.** The original roadmap listed extract →
generate-into-second-brain → backfill ai-builder. The assessment written alongside it supersedes
that: the task system exists in exactly one place today, so building a generator (template/ +
emit-manifest + golden + CI + update semantics) before it has lived in a *second* repo risks the
wrong abstraction. `NNNN` is an ordering contract, so the subtasks encode the recommended
sequence instead.

**Open questions.**

- Exact layout of the generated task subsystem inside `second-brain/` — a folder outside `vault/`,
  named to avoid devkit-owned names (`tasks/` and `todo/` are free; the devkit owns `scripts/`,
  `config/`, `data/`, `tests/`, `seeds/`, `skill/`, `desktop-e2e/`).
- Does `task-devkit` **reuse** `second-brain-devkit`'s emit/update machinery (`template/` +
  `emit-manifest.toml` + additive `update_brain.py`), or is it factored into a shared library?
  Don't decide on spec — wait until the common surface is visible.
- **Two generators → one target is a collision/ownership problem to name now.** Additive updates
  are safe from *deletion*, not from *collision*. Define who owns which folders, `.gitignore`
  lines, and README managed blocks before a second generator emits into `second-brain/`.
- Is a full devkit even needed, or something lighter? The spectrum runs manual copy →
  submodule/subtree → cookiecutter one-shot → additive-update devkit. The full devkit pays off
  only if the task *tooling* keeps evolving and you want that pushed into many targets without
  re-copying. Deciding question: after drop-in, how often does the tooling actually change?
- Concrete second-brain use cases for ai-builder's agentic workflows — the task system includes
  **ai-tasks** usable by `ai-builder` for autonomous workflows, and an `ai-builder-devkit`
  generating into `second-brain/` is *possible*, but ai-builder has no current second-brain
  purpose. Park it until a real use case appears; possibility isn't a reason.

**The real design problem.** The ai-task schema is the product; generation is plumbing. A markdown
checklist is trivial — an *agent-consumable* task spec (state model, completion reporting,
acceptance criteria, "don't let the agent mark its own homework") is the hard part. Nail that
before the generator.

## Subtasks

<!-- When a subtask is finished, run complete-task.sh --parent to mark it [x] before moving on. -->
<!-- subtask-list-start -->
- [ ] [bb5b51-0000-hand-drop-task-system-into-second-brain](bb5b51-0000-hand-drop-task-system-into-second-brain/)
- [ ] [bb5b51-0001-use-it-and-evaluate-ai-task-shape](bb5b51-0001-use-it-and-evaluate-ai-task-shape/)
- [ ] [bb5b51-0002-extract-task-devkit-on-second-need](bb5b51-0002-extract-task-devkit-on-second-need/)
- [ ] [bb5b51-0003-backfill-ai-builder-as-consumer](bb5b51-0003-backfill-ai-builder-as-consumer/)
- [ ] [bb5b51-0004-generalize-shared-engine-on-third-consumer](bb5b51-0004-generalize-shared-engine-on-third-consumer/)
- [ ] [bb5b51-0005-update-docs](bb5b51-0005-update-docs/)
<!-- subtask-list-end -->

## Notes

- **Subtask `0000` may already be partly overtaken by events.** The source roadmap predates the
  `create-project-system` generator that emitted `project/` into *this* repo on 2026-07-24 — so
  "drop a task system into `second-brain/` by hand" may now be "run that generator against
  `second-brain/`". Kept as written, since the point of the by-hand step was to *feel the ai-task
  shape* before committing to generator machinery; revisit before starting it.
- Migrated 2026-07-24 from `log/2026-07-20-task-devkit-pluggable-subsystems.md`. `log/` is for
  personal log and status writing; live task state lives here.

### Field notes from using the system (feed these into the devkit)

- **No way to retag an existing task.** `--tags` is accepted only by
  `new-user-task.sh` / `new-user-subtask.sh` at creation; there is no `set-tags.sh`, and
  `rename-subtask.sh` only changes the `NNNN`. Retagging today means either hand-editing the
  `Tags` row — outside the "scripts only" rule, though safe, since `Tags` is a leaf field with
  nothing mirrored on the filesystem — or delete-and-recreate with `--id`, which destroys the
  task's subtasks. First real gap found by using the system rather than designing it, which is
  exactly what subtask `0001` is for. A `set-field.sh` covering `Tags` and `Priority` would
  close it.
- **`Category` is the wrong name for what it does** — it is the worktree class (which files a
  task touches, so parallel branches don't collide), not a topical category, and the name
  invites exactly the misuse of reaching for it to classify a task as "video" or "education".
  Filed upstream as task 19 in `create-project-system`.
