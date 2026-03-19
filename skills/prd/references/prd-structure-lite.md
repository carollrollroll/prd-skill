# PRD Structure Reference — Lite

Use this template for **optimizations or improvements within an existing module**. Phase 1 context (Persona, Business Value, Stakeholder, North Star) is inherited from the parent PRD — no need to redefine it here.

**When to use Lite vs. Full:**
- ✅ Lite: Improving an existing flow, fixing UX friction, performance optimization, incremental feature addition within a known module
- ✅ Full: New product area, new user segment, new monetization model, or any feature that requires its own business justification

---

```markdown
# PRD: [Feature/Optimization Name]

**Author:** [Name]
**Date:** [YYYY-MM-DD]
**Status:** Draft | In Review | Approved
**Version:** 1.0
**Parent PRD:** [Link to parent module PRD]

---

# Phase 1: Context (Lite)

> Full Why & Who context is inherited from the parent PRD above. Only define what's specific to this optimization.

## As-Is / To-Be

- **Current state (As-Is):** [What's broken, slow, or suboptimal today — be specific]
- **Future state (To-Be):** [What the experience looks like after this ships]

## Success Metric for This Optimization

> Inherit the module's North Star. Identify which leading indicator this optimization moves.

| Metric | Type | Baseline | Target |
|--------|------|----------|--------|
| [Leading indicator being improved] | Leading | [Current value] | [Goal] |
| [Guardrail — must not get worse] | Counter | [Current value] | ≥ [floor] |

---

# Phase 2: What & If

## 2.1 User Stories (MoSCoW)

### Must Have — P0

- **[Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**. Because otherwise **[cost of inaction]**.
  - **Acceptance Criteria:**
    - [ ] Given [context], when [action], then [outcome]
    - [ ] Given [context], when [action], then [outcome]

### Should Have — P1

- **[Story title]**
  - As a **[user]**, I want to **[action]**, so that **[benefit]**.
  - **Acceptance Criteria:**
    - [ ] Given [context], when [action], then [outcome]

### Could Have — P2

- [Story title] — brief description

### Won't Have — P3

- [Story title] — why excluded

---

## 2.2 User Flow

### Core Path (Happy Path)
1. [Step 1 — entry point]
2. [Step 2 — key action]
3. [Decision point: if A → step X, if B → step Y]
4. [Step N — success state]

### Reverse Flow
[What happens when the user cancels, goes back, or undoes?]

### Edge Cases & Exception Paths
| Scenario | Trigger | Expected Behavior |
|----------|---------|-------------------|
| [Edge case] | [What causes it] | [What should happen] |

### Error Handling
| Error | User-Facing Message | Recovery Action |
|-------|---------------------|-----------------|
| [Error type] | [Message shown] | [How user recovers] |

---

## 2.3 Business Logic & Notes

### Authorization / RBAC
[Any permission changes? Which roles are affected?]

### Transaction Rules & Events
[Business rules governing state changes: validations, triggers, side effects]

### Audit Trail
[Are any new actions logged? Any changes to existing log entries?]

---

# Phase 3: How & Next

## 3.1 Backend Changes

### Affected Entities / Aggregates
| Entity | Change Type | Details |
|--------|-------------|---------|
| [Entity] | Add field / Modify / New entity | [Specifics] |

### API Changes
| Method | Endpoint | Change | Notes |
|--------|----------|--------|-------|
| [POST/GET/…] | /api/[resource] | New / Modified / Deprecated | |

### Status Machine Changes
[Only if state transitions are added or modified]

```
[Existing State A] --[new trigger]--> [New State X]
```

---

## 3.2 Frontend Changes

### Affected Pages
| Page | Change Type | Details |
|------|-------------|---------|
| [Page / Component] | New screen / Modified flow / New state | [Specifics] |

---

## 3.3 Technical Requirements

### Non-Functional Requirements
| ID | Type | Requirement |
|----|------|-------------|
| NF-01 | Performance | [e.g., Operation completes in < 300ms at p99] |
| NF-02 | Security | [If applicable] |

### Dependencies & Risks
[Other systems, teams, or infra this touches. What could block or break this?]

### Trade-offs
[Any deliberate shortcuts or constraints accepted for this optimization?]

---

## 3.4 Rollout

### Release Strategy
- [ ] Feature flag? Which segment gets it first?
- [ ] Gradual rollout % or full release?
- [ ] Rollback plan if counter metric degrades?

### Explicit Won't Do
[What related improvements are intentionally deferred, and why?]

---

## Open Questions

| # | Question | Owner | Due Date |
|---|----------|-------|----------|
| 1 | [Unresolved decision] | [Name] | [Date] |
```
