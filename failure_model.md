# Failure Model

**Project:** [Project Name]
**Last Updated:** [Date]

*A codified mental model of how this specific agent/system currently fails. Use this as a diagnostic runbook for edge cases and to build programmatic checks instead of relying on human due diligence.*

## Current Known Failure Modes

*(Add entries as you discover failure patterns. Template below.)*

### 1. [Name of Failure Type]
- **Symptom:** [How it manifests to the user]
- **Root Cause:** [Why the LLM or system does it]
- **Recovery Action:** [What the human or system must do when this occurs]
- **Mitigation in Evals:** [Yes/No — is this covered by the evaluation suite?]

---

*Example: "Agent excels at pandas transforms but confidently hallucinates string formatting on edge cases. Mitigation: Review all df.apply logic individually. Evals: No."*
