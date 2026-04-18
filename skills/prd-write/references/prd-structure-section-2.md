# PRD Structure — Section 2 (What & If)

````markdown
# Phase 2: What & If

## 2.1 核心 User Story
*(Optional)*

```
As a ___
I want to ___
So that I can ___.
Because otherwise ___.
```

---

## 2.2 MoSCoW User Stories & Acceptance Criteria
> Reference: [../principles/user-story-ac-principles.md](../principles/user-story-ac-principles.md)

### ID Convention (required for traceability)
- Story IDs: `US-01`, `US-02`, `US-03`...
- AC IDs: `AC-01-01`, `AC-01-02` (map to `US-01`)

### Must Have — P0
- **[Story ID: US-01] [Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**. Because otherwise **[cost of inaction]**.
  - **Acceptance Criteria:**
    - [ ] **AC-01-01 (Happy Path)** Given [context], when [action], then [outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-01-02 (Reverse Flow, optional when applicable)** Given [context], when [cancel/back/undo], then [reverse outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-01-03 (Error Handling, optional when applicable)** Given [error context], when [action], then [error outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] If not applicable: `N/A (reason)`

### Should Have — P1
- **[Story ID: US-02] [Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**.
  - **Acceptance Criteria:**
    - [ ] **AC-02-01 (Happy Path)** Given [context], when [action], then [outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-02-02 (Reverse Flow, optional when applicable)** Given [context], when [cancel/back/undo], then [reverse outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-02-03 (Error Handling, optional when applicable)** Given [error context], when [action], then [error outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] If not applicable: `N/A (reason)`

### Could Have — P2
- **[Story ID: US-03] [Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**.
  - **Acceptance Criteria:**
    - [ ] **AC-03-01 (Happy Path)** Given [context], when [action], then [outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-03-02 (Reverse Flow, optional when applicable)** Given [context], when [cancel/back/undo], then [reverse outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] **AC-03-03 (Error Handling, optional when applicable)** Given [error context], when [action], then [error outcome], and [business rule enforced]
      - Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
      - Verification: [test step + expected evidence]
    - [ ] If not applicable: `N/A (reason)`

### Won't Have — P3
- [Story title] — out of scope for **this release**; include rationale and revisit condition

### Traceability Matrix (P0 Required)
| Section 1 Pain Point / JTBD | P0 Story ID | P0 Story Title | Acceptance Criteria IDs | Section 3 Contract/Constraint Reference |
|-----------------------------|-------------|----------------|--------------------------|-----------------------------------------|
| [Pain/JTBD] | [US-01] | [Story title] | [AC-01-01 (+ optional AC-01-02/03 or N/A note)] | [API/State/RBAC/NFR ref] |

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

> Reference: [../principles/nsm-metrics-principles.md](../principles/nsm-metrics-principles.md)

### Section 1 Metric Reference (Do Not Redefine Here)
- NSM (1): [Reference to Section 1.4]
- Leading (optional): [Reference to Section 1.4]
- Lagging (optional): [Reference to Section 1.4]
- Counter (optional): [Reference to Section 1.4]

### P0 Story -> Leading Metric Contribution
| P0 Story ID | Behavior changed by this P0 | Leading metric contribution | Validation signal |
|-------------|-----------------------------|-----------------------------|-------------------|
| [US-01] | [Behavior delta] | [How this P0 moves leading] | [Event or log evidence] |

### Causality & Confounder Check
| Link | Why it is causal (not correlation) | Main confounder | Mitigation |
|------|------------------------------------|-----------------|------------|
| [P0 -> Leading -> NSM] | [Reasoning] | [Competing explanation] | [How to control] |

### Optional Data Reliability & Slice Checks
- **Data reliability thresholds:** missing rate <= [x]%, event delay <= [x] min, duplicate rate <= [x]%
- **Core slice for review:** [new vs returning / plan tier / region]

### Decision Rules (Launch / Iterate / Rollback) (Required)
- If leading is defined and reaches [threshold] within [window], continue rollout and monitor lagging (if defined).
- If leading is defined but fails while adoption is sufficient, revise P0 design/flow.
- If no leading is defined, use direct NSM movement over [window] as the primary iterate signal.
- If counter is defined and breaches [threshold], pause or rollback regardless of leading/NSM gain.
````
