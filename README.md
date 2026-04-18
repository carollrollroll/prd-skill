# PRD Skill

A skill collection for writing and reviewing Product Requirements Documents (PRDs) in Claude Code.

## Skills Included

### `/prd-write` — Write a PRD

When you ask Claude to "write a PRD", "create product requirements", or similar, this skill activates and guides you through a structured process to produce a complete, professional PRD covering:

- Problem statement & goals
- Target users & pain points
- User stories (prioritized P0/P1/P2)
- Functional & non-functional requirements
- UX flows and key screen states
- Technical considerations
- Success metrics
- Timeline & open questions

### `/prd-review` — Review a PRD

When you ask Claude to "review my PRD", "check if my PRD is ready", or similar, this skill activates a senior PM review workflow that:

- Identifies whether it's a **Full PRD** or **Lite PRD**
- Evaluates completeness across all three phases (Why & Who → What & If → How & Next)
- Classifies issues as **Fix** (PM resolves independently), **Discuss** (align with PM Lead), or **OK**
- Tags issues by problem type: `[Contradiction]`, `[Gap]`, `[Fallacy]`, `[Redundancy]`, `[Dangling]`, `[Overreach]`, `[Unowned]`
- Delivers a verdict: ✅ APPROVED / ⚠️ APPROVED WITH CONDITIONS / ❌ NEEDS REVISION

## Installation

### Claude Code

#### First-time install — all skills

```bash
git clone https://github.com/carollrollroll/prd-skill /tmp/prd-skill
mkdir -p .claude/skills
cp -r /tmp/prd-skill/skills/. .claude/skills/
```

#### First-time install — specific skill only

```bash
git clone https://github.com/carollrollroll/prd-skill /tmp/prd-skill
mkdir -p .claude/skills
cp -r /tmp/prd-skill/skills/prd-write .claude/skills/prd-write          # writing only
# cp -r /tmp/prd-skill/skills/prd-review .claude/skills/prd-review  # add review
```

#### Updating (Nth time)

```bash
cd /tmp/prd-skill && git pull
cp -r /tmp/prd-skill/skills/. .claude/skills/   # overwrites with latest
```

If you only want to update one skill:

```bash
cp -r /tmp/prd-skill/skills/prd-write .claude/skills/prd-write
```

Then invoke with `/prd-write`, `/prd-review`, or just ask Claude naturally.

---

Alternatively, use a **git submodule** so updates are tracked in your repo:

#### First-time install (submodule)

```bash
git submodule add https://github.com/carollrollroll/prd-skill .claude/prd-skill
mkdir -p .claude/skills
cp -r .claude/prd-skill/skills/. .claude/skills/   # all skills
# or copy specific skills:
# cp -r .claude/prd-skill/skills/prd-write .claude/skills/prd-write
```

#### Updating (submodule)

```bash
git submodule update --remote .claude/prd-skill
cp -r .claude/prd-skill/skills/. .claude/skills/
```

## Usage

### Writing a PRD

Just ask naturally — no special command needed:

```
Write a PRD for a dark mode feature in our web app
```

```
Help me create product requirements for a new user onboarding flow
```

```
Draft a PRD for a mobile push notification system
```

The AI will ask clarifying questions if needed, then produce a complete, copy-ready PRD in Markdown.

### Reviewing a PRD

Paste your PRD or provide a file path and ask:

```
Review my PRD
```

```
/prd-review — check if this PRD is ready to submit
```

```
Is this PRD ready? [paste PRD content]
```

The AI will output a structured review report with a clear verdict and actionable next steps.

## What You Get

**After `/prd-write`**, Claude outputs a full PRD and offers to:
- Add detail to any section
- Break epics into specific user stories
- Add technical considerations
- Write acceptance criteria
- Create a prioritized roadmap

**After `/prd-review`**, Claude outputs a structured review report with:
- Overall verdict (APPROVED / APPROVED WITH CONDITIONS / NEEDS REVISION)
- Required coverage score (Section 1: X/6 | Section 2: X/6 | Section 3: X/2)
- Itemized Fix list with specific prescriptions
- Discuss list with questions for PM Lead alignment
- OK highlights with specific praise

## Supported Tool

| Tool | Entry Point | How It Works |
|------|-------------|--------------|
| [Claude Code](https://claude.ai/code) | `skills/prd-write/SKILL.md`, `skills/prd-review/SKILL.md` | Copy to `.claude/skills/` in your project |

## Templates Included

- **SaaS Feature** — billing, RBAC, and API considerations
- **Mobile App Feature** — platform, offline, and permissions considerations
- **B2B Enterprise** — stakeholder mapping, procurement, multi-tenancy, compliance

## Structure

```
prd-skill/
├── skills/
│   ├── prd-write/
│   │   ├── SKILL.md                   # Entry point for Claude Code (/prd-write)
│   │   ├── references/
│   │   │   ├── prd-structure.md       # Full 3-phase PRD template
│   │   │   ├── prd-structure-index.md
│   │   │   ├── prd-structure-section-1.md
│   │   │   ├── prd-structure-section-2.md
│   │   │   ├── prd-structure-section-3.md
│   │   ├── principles/
│   │   │   ├── success-metrics-principles.md
│   │   │   └── persona-stakeholder-principles.md
│   │   └── templates/
│   │       ├── saas-feature.md        # SaaS-specific guidance
│   │       ├── mobile-app.md          # Mobile-specific guidance
│   │       └── b2b-enterprise.md      # B2B / Enterprise guidance
│   └── prd-review/
│       ├── SKILL.md                   # Entry point for Claude Code (/prd-review)
│       └── references/
│           └── report-template.md     # Detailed PRD review report template
└── README.md
```

## License

MIT
