# Value Capture Principles

Use this reference when drafting `Section 1.3 商業價值 Business Value`.

## 1. Core Mindset

Section 1.3 answers one question: if this feature ships, how does the business benefit — and how much does it cost us not to ship it?

User value and business value are not the same thing. Section 1.3 is explicitly about the latter.

## 2. Time-to-Value (TTV) Rule

`Usage Value / Time-to-Value` must identify the activation moment — the first point where a new user experiences the core value.

State TTV as an observable user action, not a feeling.

- Bad: "Users will quickly understand the value."
- Good: "A user who completes onboarding and runs their first report within the same session has reached the activation moment. Target: within 10 minutes of sign-up."

If TTV is long or unclear, that is a product risk. Name it.

## 3. Packaging and Pricing Rule

`Packaging / Pricing` is optional only when the feature has no pricing dimension. If it does, fill it.

Tier definitions — user limits, project limits, module inclusions, pricing, and positioning rationale — belong in a project-level subscription or pricing reference document, not in individual PRDs.

Before filling this section, ask the user: "Does this project have a subscription or pricing reference document? If so, where is it?" Read that document first; do not restate tier specs here. If no such document exists, note it as a dependency and flag that tier assignment decisions are assumptions pending definition.

For each feature, answer three questions:
1. **Minimum tier**: which tier first unlocks this feature?
2. **Upgrade anchor**: does this feature motivate an upgrade to a higher tier? If yes, which tier and why?
3. **Trial inclusion**: Trial provides full-feature access for 30 days. Should this feature be available during trial? If excluded, state the rationale.

Do not use vague answers like "to be determined by marketing." If tier assignment is genuinely undecided, flag it as an open dependency with a named owner and resolution date.

## 4. Monetization Rule

`Monetization / Economic Buyer` must name who holds the budget and what triggers their decision to pay or upgrade.

- Separate the `user` (who benefits) from the `economic buyer` (who pays). They are often different.
- Identify the trigger: a compliance requirement, a usage threshold, a team-size milestone, a feature unlock.
- If this feature does not directly affect revenue, state the indirect path (retention, upsell enablement, churn reduction) — or mark this field as not applicable with a rationale.

## 5. Opportunity Cost Rule

`Opportunity Cost / Switching Cost` requires two distinct answers:

1. **Opportunity cost of not building**: what we concretely lose — revenue, retention, competitive position — if we skip or defer this.
2. **User switching cost**: how difficult it would be for users to leave if we do not build this — and therefore how much risk we carry if we stay behind.

Both are business arguments. Neither is optional filler.

- Bad: "Users will be unhappy if we don't build this."
- Good: "Without this, enterprise prospects will not pass procurement review — we lose an estimated 3 deals already in the pipeline. Users who adopt a competitor's solution face 6+ months of data migration, which reduces their churn probability but also means we lose them permanently once they switch."

## 6. Common Anti-Patterns

- Restating user value from Section 1.1 instead of making a business value argument.
- Using "increases revenue" or "improves retention" as a complete answer without a mechanism or estimate.
- Marking Monetization as N/A on a paid feature without explanation.
- Writing Opportunity Cost only in terms of user sentiment rather than business impact.
- Leaving TTV as a vague aspiration rather than a concrete observable moment.
