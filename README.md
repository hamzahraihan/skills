# Skills For Real Engineers

Agent skills that I use every day to do real engineering — not vibe coding.

These skills are designed to be small, focused, composable, and easy to adapt. They work with any model and agent that supports the Agent Skills specification.

## Installation

Pick one method per agent.

### 1. Get the skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugin marketplace add hamzahraihan/skills
claude plugin install skills@hamzahraihan
```

</details>

<details>
<summary><strong>Codex</strong></summary>

```bash
codex plugin marketplace add hamzahraihan/skills
codex plugin add skills@hamzahraihan
```

</details>

<details>
<summary><strong>GitHub Copilot</strong> (CLI and VS Code)</summary>

```bash
copilot plugin marketplace add hamzahraihan/skills
copilot plugin install skills@hamzahraihan
```

In VS Code, run **Chat: Install Plugin From Source** and enter `https://github.com/hamzahraihan/skills`.

</details>

<details>
<summary><strong>Any other agent, or editable files</strong> (manual updates)</summary>

```bash
npx skills@latest add hamzahraihan/skills -a <agent>  # cursor, opencode, devin, windsurf, amp; omit -a to choose
```

To update later:

```bash
npx skills@latest update
```

</details>

## Skills Reference

These split on one axis: who can invoke them. **User-invoked** skills are invoked manually when you run them. **Model-invoked** skills can be triggered directly by you or reached for autonomously by the agent when the task fits.

### Engineering

Skills used for coding workflows and version control discipline.

**Model-invoked**

- **[git-micro-commit](./skills/engineering/git-micro-commit/SKILL.md)**: Make tiny, single-purpose git commits — one file or one logical change at a time — following Conventional Commits format with clean staging hygiene.

## Adding Skills

Each skill is a directory containing a `SKILL.md` with YAML frontmatter following the [Agent Skills Specification](https://agentskills.io):

```markdown
---
name: my-skill
description: What this skill does
allowed-tools: shell(git:*)
---

# My Skill

Instructions for the agent.
```
