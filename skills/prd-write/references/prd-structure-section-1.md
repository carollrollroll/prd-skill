# PRD Structure — Section 1 (Why & Who)

Use this focused template when drafting only Section 1.

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
