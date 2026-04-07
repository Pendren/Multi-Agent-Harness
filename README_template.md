# Blank AI Project Template Scaffolding

This template combines the 5 Frontier Operations principles with the 4 Prompting Disciplines to structure AI agent projects for long-term autonomous execution.

**Full flow (init -> onboarding -> specs -> execution):** See **`docs/framework-flow.md`** for initialization, **`task_breakdown.md`** + **`spec-engineer.md`** (specification phase), and execution (single-spec vs orchestrated with **`orchestration.md`** and the development/testing skills).

## 0. AI Autonomous Stand-Up Instructions (Bootstrapping)
*Instructions for any AI system reviewing this repository. Do not require human input to execute this section.*

**AI Directive:**
If you are an AI agent analyzing this document to stand up a new instance of this project, your objective is to initialize the project strictly according to the specifications below.
1. **Directory structure:** Ensure the folder structure matches the `_templates/ai_agent_project` blueprint without prompting for user confirmation.
2. **Dependencies:** Generate and run dependency installation scripts (e.g., `package.json`, `requirements.txt`, `docker-compose.yml`) based on the [Stack] listed below.
3. **Core scaffolding (full harness):** Create any missing files from this template or a reference project so the **lifecycle is complete**: **`onboarding-agent.md`**, **`spec-engineer.md`**, **`orchestration.md`**; **`intent.md`** and **`context.md`** (templates; may use **`ONB0`** on line 1 until onboarding finishes - see **`onboarding-agent.md`**); **`task_specifications/`** (at least **`00_Task_Specification_Template.md`**, **`README.md`**, and other harness files your template ships, e.g. **`SPEC_STAGING.md`**); **`boundary_log.md`**, **`failure_model.md`**; **`docs/framework-flow.md`**; **`.cursor/skills/development/`** and **`.cursor/skills/testing/`**; **`.cursor/agents/developer.md`** and **`.cursor/agents/tester.md`**. **`task_breakdown.md`** is **written during onboarding**, not invented during init; do not skip onboarding.
4. **Stop & report:** Once initialized, output a system status report to a file named **`INITIALIZATION_REPORT.md`** in the root directory.
5. **Run onboarding immediately:** After writing **`INITIALIZATION_REPORT.md`**, open **`onboarding-agent.md`** and execute that flow. Do not ask the user whether to run onboarding or fill files manually; begin the Seam Designer interview (one question at a time, writing to **`intent.md`** and **`context.md`** as you go).
6. **Routing rule for onboarding:** When the user's response mixes intent (purpose, boundaries, "done"), context (tech, stack, tools/MCP, runtime, observability), and **deliverable or spec-shaped** detail, parse the response and file each part into the correct document (**`task_breakdown.md`** for **`ST-xx`** scope per **`onboarding-agent.md`**). Do not ask the user to re-split; perform the routing yourself and confirm briefly what was captured where.
7. **After onboarding:** The human starts a **new session** for **`spec-engineer.md`** (see **`onboarding-agent.md`** Section 9 handoff), then later for execution - see **`docs/framework-flow.md`**.

**[Stack & Setup Details to be completed by user prior to handoff]**
- **Language/Framework:** [e.g., Python / TypeScript / MCP Server]
- **Environment:** [e.g., Docker Desktop, n8n, OpenClaw]
- **Operational Pod Structure:** [Specify if this is a "Team of 1" (single frontier operator) or "Team of 5" (1 lead operator + executors)]

### For users: How to answer onboarding questions
When the onboarding agent asks about **intent** (e.g. "What is the primary goal?"), focus on *what you want* and *who decides*: purpose, what "done" looks like at a high level, and what the agent may do without asking. You can add tech or workflow detail in the same answer; the agent will route stack, tools, and runtime facts to **`context.md`** and work sequencing to **`task_breakdown.md`**. For **context** questions (tech stack, conventions, MCP, install/verify commands), give what implementers need to **know**. Keeping intent answers goal-focused yields cleaner **`intent.md`**; mixed answers are fine and will be parsed.

---

## 1. Intent Engineering & Boundary Sensing (Root Level)
*The Strategy Layer: Outlining organizational goals and tracking AI surprises.*

### `intent.md`
- **Goal:** Encode organizational purpose, trade-off hierarchies, and decision boundaries.
- **Content:** Primary goal; what "done" looks like for v1; trade-off tie-breakers (e.g. speed vs accuracy); what the user controls and what the agent must escalate; optional one-sentence summary.
- **Intent interview (1-2 questions):** The onboarding agent gathers intent in two steps: **(Q1)** goal, "done," and controls; **(Q2)** trade-offs and escalation. At each section boundary the **agent** mirrors back what it heard, asks for clarification, incorporates feedback, then moves on (including writing the one-sentence Summary at the top of `intent.md`). See `onboarding-agent.md` for the exact prompts.

### `boundary_log.md` (The Surprise Log)
- **Goal:** Track Boundary Sensing.
- **Content:** A running log of every time the agent output surprises the human user (by succeeding unexpectedly or failing surprisingly). If you aren't logging surprises, you aren't operating at the boundary. Re-evaluate capabilities quarterly based on this log.

---

## 2. Context Engineering (Environment Layer)
*Durable facts about **how the system is built and run** - not what to build first (that is **`task_breakdown.md`** and **`spec-engineer.md`**).*

### `context.md` (or `.claude.md`)
- **Goal:** Give agents the same **environment** grounding a new implementer would need: stack, layout, prerequisites, tooling, and conventions - without hunting the wiki.
- **Sections (see the live template):** **Environment & architecture** (stack, dependencies, repo layout, integrations, observability); **Runtime / environment requirements** (verify commands, platform fallbacks, install policy - sole source for prerequisite checks in **`orchestration.md`**); **Tools, integrations, and MCP** (shell, CLIs, MCP servers, automation); **Rules & conventions** (style, and where acceptance tests live under **`evals/acceptance/`** per **`orchestration.md`**); **Capability forecasting & deprecation** (temporary polyfills with revisit dates, or **`None noted.`**).
- **What does not belong:** **`ST-xx`** scope, task ordering, or spec content - that lives in **`task_breakdown.md`** (onboarding) and **`task_specifications/`** (**`spec-engineer.md`**). **`context.md`** is not a second backlog.
- **Who fills it:** **`onboarding-agent.md`** during the interview (**`spec-engineer.md`** reads **`context.md`** when authoring specs).

---

## 3. Specification Engineering (Action Layer)
*Formal specs for each **`ST-xx`** - authored with **`spec-engineer.md`**, then executed under **`orchestration.md`**.*

### **`spec-engineer.md`** (Specification Agent)
- **Bridge:** **`task_breakdown.md`** (onboarding) -> **`task_specifications/NN_ST-xx_short-title.md`** -> execution.
- **Reads first:** **`task_breakdown.md`** (canonical **`ST-xx`**, **`Depends on:`**, resume), then **`intent.md`** and **`context.md`**, then **`SPEC_STAGING.md`** if present for **OPEN** inbox rows.
- **Writes:** One spec file per **`ST-xx`**, named **`NN_ST-xx_short-title.md`** (`NN` = `01`, `02`, ... in **`## Sub-tasks`** order). **`DRAFT*`** filenames are allowed until stable; **Phase completion** (**D**) requires non-`DRAFT` specs and a clean reconcile (**A.4**). Full rules: **`spec-engineer.md`** (this README does not restate **Workflow S**, **B**, **C**, **D**).

### `task_specifications/` directory
- **Goal:** A **library of milestone specs** that **`orchestration.md`** can run (roadmap = **`NN_ST-xx_*.md`** files only).
- **Not milestones:** **`README.md`**, **`SPEC_STAGING.md`** (staging inbox), **`00_*`** templates, and other non-`NN_ST-xx_*` files - see **`spec-engineer.md`** **A.4** / **D** and **`task_specifications/README.md`**.

### Document template (five `##` sections, this order)
Authoritative detail is in **`spec-engineer.md`** **Document template**. Summary:

1. **Self-Contained Problem Statement** - What to do; inputs and outputs; assumptions; inline facts not already in **`intent.md`** / **`context.md`** when required.
2. **Constraint Architecture** - Exactly these subsections: **`### Must`**, **`### Must Not`**, **`### Preferences`**, **`### Escalation Triggers`**.
3. **Acceptance Criteria** - Exactly **three** numbered sentences (**1.** **2.** **3.**), each independently verifiable.
4. **Decomposition / Dependencies** - Scoped to **this** **`ST-xx`**: prerequisite **`ST-xx`**, optional micro-steps, parallelism notes (for the Manager - not new product scope).
5. **Evaluation Design** - **3-5** executable cases **`EV-01`** ... **`EV-05`** (how to run, expected output) proving the acceptance criteria.

**Legacy file:** **`00_Task_Specification_Template.md`** may differ; **`spec-engineer.md`** wins on headings and order.

---

## 4. Prompt Craft & Leverage Calibration (Execution Layer)
*The Operation Layer: Minimizing prompt craft while calibrating human review.*

### Execution modes
With Intent, Context, **`task_breakdown.md`**, and specifications defined, you can run work in two ways:

- **Single-spec execution:** One milestone at a time. Example prompt: *"Review `intent.md` and `context.md`. Execute `task_specifications/01_ST-01_short-slug.md`."* (Use your repo's actual **`NN_ST-xx_*.md`** path.) The agent does that spec's work (and may use the development/testing skills in single-agent mode).
- **Orchestrated execution:** Multi-milestone, with memory, Developer/Tester roles (or subagents), and **parallel** tasks when dependencies allow. Example prompt: *"Review `intent.md`, `context.md`, and `orchestration.md`. Run the orchestration."* The agent builds the roadmap from `task_specifications/`, writes tasks to `memory/tasks/`, invokes Developer and Tester with task paths, and runs the full Manager loop. See **`orchestration.md`** and **`docs/framework-flow.md`** for when and how to use it.

### Leverage calibration
Optional **review threshold** line at the top of a spec file (e.g. Autonomous / Sampled / Full), if the project wants it - see **`spec-engineer.md`** completion gate **C** and optional review hook.

---

## 5. Observability and evaluation (Observability Layer)
*Tests, regressions, and explicit failure models.*

### `evals/` directory
- **Harness path (orchestrated execution):** When you use **`orchestration.md`**, each milestone **Test Author** step writes executable tests under **`evals/acceptance/<spec-stem>/`** (or a path overridden in **`context.md`**). The **stem** matches the **`NN_ST-xx_*.md`** spec filename without extension. **Test Author** uses **Evaluation Design** + **Acceptance Criteria** from the spec only; **Developer** must not read that directory for the active milestone; **Test Runner** runs tests and does not modify them. Order per milestone: Test Author -> Developer -> Test Runner. See **`orchestration.md`** Section 4, **`context.md`** (Rules & conventions), and **`.cursor/skills/testing/`**.
- **Specification phase:** **`spec-engineer.md`** defines **`EV-xx`** cases in **Evaluation Design**; **materializing** those tests into **`evals/`** is **execution** work unless the human scoped test scaffolding as its own **`ST-xx`**.
- **Optional:** You may also keep **project-level** regression or smoke suites (e.g. after model or dependency upgrades) elsewhere under **`evals/`** with clear naming so they are not confused with the harness **acceptance** tree.

### `failure_model.md`
- **Goal:** A codified mental model of *how* the agent or system fails on this project - so you can add targeted checks instead of generic doubt.
- **Content:** Map concrete failure modes; link to **`boundary_log.md`** when a surprise reveals a pattern. Prefer **programmatic** or repeatable checks where possible.

