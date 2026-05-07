---
name: prd-check
description: Use this skill when the user wants to validate a specific section of a PRD against quality principles — e.g., "/prd-check nsm", "/prd-check persona", "/prd-check story", "/prd-check flow", "/prd-check moscow", "/prd-check problem", "/prd-check value", "/prd-check rules". Use for targeted, principle-based spot checks on individual PRD sections rather than a full PRD review.
---

# PRD Check Skill

Run a focused, principle-based validation on one specific PRD section.

## Supported Checks

| Arg | 對應章節 | Principles 來源 |
|-----|---------|----------------|
| `problem` | Section 1.1 — 問題與情境 Context | `principles/problem-framing-principles.md` |
| `persona` | Section 1.2 — Persona & Stakeholders | `principles/persona-stakeholder-principles.md` |
| `value` | Section 1.3 — 商業價值 Business Value | `principles/value-capture-principles.md` |
| `nsm` | Section 1.4 — 成功指標 NSM & Metrics | `principles/nsm-metrics-principles.md` |
| `story` | Section 2.1 / 2.2 — User Story & AC | `principles/user-story-ac-principles.md` |
| `moscow` | Section 2 — MoSCoW 優先級 | `principles/moscow-prioritization-principles.md` |
| `flow` | Section 2.3 — 使用流程 User Flow | `principles/user-flow-principles.md` |
| `rules` | Section 2.4 — 業務邏輯 Business Rules | `principles/business-rules-principles.md` |

Principles 檔案路徑相對於本 skill：`../prd-write/principles/<file>.md`

---

## Workflow

### Step 1: Determine Check Type

If the user provided an arg (e.g., `nsm`, `persona`), map it to the corresponding row in the table above.

If no arg is provided, display the supported checks table and ask:
> "Which section do you want to validate? (problem / persona / value / nsm / story / moscow / flow / rules)"

### Step 2: Load Principles File

Read the corresponding `principles/<file>.md` from `../prd-write/principles/`.
This is the authoritative standard — every criterion in this check comes from that file, not from memory.

### Step 3: Locate PRD Content

Confirm where the PRD content is:
1. If the user has pasted PRD content in the conversation, extract the relevant section.
2. If the user provided a file path, read that file and extract the relevant section.
3. If neither, ask: "Please paste the relevant PRD section or provide a file path."

For section-specific checks, focus only on the section that matches the arg.
Do not evaluate out-of-scope sections even if they appear in the pasted content.

### Step 4: Run Targeted Validation

Map each principle from the principles file to the PRD content. For each criterion:

- **✅ OK** — PRD content clearly satisfies the principle
- **🔧 Fix** — Clear violation or missing content; PM can resolve independently
- **💬 Discuss** — Judgment call, ambiguity, or trade-off that needs alignment

Use the following problem type tags as prefixes on Fix / Discuss items:

| Tag | When to use |
|-----|-------------|
| `[Contradiction]` | Two statements cannot both be true |
| `[Gap]` | Implied scenario has no corresponding content |
| `[Fallacy]` | The reasoning is logically flawed |
| `[Redundancy]` | Same behavior described multiple times without added meaning |
| `[Dangling]` | References something undeclared or unowned |
| `[Overreach]` | Specifies implementation details that belong to Engineering |
| `[Unowned]` | Cross-module behavior with no clear owner |

Use one tag per item. If two apply, use the one that best describes the root cause.

Do not manufacture issues to appear thorough.
Do not penalize content that is out of scope for the selected check.

### Step 5: Output

```
## PRD Check: [Section Name]

**File / Section:** [path or section title]
**Principle Reference:** [principles filename]

---

### Findings

**🔧 Fix**
- [Tag] Issue title — specific prescription

**💬 Discuss**
- [Tag] Issue title — specific question

**✅ OK**
- What is working and why (be concrete, not vague)

---

### Verdict

[One of: ✅ Pass / ⚠️ Needs Work / ❌ Blocked]

[1–2 sentence judgment: what specifically passes or blocks, and what the PM should do next]
```

**Verdict definitions:**
- **✅ Pass** — Section satisfies the principles. Ready to proceed.
- **⚠️ Needs Work** — Structurally present but has quality issues. Can proceed with caveats; Fix items should be addressed.
- **❌ Blocked** — One or more Fix items are severe enough to block the next gate or stall execution.

---

## Tone & Style

- Write for the PRD author — direct, actionable, scannable.
- Fix items: give specific prescriptions ("Add a concrete As-Is that describes the current workaround"), not vague ones ("problem statement needs improvement").
- Discuss items: neutral — this is a decision that needs to be made, not an error.
- OK items: be concrete — cite the specific content that satisfies the principle.
- Do not penalize items outside the chosen check scope.
- Do not invent content not present in the PRD — if something is missing, it is missing.
