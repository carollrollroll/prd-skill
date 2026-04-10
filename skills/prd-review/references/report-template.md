# PRD-Review Report Template

Use this template for the **detailed prd-review output** generated after the consistency sweep.
Keep this report in a separate file and only link to it from the main PRD response.

```markdown
# PRD-Review Report: [Feature/Optimization Name]

**Generated At:** [YYYY-MM-DD HH:mm]
**PRD Version:** [e.g., 1.0]
**Reviewer:** [Name / Agent]
**Overall Status:** Pass | Pass with Risks | Blocked

---

## 1. Executive Summary

- **Status rationale:** [Why this status was given]
- **Top blockers/risks (max 3):**
  - [Risk 1]
  - [Risk 2]
  - [Risk 3]
- **Recommended next action:** [Single clear action]

---

## 2. Sweep Findings by Rule

### 2.1 Cross-Section Consistency
- **Result:** Pass | Risk | Fail
- **Checks performed:**
  - [Rule / enum / condition checked]
  - [Story/AC ↔ Flow ↔ RBAC ↔ Domain alignment check]
- **Findings:**
  - [Issue or "No issue found"]
- **Fix recommendation:**
  - [What to change]

### 2.2 Prohibition Propagation
- **Result:** Pass | Risk | Fail
- **Checks performed:**
  - [Restriction propagation check]
- **Findings:**
  - [Issue or "No issue found"]
- **Fix recommendation:**
  - [What to change]

### 2.3 P0 vs Roadmap Boundary
- **Result:** Pass | Risk | Fail
- **Checks performed:**
  - [Dependency timing check]
- **Findings:**
  - [Issue or "No issue found"]
- **Fix recommendation:**
  - [What to change]

### 2.4 Redundancy Depth Check
- **Result:** Pass | Risk | Fail
- **Checks performed:**
  - [Overlap / entry-point differentiation check]
- **Findings:**
  - [Issue or "No issue found"]
- **Fix recommendation:**
  - [What to change]

---

## 3. Issue List (Actionable)

| ID | Severity | Location | Issue | Recommendation | Owner |
|----|----------|----------|-------|----------------|-------|
| PR-01 | High / Medium / Low | [Section/Story/AC] | [Problem] | [Fix] | [Name] |

---

## 4. Change Suggestions for Next Revision

- [Suggested revision 1]
- [Suggested revision 2]
- [Suggested revision 3]
```
