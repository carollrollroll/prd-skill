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

## 9. Common Anti-Patterns

- Writing system tasks ("build API", "add table") as stories.
- Repeating flow prose as AC without pass/fail criteria.
- Merging unrelated conditions into one untestable AC.
- Missing Story/AC IDs or breaking `US-xx` -> `AC-xx-yy` mapping.
