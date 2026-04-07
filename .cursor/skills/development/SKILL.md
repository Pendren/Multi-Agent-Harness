---
name: development
description: >-
  Execute a single development task read from the project memory store. Use when the Manager
  (or Orchestrator) delegates an implementation task; the task is written to memory and the
  path is passed at invocation so multiple tasks can run in parallel with different paths.
---

# Development (execute one task from memory)

Use this skill when you are acting as the **Developer** and have been given a **task path** (or task id) in the invocation message. Your job is to execute only that task and report back.

## First step: get your task

1. **Read your task from the path or id given in the invocation.** The Manager (or Orchestrator) will say something like: "Read your task from memory/tasks/01-step2.md" or "Your task is in memory/tasks/01-step2.md."
2. **If no path or id was given,** fall back to **memory/current_task.md** (sequential mode).
3. Open that file. It contains: task text, spec id, step number, paths, and any context you need. Execute **only** what is in that file.

## While working

- **Do not add scope.** Do not do the next step or a different task unless the task file explicitly includes it.
- **Do not write tests, evals, or test code.** Your output is implementation only. If the task file asks you to "add evals" or "add tests," that is the Tester's responsibility—report that test authoring is the Tester's remit and do not add test code.
- **Do NOT read the acceptance test directory.** Tests for this task live in **evals/acceptance/** (or the path specified in the task, e.g. evals/acceptance/<task_id>/). You must **not** read that directory or any test files for the current task. Tests are written from the spec before implementation and must remain unknown to you so they can verify your work objectively.
- **Use project docs:** intent.md, context.md, and the task specification referenced in the task file. Respect constraints and escalation triggers from intent.
- **Runtime requirements:** When running commands that depend on a runtime requirement (e.g. a language runtime, a local service), use the verify and platform fallbacks in the **Runtime / environment requirements** table in **context.md**. If the primary command fails (e.g. `python` not found), try the documented alternative (e.g. `py` on Windows) before concluding the requirement is missing. If a requirement remains missing after trying alternatives, report it and do not assume it is satisfied.
- **Produce the requested artifacts** (code, config, documents) and put them where the spec or task file indicates.
- **Write progress to memory** if the Manager has asked you to (e.g. update progress.md or a task status); otherwise report results in your reply.

## When done

- **Report clearly:** what you produced, where it lives, any failures or uncertainties.
- If the Manager passed a task path, you have no ongoing identity—you were "Developer for that path." The Manager will invoke you again with another path if needed (possibly in parallel with another invocation).

## Summary

- **Input:** Task path or id in the invocation message (or memory/current_task.md).
- **Behavior:** Read that file → execute only that task → produce artifacts → report back.
- **Output:** Where artifacts live; pass/fail; any blockers or questions.
