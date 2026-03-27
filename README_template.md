# Blank AI Project Template Scaffolding

This template combines the 5 Frontier Operations principles with the 4 Prompting Disciplines to structure AI agent projects for long-term autonomous execution.

**Full flow (init → onboarding → specs → execution):** See **`docs/framework-flow.md`** for how initialization, the intent/context interview, spec creation, and execution (single-spec vs orchestrated) fit together and where **`orchestration.md`** and the development/testing skills are used.

## 🤖 0. AI Autonomous Stand-Up Instructions (Bootstrapping)
*Instructions for any AI system reviewing this repository. Do not require human input to execute this section.*

**AI Directive:**
If you are an AI agent analyzing this document to stand up a new instance of this project, your objective is to initialize the project strictly according to the specifications below.
1. **Directory Structure:** Ensure the folder structure matches the `_templates/ai_agent_project` blueprint without prompting for user confirmation.
2. **Dependencies:** Generate and run dependency installation scripts (e.g., `package.json`, `requirements.txt`, `docker-compose.yml`) based on the [Stack] listed below.
3. **Core Scaffolding:** Create the missing files from the list below if they do not exist.
4. **Stop & Report:** Once initialized, output a system status report to a file named `INITIALIZATION_REPORT.md` in the root directory.
5. **Execution scaffold:** Ensure `orchestration.md`, the skills (`.cursor/skills/development/`, `.cursor/skills/testing/`), and the Developer/Tester subagents (`.cursor/agents/developer.md`, `.cursor/agents/tester.md`) exist (create from template or copy from a reference project). These capture the execution design: tasks in memory, dev/test skills, task path passed on invoke, parallel when dependencies allow. See `docs/framework-flow.md` for how they fit the full flow.
6. **Run onboarding immediately:** After writing `INITIALIZATION_REPORT.md`, open `onboarding-agent.md` and execute that flow. Do not ask the user whether to run onboarding or fill files manually; begin the Seam Designer interview (one question at a time, writing to `intent.md` and `context.md` as you go).
7. **Routing rule for onboarding:** When the user's response mixes intent (purpose, boundaries, "done"), context (tech, data sources, workflows, observability), and specification-level detail, parse the response and file each part into the correct document. Do not ask the user to re-split; perform the routing yourself and confirm briefly what was captured where.

**[Stack & Setup Details to be completed by user prior to handoff]**
- **Language/Framework:** [e.g., Python / TypeScript / MCP Server]
- **Environment:** [e.g., Docker Desktop, n8n, OpenClaw]
- **Operational Pod Structure:** [Specify if this is a "Team of 1" (single frontier operator) or "Team of 5" (1 lead operator + executors)]

### For users: How to answer onboarding questions
When the onboarding agent asks about **intent** (e.g. "What is the primary goal?"), focus on *what you want* and *who decides*: purpose, what "done" looks like at a high level, and what the agent may do without asking. You can add tech or workflow detail in the same answer; the agent will file it in `context.md`. For **context** questions (tech stack, conventions), give the details the next agent needs to "know." Keeping intent answers goal-focused yields cleaner `intent.md`; mixed answers are fine and will be parsed.

---

## 1. Intent Engineering & Boundary Sensing (Root Level)
*The Strategy Layer: Outlining organizational goals and tracking AI surprises.*

### `intent.md`
- **Goal:** Encode organizational purpose, trade-off hierarchies, and decision boundaries.
- **Content:** Primary goal; what "done" looks like for v1; trade-off tie-breakers (e.g. speed vs accuracy); what the user controls and what the agent must escalate; optional one-sentence summary.
- **Intent interview (1–2 questions):** The onboarding agent gathers intent in two steps: **(Q1)** goal, "done," and controls; **(Q2)** trade-offs and escalation. At each section boundary the **agent** mirrors back what it heard, asks for clarification, incorporates feedback, then moves on (including writing the one-sentence Summary at the top of `intent.md`). See `onboarding-agent.md` for the exact prompts.

### `boundary_log.md` (The Surprise Log)
- **Goal:** Track Boundary Sensing.
- **Content:** A running log of every time the agent output surprises the human user (by succeeding unexpectedly or failing surprisingly). If you aren't logging surprises, you aren't operating at the boundary. Re-evaluate capabilities quarterly based on this log.

---

## 2. Context Engineering & Capability Forecasting (Environment Layer)
*The Environment Layer: Providing the right tokens and planning for obsolescence.*

### `context.md` (or `.claude.md`)
- **Goal:** Curate the optimal set of background tokens.
- **Content:** The institutional context a new human team member would need. DB schemas, coding conventions, architectural decisions, and communication preferences. 
- **Capability Forecasting:** Explicitly track which custom scaffolding in this project is a temporary polyfill (expected to be natively handled by the foundation model in 6-12 months).

---

## 3. Specification Engineering & Seam Design (Action Layer)
*The Blueprint Layer: Turning tasks into autonomous specifications.*

### `task_specifications/` Directory
- **Goal:** A library of project tasks broken down using the 5 Specification Primitives.
- **Template for each spec:**
  1. **Self-Contained Statement:** State the task with zero implicit contextual assumptions.
  2. **Acceptance Criteria:** Exactly what verifiable output signals the task is done.
  3. **Constraint Architecture:** The *Musts*, *Must Nots*, *Preferences*, and *Escalation Triggers*.
  4. **Decomposition:** How a planner agent should break this large task into independent <2 hour subtasks.
  5. **Seam Design (Trigger/Output):** Define the exact "seam" (the verifiable artifact) passed back to a human or another system.

---

## 4. Prompt Craft & Leverage Calibration (Execution Layer)
*The Operation Layer: Minimizing prompt craft while calibrating human review.*

### Execution modes
With Intent, Context, and Specifications defined, you can run work in two ways:

- **Single-spec execution:** One milestone at a time. Example prompt: *"Review `intent.md` and `context.md`. Execute `task_specifications/01_X.md`."* The agent does that spec's work (and may use the development/testing skills in single-agent mode).
- **Orchestrated execution:** Multi-milestone, with memory, Developer/Tester roles (or subagents), and **parallel** tasks when dependencies allow. Example prompt: *"Review `intent.md`, `context.md`, and `orchestration.md`. Run the orchestration."* The agent builds the roadmap from `task_specifications/`, writes tasks to `memory/tasks/`, invokes Developer and Tester with task paths, and runs the full Manager loop. See **`orchestration.md`** and **`docs/framework-flow.md`** for when and how to use it.

### Leverage Calibration
Every task specification must define its review threshold:
- *Autonomous (0% review)*
- *Sampled (10% review)*
- *Full Review (100% review)*

---

## 5. Failure Model Maintenance (Observability Layer)
*The Auditing Layer: Anticipating specific failures instead of generic skepticism.*

### `evals/` Directory
- **Goal:** 3-5 standard test cases (known good inputs and outputs) per critical agent function. Run these systematically after every model update to catch regressions and prevent the "80% problem".

### `failure_model.md`
- **Goal:** A codified mental model of *how* the agent currently fails.
- **Content:** Map specific failures (e.g., "Agent excels at pandas transforms but frequently drops implicit nulls"). Build specific programmatic checks for these failures rather than relying on human due diligence.
