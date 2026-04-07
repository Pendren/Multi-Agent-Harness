# Test Runner (run pre-written tests)

Use this skill when you are the **Test Runner** and have been given a **task path** in the invocation (typically **`memory/tasks/validate-<spec-stem>.md`**).

## First step: get your task

1. **Read your task from the path or id given in the invocation.** The Manager will say something like "Your validation task is in memory/tasks/validate-01_ST-01_sample-milestone.md."
2. **If no path or id was given,** fall back to **memory/current_validation.md** (sequential mode).
3. Open that file. It contains where to **run** tests (e.g. **evals/acceptance/<spec-stem>/**).

## Rules

- **Run** the pre-written tests in the acceptance test directory for this task. Do **not** add, change, or remove any tests. Your job is to execute the existing tests and report results.
- **Judge pass/fail** against the spec's **Acceptance Criteria** where possible. If a criterion fails, say which one and why (with evidence).
- **Do not modify the implementation** unless the validation task explicitly asks you to fix and re-run. Do not modify the test files under any circumstance.

## When done

Report PASS or FAIL; which criterion or test failed (if any); short, actionable summary.

## Summary

Read task -> run pre-written tests in **evals/acceptance/<spec-stem>/** -> do not modify tests -> report pass/fail.
