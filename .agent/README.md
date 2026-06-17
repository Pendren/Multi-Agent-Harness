# Canonical agent and skill instructions

This folder is **platform- and model-agnostic**: it holds the **source of truth** for worker behavior (Developer, Test Author, Test Runner) and their skills.

- **`agents/`** — Role prompts (what each worker is and how it starts).
- **`skills/`** — Executable procedure for each role (one `SKILL.md` per skill directory).

**How to use this in a project**

1. **Edit behavior here** — When you change how a worker behaves, change the matching file under **`agents/`** or **`skills/`** only. All supported platforms should stay aligned by reading these files.
2. **Platform folders are adapters** — Each tool keeps its own discovery layout (for example **`.cursor/agents/`** and **`.cursor/skills/`** in Cursor). Those files are **thin wrappers**: they register the agent or skill with the product and tell the model to **read the corresponding file under `.agent/`** and follow it.

**Adding a new platform**

Create a sibling folder (for example **`.codex/`**) and add the markdown files that platform expects, each pointing at the same paths under **`.agent/`**. Keep UI-specific metadata (names, descriptions) in the platform file if the product requires it.
