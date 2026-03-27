# Assessment: WorkBrain refinements vs baseline template

This document summarizes how the **WorkBrain** project refined the baseline AI Agent Project template and what was added back to the template so future uses benefit.

---

## Baseline template (before WorkBrain)

The original template at `ai_agent_project` contained:

- **README_template.md** — Bootstrapping (§0), five framework sections; execution = single "Execute task_specifications/…" only.
- **onboarding-agent.md** — Intent (Q1/Q2) and context interview; terminal step: create specs then execute first, or execute existing spec. No orchestration, no execution scaffold.
- **intent.md**, **context.md** — Placeholders with section structure.
- **task_specifications/00_Task_Specification_Template.md** — Five specification primitives.
- **task_specifications/README.md** — Create specs, execute first; single-spec execution only.
- **boundary_log.md** — Surprise log + failure model combined.

**Missing from baseline:** orchestration, execution design (dev/test skills, memory/tasks, parallel), framework flow doc, separate failure_model.md, Cursor skills and agents.

---

## Changes made in WorkBrain (refinements)

1. **Orchestration** — Added `orchestration.md`: Orchestrator/Manager loop, roadmap from specs, memory (roadmap, progress, **tasks**, failures, context), development and testing **skills**, task path passed on invoke, **parallel** invocation when dependencies allow, escalation after three failed cycles.
2. **Development and testing skills** — Added `.cursor/skills/development/` and `.cursor/skills/testing/`: agents read task from **memory path** given in invocation (or fallback current_task/current_validation); supports parallelism via multiple task files and multiple invocations.
3. **Developer and Tester subagents** — Added `.cursor/agents/developer.md` and `.cursor/agents/tester.md`: fixed subagents that follow the skills and read task path from invocation.
4. **Framework flow** — Added `docs/framework-flow.md`: Init → Onboarding → Spec creation (optional review) → Execution (single-spec **or** orchestrated). Clarifies where orchestration is used (Phase 4 only).
5. **Execution modes** — Two options: **single-spec** ("Execute task_specifications/X.md") and **orchestrated** ("Run orchestration" with roadmap, memory, skills, parallel).
6. **Onboarding updates** — Terminal step: create specs, optionally review each spec with user, then execute **single or orchestrated**; step 8: ensure orchestration.md and skills exist.
7. **README updates** — Execution scaffold (ensure orchestration + skills + agents); §4 describes both execution modes; link to framework-flow at top.
8. **task_specifications/README** — Optional spec review; execute single or orchestrated with pointers to orchestration.md and framework-flow.
9. **failure_model.md** — Separate file (WorkBrain; template had it inside boundary_log). Template now includes a minimal failure_model.md for consistency with README §5.

---

## What was added to the template

So that every **new** project created from the template gets the same design:

| Added to template | Purpose |
|-------------------|--------|
| **orchestration.md** | Full orchestration prompt: roadmap, memory/tasks, dev/test skills, task path on invoke, parallel when safe, escalation. |
| **docs/framework-flow.md** | End-to-end flow and where orchestration fits (Phase 4, Option B). |
| **docs/ASSESSMENT_WorkBrain_refinements.md** | This file: what changed and why. |
| **.cursor/skills/development/SKILL.md** | Development skill: read task from path in invocation, execute only that task. |
| **.cursor/skills/testing/SKILL.md** | Testing skill: read validation task from path, run checks, report pass/fail. |
| **.cursor/agents/developer.md** | Developer subagent: follows development skill, reads path from invocation. |
| **.cursor/agents/tester.md** | Tester subagent: follows testing skill, reads path from invocation. |
| **failure_model.md** | Minimal placeholder for known failure modes (README §5). |

---

## What was updated in the template

| File | Change |
|------|--------|
| **README_template.md** | Added execution scaffold (step 5: ensure orchestration + skills + agents). Renumbered steps 5→6, 6→7. Added framework-flow link at top. §4: two execution modes (single-spec and orchestrated) with pointer to orchestration.md and framework-flow. |
| **onboarding-agent.md** | Step 8: ensure orchestration.md and .cursor/skills/development and testing exist. Terminal step: create specs, optionally review each spec; then execute **single spec** or **orchestrated** (with pointers to orchestration.md and docs/framework-flow.md). |
| **task_specifications/README.md** | How to proceed: add optional review step. "Once specs exist": **single spec** or **orchestrated** execution with pointers to orchestration.md and docs/framework-flow.md. |

---

## Result

New projects created from this template now:

1. **Include** orchestration, dev/test skills, and Developer/Tester agents from the start.
2. **Document** the full flow (init → onboarding → specs → execution) and where orchestration is used.
3. **Offer** both single-spec and orchestrated execution after specs exist.
4. **Guide** the user at end of onboarding: new session → create specs (and optionally review) → execute single or orchestrated.

The baseline framework is unchanged in intent (intent.md, context.md, five primitives, boundary_log). The **additions** are the execution layer (orchestration, skills, agents, memory/tasks, parallel) and the clear flow so the conversation stays natural and all documents stay aligned with the framework.

---

## Additional template refinements (later)

Further refinements were added to the template so all bootstrapped projects benefit:

| Refinement | Purpose |
|------------|---------|
| **§1a Subagent capability establishment** | Before milestone work, establish whether Developer/Tester can be spawned. If not, notify the human and write notification timestamp; on any later invocation, if 10+ minutes have passed with no acknowledgement, Orchestrator may proceed with fallback (single-agent mode) and must log attempts and fallback use in memory/subagent_capability_and_fallback.md. |
| **Manager request-back** | When a Manager agent (e.g. a subagent) cannot spawn Developer or Tester (e.g. nested subagents not supported), the Manager sends a request back to the Orchestrator to spawn the needed agent for that task; the Orchestrator spawns it with the task path. |
| **§2b Test–implementation separation** | Fixed order per task: **Test Author (Tester) first** — writes acceptance tests from task/spec/intent/context only to evals/acceptance/<id>/; **Developer** — implements without reading evals/acceptance/; **Test Runner (Tester)** — runs pre-written tests only, does not modify tests. Manager does not write tests or implementation. Ensures tests are unbiased (from spec, not from code). |
| **Acceptance test directory** | evals/acceptance/ (or path in context). Test Author may write; Developer must not read; Test Runner may read and run, must not modify. Documented in context.md §2 and orchestration.md §2b. |
| **Development skill** | Explicit rule: Developer must NOT read the acceptance test directory for the current task. |
| **Testing skill** | Two modes: Test Author (write from spec only, no implementation; write to evals/acceptance/<id>/, then exit) and Test Runner (run pre-written tests only; do not add, change, or remove tests). |
| **Task types** | memory/tasks/ now includes test-author-<id>.md in addition to <id>.md (implementation) and validate-<id>.md (run tests). |
| **memory/subagent_capability_and_fallback.md** | New memory file for subagent attempts, notification timestamp, and fallback log (what was attempted, that fallback was used, timing). |

These refinements keep the template project-agnostic; no project-specific names or examples are used.
