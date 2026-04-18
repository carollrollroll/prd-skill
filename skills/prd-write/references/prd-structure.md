# PRD Structure Reference

Consolidated output template.

---

````markdown
# PRD: [Feature/Product Name]

**Author:** [Name]
**Date:** [YYYY-MM-DD]
**Status:** Draft | In Review | Approved
**Version:** 1.0

---

### Lite Mode Header (required only when `mode=lite`)
```markdown
**Parent PRD:** [Link]
**Parent Section 1 Reference:** [Specific subsection/anchor(s) reused in this Lite PRD]
```

---

# Phase 1: Why & Who

## 1.1 問題與情境 Context

### As-Is / To-Be
- **Current state (As-Is):** [How users solve this today and what's broken about it]
- **Future state (To-Be):** [What the experience looks like after this ships]

### Market Trend / Why Now?
[What's changed in the market, technology, or user behavior that makes this the right time?]

### Value Proposition / Why Us?
[What unique advantage do we have? Why can't users get this elsewhere?]

---

## 1.2 Persona & Stakeholders
Reference: `../principles/persona-stakeholder-principles.md`

### Persona & Requirements
| Role | JTBD (When/Want/So I can) | Internal (Mindset/Cognitive Load) | External (Stakeholder Dynamics) | Result (Responsibility/Risk) |
|------|----------------------------|-----------------------------------|----------------------------------|------------------------------|
| [Primary role] | When ___, I want to ___, so I can ___ | [What drives or burdens this role mentally] | [How this role interacts with or is constrained by others] | [What this role must own and what risk it bears] |
| [Secondary role] | When ___, I want to ___, so I can ___ | [What drives or burdens this role mentally] | [How this role interacts with or is constrained by others] | [What this role must own and what risk it bears] |

### Stakeholder Relationship (ASCII)
*(Optional)*

```text
[External Factor: Regulation/Policy/SLA/Deadline] --> [Supervisor]
[Requester] --> [Supervisor] --> [Committee Member] --> [Chairman]
      \                |                 |                  /
       \               v                 v                 /
        -------------- [Secretary] -----------------------
```

---

## 1.3 商業價值 Business Value

### Usage Value / Time-to-Value (TTV)
[How quickly does a new user experience the core value? What's the activation moment?]

### Packaging / Pricing
*(Optional)*

[Which tier or plan includes this? Is it gated? How does it appear in pricing?]

### Monetization / Economic Buyer
*(Optional)*

[Who pays? What triggers a purchase or upgrade decision related to this feature?]

### Opportunity Cost / Switching Cost
- **Opportunity cost of not building:** [What do we lose by skipping this?]
- **User switching cost:** [How hard is it for users to leave if we don't build this?]

---

## 1.4 成功指標 Success Metrics

### NSM Direction (Problem-First)
- **Problem being solved:** [What user pain is reduced]
- **Behavior change we expect first:** [What users should do differently]
- **North Star Metric (exactly 1):** [The single metric that best represents sustainable user value]
- **Why this NSM (not vanity):** [Why this reflects real value]

### Required Metric Contract (Must Fill)
| Type | Metric | Definition | Denominator | Baseline Window | Target | Owner |
|------|--------|------------|-------------|-----------------|--------|-------|
| NSM (required, exactly 1) | [Metric name] | [Exact definition/formula] | [All / Active / Affected users] | [e.g., last 28 days] | [Time-bound target] | [Name/Role] |

### Optional Metrics (Fill only if needed)
| Type | Metric | Definition | Denominator | Baseline Window | Target | Owner |
|------|--------|------------|-------------|-----------------|--------|-------|
| Leading (optional, 0..1) | [Early signal] | [Exact definition/formula] | [User set] | [e.g., 7 days] | [Time-bound target] | [Name/Role] |
| Lagging (optional, 0..1) | [Outcome metric] | [Exact definition/formula] | [User set] | [e.g., 28 days] | [Time-bound target] | [Name/Role] |
| Counter (optional, 0..1) | [Guardrail] | [Exact definition/formula] | [User set] | [e.g., 7/28 days] | [Acceptable limit] | [Name/Role] |

### Hypothesis Validation (Structured, Required)
| Field | Content |
|------|---------|
| Hypothesis | [If we solve X problem for Y user in Z context, then NSM should move because ...] |
| In Scope | [What this test validates in this PRD] |
| Out of Scope | [What this test does NOT validate] |
| Success Signal (optional) | [What observation supports the hypothesis] |
| Failure Signal (optional) | [What observation weakens/rejects the hypothesis] |

---

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
| Layer | Step 1: Entry | Step 2: Key Action | Step 3: Confirmation | Step 4: Exit |
|-------|---------------|--------------------|----------------------|--------------|
| **User Action** | [Entry action] | [Key action] | [Confirmation action] | [Exit action] |
| **Frontstage** (UI response) | [UI behavior] | [UI behavior] | [UI behavior] | [UI behavior] |
| **Backstage** (backend process) | [Backend behavior] | [Backend behavior] | [Backend behavior] | [Backend behavior] |
| **Support Processes** (external systems) | [External interaction] | [External interaction] | [External interaction] | [External interaction] |

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

---

# Phase 3: How & Next

## 3.1 關鍵後端實體

### Domain Model & Bounded Context
[Which domain/module owns this? What are the boundaries and dependencies?]

### Entity / Aggregate (Domain Contract)
| Entity | Key Fields | Relationships |
|--------|-----------|---------------|
| [Entity 1] | [Fields] | [Related to] |
| [Entity 2] | [Fields] | [Related to] |

### API Contract (Intent-Level)
| Method | Endpoint | Input Intent | Output Intent | Notes |
|--------|----------|--------------|---------------|-------|
| POST | /api/[resource] | [What conditions/data are required] | [What business outcome/data is returned] | |
| GET | /api/[resource]/:id | [What can be queried and by whom] | [What information is returned] | |

### Status Machine
[Enumerate all states and valid transitions]

```
[State A] --[trigger]--> [State B] --[trigger]--> [State C]
                                  \--[trigger]--> [State D]
```

---

## 3.2 關鍵前端頁面

### Key Pages
| Page | Purpose | Key Actions |
|------|---------|-------------|
| [Page name] | [What user does here] | [Primary CTA / interactions] |

### UI States & Permission Visibility
| Surface | Loading | Empty | Error | Success | Visibility Rule |
|---------|---------|-------|-------|---------|-----------------|
| [Page / Component] | [State behavior] | [State behavior] | [State behavior] | [State behavior] | [Who can see this and under what condition] |

### Data Scale Assumption
[Expected data volume (e.g., list size, growth rate) and whether pagination/lazy loading is required]

### Sitemap URLs
```
/[feature]
/[feature]/:id
/[feature]/:id/[sub-resource]
```

---

## 3.3 技術需求 Technical Requirements & Constraints

### Non-Functional Requirements (NFR)
| ID | Type | Requirement |
|----|------|-------------|
| NF-01 | Performance | [e.g., API response < 200ms at p99] |
| NF-02 | Security | [e.g., All PII encrypted at rest and in transit] |
| NF-03 | Availability | [e.g., 99.9% uptime SLA] |
| NF-04 | Accessibility | [e.g., WCAG 2.1 AA] |

### System Boundary / Dependencies & Integrations
[What external systems, APIs, or internal services does this depend on? What breaks if they're unavailable?]

### Trade-offs & Consequences
[Explicit decisions made and what is accepted as a result]

---

## 3.4 發展藍圖 Roadmap
*(Optional)*

### Capability Roadmap & Scalability
| Phase | Scope | Notes |
|-------|-------|-------|
| v1.0 (this PRD) | [What ships now] | |
| v1.1 | [Near-term follow-on] | |
| v2.0 | [Longer-term evolution] | |

### Future Epics
[Features that are clearly valuable but deferred — with rationale for why not now]

### Explicit Won't Do
[Features that are out of long-term scope and the rationale]

---

## Open Questions
| # | Question | Owner | Due Date | Status |
|---|----------|-------|----------|--------|
| 1 | [Unresolved decision] | [Name] | [Date] | Open |
| 2 | [Unresolved decision] | [Name] | [Date] | Open |

---

## Appendix

[Supporting research, data, mockups, Figma links, related documents, prior art]
````
