# PRD Structure Reference

Use this three-phase template when generating PRDs. Phases represent a progression from strategy → definition → implementation.
In this document, **Phase** and **Section** are equivalent terms.

Recommended authoring mode:
- **MVP PRD first:** complete all required sections first, then enrich optional sections.
- **Required by default:** As-Is/To-Be, JTBD, Success Metrics, P0 Stories + AC, Core/Edge/Error Flow, RBAC, Dependencies, Trade-offs, Open Questions (if any).
- **Optional by context:** Stakeholder table, Service Blueprint, detailed roadmap/future epics.

Focused references (recommended for section-by-section drafting):
- [prd-structure-index.md](prd-structure-index.md)
- [prd-structure-section-1.md](prd-structure-section-1.md)
- [prd-structure-section-2.md](prd-structure-section-2.md)
- [prd-structure-section-3.md](prd-structure-section-3.md)
- [../principles/persona-stakeholder-principles.md](../principles/persona-stakeholder-principles.md)
- [../principles/success-metrics-principles.md](../principles/success-metrics-principles.md)

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

> Define the value, the audience, and how to prove it worked.

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

Use this section as a compact structure. For detailed writing rules and examples, see `../principles/persona-stakeholder-principles.md`.

### Persona & Requirements
| Role | JTBD (When/Want/So I can) | Internal (Mindset/Cognitive Load) | External (Stakeholder Dynamics) | Result (Responsibility/Risk) |
|------|----------------------------|-----------------------------------|----------------------------------|------------------------------|
| [Primary role] | When ___, I want to ___, so I can ___ | [What drives or burdens this role mentally] | [How this role interacts with or is constrained by others] | [What this role must own and what risk it bears] |
| [Secondary role] | When ___, I want to ___, so I can ___ | [What drives or burdens this role mentally] | [How this role interacts with or is constrained by others] | [What this role must own and what risk it bears] |

### Stakeholder Relationship (ASCII)
*(Optional — include when role interaction is complex.)*

```text
[External Factor: Regulation/Policy/SLA/Deadline] --> [Supervisor]
[Requester] --> [Supervisor] --> [Committee Member] --> [Chairman]
      \                |                 |                  /
       \               v                 v                 /
        -------------- [Secretary] -----------------------
```

- Add evidence notes when available (`Interview` / `Data` / `Ticket` / `Hypothesis` / `Market Observation`) to strengthen requirement confidence.

---

## 1.3 商業價值 Business Value

### Usage Value / Time-to-Value (TTV)
[How quickly does a new user experience the core value? What's the activation moment?]

### Packaging / Pricing
*(Optional — required only if this feature changes packaging, gating, or pricing.)*

[Which tier or plan includes this? Is it gated? How does it appear in pricing?]

### Monetization / Economic Buyer
*(Optional — required only when purchase/upgrade behavior is part of feature value.)*

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

Map the core path across four layers. Each column is one step in the flow; each row is a different layer of the system.

| Layer | Step 1: Entry | Step 2: Key Action | Step 3: Confirmation | Step 4: Exit |
|-------|---------------|--------------------|----------------------|--------------|
| **User Action** | User clicks "[CTA]" on [page] | User fills in [form / selects option] | User sees success state | User navigates away or continues |
| **Frontstage** (UI response) | [Page / modal loads], loading spinner shown | Form validation runs inline | Success toast / confirmation screen rendered | State persisted in UI |
| **Backstage** (backend process) | Auth check, session validated | [API endpoint] called, business rules applied, DB write | Response returned, event emitted (e.g., `resource.created`) | Async jobs triggered (e.g., email, webhook) |
| **Support Processes** (external systems) | — | [Third-party service / internal microservice] called if needed | Notification service sends email/push | Audit log written, analytics event fired |

> **Line of visibility** sits between Frontstage and Backstage — users see above this line, never below.
> **Line of internal interaction** sits between Backstage and Support Processes — marks calls to systems outside this team's ownership.

Fill in only the steps that exist in your core path. Add or remove columns as needed.

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

---

# Phase 3: How & Next

> Define how to build it and what comes after.

## 3.1 關鍵後端實體

### Domain Model & Bounded Context
[Which domain/module owns this? What are the boundaries and dependencies?]

### Entity / Aggregate (Domain Contract)
> Capture business-level entities and relationships. Avoid internal schema micromanagement unless explicitly requested.

| Entity | Key Fields | Relationships |
|--------|-----------|---------------|
| [Entity 1] | [Fields] | [Related to] |
| [Entity 2] | [Fields] | [Related to] |

### API Contract (Intent-Level)
> Define API intent and contract boundaries (what/when), not internal implementation details (how).

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
[Explicit decisions made and what we're accepting as a result — e.g., "we chose eventual consistency to avoid distributed locks, accepting that users may see stale data for up to 30s"]

---

## 3.4 發展藍圖 Roadmap
*(Optional for v1 execution; required when this PRD is used for multi-quarter planning.)*

### Capability Roadmap & Scalability
| Phase | Scope | Notes |
|-------|-------|-------|
| v1.0 (this PRD) | [What ships now] | |
| v1.1 | [Near-term follow-on] | |
| v2.0 | [Longer-term evolution] | |

### Future Epics
[Features that are clearly valuable but deferred — with rationale for why not now]

### Explicit Won't Do
[Features that are **long-term or permanently** out of scope — why, and what to say if asked]

> Distinction rule: **Won't Have (P3)** = not in this release; **Explicit Won't Do** = long-term or permanent out of scope.

---

## Open Questions
> If any open question exists, a named owner is mandatory.

| # | Question | Owner | Due Date | Status |
|---|----------|-------|----------|--------|
| 1 | [Unresolved decision] | [Name] | [Date] | Open |
| 2 | [Unresolved decision] | [Name] | [Date] | Open |

---

## Appendix

[Supporting research, data, mockups, Figma links, related documents, prior art]
````
