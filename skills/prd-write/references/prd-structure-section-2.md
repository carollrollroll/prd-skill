# PRD Structure — Section 2 (What & If)

Use this focused template when drafting only Section 2.

````markdown
# Phase 2: What & If

> Define what the product looks like and what scenarios it handles.

## 2.1 核心 User Story
*(Optional summary — skip this section if your P0 stories in 2.2 already clearly express the core value and cost of inaction.)*

```
As a ___
I want to ___
So that I can ___.
Because otherwise ___.
```

---

## 2.2 MoSCoW User Stories & Acceptance Criteria

### ID Convention (required for traceability)
- Story IDs: `P0-S1`, `P0-S2`, `P1-S1`...
- AC IDs: `AC-1`, `AC-2` (or scoped format like `P0-S1-AC1`, `P0-S1-AC2`)

### Must Have — P0
> Core flow is broken without these.
> Assign explicit Story ID and AC IDs for traceability.

- **[Story ID: P0-S1] [Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**. Because otherwise **[cost of inaction]**.
  - **Acceptance Criteria:**
    - [ ] **AC-1** Given [context], when [action], then [outcome]
    - [ ] **AC-2** Given [context], when [action], then [outcome]

### Should Have — P1
> Flow works without these, but a workaround is needed.

- **[Story ID: P1-S1] [Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**.
  - **Acceptance Criteria:**
    - [ ] **AC-1** Given [context], when [action], then [outcome]

### Could Have — P2
> Nice-to-have; improves experience but doesn't affect core goal.

- [Story title] — brief description

### Won't Have — P3
> Explicitly out of scope for this version.

- [Story title] — out of scope for **this release**; include rationale and revisit condition

### Traceability Matrix (P0 Required)
> Full mode maps to current PRD Section 1. Lite mode maps to parent PRD Section 1 anchors.

| Section 1 Pain Point / JTBD | P0 Story ID | P0 Story Title | Acceptance Criteria IDs | Section 3 Contract/Constraint Reference |
|-----------------------------|-------------|----------------|--------------------------|-----------------------------------------|
| [Pain/JTBD] | [P0-S1] | [Story title] | [AC-1, AC-2] | [API/State/RBAC/NFR ref] |

---

## 2.3 使用流程 User Flow & Use Cases

### Core Path (Happy Path)
1. [Step 1 — entry point]
2. [Step 2 — key action]
3. [Decision point: if A → go to step X, if B → go to step Y]
4. [Step N — success state]

### Reverse Flow
[What happens when the user cancels, goes back, or undoes? Define each exit point.]

### Edge Cases & Exception Paths
| Scenario | Trigger | Expected Behavior |
|----------|---------|-------------------|
| [Edge case 1] | [What causes it] | [What should happen] |
| [Edge case 2] | [What causes it] | [What should happen] |

### Guardrails & Error Handling
| Error | User-Facing Message | Recovery Action |
|-------|---------------------|-----------------|
| [Error type] | [Message shown] | [How user recovers] |

> Scope rule: use **Edge Cases** for non-error variant scenarios; use **Error Handling** for explicit failure states and recovery.

### Multi-User Interaction (Concurrent Access & Conflict)
[How does the system behave when multiple users act on the same resource simultaneously? Define conflict resolution strategy.]

### Service Blueprint (Optional)
[Include only when cross-layer visibility is needed for alignment.]

---

## 2.4 業務邏輯 Business Logic & Important Notes

### Authorization / RBAC / Do's & Don'ts
| Role | Can Do | Cannot Do |
|------|--------|-----------|
| [Role 1] | | |
| [Role 2] | | |

### Transaction Rules & Events
[Business rules that govern state changes: validations, triggers, side effects]

### Audit Trail & Versioning
[What actions are logged? Who can see the log? Is versioning/rollback required?]

### Source of Truth & Data Export
[What is the canonical data source? What export formats are supported?]

---

## 2.5 NSM Validation via P0 (Required for P0 Changes)

> Section 1 owns NSM direction. This section proves P0 can move it.
> Reference: [../principles/success-metrics-principles.md](../principles/success-metrics-principles.md)

### Section 1 Metric Reference (Do Not Redefine Here)
- NSM (1): [Reference to Section 1.4]
- Leading (optional): [Reference to Section 1.4]
- Lagging (optional): [Reference to Section 1.4]
- Counter (optional): [Reference to Section 1.4]

### P0 Story -> Leading Metric Contribution
| P0 Story ID | Behavior changed by this P0 | Leading metric contribution | Validation signal |
|-------------|-----------------------------|-----------------------------|-------------------|
| [P0-S1] | [Behavior delta] | [How this P0 moves leading] | [Event or log evidence] |

> If no leading metric is defined, replace "Leading metric contribution" with "Direct NSM contribution rationale".

### Causality & Confounder Check
| Link | Why it is causal (not correlation) | Main confounder | Mitigation |
|------|------------------------------------|-----------------|------------|
| [P0 -> Leading -> NSM] | [Reasoning] | [Competing explanation] | [How to control] |

### Optional Data Reliability & Slice Checks (Use when risk is non-trivial)
- **Data reliability thresholds:** missing rate <= [x]%, event delay <= [x] min, duplicate rate <= [x]%
- **Core slice for review:** [new vs returning / plan tier / region]

### Decision Rules (Launch / Iterate / Rollback) (Required)
- If leading is defined and reaches [threshold] within [window], continue rollout and monitor lagging (if defined).
- If leading is defined but fails while adoption is sufficient, revise P0 design/flow.
- If no leading is defined, use direct NSM movement over [window] as the primary iterate signal.
- If counter is defined and breaches [threshold], pause or rollback regardless of leading/NSM gain.
````
