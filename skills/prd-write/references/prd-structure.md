# PRD Structure Reference

Use this three-phase template when generating PRDs. Phases represent a progression from strategy → definition → implementation.

---

```markdown
# PRD: [Feature/Product Name]

**Author:** [Name]
**Date:** [YYYY-MM-DD]
**Status:** Draft | In Review | Approved
**Version:** 1.0

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

## 1.2 Persona 與用戶心理

### Role Play / Job To Be Done (JTBD)
| Persona | Role | Core Job To Be Done |
|---------|------|---------------------|
| [Primary] | [Job title / context] | When ___, I want to ___, so I can ___ |
| [Secondary] | [Job title / context] | When ___, I want to ___, so I can ___ |

### User Motivation / Cognitive Load
- **Internal triggers:** [Emotional or habitual motivations driving use]
- **External triggers:** [Notifications, prompts, or events that bring users in]
- **Cognitive load concerns:** [What mental effort should we minimize?]

### Stakeholder Relationship
| Stakeholder | Interest | Influence | Notes |
|-------------|----------|-----------|-------|
| [Name/Role] | [What they want] | High / Med / Low | |

### Responsibility & Risk
- **Owner:** [Who is accountable for outcomes]
- **Risks:** [What could go wrong, and who absorbs the cost]

---

## 1.3 商業價值 Business Value

### Usage Value / Time-to-Value (TTV)
[How quickly does a new user experience the core value? What's the activation moment?]

### Packaging / Pricing
[Which tier or plan includes this? Is it gated? How does it appear in pricing?]

### Monetization / Economic Buyer
[Who pays? What triggers a purchase or upgrade decision related to this feature?]

### Opportunity Cost / Switching Cost
- **Opportunity cost of not building:** [What do we lose by skipping this?]
- **User switching cost:** [How hard is it for users to leave if we don't build this?]

---

## 1.4 成功指標 Success Metrics

### North Star Metric
**[The single metric that best represents user value delivered]**

| Type | Metric | Baseline | Target |
|------|--------|----------|--------|
| Leading | [Early signal that we're on track] | | |
| Lagging | [Outcome metric, measured later] | | |
| Counter | [Guardrail — must not get worse] | | |

### Hypothesis Validation
[What assumption are we testing? What result would prove/disprove it?]

### Expected Timeline
[When do we expect to see meaningful signal on each metric above?]

---

# Phase 2: What & If

> Define what the product looks like and what scenarios it handles.

## 2.1 核心 User Story

```
As a ___
I want to ___
So that I can ___.
Because otherwise ___.
```

---

## 2.2 MoSCoW User Stories & Acceptance Criteria

### Must Have — P0
> Core flow is broken without these.

- **[Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**. Because otherwise **[cost of inaction]**.
  - **Acceptance Criteria:**
    - [ ] Given [context], when [action], then [outcome]
    - [ ] Given [context], when [action], then [outcome]

### Should Have — P1
> Flow works without these, but a workaround is needed.

- **[Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**.
  - **Acceptance Criteria:**
    - [ ] Given [context], when [action], then [outcome]

### Could Have — P2
> Nice-to-have; improves experience but doesn't affect core goal.

- [Story title] — brief description

### Won't Have — P3
> Explicitly out of scope for this version.

- [Story title] — why excluded and when it might be revisited

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

# Phase 3: How & Next

> Define how to build it and what comes after.

## 3.1 關鍵後端實體

### Domain Model & Bounded Context
[Which domain/module owns this? What are the boundaries and dependencies?]

### Entity / Aggregate (DB Prototype)
| Entity | Key Fields | Relationships |
|--------|-----------|---------------|
| [Entity 1] | [Fields] | [Related to] |
| [Entity 2] | [Fields] | [Related to] |

### Key Functions / API Contract (API Prototype)
| Method | Endpoint | Request | Response | Notes |
|--------|----------|---------|----------|-------|
| POST | /api/[resource] | [body schema] | [response schema] | |
| GET | /api/[resource]/:id | | [response schema] | |

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

### Capability Roadmap & Scalability
| Phase | Scope | Notes |
|-------|-------|-------|
| v1.0 (this PRD) | [What ships now] | |
| v1.1 | [Near-term follow-on] | |
| v2.0 | [Longer-term evolution] | |

### Future Epics
[Features that are clearly valuable but deferred — with rationale for why not now]

### Explicit Won't Do
[Features that seem related but are permanently or long-term out of scope — why, and what to say if asked]

---

## Open Questions

| # | Question | Owner | Due Date | Status |
|---|----------|-------|----------|--------|
| 1 | [Unresolved decision] | [Name] | [Date] | Open |
| 2 | [Unresolved decision] | [Name] | [Date] | Open |

---

## Appendix

[Supporting research, data, mockups, Figma links, related documents, prior art]
```
