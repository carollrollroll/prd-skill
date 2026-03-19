# PRD Skill

A skill for writing clear, structured Product Requirements Documents (PRDs) — works with Claude Code, OpenAI Codex CLI, and Gemini CLI.

## What It Does

When you ask Claude to "write a PRD", "create product requirements", or similar, this skill activates and guides you through a structured process to produce a complete, professional PRD covering:

- Problem statement & goals
- Target users & pain points
- User stories (prioritized P0/P1/P2)
- Functional & non-functional requirements
- UX flows and key screen states
- Technical considerations
- Success metrics
- Timeline & open questions

## Installation

### Claude Code

Copy the skill into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/carollrollroll/prd-skill /tmp/prd-skill
mkdir -p .claude/skills
cp -r /tmp/prd-skill/skills/prd .claude/skills/prd
```

Then invoke it with `/prd` or just ask Claude naturally.

Alternatively, use a git submodule to keep it up to date:

```bash
git submodule add https://github.com/carollrollroll/prd-skill .claude/prd-skill
mkdir -p .claude/skills
cp -r .claude/prd-skill/skills/prd .claude/skills/prd
```

### Codex CLI / Gemini CLI

```bash
git clone https://github.com/carollrollroll/prd-skill
cp -r prd-skill/skills .claude/skills   # Codex picks up AGENTS.md
```

Or run Codex / Gemini directly from the cloned directory:

```bash
cd prd-skill
codex "write a PRD for a dark mode feature"
gemini "write a PRD for a new onboarding flow"
```

## Usage

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

## What You Get

After running the skill, Claude will output a full PRD and offer to:
- Add detail to any section
- Break epics into specific user stories
- Add technical considerations
- Write acceptance criteria
- Create a prioritized roadmap

## Supported CLI Tools

| Tool | Entry Point | How It Works |
|------|-------------|--------------|
| [Claude Code](https://claude.ai/code) | `skills/prd/SKILL.md` | Copy to `.claude/skills/prd/` in your project |
| [OpenAI Codex CLI](https://github.com/openai/codex) | `AGENTS.md` | Read automatically as agent instructions |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | `GEMINI.md` | Read automatically as system context |

All three tools share the same `references/` and `templates/` content — only the entry point differs.

## Templates Included

- **SaaS Feature** — billing, RBAC, and API considerations
- **Mobile App Feature** — platform, offline, and permissions considerations
- **B2B Enterprise** — stakeholder mapping, procurement, multi-tenancy, compliance

## Structure

```
prd-skill/
├── AGENTS.md                      # Entry point for OpenAI Codex CLI
├── GEMINI.md                      # Entry point for Gemini CLI
├── skills/
│   └── prd/
│       ├── SKILL.md               # Entry point for Claude Code
│       ├── references/
│       │   ├── prd-structure.md       # Full 3-phase PRD template
│       │   └── prd-structure-lite.md  # Lite template (Phase 2 & 3 only)
│       └── templates/
│           ├── saas-feature.md        # SaaS-specific guidance
│           ├── mobile-app.md          # Mobile-specific guidance
│           └── b2b-enterprise.md      # B2B / Enterprise guidance
└── README.md
```

## License

MIT
