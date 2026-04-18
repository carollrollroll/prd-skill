# PRD Structure Index (Focused Mode)

Use this index when drafting PRDs section-by-section.

## File Map
- Section 1 (Why & Who): [prd-structure-section-1.md](prd-structure-section-1.md)
- Section 2 (What & If): [prd-structure-section-2.md](prd-structure-section-2.md)
- Section 3 (How & Next): [prd-structure-section-3.md](prd-structure-section-3.md)
- Full consolidated template: [prd-structure.md](prd-structure.md)

## Supporting References
- Persona & Stakeholders writing guide: [../principles/persona-stakeholder-principles.md](../principles/persona-stakeholder-principles.md)
- NSM metrics writing guide: [../principles/nsm-metrics-principles.md](../principles/nsm-metrics-principles.md)
- User Story & AC writing guide: [../principles/user-story-ac-principles.md](../principles/user-story-ac-principles.md)

## Boundary Contract (Principles vs Structure)
- `principles/`: writing methods, decision rules, quality criteria, anti-patterns.
- `references/prd-structure*.md`: output format definitions only (section order, required fields, ID conventions, table/markdown skeletons).
- If a new rule answers "how to write/judge quality", place it in `principles/` and only link to it from structure files.

## Mode Selection (Full vs Lite)
Use the same section files for both modes. Lite is a generation/review mode, not a separate template file.

- **Full mode**: new product area, new user segment, new monetization model, or any feature needing standalone business justification.
- **Lite mode**: optimization inside an existing module where parent PRD already defines Why & Who.

If unsure, ask: "Does a parent PRD already define the Why & Who for this area?" If yes -> Lite. If no -> Full.

## Lite Mode Rules
When `mode=lite`, apply these constraints:
1. Do not draft Section 1 content in this PRD.
2. Add `Parent Section 1 Reference` before Section 2 starts:
   - Parent PRD link
   - Referenced Section 1 anchor(s) (pain point/JTBD/NSM) used by this Lite PRD
3. Start authoring from Section 2, then Section 3.
4. Section 2 and Section 3 follow normal structure, but describe only changed/new/removed behaviors.
5. Traceability remains mandatory for P0 stories and must map to parent Section 1 anchors.

### Lite Header (required)
```markdown
**Parent PRD:** [Link]
**Parent Section 1 Reference:** [Specific subsection/anchor(s) reused in this Lite PRD]
```

### Lite Validation Checklist (required before drafting Section 2)
1. `Parent PRD` link is accessible to reviewers.
2. `Parent Section 1 Reference` points to specific anchors (not just document title).
3. At least one parent pain point/JTBD anchor is mapped in Section 2 Traceability Matrix.

### Story & AC ID Convention (for Traceability Matrix)
Use explicit Story IDs and AC IDs so matrix mapping is unambiguous:
- Story examples: `US-01`, `US-02`
- Acceptance criteria examples: `AC-01-01`, `AC-01-02` (map to `US-01`)

## Gate Rules
1. Full mode: do not draft Section 2 until Section 1 is explicitly approved.
2. Lite mode: Section 1 gate is satisfied by validated parent reference; drafting starts from Section 2.
3. Do not draft Section 3 until Section 2 is explicitly approved.
4. Section 3 must stay contract-level (ownership, constraints, interfaces), not implementation micromanagement.
5. "Explicitly approved" should be recorded as a clear review signal (e.g., "Section 1 approved on [date]" or PR comment link).

## Required Cross-Section Integrity
1. Every P0 Story in Section 2 must map to a Section 1 pain point/JTBD.
2. Every P0 Story/AC must map to a Section 3 contract or constraint.
3. If any open question exists, it must have a named owner.
4. Distinction rule:
   - `Won't Have (P3)`: out of scope for this release.
   - `Explicit Won't Do`: long-term or permanent out of scope.
