# MoSCoW Prioritization Principles

Use this reference when classifying user stories by priority in PRDs, especially in `Section 2`.

## 1. Core Mindset (Value and Observability First)

1. MoSCoW is not a task importance list; it is a release-scope decision model.
2. Priority must be judged by impact on product operability and success metric outcomes.
3. `Must` protects minimum product viability and metric observability.
4. `Should` increases target hit probability with acceptable temporary workaround.
5. `Could` improves upside performance but does not define release success.
6. `Won't` is explicit scope exclusion for this iteration, with documented rationale.

## 2. Category Definitions (User Story Level)

### 2.1 `Must Have`
- Without this story, the product cannot operate effectively for this release goal.
- Without this story, core success metrics cannot be observed or validated.
- With this story, baseline value delivery is possible and measurement is actionable.

### 2.2 `Should Have`
- Without this story, the product can still run with manual workaround or operational compensation.
- With this story, the chance of reaching success metric targets improves materially.
- Delay is acceptable until the next release if workaround cost and risk are controlled.

### 2.3 `Could Have` / `Nice to Have`
- Without this story, the product still runs smoothly and release success remains valid.
- With this story, metric performance can become stronger and user experience more polished.
- These stories are common candidates for next-iteration highlights.

### 2.4 `Won't Have` (This Iteration)
- Without this story, this release is not materially harmed.
- Story is out of current core scope, belongs to another product-line/mode extension, or has unacceptable current technical cost.
- Keep the idea visible: document why it is excluded now and when to revisit.

## 3. Decision Rules (How to Classify Fast)

Classify each story with this sequence:

1. If removed, does release viability break or metric observability disappear?
   - Yes -> `Must`
   - No -> Go to step 2
2. If removed, can team compensate through a bounded workaround?
   - Yes -> `Should`
   - No -> Go to step 3
3. If removed, does release still succeed with no major risk?
   - Yes -> `Could`
   - No -> Re-evaluate scope or split the story, then classify again
4. If story is outside this iteration's strategic scope or cost envelope:
   - Mark as `Won't` with explicit reason

## 4. Roadmap Priority Mapping (Execution Default)

Use this default mapping when converting MoSCoW into delivery sequence:

- `P` stands for `Priority` (`P0` = `Priority 0`, `P1` = `Priority 1`, `P2` = `Priority 2`).
- `Must Have` -> `P0`
- `Should Have` -> `P1`
- `Could/Nice to Have` -> `P2`
- `Won't Have` -> Out of current roadmap scope

If a team wants to break this mapping, they must document explicit justification and risk.

## 5. Documentation Contract (Mandatory for Alignment)

For each prioritized story, record:

| Field | Why it is required |
|------|---------------------|
| Priority (`Must/Should/Could/Won't`) | Forces explicit trade-off |
| Metric linkage | Prevents "important but unmeasurable" scope |
| Workaround (for `Should`) | Proves delay feasibility |
| Exclusion reason (for `Won't`) | Avoids repeated scope relitigation |
| Revisit trigger/date (for `Won't`, optional but recommended) | Preserves strategic continuity |

## 6. Guardrails (Anti-Inflation)

- `Must` count guideline by release:
  - `<=10`: normal
  - `11..15`: warning zone, require explicit scope-risk review
  - `>15`: too many, should reduce or split scope before commit
- Any `Must` without metric observability justification should be downgraded or rewritten.
- `Should` must include a concrete temporary workaround; otherwise reconsider as `Must`.
- `Won't` must not mean "ignored"; it must include a decision rationale.

## 7. Common Anti-Patterns

- Marking stakeholder preference as `Must` without release-viability evidence.
- Defining `Should` stories without workable manual compensation.
- Using `Could` to hide unresolved requirement conflicts.
- Treating `Won't` as a backlog trash bin without rationale or revisit condition.
