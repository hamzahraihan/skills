# Agent Skills

This repository contains agent skills — small, focused `SKILL.md` files that teach coding agents how to perform specific tasks.

Skills live in `skills/<category>/<name>/SKILL.md`. Add new skills by creating a new directory under `skills/` with a `SKILL.md` that follows the [Agent Skills Specification](https://agentskills.io).

## Installing

Use the [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add <your-username>/skills
```

Pick the skills you want, or install all:

```bash
npx skills add <your-username>/skills --skill '*'
```

## Skill Format

Each skill is a directory containing a `SKILL.md` with YAML frontmatter:

```markdown
---
name: my-skill
description: What this skill does
allowed-tools: shell(git:*)
---

# My Skill

Instructions for the agent.
```

See `skills/engineering/git-micro-commit/SKILL.md` for an example.