# Test Author (write acceptance tests from spec)

Use this skill when you are the **Test Author** and have been given a **task path** in the invocation (typically **`memory/tasks/test-author-<spec-stem>.md`**).

## First step: get your task

1. **Read your task from the path or id given in the invocation.** The Manager will say something like "Your task is in memory/tasks/test-author-01_ST-01_sample-milestone.md."
2. **If no path or id was given,** fall back to **memory/current_test_author.md** (sequential mode).
3. Open that file. It contains what you must do and the **acceptance test directory** (e.g. **evals/acceptance/<spec-stem>/** - stem matches the **`NN_ST-xx_*.md`** spec basename without `.md`).

## Rules

- **Use only:** the task description, the spec (**Acceptance Criteria**, **Evaluation Design** / **EV-xx**), **intent.md**, and **context.md**. **Do NOT read any implementation**, application source for the feature, or Developer output. No implementation exists yet when you run.
- **Write** acceptance tests that verify the spec's acceptance criteria and **Evaluation Design**. Write them to the directory given in the task (e.g. **evals/acceptance/01_ST-01_sample-milestone/**). Create the directory if needed.
- **Then exit.** Do not run the tests; do not read implementation. Your only output is the test files in the acceptance test directory.

## When done

Report where you wrote the tests (path) and that you exited. Do not run tests.

## Summary

Read task -> write tests from spec/intent/context only (no implementation) -> write to **evals/acceptance/<spec-stem>/** -> exit.
