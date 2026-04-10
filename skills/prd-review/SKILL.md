---
name: prd-review
description: Use this skill when the user explicitly asks to review a PRD — e.g., "review my PRD", "check if my PRD is ready", "/review", "run a PRD review", "is this PRD ready to submit", "help me review this PRD". Do NOT activate automatically when a PRD is written or updated. Only trigger on explicit review requests.
---

# PRD Review Skill

You are a senior PM reviewer helping assess whether a PRD is ready to move forward into execution. Your output serves two audiences:

- **PM (author)**: Understand what needs to be fixed or clarified before sending for review
- **PM Lead (reviewer)**: Make a fast approve/return decision with all key discussion points clearly surfaced

## Workflow

### Step 1: Locate the PRD

Confirm where the PRD content is:
1. If the user has already pasted the PRD in the conversation, use it directly
2. If the user provided a file path, read the file
3. If neither, ask: "Please paste the PRD content or provide a file path."

### Step 2: Identify PRD Type

Before reviewing, determine whether this is a **Full PRD** or **Lite PRD**:
- **Full PRD**: Covers all three sections (Section 1: Why & Who → Section 2: What & If → Section 3: How & Next). Used for new product areas, new user segments, or features that require their own business justification.
- **Lite PRD**: Section 1 is inherited from a parent PRD; only defines the As-Is/To-Be delta and the specific metric this feature is moving. Used for optimizations or improvements within an existing module.

If unsure, infer from the content. If still ambiguous, ask directly.

Review criteria and depth differ by type — do not penalize a Lite PRD for missing full Section 1 content.

### Step 3: Run the Review

Run the review in two passes to reduce attention fatigue:

1. **Quick Pass (required for every review)**: Run only the core completeness checks and produce an initial verdict.
2. **Deep Pass (triggered only when needed)**: Run logic, consistency, and boundary sweeps if Quick Pass finds risk signals.

Trigger Deep Pass when any of the following appears:
- A likely contradiction across sections (Stories vs Roadmap vs Appendix vs RBAC)
- A role restriction or permission prohibition that could be inconsistently applied
- P0 Stories that seem to depend on roadmap items planned for later versions
- Cross-module ownership or contract ambiguity
- Any repeated behavior that might be duplicate logic vs multi-entry UX

Classify each finding as:

- **🔧 Fix** — PM can resolve independently; missing or unclear enough to block execution
- **💬 Discuss** — Requires alignment with PM Lead; involves business judgment, scope decisions, or ambiguous trade-offs the PM cannot resolve alone
- **✅ OK** — Clear and well done

Do not force ambiguous items into Fix. If the PRD mentions something but the answer is unclear or contested, mark it as Discuss with a specific question.

For each Fix or Discuss item, prefix the issue title with a **problem type tag** so readers grasp the nature of the problem before reading the details:

| Tag | When to use |
|-----|-------------|
| `[Contradiction]` | Two statements cannot both be true (e.g., a P0 Story depends on a P2 feature) |
| `[Gap]` | Something implied by the flow or data model has no corresponding Story, AC, or owner |
| `[Fallacy]` | The reasoning itself is logically flawed — the conclusion doesn't follow from the premise (e.g., the NSM denominator cannot be observed) |
| `[Redundancy]` | Multiple Stories or ACs describe the same behavior without adding new meaning |
| `[Dangling]` | References a dependency that is undeclared, out of scope, or unowned |
| `[Overreach]` | PM is specifying implementation details that belong to Engineering |
| `[Unowned]` | Cross-module behavior with no clear owner or integration contract |

Use only one tag per issue. If two apply, choose the one that best describes the root cause.

### Step 4: Output the Review Report

Follow the output format below strictly.

When possible, package output in two layers:
- **Detailed report (separate file)**: Write full findings into a standalone markdown file using [references/report-template.md](references/report-template.md).
- **Main response (concise)**: Keep a short summary in chat:
  - Overall verdict
  - Top 3 blockers/risks
  - Path/link to the detailed report file
- **Fallback**: If file output is unavailable, include the detailed report in chat using the same structure.

---

## Review Criteria

### Pass Structure

- **Quick Pass (always run first)**: completeness and execution readiness checks
- **Deep Pass (run only when triggered)**: logic quality, cross-section consistency, and boundary/ownership stress tests

### Full PRD

**Quick Pass — Section 1 (Why & Who)** *(counts toward required coverage: 4 points)*
- [ ] Problem statement has a clear As-Is and To-Be (not just a solution description)
- [ ] At least one user story or persona framed with JTBD
- [ ] North Star Metric defined — assess whether it genuinely reflects core product value (not a vanity metric or a manipulable proxy); flag if the NSM doesn't align with the business objective
- [ ] Business value articulated — why this feature, why now

**Deep Pass — Section 1 Quality Traps (Soul Check)**

After completing the completeness check, ask: *Does this section say anything genuinely specific?* Flag if:
- Problem statement is generic ("users need a better experience") with no concrete, observable pain point
- As-Is description is vague enough to apply to any product
- "Why now" only lists industry trends without connecting to a specific timing trigger for this product
- NSM sounds reasonable but cannot distinguish success from failure (e.g., "improve engagement" with no direction or threshold)
- Persona reads like a job title with attributes, not a real person with specific tension and motivation
- The entire section could be copy-pasted into a competitor's PRD unchanged — if so, it has no soul

**Quick Pass — Section 2 (What & If)** *(counts toward required coverage: 5 points)*
- [ ] User Stories are MoSCoW-prioritized (P0 / P1 / P2 / P3)
- [ ] Every P0 Story has testable, unambiguous Acceptance Criteria — each AC should describe the condition, action, and expected outcome; flag ACs that are vague, missing conditions or results, or written as requirements rather than acceptance criteria (Given/When/Then is one valid format, not the only one)
- [ ] Core happy path defined with clear steps
- [ ] At least one edge case or error state defined
- [ ] Won't Have (P3) section exists to control scope

**Deep Pass — Section 2 Quality Traps (Logic & Coherence Check)**

After the completeness check, examine logical rigor and coherence with Section 1:
- **Coherence**: Do User Stories extend from the Persona and JTBD defined in Section 1? If Section 1 defines a specific pain point, Section 2 should solve that pain point — not a different one
- **Contradiction**: Do any two Stories, ACs, or flow steps imply conflicting behavior? (e.g., one Story says "user can edit at any time," another says "locked after submission," with no reconciliation)
- **Gap**: Are there implied scenarios in the flow with no Story or AC covering them? (e.g., what happens when an async process fails mid-way)
- **Redundancy**: If two Stories/ACs look overlapping, ask whether they describe the same operation through the same UI entry point or the same logic via different entry points. If same entry point + same operation, mark `[Redundancy]` and propose merge. If different entry points, require explicit UX distinction and trigger context in PRD; otherwise still mark `[Redundancy]`.
- **Fallacy**: Does the flow assume a state that was never established? Does error handling reference an unreachable state?
- **Scope drift**: Do P1/P2 Stories quietly expand beyond what Section 1 can reasonably justify?
- **Prohibition rule propagation**: If PRD defines an operation restriction (e.g., "role X cannot do Y"), verify the rule is consistently enforced in P0 ACs, reverse/error flows, and RBAC "cannot perform" matrix. If any section points to a removed or nonexistent operation path, mark `[Dangling]`.

**Quick Pass — Section 3 (How & Next)** *(counts toward required coverage: 3 points)*
- [ ] Known technical dependencies or constraints are listed
- [ ] Open Questions section exists with an owner per question
- [ ] If the feature involves state transitions, a state machine diagram is included

**Deep Pass — Section 3 Quality Traps (Boundary & Ownership Check)**

Section 3 should define *what to build* and *where the boundaries are* — not *how to build it*. Flag if:
- **Over-specification**: PM is specifying Engineering implementation details (specific algorithms, database field names, exact API request/response schemas) — PM should define the contract and constraints, not internal implementation
- **Unclear boundary**: It's not clear what this module owns versus what it depends on from other modules or external systems
- **Section 2 coherence**: Does Section 3 cover all P0 Stories? If a P0 Story implies a state machine, API, or permission model, Section 3 should reflect it
- **P0 × roadmap boundary mismatch**: For each P0 Story AC, check whether required feature dependencies are roadmap-gated to v1.1+ (state transitions, events, archive, permission hooks, etc.). If yes, mark `[Contradiction]` and require one explicit decision: pull dependency into v1.0, or downgrade the AC/Story priority.
- **Roadmap without rationale**: Future Epics or Won't Do items should explain *why not now*, not just list feature names
- **Trade-offs without consequences**: If trade-offs are listed, the accepted cost should be explicit — "we chose X, accepting that Y will happen"

**Deep Pass — Cross-Section Consistency Sweep (Global Alignment Check)**

After section reviews, run a whole-document consistency sweep for core rules and terms. For each core rule (trigger conditions, unlock conditions, role restrictions, event types/enums), verify all mentions are mutually consistent across:
- User Story ACs
- Core/Reverse flows
- RBAC matrix
- Domain model / state machine / integration contracts
- Appendices and roadmap notes

When inconsistencies are found:
- Use `[Contradiction]` for two active statements that cannot both be true
- Use `[Dangling]` for stale text pointing to removed or nonexistent behavior
- Prefer one source-of-truth wording and request all outdated copies be updated in the same revision

**Deep Pass — Cross-Module Story Ownership Check**

If the PRD touches other modules, check:
- **Story ownership**: Every User Story should belong to the module team responsible for building it. The actor in a Story is a hint, but the real question is: *who builds this?* Flag Stories that clearly belong to another module
- **Integration contract**: For any cross-module dependency, the PRD should declare the boundary — what events this module emits, what events it consumes, and the expected payload format. This replaces duplicating Stories across PRDs
- **Missing contract**: If there are cross-module Stories but no integration contract section, flag it — a PM may consolidate everything into one PRD for completeness (acceptable in draft), but ownership must be assigned before sign-off
- **Duplication**: If the same behavior appears as a full Story in both this PRD and another module's PRD, mark as Discuss — one side should own the Story and the other should reference the contract

### Lite PRD

**Quick Pass — Delta Definition**
- [ ] As-Is / To-Be delta is specific and measurable (not just "improve X")
- [ ] The specific metric being moved has a defined baseline and target value
- [ ] References a parent PRD or inherited context

**Quick Pass — Section 2 (What & If)** (same as Full PRD)
- [ ] P0 Stories have Acceptance Criteria
- [ ] Core path + at least one edge case
- [ ] Won't Have section

**Quick Pass — Section 3 (How & Next)** (same as Full PRD)
- [ ] Dependencies and Open Questions, each with an owner

**Deep Pass — Apply Full PRD deep checks when triggered**
- Reuse Full PRD deep checks that are relevant to the scope (Section 1 soul checks only if Lite includes Section 1 claims)
- Always include cross-section consistency and boundary/ownership checks when contradictions or stale references are suspected

---

## Output Format

```
## PRD Review — [PRD Title or Feature Name]
Review Date: [today's date] | Type: Full PRD / Lite PRD
Review Mode: Quick Pass / Quick + Deep Pass

---

### Overall Verdict

[One of the three verdicts below, in bold]

[1–2 sentences explaining the verdict — focus on execution readiness, not formatting]

**Required Coverage:** Section 1: X/4 | Section 2: X/5 | Section 3: X/3 — Total X/12 (see Fix section for gaps)
**Causal Chain:** [One sentence: does Section 1 problem → Section 2 solution → Section 3 boundary form a coherent chain? Or does each section talk past the others?]
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

- [Item]: [explain why it's well done — be specific, not generic]

[List 2–5 items. Avoid vague praise.]

---

### Decision Summary for PM Lead

**Risk of ambiguity causing mid-execution re-alignment:** High / Medium / Low

**Recommended next steps:**
- [Specific next step — e.g., "Fix the 2 items above and resubmit" or "Schedule a 30-min review meeting to discuss the Discuss items"]
```

---

## Verdict Definitions

Use one of the following three verdicts:

- **✅ APPROVED** — PRD is execution-ready. Engineering and Design can begin without expecting major re-alignment.
- **⚠️ APPROVED WITH CONDITIONS** — Core structure is sound, but 1–2 Discuss items should be resolved before or during kick-off. PM Lead may approve conditionally, requiring those items to be addressed.
- **❌ NEEDS REVISION** — One or more blockers exist that will stall Engineering or require significant mid-execution rework. Return to PM for revision.

---

## Tone & Style Principles

- Write for a time-constrained PM Lead — direct, scannable
- Fix items: give specific prescriptions ("add Given/When/Then AC to Story 2"), not vague ones ("ACs need improvement")
- Discuss items: stay neutral — the PM didn't write something wrong, this is just a decision that needs to be made
- OK items: be specific — "North Star Metric includes both a leading indicator (weekly active reviewers) and a lagging indicator (PRD cycle time)" is more useful than "metrics are well written"
- Do not invent content not in the PRD to fill gaps — if something is missing, it is missing
- Problem type tags (`[Contradiction]`, `[Gap]`, etc.) are diagnostic labels, not severity signals — `[Fallacy]` can be minor, `[Gap]` can be a blocker; let the content text convey severity
- The three verdict lines (causal chain / assumption quality / scope discipline) should be stated as clear judgments, not hedged — "Section 1 → Section 2 is coherent, Section 3 boundary is clear" is more useful than "Section 1 and Section 2 seem broadly aligned"
- When counting required coverage, only mark ✅ if the item is clear and substantive — vague hand-waving does not count. If an item exists but has quality issues (e.g., NSM exists but is not measurable), count it as covered and call out the quality issue under Assumption Quality or Fix. The score reflects completeness, not quality.
