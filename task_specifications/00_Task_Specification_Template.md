# Task Specification Template

**Task Name:** [Name of Task]
**Review Threshold:** [Autonomous (0%) | Sampled (10%) | Full (100%)]

*This document defines the blueprint for a specific autonomous task passing between human and agent. It relies on the 5 Primitives of Specification Engineering.*

## 1. Zero-Assumption Problem Statement
- *Describe the task assuming the agent has no implicit context. What exact inputs will it receive and what must it produce?*
- [Input:]
- [Expected Output:]

## 2. Acceptance Criteria (What "Done" Looks Like)
- *Write exactly 3 independent sentences that a third party could use to verify the output without asking you any questions. The agent must pass these before it stops working.*
1. [Condition 1]
2. [Condition 2]
3. [Condition 3]

## 3. Constraint Architecture
- **Must Do:** [Essential requirements]
- **Must Not Do:** [Critical boundaries (e.g., Do not import unauthorized libraries)]
- **Preferences:** [If multiple approaches work, prefer X]
- **Escalation Triggers:** [If X happens, stop and ask the human]

## 4. Sub-Task Decomposition
- *How a planner agent should break this task down into verifiable chunks of < 2 hrs.*
- **Role split:** Per orchestration §2b, the order per task is **Test Author (Tester) → Developer → Test Runner (Tester)**. The Tester in Test Author mode writes acceptance tests from the spec only to evals/acceptance/<task_id>/ before any implementation. The Developer implements from task/spec only and **must not read** evals/acceptance/. The Tester in Test Runner mode runs the pre-written tests only and does not modify them. The Manager does not write tests or implementation; only assigns these tasks.
- **Step 1:** [First verifiable chunk]
- **Step 2:** [Second verifiable chunk]

## 5. Seam Design & Evaluation 
- **Trigger:** How is this task initiated?
- **Output Artifact:** Where does the final deliverable live?
- **Eval Design:** What scenarios must pass for this spec to be considered done? (Describe pass conditions only. The Test Author (Tester) writes tests from this and the acceptance criteria to evals/acceptance/<task_id>/ before implementation; the Test Runner runs those tests and does not modify them.)
