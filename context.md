ONB0
# Context Engineering

**Project:** [Project Name]
**Date:** [Current Date]

*This document tells the agent "what to know". It curates the optimal set of tokens required for the agent to understand the environment without asking human questions.*

*During onboarding, tech stack, data sources, workflow descriptions, observability strategy, and UI requirements belong here; purpose and decision boundaries belong in `intent.md`.*

## 1. Environment & Architecture
- **Tech Stack:** [e.g., Python 3.11, Next.js, Postgres]
- **Key Dependencies:** [List crucial libraries/versions]
- **Directory Layout Details:** [Explain where things live]

## 1a. Runtime / environment requirements

*What must be installed and present for the project to run (prerequisites). Established during onboarding; orchestration verifies these before starting work that depends on them. If a requirement is not present, the agent follows the **requirement failure state** in intent.md (try alternatives, attempt install if allowed, then escalate).*

| Requirement | Verify (command or check) | Platform fallbacks | Agent may install if missing? |
|-------------|---------------------------|--------------------|-------------------------------|
| [Example: Python 3.x] | [e.g. `python --version` or `py --version`] | [e.g. On Windows: if `python` not found, use `py`] | [yes / no / suggest only] |

*Onboarding agent adds one row per requirement the user names; replace or extend the example row as needed.*

- **When to verify:** Orchestration checks requirements at initialization and before starting milestones that depend on them. Development and testing skills use the verify/fallback rules when running commands (e.g. try the documented alternative before concluding a requirement is missing).

## 2. Rules & Conventions
- **Coding Style / Tone of Voice:** [e.g., Follow PEP8, use descriptive variable names, write in a professional but approachable tone]
- **Acceptance test directory (test-implementation separation):** Acceptance tests are written from the spec **before** implementation and live under **evals/acceptance/** (per-task subdirs e.g. evals/acceptance/01-step2/). The Developer must not read this directory; the Test Author writes here from spec only; the Test Runner runs tests here and does not modify them. See **orchestration.md**, Section 4 (execution loop: Test Author, Developer, Test Runner).
- **Data Structures / DB Schema Context:** [Provide relevant schemas or links to them]

## 3. Spec Candidates / First Specs to Draft
*After onboarding, `task_specifications/` contains only the template (`00_Task_Specification_Template.md`). No concrete specs exist yet. During onboarding, the agent fills this section with a short list of suggested first specs derived from the project (workflows/features the user described). The next session should create initial task specifications from `intent.md` and this file, then execute the first one.*
- [Agent fills during onboarding: e.g. "First feature", "Integration layer", "API or UI surface" — one line per candidate; add v1 order note if applicable]

## 4. Capability Forecasting & Deprecation
*What custom code or scaffolding exist here that we expect foundation models to handle natively in 6-12 months?*
- **Temporary Polyfill:** [e.g., Custom chunking logic for RAG]
- **Review Date:** [Set a date 3 months out to test if the model can do this natively yet]
