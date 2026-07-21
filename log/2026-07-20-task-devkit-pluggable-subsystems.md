# Task-devkit & pluggable markdown subsystems (roadmap)

**Date:** 2026-07-20
**Sparked by:** deciding where to track second-brain *maintenance* tasks (capture / verify / write-a-note
items — not project or coding tasks). Landed on a folder in the `second-brain/` repo **outside** the
PARA `vault/`. That concrete need generalized into a broader pattern worth recording.

## The idea
Generalize the `second-brain-devkit` "generator" model into a family of **pluggable markdown
subsystems** — self-contained tooling that a *devkit* **generates into** a target repo for a specific
purpose. `second-brain-devkit` is the first instance (it generates a brain); a **task system** is the
next.

## Concrete steps
1. **Extract the task system out of `ai-builder` into its own repo: `task-devkit`.**
2. **`task-devkit` generates a task system into `second-brain/`** — directly analogous to how
   `second-brain-devkit` generates a brain: tooling dropped into a target repo, outside the semantic
   vault, to track brain-storage tasks.
3. **Backfill `ai-builder`** so that `task-devkit` also generates *ai-builder's* task system — i.e.
   ai-builder becomes a **consumer** of task-devkit's output rather than owning the task code itself.

## The pattern (why it matters)
- **Pluggable markdown subsystems** dropped into target repos for specific purposes.
  `second-brain-devkit` = one instance; `task-devkit` = another. New subsystem → new `*-devkit` repo
  that emits into any target. **It scales well.**
- **Mechanism that makes it safe (validated 2026-07-20):** the devkit's `update_brain.py` is
  **strictly additive** — it only writes files from its `template/` tree, **never deletes unmanaged
  content**, and preserves user territory (`vault/`, `config/`, `data/`, `CLAUDE.md`). So a generated
  subsystem can be dropped into a target repo without clobbering the user's own content. That
  additive-update property is exactly what makes "pluggable subsystems" viable.

## ai-tasks & the agentic angle
- The task system includes **"ai-tasks"** — tasks usable by `ai-builder` for **autonomous agentic
  workflows**.
- **Possible next step:** turn `ai-builder` into an **`ai-builder-devkit`** that generates into
  `second-brain/`.
- `ai-builder` has **no current second-brain purpose**, but there may be use cases — TBD.

## Open questions
- Exact layout of the generated task subsystem inside `second-brain/` (folder outside `vault/`;
  naming that avoids devkit-owned names — `tasks/` and `todo/` are free; devkit owns `scripts/`,
  `config/`, `data/`, `tests/`, `seeds/`, `skill/`, `desktop-e2e/`).
- Does `task-devkit` **reuse** `second-brain-devkit`'s emit/update machinery (`template/` +
  `emit-manifest.toml` + additive `update_brain.py`), or factor it into a shared library?
- Concrete second-brain use cases for ai-builder's agentic workflows.
