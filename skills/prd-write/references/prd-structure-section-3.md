# PRD Structure — Section 3 (How & Next)

Use this focused template when drafting only Section 3.

````markdown
# Phase 3: How & Next

> Define how to build it and what comes after.

## 3.1 關鍵後端實體

### Domain Model & Bounded Context
[Which domain/module owns this? What are the boundaries and dependencies?]

### Entity / Aggregate (Domain Contract)
> Capture business-level entities and relationships. Avoid internal schema micromanagement unless explicitly requested.

| Entity | Key Fields | Relationships |
|--------|-----------|---------------|
| [Entity 1] | [Fields] | [Related to] |
| [Entity 2] | [Fields] | [Related to] |

### API Contract (Intent-Level)
> Define API intent and contract boundaries (what/when), not internal implementation details (how).

| Method | Endpoint | Input Intent | Output Intent | Notes |
|--------|----------|--------------|---------------|-------|
| POST | /api/[resource] | [What conditions/data are required] | [What business outcome/data is returned] | |
| GET | /api/[resource]/:id | [What can be queried and by whom] | [What information is returned] | |

### Status Machine
[Enumerate all states and valid transitions]

```
[State A] --[trigger]--> [State B] --[trigger]--> [State C]
                                  \--[trigger]--> [State D]
```

---

## 3.2 關鍵前端頁面

### Key Pages
| Page | Purpose | Key Actions |
|------|---------|-------------|
| [Page name] | [What user does here] | [Primary CTA / interactions] |

### UI States & Permission Visibility
| Surface | Loading | Empty | Error | Success | Visibility Rule |
|---------|---------|-------|-------|---------|-----------------|
| [Page / Component] | [State behavior] | [State behavior] | [State behavior] | [State behavior] | [Who can see this and under what condition] |

### Data Scale Assumption
[Expected data volume (e.g., list size, growth rate) and whether pagination/lazy loading is required]

### Sitemap URLs
```
/[feature]
/[feature]/:id
/[feature]/:id/[sub-resource]
```

---

## 3.3 技術需求 Technical Requirements & Constraints

### Non-Functional Requirements (NFR)
| ID | Type | Requirement |
|----|------|-------------|
| NF-01 | Performance | [e.g., API response < 200ms at p99] |
| NF-02 | Security | [e.g., All PII encrypted at rest and in transit] |
| NF-03 | Availability | [e.g., 99.9% uptime SLA] |
| NF-04 | Accessibility | [e.g., WCAG 2.1 AA] |

### System Boundary / Dependencies & Integrations
[What external systems, APIs, or internal services does this depend on? What breaks if they're unavailable?]

### Trade-offs & Consequences
[Explicit decisions made and what we're accepting as a result]

---

## 3.4 發展藍圖 Roadmap
*(Optional for v1 execution; required when this PRD is used for multi-quarter planning.)*

### Capability Roadmap & Scalability
| Phase | Scope | Notes |
|-------|-------|-------|
| v1.0 (this PRD) | [What ships now] | |
| v1.1 | [Near-term follow-on] | |
| v2.0 | [Longer-term evolution] | |

### Future Epics
[Features that are clearly valuable but deferred — with rationale for why not now]

### Explicit Won't Do
[Features that are long-term or permanently out of scope — why, and what to say if asked]

> Distinction rule: **Won't Have (P3)** = not in this release; **Explicit Won't Do** = long-term or permanent out of scope.

---

## Open Questions
> If any open question exists, a named owner is mandatory.

| # | Question | Owner | Due Date | Status |
|---|----------|-------|----------|--------|
| 1 | [Unresolved decision] | [Name] | [Date] | Open |
| 2 | [Unresolved decision] | [Name] | [Date] | Open |

---

## Appendix

[Supporting research, data, mockups, Figma links, related documents, prior art]
````
