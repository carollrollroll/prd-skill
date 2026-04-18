# Persona & Stakeholder Principles

Use this reference when drafting `Section 1.2 Persona & Stakeholders`.

## 1. Core Mindset

Persona is not a character profile. Persona is a decision model for user requirements.

## 2. Canonical Persona Model

Use this exact five-column model in `Persona & Requirements`:

1. `Role`
2. `JTBD (When/Want/So I can)`
3. `Internal (Mindset/Cognitive Load)`
4. `External (Stakeholder Dynamics)`
5. `Result (Responsibility/Risk)`

Field intent:
- `Role`: decision-relevant context only.
- `JTBD`: user job and intended outcome.
- `Internal`: internal positive/negative drivers and cognitive burden.
- `External`: stakeholder pressure, dependencies, and constraints.
- `Result`: ownership boundary and downside if things fail.

## 3. Persona Priority Rule (Set Early)

Define persona priority at the start of Section 1.2, not only when conflicts appear.

Use these four dimensions to rank `Primary` and `Secondary` personas:

1. `Risk Ownership`: who bears the consequence if decisions fail.
2. `JTBD Criticality`: whether this persona's JTBD is on the critical path.
3. `Decision Authority`: whether this persona can gate or unblock progress.
4. `Usage Frequency`: how often and how broadly this persona uses the workflow.

Default order: `Risk Ownership` > `JTBD Criticality` > `Decision Authority` > `Usage Frequency`.

## 4. Decision Mapping Rule (Mandatory)

Each persona row must map to concrete outputs:

| Persona Column | Product Decision Output |
|----------------|-------------------------|
| Role + JTBD | Feature scope |
| Internal | UX complexity and cognitive support design |
| External | Workflow, collaboration, and governance design |
| Result | Guardrails, audit, and risk control requirements |

If no decision output exists, the row is non-actionable.

## 5. Stakeholder Relationship Rule

- `Stakeholder Relationship` can be expressed in `ASCII`.
- Focus on role-to-role interaction structure only: who interacts with whom, and in what sequence.
- Do not encode feature logic in the relationship map.
- Include key external influence factors in the map as separate nodes (e.g., regulation, policy, SLA, deadline), with arrows to the roles they influence.
- `Persona & Requirements` defines decision content; `Stakeholder Relationship (ASCII)` defines interaction structure.
- Roles that materially affect decisions, especially final approvers, should be reflected in `Result` with clear traceability.

## 6. Evidence Source Guidance

- Evidence notes are recommended, not mandatory.
- Acceptable source types:
  - `Interview`
  - `Data`
  - `Ticket`
  - `Hypothesis`
  - `Market Observation`
- If `Hypothesis` is used, define validation path in Section 2 (story/AC or experiment).

## 7. Common Anti-Patterns

- Writing demographic persona instead of decision persona.
- Mixing internal and external forces without making decision implications explicit.
- Listing responsibility/risk vaguely without product safeguard implications.
- Making a relationship map that has no effect on `External` or `Result` decisions.
