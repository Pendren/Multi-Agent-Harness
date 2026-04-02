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
3. Open that file. It must point you to a **Task Specification** path (`task_specifications/<NN>_*.md`) and the work scope. Execute **only** what is in that task file.

## While working

- **Do not add scope.** Do not do the next step or a different task unless the task file explicitly includes it.
- **Do not write tests, evals, or test code.** Your output is implementation only. If the task file asks you to "add evals" or "add tests," that is the Tester's responsibility—report that test authoring is the Tester's remit and do not add test code.
- **Spec reading (execution firewall):** From the spec file, you may read **only** **§1 Self-Contained Problem Statement** and **§2 Constraint Architecture** (the task file may quote extra constraints explicitly). You **must not** read **§3 Acceptance Criteria**, **§4 Decomposition/Dependencies**, or **§5 Evaluation Design**—those would leak test intent.
- **Do NOT read the acceptance test directory.** Tests live under **evals/acceptance/<task_id>/**. Do not open that path or any test files for the current task.
- **Use project docs:** **intent.md** and **context.md** for global rules and environment. Respect Must Escalate and runtime rules from those files and from **§2** of the spec.
- **Runtime requirements:** When running commands that depend on a runtime requirement (e.g. a language runtime, a local service), use the verify and platform fallbacks in context.md (§1a Runtime / environment requirements). If the primary command fails (e.g. `python` not found), try the documented alternative (e.g. `py` on Windows) before concluding the requirement is missing. If a requirement remains missing after trying alternatives, report it and do not assume it is satisfied.
- **Produce the requested artifacts** (code, config, documents) and put them where the spec or task file indicates.
- **Write progress to memory** if the Manager has asked you to (e.g. update progress.md or a task status); otherwise report results in your reply.

## When done

- **Report clearly:** what you produced, where it lives, any failures or uncertainties.
- If the Manager passed a task path, you have no ongoing identity—you were "Developer for that path." The Manager will invoke you again with another path if needed (possibly in parallel with another invocation).

## Summary

- **Input:** Task path or id in the invocation message (or memory/current_task.md).
- **Behavior:** Read that file → execute only that task → produce artifacts → report back.
- **Output:** Where artifacts live; pass/fail; any blockers or questions.
