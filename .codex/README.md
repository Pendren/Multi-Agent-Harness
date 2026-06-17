# Codex adapter (placeholder)

This folder is reserved for **OpenAI Codex** (or similar) project-local config and prompts.

**Pattern:** Add the files Codex expects under this tree, and keep them as **thin wrappers** that point to the canonical definitions under **`.agent/agents/`** and **`.agent/skills/`**, matching the structure used in **`.cursor/`**.

The harness ships without Codex-specific filenames here because layouts vary by Codex version and workflow; copy the idea from **`.cursor/agents/*.md`** and **`.cursor/skills/*/SKILL.md`** when you wire Codex to this template.
