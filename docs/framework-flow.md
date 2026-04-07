# Framework flow: from initialization to execution

This document describes how the project moves from a blank (or templated) repo to robust intent, context, specs, and execution - and **where orchestration fits**. Use it so each phase flows naturally and all framework criteria are met.

---

## Overview

| Phase | What happens | Who drives | Output |
|-------|----------------|------------|--------|
| **1. Initialization** | Directory structure, dependencies, scaffold files | AI (bootstrapping instructions in **README_template.md** Section 0) | INITIALIZATION_REPORT.md; triggers onboarding |
| **2. Onboarding** | Interview to fill intent, context, and **task_breakdown.md** | AI (onboarding-agent.md); user answers | intent.md, context.md, **task_breakdown.md**, 00 template, boundary_log |
| **3. Spec creation** | **`spec-engineer.md`**: one **`NN_ST-xx_*.md`** per sub-task; optional review | AI in a **new session**; user prompts | task_specifications/01_….md, 02_….md, … |
| **4. Execution** | Run work: single-spec or full orchestration | AI; user chooses mode and prompts | Delivered work; memory/ if orchestrated |

**Orchestration** is used in **Phase 4** when you want **multi-milestone, memory-based, parallel-capable** execution. It is **not** used during onboarding or spec creation.

---

## Phase 1: Initialization

- **Trigger:** AI (or user) runs the bootstrapping instructions in **README_template.md** Section 0 (AI Autonomous Stand-Up).
- **Actions:** Ensure directory structure, install dependencies, create missing scaffold files (intent.md, context.md, onboarding-agent.md, **spec-engineer.md**, task_specifications/00_Task_Specification_Template.md, boundary_log.md, failure_model.md, **orchestration.md**, **.cursor/skills/development/**, **.cursor/skills/testing/**, **.cursor/agents/developer.md**, **.cursor/agents/tester.md**). Write **INITIALIZATION_REPORT.md**.
- **Next:** **Immediately** run the onboarding flow (open onboarding-agent.md and execute). Do not ask the user whether to run onboarding; begin the interview.

**Template capture:** The template (or init) must include **orchestration.md** and the two skills so every new project gets the same execution design (dev + test skills, memory/tasks, parallel when safe).

---

## Phase 2: Onboarding (interview → intent + context)

- **Trigger:** Right after init (or when the user loads onboarding-agent.md).
- **Driver:** **onboarding-agent.md** ("Seam Designer"): one question at a time, mirror back at section boundaries, **file progressively** to intent.md and context.md (do not wait until the end).
- **Routing:** If the user's answer mixes intent (goal, "done," controls, trade-offs, escalation), context (tech, data sources, workflows), and spec-level detail, **parse and route** each part to the correct document. Confirm briefly what was captured where.
- **Intent:** Two questions (Q1: goal, "done," controls; Q2: trade-offs, escalation). Mirror back after each; write Summary at top of intent.md after Q2.
- **Context:** Tech stack, tools/MCP, conventions, dependencies, observability, runtime table (see **context.md**). Mirror back before closing.
- **Task breakdown:** **`task_breakdown.md`** lists **`ST-xx`** sub-tasks for **`spec-engineer.md`** (not executable specs). **Do not** create numbered spec files during onboarding.
- **Scaffold:** Ensure task_specifications/00_Task_Specification_Template.md and boundary_log.md exist.
- **Terminal step (critical):** End the onboarding session cleanly. Tell the user to **kill the session** (context is cluttered). Then give the **next step** clearly (see below).

**Next step after onboarding (tell the user):**

- You now have intent.md, context.md, and **task_breakdown.md**, but **no numbered specs** yet.
- In a **new session**, the user can:
  1. **Specification Engineering:** Run **`spec-engineer.md`** (use the copy-paste prompt from **onboarding-agent.md** Section 9) until **Phase completion** in that file: one **`NN_ST-xx_*.md`** per **`ST-xx`**, **`SPEC_STAGING.md`** drained, no blocking **`DRAFT*`**. Optionally **review** each spec with the user.
  2. **Execute:** Once specs exist, run a **single spec** or **orchestrated execution** (see **Phase 4**).

So the transition from onboarding to "what's next" is: **new session → `spec-engineer.md` (specs) → (optional review) → execute (single or orchestrated)**. Orchestration is one of the two execution options, not part of onboarding or spec authoring.

---

## Phase 3: Spec creation (and optional review)

- **Trigger:** User starts a **new session** and runs **`spec-engineer.md`** with **`task_breakdown.md`**, **`intent.md`**, and **`context.md`** already on disk (see **Preconditions** in **`spec-engineer.md`**).
- **Actions:** The Specification Agent produces **`task_specifications/NN_ST-xx_*.md`** files per **`spec-engineer.md`**, uses **`SPEC_STAGING.md`** as needed, and declares **Phase completion** only when **`spec-engineer.md`** section **D** is satisfied.
- **Optional:** User may ask to **review each spec one at a time** against the five primitives in **`spec-engineer.md`** and refine until robust.
- **Output:** A set of concrete, reviewable task specifications. No execution yet unless the user explicitly asks to run work in the same session.

**Next:** User chooses execution mode (single-spec or orchestrated) and prompts accordingly.

---

## Phase 4: Execution

Two modes:

### A. Single-spec execution

- **When:** One milestone or one spec to run; no need for full roadmap, memory, or parallel.
- **Prompt (example):** "Review intent.md and context.md. Execute task_specifications/01_X.md."
- **Behavior:** Agent reads intent, context, and that spec; does the work (and may use the development/testing skills in single-agent mode); reports when done. No orchestration.md, no memory/tasks/, no multi-milestone loop.

### B. Orchestrated execution

- **When:** Long multi-stage project; you want roadmap from all specs, durable memory, Developer/Tester subagents (or roles), and **parallel** tasks when dependencies allow.
- **Prompt (example):** "Review intent.md, context.md, and orchestration.md. Run the orchestration: build the roadmap from task_specifications/, use memory and the development and testing skills, run the Manager loop (and parallel invocation when safe)."
- **Prerequisites:** intent.md, context.md, and at least one (ideally all) numbered task spec(s). Orchestration.md and .cursor/skills/development/ and .cursor/skills/testing/ must exist (from template or init).
- **Behavior:** Agent acts as Orchestration Agent: establishes subagent capability (**orchestration.md** Section 1a); initializes from intent and context; builds roadmap from specs; finalizes roadmap in memory; then runs the Manager loop. Per task: Test Author (Tester) writes tests from spec to evals/acceptance/<id>/ first; Developer implements (must not read acceptance tests); Test Runner (Tester) runs pre-written tests only. Writes tasks to memory/tasks/, invokes Developer and Tester with task paths, supports parallel when deps allow, escalates per **orchestration.md** Section 6 (progress and retry). If subagent invocation is not possible, notifies human and may use fallback after 10 minutes (see **orchestration.md** Section 1a). See **orchestration.md** for full instructions.

**Where orchestration fits:** Only in **Phase 4, Option B**. It is the "full" execution path. Option A is the "single spec" path. Both fulfill the framework; orchestration adds memory, skills, and parallelism for multi-milestone work.

---

## Making the conversation flow naturally

1. **Init:** No user choice - "run onboarding immediately" after init so the user is not stuck on "what do I do?"
2. **Onboarding:** One question at a time, mirror back, file as you go, confirm what was captured where. At the end, **one clear terminal message**: scaffolding complete, kill session, then "in a new session do X or Y" (create specs, then execute single or orchestrated).
3. **Spec creation:** User starts **`spec-engineer.md`** after onboarding (new session). User can say "review each spec with me" for quality. No need to mention orchestration until execution.
4. **Execution:** User says either "execute task_specifications/01_X.md" (single) or "run orchestration" / "run the orchestration from orchestration.md" (full). The framework flow doc and **README_template.md** Section 4 should state both options and point to orchestration.md for Option B.

That way the user always knows: **init → onboard → (new session) `spec-engineer.md` → (optional) review specs → execute (single or orchestrated)**. Orchestration is clearly the "full execution" option after specs exist.
