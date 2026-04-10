# Template: B2B Enterprise Feature PRD

Use this as a starting point for B2B or enterprise-facing features. Emphasis is on stakeholder complexity, monetization alignment, and procurement/compliance considerations.

Quick usage guidance:
- **MVP-first (recommended):** start with stakeholder map, 2-4 P0 stories, RBAC minimum, top 3 dependencies, and 3-5 success metrics.
- **Advanced depth (optional):** expand compliance, integration surface, and rollout/roadmap only when required by deal size or risk.

---

## Phase 1 Emphasis — B2B-Specific Angles

### Stakeholder Relationship (誰影響決策)
In B2B there are typically 3–4 distinct roles involved. Map them explicitly:

| Role | Type | Motivation | Blocker |
|------|------|-----------|---------|
| **Economic Buyer** | Decision maker (e.g., VP, CTO) | ROI, cost reduction, compliance | Budget cycle, procurement process |
| **Champion** | Internal advocate (e.g., team lead) | Productivity, personal credibility | Adoption risk, internal politics |
| **End User** | Daily operator | Ease of use, reduced friction | Learning curve, habit change |
| **IT / Security** | Gatekeeper | Security, integrations, supportability | Compliance requirements, SSO/SAML |

### Monetization / Economic Buyer
- Which pricing tier or contract type covers this? (seat-based / usage-based / platform fee)
- Does this unlock upsell to a higher tier or expand existing ACV?
- Who signs off on the purchase — and what does their approval process look like?

### Opportunity Cost / Switching Cost
- Enterprise switching cost is typically high — document defensibility through data gravity, integrations, and workflow fit (avoid relying on forced lock-in alone)
- What does a competitive displacement scenario look like? What would make a customer stay vs. leave?

### Time-to-Value (TTV)
- Enterprise users expect a longer onboarding ramp — what's the "first value moment" within the first 30 days?
- Who drives activation: the end user or an admin/CSM?

---

## Phase 2 Emphasis — B2B-Specific User Stories

### Must-Have Story Patterns to Consider

- As a **team admin**, I want to **[manage member access and roles]**, so that **[I control what my team can see and do]**. Because otherwise **[I can't enforce our internal access policy]**.
- As an **economic buyer**, I want to **[see usage reports and ROI metrics]**, so that **[I can justify the renewal to my leadership]**. Because otherwise **[the contract is at risk at renewal time]**.
- As an **IT/security admin**, I want to **[enforce SSO and disable password login]**, so that **[all access goes through our identity provider]**. Because otherwise **[we fail our SOC 2 audit]**.
- As a **new team member**, I want to **[get up to speed without depending on my manager]**, so that **[I'm productive within my first week]**. Because otherwise **[onboarding blocks team throughput]**.

### Authorization / RBAC — B2B Defaults
Enterprise features typically require at minimum:

| Role | Typical Permissions |
|------|---------------------|
| Organization Owner | Full control including billing, member management, deletion |
| Admin | Manage members, configure settings, view all data |
| Member | Use core features within their scope |
| Viewer / Guest | Read-only, limited to shared resources |
| API / Service Account | Programmatic access, scoped to specific resources |

### Multi-Tenant Considerations
- Data must be strictly isolated per organization — no cross-tenant data leakage
- Admins should only see and manage their own org's data
- If a feature is org-configurable (e.g., SSO, custom domains), define which role controls it

### Audit Trail & Compliance
Enterprise customers typically require:
- [ ] All privileged actions logged with actor, timestamp, and resource ID
- [ ] Logs retained for [X days/years] per compliance requirement (e.g., SOC 2, GDPR, HIPAA)
- [ ] Log export available (CSV / SIEM integration)
- [ ] Admin-visible audit log UI within the product

---

## Phase 3 Emphasis — B2B-Specific Technical Concerns

### Multi-Tenancy Architecture
- Is tenant isolation enforced at the DB level (separate schemas/DBs) or application level (org_id scoping)?
- What's the blast radius if a bug causes cross-tenant data exposure?

### Integration Surface
Enterprise customers expect integrations. Flag which are P0 vs. future:
- **SSO / SAML / OIDC** — often a hard blocker for procurement
- **SCIM (user provisioning)** — needed for large orgs to manage seats via their IdP
- **Webhooks / Event streaming** — so customers can trigger downstream workflows
- **API access** — enterprise tier customers often build internal tooling on top of your API

### SLA & Support Tier
- Does this feature require a different uptime SLA for enterprise customers?
- Is there a dedicated support path (e.g., Slack connect, CSM) that affects how errors surface?

---

## B2B-Specific Success Metrics to Consider

| Metric | Notes |
|--------|-------|
| Feature adoption rate by org (not just user) | An org is "adopted" when ≥ N members use it within 30 days |
| Enterprise renewal rate impact | Track cohort renewal rate for orgs that used the feature vs. those that didn't |
| Time-to-activation (admin setup → first end-user action) | Measures onboarding friction |
| Support ticket volume per org | High volume = adoption friction or UX gap |
| API usage volume | Proxy for deep integration and stickiness |
| Expansion ACV triggered by feature | Did this feature drive upsell to a higher tier? |

---

## Common B2B Pitfalls to Flag in Open Questions

- [ ] Does this feature need to be gated by pricing tier? Which tiers?
- [ ] Is SSO/SAML required before enterprise customers can use this?
- [ ] Do we need a per-org feature flag during rollout (for phased release to enterprise accounts)?
- [ ] Are there data residency or regional requirements for any target customers?
- [ ] Does the feature surface PII that requires DPA / data processing agreements?
