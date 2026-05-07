# User Flow & Use Cases Principles

Use this reference when drafting `Section 2.3`.

## 1. Core Mindset

A flow is a service map, not a narration of clicks. Its job is to reveal the complete closed loop of an intent — from trigger through every state transition back to stable ground — so nothing is left stranded halfway.

Section 2.3 is organized in three layers: happy path, reverse flow, and branch flows. Each layer carries its own use cases. Business rules (pre-checks and side effects) live inside each use case — not in a separate section.

Phase 2 flows describe business intent, not UI mechanics. The reader should understand what the user is trying to accomplish and what the system must handle — not which button gets pressed.

## 2. Three-Layer Structure

**正流程 Happy Path** — primary actor achieves the intended outcome without interruption. Start here. Build the complete happy path before adding reverse or branch flows. This is the spine of the service map; every other layer branches off it.

**逆流程 Reverse Flow** — actor cancels, goes back, or undoes. For each reversal scenario: name the trigger, the state the system returns to, and whether data is preserved or discarded. Reverse flows are not edge cases — they are expected behavior that must be designed, not assumed.

**分支流程 Branch Flow** — conditions that cause the flow to deviate from the happy path. A branch exists when a different condition produces a materially different end state. Each branch must reach a defined end state — not "TBD" and not a dead end. Branches that end in errors must say whether the user can recover.

## 3. Use Case Structure Per Layer

Each use case within a layer follows the same block format:

- **Actor**: who performs the action (primary role; omit if same as layer-level actor)
- **Trigger**: the specific event or condition that initiates this use case
- **Flow**: numbered steps alternating between actor action and observable system response
- **Business Rules**:
  - *Pre-checks*: validation and authorization conditions that must pass before the action completes
  - *Side effects*: system actions beyond the primary write — sub-records, notifications, status cascades, external calls

Business rules belong inside the use case block they govern. Do not collect them into a separate section — that separation is what creates redundancy.

## 4. Build the Map: Happy Path First, Then Close the Loop

Start from use cases to identify the critical path. Once the happy path exists, ask: is every state reachable from this path also escapable? A flow is only complete when every state has a way forward or a defined resolution.

State completeness check:
- Can the user enter this state from the happy path?
- Is there a clear next step or resolution from this state?
- If the system fails here, what does the user see and can they recover?

## 5. Roles: Primary Actor First, Supporting Actors Second

Design each use case from the primary actor's perspective first. Supporting actors appear only when their action blocks or unlocks a state transition for the primary actor. If two roles have equal weight in the same use case, it likely covers two separate use cases — split them.

## 6. Intent Level: Business Logic, Not UI Mechanics

Describe what the user is trying to accomplish, not how the interface is arranged.

- Too vague: "User manages the project." (What changes? What's the end state?)
- Too specific: "User clicks the Create button in the top-right drawer." (UI detail — belongs in UI Spec.)
- Right level: "User creates a project and sets its initial scope and ownership."

The test: if the UI were redesigned tomorrow, would this flow step still be true?

## 7. Two Perspectives: User Flow vs Service Blueprint

**User Flow** (default): describes what the user experiences — intent, observable state transitions, multi-actor handoffs.

**Service Blueprint** (optional): separates what the user sees (frontend) from what happens behind the scenes (backend). Use this when invisible system behavior — async processing, external integrations, background state changes — must be understood to design correctly.

## 8. Scope Rules

1. Every `Must Have` story requires at least one fully described use case in the happy path layer.
2. Assign stable IDs: `UC-[module]-[number]` (e.g., `UC-PRJ-001`). IDs must not change after review.
3. `Won't Have` stories do not require flows.
4. Flows do not prescribe UI layout, API design, or implementation approach.

## 9. Common Anti-Patterns

- Writing only the happy path and marking reverse and branch flows as "TBD."
- Separating business rules into a standalone section instead of embedding them in each use case.
- Using vague intent ("user manages X") without defining what state changes result.
- Prescribing UI mechanics ("user clicks the modal close button") instead of the business action ("user cancels the operation").
- Designing use cases in isolation instead of tracing the full loop from trigger to stable end state.
- Defining a branch that has no defined end state — every path must land somewhere.
