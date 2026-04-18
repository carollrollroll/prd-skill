# NSM Metrics Principles

Use this reference when defining metrics in PRDs, especially in `Section 1.4` and `Section 2.5`.

## 1. Core Mindset (Problem First)

1. North Star Metric (NSM) starts from the problem we solve, not from what is easy to measure.
2. Measurement exists to validate value delivery, not to replace product thinking.
3. Section 1 defines direction; Section 2 proves product behavior can move that direction.
4. Keep metrics minimal and decision-oriented: precision over quantity.
5. Every metric must have a clear action if it moves (or does not move).

## 2. Role Split by Section

### 2.1 Section 1 (`Why & Who`) owns NSM direction
- Define the core problem and expected behavior change.
- Define one NSM that best represents sustainable user value.
- Explain why this NSM is not a vanity metric.

### 2.2 Section 2 (`What & If`) validates causality via P0
- P0 stories are evidence paths, not the strategic objective itself.
- Show how each P0 behavior contributes to the NSM movement.
- Define validation and rollback rules before build/launch.

## 3. Minimal Metric Set (Default Rule)

- NSM: exactly `1`
- Leading metric: `0..1` (optional, recommended when early signal is clear)
- Lagging metric: `0..1` (optional, recommended when longer-term outcome is observable)
- Counter metric: `0..1` (optional, recommended when local optimization risk is material)

If a team wants more than one leading/lagging/counter metric, they must provide:
1. Explicit risk of omission
2. Distinct decision purpose (not duplicate signal)
3. Named owner for each extra metric

## 4. Formula-Like Decomposition

Use this decomposition to keep logic coherent:

- `Problem -> Behavior Change -> Leading -> NSM -> Lagging`
- `Counter` watches for value illusion or system harm.

Suggested PRD sentence pattern:
- "If we solve `[problem]`, users will do `[behavior]` more consistently, which moves `[leading]`, then `[NSM]`, and later `[lagging]`, while `[counter]` must not degrade."

## 5. Metric Contract (Required Fields)

| Field | Why it is required |
|------|---------------------|
| Metric name | Aligns language across teams |
| Exact definition/formula | Prevents interpretation drift |
| Event/source of truth | Ensures reproducibility |
| Baseline (date range) | Gives context for target difficulty |
| Target (time-bound) | Enables commitment and review |
| Owner | Makes follow-up accountable |
| Decision trigger | Defines what action follows movement |
| Known blind spot | Surfaces metric limits early |

### Required vs Optional (to keep focus)

Required for every PRD:
1. One NSM in Section 1.4 with clear problem linkage
2. NSM metric contract basics: definition, denominator, baseline window, target, owner
3. Structured hypothesis validation: hypothesis, in-scope, out-of-scope

Optional (add only when needed):
1. Leading metric
2. Lagging metric
3. Counter metric
4. Core metric slice (new/returning users, plan tier, region, etc.)
5. Data reliability thresholds (missing, delay, duplicate)
6. Success/failure signal thresholds for hypothesis judgment

## 6. Causality Sanity Check (Before Approval)

1. What exact user problem is being reduced?
2. Which behavior should change first if we are truly solving it?
3. Why does that behavior causally move the chosen NSM?
4. What can fake improvement without real user value?
5. If counter is used, does it reliably catch that failure mode?

If any answer is unclear, do not lock targets yet; refine definitions first.

## 7. Common Anti-Patterns

- Choosing metrics first, then backfilling the problem story.
- Treating P0 completion as proof of value.
- Counting exposure (`view`, `impression`) as value delivery.
- Adding many metrics that do not change decisions.
- Having no explicit rollback condition when counter degrades.
