# Template: SaaS Feature PRD

Use this as a starting point for SaaS product feature requests.

Typical sections to emphasize:
- **Billing impact**: Does this affect pricing tiers or gating?
- **Multi-tenancy**: Does this work correctly per-organization?
- **Permissions/RBAC**: Who in the org can access this?
- **API exposure**: Should this be available via API for enterprise customers?
- **Onboarding**: How do new users discover and learn this feature?

## SaaS-Specific User Stories to Consider

- As a **free tier user**, I want to **[try the feature]**, so that **[I understand its value before upgrading]**. Because otherwise **[I won't evaluate enough value to upgrade]**.
- As a **team admin**, I want to **[manage access]**, so that **[I control what my team sees]**. Because otherwise **[I risk exposing data to the wrong members]**.
- As an **API user**, I want to **[access this via API]**, so that **[I can integrate it into my workflow]**. Because otherwise **[I need manual workarounds that don't scale]**.

## SaaS-Specific Success Metrics to Consider

- Feature adoption rate (% of eligible users who use it within 30 days)
- Upgrade conversion rate from free to paid triggered by this feature
- Support ticket volume related to the feature
- API usage volume (if applicable)
