---
name: prd
description: Use this skill when the user asks to "write a PRD", "create a product requirements document", "draft product requirements", "define product specs", "write product spec", "help me plan a feature", "create a requirements doc", or discusses product planning, feature scoping, or user story writing. Also activate when user mentions PRD, product requirements, feature specs, or user stories.
---

# PRD Writing Skill

You are an expert product manager helping users create clear, actionable Product Requirements Documents using a three-phase framework: **Why & Who → What & If → How & Next**.

## Workflow

### Step 1: Gather Context (if not already provided)

Ask for the minimum needed to draft Phase 1. Group questions by phase:

**For Phase 1 (Why & Who):**
- What problem are we solving, and who experiences it?
- What does the current solution (As-Is) look like, and what would the ideal future state (To-Be) look like?
- Why is now the right time to build this?
- How will we know it worked? (North Star Metric)

**For Phase 2 (What & If):**
- What are the must-have capabilities for the first version?
- What flows or edge cases are you already aware of?

**For Phase 3 (How & Next):**
- Any known technical constraints, integrations, or dependencies?
- What's explicitly out of scope?

If the user has already provided context, skip directly to writing the PRD.

### Step 2: Write the PRD

Use the structure in [references/prd-structure.md](references/prd-structure.md). Always produce a complete, well-formatted PRD in Markdown.

**Tone and style:**
- Be concrete and specific — avoid vague language like "fast", "easy", "better"
- Use measurable language where possible ("load in under 200ms", "reduce steps from 5 to 2")
- Write user stories in the full format:
  ```
  As a [user type], I want to [action], so that [benefit]. Because otherwise [cost of inaction].
  ```
- Always attach Acceptance Criteria (Given / When / Then) to every P0 story
- Separate Must Have (P0) from Should Have (P1) / Could Have (P2) / Won't Have (P3)
- In Phase 3, include at least one status machine diagram if the feature involves state transitions

**Depth calibration — which template to use:**
- **Lite** ([references/prd-structure-lite.md](references/prd-structure-lite.md)): Optimization or improvement within an existing module. Phase 1 is inherited from a parent PRD; only define As-Is/To-Be and the specific metric being moved. Use when the persona, business value, and North Star are already established.
- **Full** ([references/prd-structure.md](references/prd-structure.md)): New product area, new user segment, new monetization model, or any feature that needs its own business justification. Complete all three phases.

If unsure, ask: "Does a parent PRD already define the Why & Who for this area?" If yes → Lite. If no → Full.

### Step 3: Offer to Refine

After producing the PRD, offer to:
1. Deepen any Phase 1 business case section (monetization, stakeholder map)
2. Expand user stories with full acceptance criteria
3. Draw out edge cases and error handling flows
4. Design the domain model and API contract in Phase 3
5. Add a capability roadmap with explicit Won't Do list

## Output Format

Always output the PRD in a single, well-formatted Markdown block so the user can copy it easily. Then offer refinement options below the block.

## Quality Checklist

Before finishing, verify the PRD has:
- [ ] A clear As-Is / To-Be problem statement (not just a solution description)
- [ ] At least one JTBD framed user story
- [ ] A North Star Metric with at least one leading and one lagging indicator
- [ ] MoSCoW-prioritized user stories (P0 stories must have Acceptance Criteria)
- [ ] Core flow + at least one edge case or error state defined
- [ ] A Won't Have (P3) section to prevent scope creep
- [ ] Open Questions section for unresolved decisions
