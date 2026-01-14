---
name: skill-developer
description: Create and maintain Codanna profile skills for Codex. Use when adding skills, defining triggers, or mapping skills to Codex workflows. Covers skill structure, frontmatter, lightweight trigger rules, and AGENTS.md integration.
---

# Skill Developer Guide (Codex)

This skill explains how to add and maintain Codanna skill documentation inside the Codex profile. Codex does **not** auto-activate skills; instead, skills act as curated guidance for when to use Codanna workflows.

## When to Use This Skill

- Creating new skills under `skills/`
- Updating `skills/skill-rules.json`
- Aligning skills with AGENTS.md guidance
- Refining skill descriptions and trigger keywords

## Skill System Overview (Codex)

- **Skills are documentation**: They describe when and how to approach a task.
- **Manual activation**: Reference skill docs when prompts indicate the topic.
- **AGENTS.md remains the source of truth** for Codex project instructions.

### Core Locations

- `skills/{skill-name}/SKILL.md` - Skill content
- `skills/skill-rules.json` - Reference trigger patterns (manual, advisory)
- `AGENTS.md` - Project instructions for Codex

## Quick Start: Create a New Skill

### Step 1: Create the Skill File

**Location:** `skills/{skill-name}/SKILL.md`

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

Add an entry in `skills/skill-rules.json` to document when the skill should be used manually.

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

### Step 3: Map to AGENTS.md

If the skill introduces a new workflow, add a short pointer in `AGENTS.md` so Codex users see the path.

## Testing & Validation

- Manually apply the skill guidance when prompts match the triggers.
- Verify instructions are concise and actionable.
- Confirm the skill content remains under 500 lines.

## Best Practices

- Prefer “why” guidance over obvious commentary.
- Keep descriptions rich with trigger keywords.
- Use progressive disclosure: link to deeper docs instead of dumping everything inline.

## Quick Reference

- Create `SKILL.md`
- Add `skill-rules.json` entry (reference only)
- Mention in `AGENTS.md` when relevant
- Apply skill guidance manually during Codex chats

---

**Note:** Codex does not implement Claude’s hook-based skill auto-activation, so skills are manual guidance only.
