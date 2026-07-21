# Daily plan — 2026-07-21

**What this repo is (for a newcomer):** `captains-log` is a personal engineering log — learning
notes, design decisions, and roadmap thinking captured as dated entries, tracked by project-status so
the reasoning behind the portfolio is recorded alongside the code.

**Last implemented:** logged the **task-devkit / pluggable-markdown-subsystems** roadmap (2026-07-20)
— generalizing the second-brain-devkit generator model into subsystems dropped into target repos.

**Focus / plan:**
- Read **Agent Quality** (Google/Kaggle) — the agent evaluation + observability whitepaper
  (trajectory-as-truth, the logging/tracing/metrics pillars, LLM-as-a-judge), front to back.
- Read **Introduction to Agents** (Google/Kaggle) — the model-plus-harness primer, front to back.
- Reach for the **Pi** AI coding harness — install and drive it end-to-end on a small task.
- **Set up Claude Desktop to behave without per-prompt reminders** — global custom instructions
  (standing preferences once) + adopt **Projects** to partition/scope chats.
- Sketch **task-devkit**: what the generated task subsystem looks like inside a target repo (a folder
  outside `vault/`; `tasks/`/`todo/` naming; whether to reuse the additive `update_brain` machinery).
- **Add the task-system to captains-log's daily-plan** — dogfood the task-devkit subsystem by wiring
  it into this repo's own plan.
- **Re-read The New SDLC With Vibe Coding** (Google/Kaggle) — a second pass, front to back, now that
  I've been through it once; consolidate the takeaways. (Last — after the other papers.)

### References
- Agent Quality — https://www.kaggle.com/whitepaper-agent-quality
- The New SDLC With Vibe Coding — https://www.kaggle.com/whitepaper-the-new-SDLC-with-vibe-coding (mirror: https://addyosmani.com/blog/new-sdlc-vibe-coding/)
- Introduction to Agents — https://www.kaggle.com/whitepaper-introduction-to-agents
- Pi coding-agent harness — https://github.com/earendil-works/pi (docs: https://pi.dev/)

```
morning ───────── midday ───────── afternoon ─────── evening
 [Agent Quality   [Pi harness]     [task-devkit      [SDLC paper]
  + Intro to       install +        sketch +          second pass
  Agents] read     drive            task-system;      (re-read,
                                    Desktop config]    last)
```
