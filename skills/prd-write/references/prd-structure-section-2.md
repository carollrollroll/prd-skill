# PRD Structure — Section 2 (What & If)

````markdown
# Phase 2: What & If

## 2.1 核心 User Story
*(Optional)*
> Reference: [../principles/user-story-ac-principles.md](../principles/user-story-ac-principles.md)

```
As a ___
I want to ___
So that I can ___.
Because otherwise ___.
```

---

## 2.2 MoSCoW User Stories & Acceptance Criteria
> Reference: [../principles/user-story-ac-principles.md](../principles/user-story-ac-principles.md)
> Reference: [../principles/moscow-prioritization-principles.md](../principles/moscow-prioritization-principles.md)

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
> Reference: [../principles/user-flow-principles.md](../principles/user-flow-principles.md)

### 正流程 Happy Path
[Primary actor achieves the intended outcome without interruption. Describe the key sequence at a high level.]

**Use Cases:**

#### UC-[module]-001: [Use Case Name]
**Actor**: [Primary role]
**Trigger**: [What initiates this use case]
**Flow**:
1. [Actor action → observable system response]
2. [Next step]
3. [Outcome: end state the user observes]
**Business Rules**:
- Pre-checks: [validation and authorization conditions that must pass]
- Side effects: [system actions beyond the primary write — sub-records, notifications, cascades]

---

### 逆流程 Reverse Flow
[Actor cancels, goes back, or undoes. What state does the system return to? What data is preserved or discarded?]

**Use Cases:**

#### UC-[module]-00N: [Use Case Name]
**Trigger**: [What initiates this reverse — cancel action, timeout, system condition]
**Flow**:
1. [Step → system response]
2. [End state after reversal]
**Business Rules**:
- Pre-checks: [conditions checked before reversal is allowed]
- Side effects: [data released, reservations cancelled, notifications sent]

---

### 分支流程 Branch Flow
[Conditions that cause the flow to deviate from the happy path. Each branch has its own end state.]

**Use Cases:**

#### UC-[module]-00N: [Branch Name]
**Trigger / Condition**: [What causes this branch — permission check fails, validation error, external dependency unavailable]
**Flow**:
1. [Step → system response]
2. [End state: what the user sees and whether recovery is possible]
**Business Rules**:
- Pre-checks: [conditions that route into this branch]
- Side effects: [what the system does when this branch is taken]

---

### Multi-User Interaction (when applicable)
[How does the system behave when multiple users act on the same resource simultaneously? Define conflict resolution strategy.]

### Service Blueprint (Optional)
[Include only when invisible system behavior materially affects user-visible outcomes — async processing, external integrations, background state changes.]

---

## 2.4 業務規則 Business Rules
> Reference: [../principles/business-rules-principles.md](../principles/business-rules-principles.md)

### Authorization / RBAC
| Role | Action | Permission | Condition (if any) |
|------|--------|------------|-------------------|
| [Role] | [Action] | ✅ / ❌ / Conditional | [e.g., owner only, same tenant] |

### Audit Trail & Versioning
[Which entities need history? Type: audit log (who/when) or snapshot (full state). Scope: which fields, what triggers a new entry, retention period.]

### Source of Truth & Data Export
**Data sources:** [For each key field or entity — user input / computed / external system / seeded. For external sources: freshness expectation and unavailability behavior.]

**Exports:** [What data, what format, to whom, on-demand or scheduled. Note any data governance constraints.]

````
