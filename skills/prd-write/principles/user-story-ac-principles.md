# User Story & Acceptance Criteria Principles

Use this reference when drafting `Section 2.1` and `Section 2.2`.

## 1. Core Mindset

1. A user story is a user-goal statement, not a feature label.
2. AC defines observable pass/fail conditions, not implementation steps.
3. Stories define intent; AC defines verifiable behavior boundaries.
4. Decision priority when trade-offs exist: `Verifiability > Consistency > Conciseness`.

## 2. User Story Writing Contract

Default structure:

```text
As a [role],
I want to [action/outcome],
so that [benefit].
Because otherwise [cost of inaction].
```

Quality checks:

1. `Role` is decision-relevant (not generic "user").
2. `I want` describes user outcome (not internal solution).
3. `So that` links to value/metric direction.
4. For P0, include `Because otherwise` to make risk explicit.

## 3. Story Slicing Rules

1. One story = one coherent user goal.
2. Split when outcomes are independent.
3. Split when one story mixes roles.
4. Split when a story has `>=10` ACs or `>=2` unrelated scenario families.
5. Preserve traceability IDs when splitting (e.g., `US-01` -> `US-01A`, `US-01B`).
6. **Split Create and Edit into separate stories when they have different entry points** (e.g., Create triggered from List page modal; Edit triggered from Detail page). A single story must not silently bundle both — if the preconditions, entry UI, and form context differ, they are different user goals.

## 3.5. AC Derivation from Story Terms

AC writing must start from the User Story itself, not the author's intuition. Before writing any AC, decompose every key **noun** and **verb** in the story text and ask: "What constraint does this concept impose on the system?"

**Decomposition steps:**

1. **Nouns** (entities, roles, data) — For each noun, ask: What attributes does it have? Who can read/modify it? What are its valid states?
2. **Verbs** (actions, outcomes) — For each verb, ask: What triggers it? What is the observable result? What are the preconditions?
3. **"So that" clause** — Work backwards from the stated benefit: what must be true for the user to achieve it?
4. **Gap check** — After writing ACs from the above, ask: "Are there implied concepts not yet covered?" Add ACs for any gap found.

**Example — US-01:**
> "As a System Owner, I want to **create** a new **ADR** with **structured fields** so that my **decision is captured completely**."

| Story term | Question | → AC focus |
|------------|---------|------------|
| System Owner | Who has permission to create? What can other roles do? | Permission / RBAC boundary |
| ADR | What entity is created? What fields does it have? | Field definition |
| structured fields | Which fields are required vs. optional? | Validation rules |
| decision is captured completely | What does "complete" mean? Author, timestamp, ID? | Record integrity |
| (implied) | What if the action fails or is cancelled? | Error Handling + Reverse Flow |

**Rule:** Any key noun or verb in the User Story with no corresponding AC is a coverage `[Gap]`. Flag it during review.

---

## 4. AC Contract

Baseline pattern:

```text
Given [context/precondition],
when [user/system action],
then [observable outcome],
and [business rule enforced].
Field Definitions: [field_name: type/required/constraints, optional: default/example/source/format/unit/notes]
Verification: [test step + expected evidence]
```

AC quality checks:

1. Each AC is independently testable (`pass` or `fail`).
2. `Then` is externally observable (UI/state/event/permission).
3. Avoid ambiguous words unless threshold is defined.
4. Keep AC implementation-agnostic unless explicitly required.
5. Every AC must include `Field Definitions` and `Verification`.

## 5. Scenario Coverage Rules

1. Every story must include at least `1` `Happy Path` AC.
2. Add `Reverse Flow` AC when cancel/back/undo (or equivalent reversal) exists.
3. Add `Error Handling` AC when identifiable failure modes exist.
4. If `Reverse Flow` or `Error Handling` does not apply, add `N/A (reason)`.
5. `Won't` stories do not require AC.

## 6. Traceability Rule (Section 1 -> Story -> AC -> Section 3)

For each P0 story, record:

1. Section 1 pain point or JTBD anchor
2. Story ID (`US-01`)
3. AC IDs (`AC-01-01`, `AC-01-02`...)
4. Section 3 contract/constraint reference

ID mapping rule:
- `US-02` maps only to `AC-02-xx`.

## 7. Field Definitions Dictionary

Required attributes:

1. `type`
2. `required` status (`required` / `optional` / conditionally required)
3. core constraints (`range`, `enum`, `uniqueness`, `nullability`, etc.)

Optional attributes:

1. `default`
2. `example`
3. `source`
4. `format`
5. `unit`
6. `notes`

## 8. Canonical Minimal Example

```text
Story: US-01
As a customer,
I want to submit an order,
so that I can complete my purchase.
Because otherwise I cannot receive the product.

AC-01-01 (Happy Path)
Given a valid cart and shipping info,
when the customer confirms checkout,
then the system creates one order and shows confirmation,
and order creation is idempotent for repeated submit in the same session.
Field Definitions: `cart_id` (uuid, required), `shipping_address_id` (uuid, required), `order_id` (uuid, generated, unique, optional: example=`ord_123`).
Verification: Submit checkout twice with same payload; verify only one `order_id` is created.

AC-01-02 (Reverse Flow)
Given the customer is on checkout page,
when the customer taps cancel,
then the system returns to cart without creating an order,
and inventory reservation is released.
Field Definitions: `reservation_status` (enum: reserved/released, required), `order_id` (must remain null).
Verification: Tap cancel; verify redirect to cart and `reservation_status=released`.

AC-01-03 (Error Handling)
Given missing required shipping info,
when checkout is submitted,
then submission is blocked and validation errors are shown,
and no payment authorization request is sent.
Field Definitions: `shipping_address_id` (uuid, required), `validation_error_code` (string, required when invalid), `payment_auth_request_id` (must remain null).
Verification: Submit without `shipping_address_id`; verify validation error and no `payment_auth_request_id`.
```

## 10. Entity Lifecycle Coverage (Status Machine Cross-Check)

When a PRD defines a Status Machine or state/permission table for an entity:

1. List every user-executable action marked available (✅) per status in the Status Machine.
2. Verify each action has at least one User Story covering it as a **standalone user goal** — not merely as a side-effect of another story.
3. Apply Slicing Rule 6: if Create and Edit have different entry points, they must be separate stories.
4. A ✅ action in the Status Machine with no corresponding US is a `[Gap]` finding.

**Common missed patterns:**

| Missed action | Symptom |
|---------------|---------|
| Edit existing entity (draft/active state) | Create US exists, but no Edit US; detail page ends up read-only |
| Delete / Archive from detail page | Delete only covered in list-page bulk action; detail page has no entry point |
| Status transition trigger (e.g., draft → committed) | Mentioned in Status Machine but no US defines the UI trigger or confirmation flow |
| Undo / Revert after state change | Reverse Flow mentioned in flow diagram but no US owns the revert action |

**Check procedure for `/prd-check story`:**

1. Locate the Status Machine section of the PRD.
2. For each entity status row, extract every ✅ column.
3. For each ✅ action, search the US table for a story where that action is the **primary** user goal (not a sub-step).
4. Report missing stories as `[Gap]` findings under `🔧 Fix`.

---

## 9. Common Anti-Patterns

- Writing system tasks ("build API", "add table") as stories.
- Repeating flow prose as AC without pass/fail criteria.
- Merging unrelated conditions into one untestable AC.
- Missing Story/AC IDs or breaking `US-xx` -> `AC-xx-yy` mapping.
