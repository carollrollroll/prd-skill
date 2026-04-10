# PRD-Review Report Template

Use this template for the **detailed prd-review output**.
Keep this report in a separate file and only link to it from the main PRD response.

```markdown
## PRD Review — [PRD Title or Feature Name]
Review Date: [today's date] | Type: Full PRD / Lite PRD

---

### Overall Verdict

[One of the three verdicts below, in bold]

[1-2 sentences explaining the verdict — focus on execution readiness, not formatting]

**Gate Decision:** [For full review: "Execution-ready gate: Pass / Conditional / Fail". For section-only review use exactly one: "Ready to proceed to Section 2" / "Ready to proceed to Section 3" / "Ready for execution handoff".]
**Required Coverage:** [For full review: Section 1: X/5 | Section 2: X/6 | Section 3: X/2 — Total X/13. For section-only review: show only the reviewed section score and mark others as N/A.]
**Causal Chain:** [One sentence: does Section 1 problem → Section 2 solution → Section 3 boundary form a coherent chain? Or does each Section talk past the others?]
**Assumption Quality:** [One sentence: are the NSM and assumptions genuinely measurable? If there are structurally unmeasurable items, call them out inline with `[Fallacy]`]
**Scope Discipline:** [One sentence: do P1/P2 Stories stay within the scope Section 1 can justify? Or is there quiet scope expansion?]

---

### 🔧 Fix (PM resolves independently)

> These issues can be resolved by the PM alone. Recommended to fix before sending for review.

1. **[Tag] [Issue Title]**
   - Problem: [what is missing or unclear]
   - Impact: [what will break or get blocked in execution if not fixed]
   - Suggestion: [specific fix]

[Repeat this format for each Fix item. If none, write "None — no items require independent fixes."]

---

### 💬 Discuss (align with PM Lead)

> These are not mistakes — they are decisions or trade-offs that require a higher-level call before moving forward. Bring these with specific questions to the review meeting.

1. **[Tag] [Issue Title]**
   - Current state: [what the PRD currently says or implies]
   - Question: [the specific decision or alignment needed]
   - Why it matters: [what happens in execution if this remains unresolved]

[Repeat this format for each Discuss item. If none, write "None — no items require Lead alignment."]

---

### ✅ OK (well done)

1. **[Item]**: [explain why it's well done — be specific, not generic]

[List 2-5 items. Avoid vague praise. If both Fix and Discuss are `None`, expand praise with 3-6 concrete strengths.]

---

### Decision Summary for PM Lead

**Risk of ambiguity causing mid-execution re-alignment:** High / Medium / Low

**Recommended next steps:**
- [Specific next step — e.g., "Fix the 2 items above and resubmit" or "Schedule a 30-min review meeting to discuss the Discuss items"]
```
