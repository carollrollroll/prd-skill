# Business Rules Principles

Use this reference when drafting `Section 2.4`.

## 1. Core Mindset

Section 2.4 is where PM makes feasibility reasoning explicit before product design is locked.

PM writes from a business policy perspective — articulating who should have access, what data must be preserved, and what the product depends on. SA reads the same section and translates each decision into technical constraints: authorization design, schema choices, integration scope.

The writing standard: PM's reasoning must be specific enough that SA can make design decisions without a follow-up question.

- Fails: "Admins have full access."
- Passes: "Project Managers can invite team members but cannot change the tenant's subscription plan."

If PM cannot write a specific rule, that is a signal the business logic has not been fully thought through — not a reason to leave it vague.

## 2. Permission Control (RBAC)

PM decides the business policy: who should be allowed to do what, and why. This is not an implementation spec — it is a business decision about trust and responsibility boundaries.

Express role-action relationships as an RBAC table. Then document the cases the table cannot express:

- Ownership: "can edit only if they are the assigned owner"
- Tenant scope: "can view only within the same tenant"
- Status lock: "cannot modify after status is Approved"
- Delegation: "can act on behalf of if explicitly granted"

For each conditional rule, state the condition and which actions it affects. SA uses this to decide what belongs in middleware, service layer, or JWT claim validation.

**PM asks:** Who in our business should have this power, and who shouldn't — and is that decision defensible?

**SA translates:** Which endpoints need which roles? Which permissions require runtime checks beyond role lookup?

## 3. Version Records

PM decides whether history matters and why. The reason determines the type.

**Audit log** — who did what, when. Use when traceability is the goal: compliance, accountability, debugging. Lightweight; append-only.

**Snapshot** — full state at a point in time. Use when the system must reproduce or roll back to a past state exactly. Higher cost; justify it explicitly.

For each entity that needs history, PM states:
- Why history is needed (compliance requirement, trust, undo capability, historical analysis)
- Which type fits that need
- Which fields or state changes trigger a new record entry

If PM cannot name a reason, do not version the entity. Versioning has schema and performance cost that must be earned.

**PM asks:** Will anyone ever need to know what this looked like at a past point in time — and for what purpose?

**SA translates:** What schema changes are needed? What operations must write to the history table?

## 4. Data Sources and Exports

Two questions with different stakes, treated separately.

**Data sources — dependency and trust:**
For each key entity or field, PM states where the value comes from: user input, computed from other system data, pulled from an external system, or seeded. For external sources, PM states: how fresh the data needs to be, and what the product does when the source is unavailable. This is a product dependency decision — SA uses it to know what to call, what trust level to assign, and what fallback to design.

**Exports — boundary and governance:**
For each export requirement, PM states: what data is included, what format, who receives it, and whether it is on-demand or scheduled. If data contains personally identifiable or sensitive information, PM flags it here. This is a product boundary decision — SA uses it to design export APIs and apply data governance.

**PM asks:** What does our product depend on that we don't control? And what are we responsible for when data leaves the system?

**SA translates:** What external systems does this product call? What does it expose outward, and to whom?

## 5. Common Anti-Patterns

- Writing RBAC as prose ("admins have full access") without a structured table or explicit conditional rules.
- Omitting conditional permissions — ownership, tenant scope, status locks — because they seem obvious.
- Saying "version history required" without stating why, which type, or what triggers a new record.
- Leaving data sources unspecified — SA should not discover mid-implementation that a field comes from an external system.
- Writing rules that restate what user stories already say — restating behavior is not a business rule.
- Keeping rules vague because the business decision hasn't been made yet — surface the open decision explicitly rather than writing around it.
