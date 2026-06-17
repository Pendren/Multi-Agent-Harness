# Specification staging (inbox)

**Purpose:** Durable holding area for fragments that are **relevant to specification** but **not yet safe** to write into a formal `NN_ST-xx_*.md` file. The Specification Agent **captures** here when [promotion gates](#promotion-gates) fail.

**Not for:** Skipping **`task_breakdown.md`** updates. Unresolved **`Depends on:`** relationships must be **edited in the breakdown** (or explicitly marked **TBD** there with a one-line note)—staging does **not** replace that resolution.

**Authoritative list:** **`task_breakdown.md`** is the **only** source of truth for **which** **`ST-xx`** exist, how they **depend** on each other, and **structural** decisions (splits, reparenting, active focus). **Record every such change in that file** in the **same session** as the decision so work can **resume** after a crash or stop without relying on chat history.

---

## Promotion gates

Move a fragment from this inbox into a spec **only** when **all** applicable checks pass:

1. **Owning `ST-xx`** — The fragment’s **`ST-xx`** is listed in **`task_breakdown.md`** and matches the filename you will edit. **TBD is not allowed** unless **both** apply: (**a**) the **human** has **explicitly confirmed** in the thread how to triage or which **`ST-xx`** owns the fragment, and (**b**) **`task_breakdown.md`** is **updated in the same session** to record that decision (e.g. clarified **`Depends on:`**, a new **`ST-xx`** entry, or a **one-line note** under **Sub-tasks** / **`## Specification resume`**). **Chat-only** agreement is **not** enough—**disk** must match before **`Target ST-xx: TBD`** may appear or before promotion from **TBD** to a concrete **`ST-xx`**.
2. **Target section (primitive)** — Identified as **Section 1** (Self-Contained Problem Statement) through **Section 5** (Evaluation Design), matching the **Document template** order in **`spec-engineer.md`**.
3. **Dependency honesty** — If the fragment clearly belongs to work **downstream** of another sub-task, **`Depends on:`** in `task_breakdown.md` is **already consistent** with that story, **or** the breakdown is updated in the same session **or** the fragment stays **OPEN** here until it is.
4. **Section sequence (first block)** — Do **not** promote into **Section 3**, **Section 4**, or **Section 5** until **Section 1** and **Section 2** in that **`ST-xx`** spec contain **non-trivial** content (not empty placeholders). Until then, keep those fragments **OPEN** here.
5. **Section maturity (AC before eval)** — Do **not** promote into **Section 5** until **Section 3 Acceptance Criteria** in that **`ST-xx`** spec contains **exactly three** numbered sentences (**1.** **2.** **3.**), matching **`spec-engineer.md`** **Completion gate** (**C**). Until then, keep eval-shaped notes in this inbox.

---

## Open entries

*(Append new entries below. Each entry is **OPEN** until promoted into a spec or **VOID** if duplicate/noise.)*

---

## Resolved

*(Optional: move **PROMOTED** or **VOID** entries here with one-line destination for audit.)*

---

## Entry format (agent)

Use ids **`STG-YYYY-MM-DD-NNN`** (example: **`STG-2026-04-03-001`**): **date** = UTC or local **calendar date** of capture, **NNN** = `001`, `002`, … **for that date**. Before creating a new id, **scan** existing **OPEN** and **Resolved** entries and set **NNN** to **one plus** the highest **NNN** already used **for that date** (per project).

```markdown
### STG-YYYY-MM-DD-NNN — OPEN | PROMOTED | VOID

- **Captured:** <date>
- **Quote or tight paraphrase:** <text>
- **Target ST-xx:** ST-xx | TBD (TBD **only** if human confirmed **and** **`task_breakdown.md`** updated same session—see gate 1)
- **Target section:** Section 1 | Section 2 | Section 3 | Section 4 | Section 5 | TBD
- **Depends / blocking:** <none | blocked on ST-xx | TBD—needs breakdown edit>
- **Breakdown ref:** <`task_breakdown.md` heading or line updated this session, if any—required when Target ST-xx was TBD>
- **Resolution:** <empty until PROMOTED → `path` + Section N or VOID reason>
```
