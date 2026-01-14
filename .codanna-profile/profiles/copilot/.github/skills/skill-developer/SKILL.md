---
name: skill-developer
description: Create and maintain Codanna profile skills for Copilot. Use when adding skills, defining triggers, or mapping skills to prompt files and custom agents. Covers skill structure, frontmatter, lightweight trigger rules, and Copilot prompt/agent integration.
---

# Skill Developer Guide (Copilot)

This skill explains how to add and maintain Codanna skill documentation inside the Copilot profile. Copilot does **not** auto-activate skills; instead, skills act as curated guidance for when to use prompt files or custom agents.

## When to Use This Skill

- Creating new skills under `.github/skills/`
- Updating `skill-rules.json`
- Aligning skills with prompt files or custom agents
- Refining skill descriptions and trigger keywords

## Skill System Overview (Copilot)

- **Skills are documentation**: They describe when and how to approach a task.
- **Manual activation**: Use Copilot slash commands or agent selection to apply a skill.
- **Prompt files map to skills**: Create a prompt file per high-value skill so users can invoke it quickly.

### Core Locations

- `.github/skills/{skill-name}/SKILL.md` - Skill content
- `.github/skills/skill-rules.json` - Reference trigger patterns (manual, advisory)
- `.github/prompts/*.prompt.md` - Slash-command prompts
- `.github/agents/*.agent.md` - Custom agents for multi-step work

## Quick Start: Create a New Skill

### Step 1: Create the Skill File

**Location:** `.github/skills/{skill-name}/SKILL.md`

**Template:**

```markdown
---
name: my-new-skill
description: Brief description including keywords that should trigger this skill. Be explicit about topics and use cases.
---

# My New Skill

## Purpose
What this skill helps with

## When to Use
Specific scenarios and conditions

## Key Information
Guidance, patterns, and examples
```

**Best Practices:**

- Use lowercase names with hyphens.
- Keep skill docs under 500 lines.
- Use clear headings and short paragraphs.

### Step 2: Add Optional Trigger Rules

Add an entry in `.github/skills/skill-rules.json` to document when the skill should be used manually.

```json
{
  "my-new-skill": {
    "type": "domain",
    "priority": "medium",
    "description": "Guide for <topic>",
    "promptTriggers": {
      "keywords": ["keyword1", "keyword2"],
      "intentPatterns": ["(create|add).*?topic"]
    }
  }
}
```

### Step 3: Map to a Prompt File (Optional)

Create a matching prompt file so users can invoke the skill by name:

```text
.github/prompts/my-new-skill.prompt.md
```

Set the `name` to match the skill and include an `argument-hint` to guide usage.

### Step 4: Map to a Custom Agent (Optional)

If the skill requires multi-step work, create or extend a custom agent in `.github/agents/`.

## Testing & Validation

- Manually invoke the prompt file from Copilot chat.
- Verify instructions are concise and actionable.
- Confirm the skill content remains under 500 lines.

## Best Practices

- Prefer “why” guidance over obvious commentary.
- Keep descriptions rich with trigger keywords.
- Use progressive disclosure: link to deeper docs instead of dumping everything inline.

## Quick Reference

- Create `SKILL.md`
- Add `skill-rules.json` entry (reference only)
- Create prompt or agent for easy activation
- Test via Copilot chat/agent mode

---

**Note:** Copilot does not implement Claude’s hook-based skill auto-activation, so skills are manual guidance only.
