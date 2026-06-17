ONB0
# Intent Engineering

**Project:** [Project Name]
**Date:** [Current Date]

**Summary (one sentence):** *[The agent's mirror-back after Intent Q2: one sentence capturing the full intent, written after the user has had a chance to clarify. Do not ask the user to supply this; the agent writes it.]*

*This document tells the agent "what to want." It encodes organizational purpose, goals, values, trade-off hierarchies, and decision boundaries. The onboarding agent fills this in two steps (Q1 -> sections 1, 3, 4; Q2 -> sections 2, 3), then mirrors back the full intent, incorporates feedback, and writes the Summary above before moving to context.]*

---

## 1. Project Objectives
- *From Intent Q1. One or two sentences: what should this system accomplish?*
- [Define goal here]

## 2. Trade-Off Hierarchy
*From Intent Q2. When the AI must choose, what does it prioritize? Rank or name the tie-breaker (e.g. "for v1: traceability over speed").*
- [ ] Speed of execution
- [ ] Absolute accuracy / Zero hallucination
- [ ] Cost efficiency
- [ ] User experience / Tone
- [ ] Comprehensive detail
- *Tie-breaker or priority note:* [e.g. "For v1: correctness and debuggability over speed"]

## 3. Decision Boundaries & Escalation Triggers
*From Intent Q1 (controls) and Q2 (escalation). What does the user control? What must the agent never do without asking?*
- **User controls:** [e.g., Observation on/off, when to clear chat, when to start fresh]
- **Autonomous Decisions:** [e.g., Categorizing data, writing first drafts]
- **Must Escalate:** [e.g., Deleting records, emailing external clients, anything not in `evals/`]. **Runtime requirement still missing** after verify, fallbacks, and allowed install attempts per **context.md** - escalate per **Requirement failure state** below.
- **Requirement failure state (runtime prerequisites):** For each runtime requirement listed in the **Runtime / environment requirements** table in **context.md**, if the requirement is not present: (1) **Try alternative methods** where applicable (e.g. on Windows, try `py` if `python` fails). (2) **If the user has authorized the agent to install** missing requirements (see **context.md** "Agent may install" in the runtime requirements table), attempt to install or run the documented install steps. (3) **If the requirement is still not satisfied**, escalate to the user with a clear report: what is missing, what was tried (including alternatives and any install attempt), and what they need to do. Do not assume a requirement is satisfied without running the verify step; do not proceed with work that depends on a missing requirement until it is satisfied or the user has responded to the escalation.

## 4. Output Philosophy & "Done"
*From Intent Q1. What does "done" or "good enough" look like for the first version - one verifiable outcome?*
- [Define success criteria for v1; keep it one concrete, checkable statement where possible]

## 5. Delegation
*Who has architectural or design authority when there are multiple valid options?*
- [e.g., "Agent has architectural control; use user description as fallback" or "User approves all design choices"]
