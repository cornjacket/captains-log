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

## Assessment — sequence it, don't front-load the framework
The pattern is sound; the risk is *sequencing*, not the idea.

- **Premature generalization is the danger.** The task system exists in exactly one place today.
  Building a generator (template/ + emit-manifest + golden + CI + update semantics) before it has
  lived in a *second* repo risks the wrong abstraction. second-brain-devkit earned its machinery
  because a brain is genuinely complex; a task system may not.
- **Do you even need a devkit, or something lighter?** Spectrum: manual copy → submodule/subtree →
  cookiecutter one-shot → full additive-update devkit. The full devkit pays off **only if the task
  *tooling* keeps evolving and you want that pushed into many targets without re-copying.** Deciding
  question: after drop-in, how often does the tooling change? Rarely → submodule/cookiecutter.
- **Shared-machinery is the real architecture call** (reuse the engine vs a shared library). Don't
  decide it on spec — wait until task-devkit exists and the common surface is visible. Don't abstract
  the abstraction early.
- **"Scales well" is true for the *right* subsystems**, not all — each instance carries a fixed cost
  (its own golden, CI, update contract). Worth it for complex + shared + evolving subsystems only.
- **Two generators → one target = a collision/ownership problem to name now.** Additive updates are
  safe from *deletion*, not from *collision*. Define who owns which folders / `.gitignore` lines /
  README managed blocks before a second generator emits into `second-brain/`.
- **The ai-task schema is the product; generation is plumbing.** A markdown checklist is trivial; an
  *agent-consumable* task spec (state model, completion reporting, acceptance criteria, "don't let
  the agent mark its own homework") is the real design problem. Nail that before the generator.
- **ai-builder → second-brain is a solution seeking a problem** — park it until a concrete use case
  appears. Possibility isn't a reason.

**Recommended sequence:** (1) drop a task system into `second-brain/` **by hand** (folder outside
`vault/`) and use it a few weeks — especially to feel the ai-task shape; (2) extract `task-devkit`
**only on the second real need** (ai-builder), and pick devkit-vs-lighter by how much the tooling
churns; (3) generalize the shared engine / ai-builder-devkit **on the third** consumer, not before.
