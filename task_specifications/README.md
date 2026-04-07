# Task Specifications

This directory holds **concrete task specifications** (files matching `NN_ST-xx_short-title.md` per **`spec-engineer.md`**) that an agent can execute. Each spec follows the five primitives in **`spec-engineer.md`**. **`00_Task_Specification_Template.md`** is a starter scaffold; if anything disagrees, **`spec-engineer.md`** wins on section order, headings, and gates.

**Staging:** **`SPEC_STAGING.md`** is the **inbox** for fragments not yet promotable into a spec; the Specification Agent drains it as sub-tasks and sections mature. It is **not** an executable spec, does **not** use the **`NN_ST-xx_*.md`** pattern, and is **excluded** from **`ST-xx`** reconcile and from **roadmap** / milestone lists - **orchestration** should treat only numbered **`NN_ST-xx_*.md`** files as work items (see **`spec-engineer.md`** Workflow **S** and **A.4**).

## After onboarding

Right after onboarding, **only the template exists** (`00_Task_Specification_Template.md`). **Structural** work items live in **`task_breakdown.md`** at the project root; there are no numbered specs yet.

**How to proceed:** In a fresh session, run **`spec-engineer.md`** from **Fresh session - start here** (see the copy-paste block in **`onboarding-agent.md`** Section 9). Preconditions: **`intent.md`**, **`context.md`**, **`task_breakdown.md`**, and no **`ONB0`** on line 1 of the global files.

1. Confirm preconditions and **`task_breakdown.md`** **`ST-xx`** list.
2. Produce one **`NN_ST-xx_*.md`** per sub-task; use **`SPEC_STAGING.md`** per Workflow **S** when needed.
3. Optionally **review** each spec with the user against the five primitives.
4. Declare **Phase completion** only per **`spec-engineer.md`** section **D**.
5. **Execute** in a later session: single spec or full **`orchestration.md`** (see below).

**Once specs exist - execution:**

- **Single spec:** *"Review `intent.md`, `context.md`, and execute `task_specifications/[NN_ST-xx_*.md]`."*
- **Orchestrated (multi-milestone, memory, parallel):** *"Review `intent.md`, `context.md`, and `orchestration.md`. Run the orchestration."* Uses the roadmap from these specs, the development, test-author, and test-runner skills, and `memory/tasks/`. Per task, execution order is Test Author -> Developer -> Test Runner (test-implementation separation; see **`orchestration.md`** Section 4). See **`orchestration.md`** and **`docs/framework-flow.md`**.
