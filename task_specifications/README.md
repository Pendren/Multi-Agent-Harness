# Task Specifications

This directory holds **concrete task specifications** (files matching `NN_ST-xx_short-title.md` per **`spec-engineer.md`**) that an agent can execute. Each spec follows the five primitives in **`spec-engineer.md`** (the numbered template in `00_Task_Specification_Template.md` is legacy scaffolding—**`spec-engineer.md`** wins on section order and headings).

**Staging:** **`SPEC_STAGING.md`** is the **inbox** for fragments not yet promotable into a spec; the Specification Agent drains it as sub-tasks and sections mature. It is **not** an executable spec, does **not** use the **`NN_ST-xx_*.md`** pattern, and is **excluded** from **`ST-xx`** reconcile and from **roadmap** / milestone lists—**orchestration** should treat only numbered **`NN_ST-xx_*.md`** files as work items (see **`spec-engineer.md`** Workflow **S** and **A.4**).

## After onboarding

Right after onboarding, **only the template exists** (`00_Task_Specification_Template.md`). There are no numbered specs yet.

**How to proceed:** In a fresh session, ask the agent to:

1. Review `intent.md` and `context.md`.
2. **Create** initial task specifications from the project goals and the "Spec candidates / first specs to draft" list in `context.md`.
3. Save them here as numbered files (e.g. `01_….md`, `02_….md`).
4. Optionally **review** each spec with the user one at a time against the five specification primitives so they are robust.
5. **Execute** either a single spec or the full orchestration (see below).

Example prompt to create then run first spec: *"Review `intent.md` and `context.md`. Create initial task specifications from the Spec candidates in context, save them under `task_specifications/`, then execute the first spec."*

**Once specs exist — execution:**

- **Single spec:** *"Review `intent.md`, `context.md`, and execute `task_specifications/[task_name].md`."*
- **Orchestrated (multi-milestone, memory, parallel):** *"Review `intent.md`, `context.md`, and `orchestration.md`. Run the orchestration."* Uses the roadmap from these specs, the development and testing skills, and `memory/tasks/`. Per task, execution order is Test Author → Developer → Test Runner (test-implementation separation; see **orchestration.md** Section 4). See `orchestration.md` and `docs/framework-flow.md`.
