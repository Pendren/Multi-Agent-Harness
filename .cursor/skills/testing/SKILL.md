---
name: testing
description: >-
  Test Author: write acceptance tests from task/spec only (no implementation).
  Test Runner: run pre-written tests only; do not modify tests.
  Use when the Manager delegates a test-author or validation task; path passed at invocation.
---

# Testing (Test Author and Test Runner)

Use this skill when you are the **Tester** and have been given a **task path** in the invocation. The task file name tells you the mode: **`test-author-`** prefix = write tests from spec only; **`validate-`** prefix = run pre-written tests only.

## First step: get your task

1. **Read your task from the path or id given in the invocation.** The Manager will say something like "Your task is in memory/tasks/test-author-01-step2.md" or "Your validation task is in memory/tasks/validate-01-step2.md."
2. **If no path or id was given,** fall back to **memory/current_validation.md** (sequential mode).
3. Open that file. It contains what you must do and where to write or run tests (e.g. evals/acceptance/<task_id>/).

---

## Mode A: Test Author (task path contains "test-author")

**When your task is a test-author task** (e.g. memory/tasks/test-author-01-step2.md):

- **Use only:** the task description, the spec (Acceptance Criteria, Eval Design), intent.md, and context.md. **Do NOT read any implementation**, source code for the feature, or Developer output. No implementation exists yet when you run.
- **Write** acceptance tests that verify the spec's acceptance criteria and the scenarios in the spec's Eval Design. Write them to the **acceptance test directory** given in the task (e.g. **evals/acceptance/01-step2/**). Create the directory if needed.
- **Then exit.** Do not run the tests; do not read implementation. Your only output is the test files in the acceptance test directory.

---

## Mode B: Test Runner (task path contains "validate")

**When your task is a validation task** (e.g. memory/tasks/validate-01-step2.md):

- **Run** the pre-written tests in the acceptance test directory for this task (e.g. evals/acceptance/01-step2/). Do **not** add, change, or remove any tests. Your job is to execute the existing tests and report results.
- **Judge pass/fail** against the spec's Acceptance Criteria only. If a criterion fails, say which one and why (with evidence).
- **Do not modify the implementation** unless the validation task explicitly asks you to fix and re-run. Do not modify the test files under any circumstance.

---

## When done

- **Test Author:** Report where you wrote the tests (path) and that you exited. Do not run tests.
- **Test Runner:** Report PASS or FAIL; which criterion or test failed (if any); short, actionable summary.

---

## Summary

- **Test Author:** Read task → write tests from spec/intent/context only (no implementation) → write to evals/acceptance/<id>/ → exit.
- **Test Runner:** Read task → run pre-written tests in evals/acceptance/<id>/ → do not modify tests → report pass/fail.
