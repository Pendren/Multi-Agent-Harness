ONB0
# Context Engineering

**Project:** [Project Name]
**Date:** [Current Date]

*This document tells the agent **what is true about the environment**: stack, layout, runtime prerequisites, tooling (including MCP), integrations, and durable technical conventions.*

*It does **not** define **what** to build or **in what order** - that is **`task_breakdown.md`** (structure) and **`spec-engineer.md`** (specifications). Purpose, trade-offs, and escalation live in **`intent.md`**. Mixed interview content that is deliverable-shaped still belongs in **`task_breakdown.md`**, not here, except for **project-wide durable** technical facts (see **`onboarding-agent.md`** Section 2).*

---

## 1. Environment & architecture

- **Tech stack:** [e.g., Python 3.11, Next.js, Postgres]
- **Key dependencies:** [libraries and versions that matter for build, test, and CI]
- **Repository layout:** [where application code, configs, tests, docs, and harness files live]
- **Data sources & integrations:** [APIs, databases, queues, external services---how the repo connects]
- **Observability:** [logging, metrics, or tracing expectations if relevant]

---

## 2. Runtime / environment requirements

*What must be installed for builds, tests, or local runs. Onboarding adds one table row per requirement the user names. This table is the **sole** source for prerequisite checks in orchestration and skills. If something is missing, follow **`intent.md`** (requirement failure state).*

| Requirement | Verify (command or check) | Platform fallbacks | Agent may install if missing? |
|-------------|---------------------------|--------------------|-------------------------------|
| [Example: Python 3.x] | [e.g. `python --version` or `py --version`] | [e.g. On Windows: if `python` not found, use `py`] | [yes / no / suggest only] |

- **When to verify:** **`orchestration.md`** at initialization; Developer and Tester skills when running commands (try documented fallbacks before concluding a requirement is missing).

---

## 3. Tools, integrations, and MCP

*Facts about **how** work is done in this repo: shells, CLIs, MCP servers, and other agent-visible tools. List only what the user confirms in onboarding or what **`intent.md`** names as project truth.*

- **Shell / CLI:** [e.g., PowerShell, bash, required global CLIs]
- **Package managers:** [e.g., npm, pip, uv, pnpm]
- **MCP (Model Context Protocol):** [servers available in this workspace; purpose; auth or setup notes if any]
- **Other automation / agent tools:** [e.g., cloud CLIs, internal scripts]

If nothing applies yet, write **`None noted.`** as the only bullet under this heading.

---

## 4. Rules & conventions

- **Coding style / tone:** [e.g., PEP 8, formatter, commit conventions]
- **Acceptance test layout (test-implementation separation):** Acceptance tests are written from the spec **before** implementation and live under **`evals/acceptance/<spec-stem>/`**. The Developer must not read that tree for the active milestone; the Test Author writes from the spec only; the Test Runner runs tests and does not modify them. See **`orchestration.md`**, Section 4.

---

## 5. Capability forecasting & deprecation

*Onboarding uses the decision table in **`onboarding-agent.md`** Section 5 (Context) for when to add a forecasting bullet vs. **`None noted.`** Do not leave this subsection empty.*

- **Temporary polyfill / tooling glue:** [description, or **`None noted.`**]
- **Revisit date:** [date, or **`None noted.`**]
