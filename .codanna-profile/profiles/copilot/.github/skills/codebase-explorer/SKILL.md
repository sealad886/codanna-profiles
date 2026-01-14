---
name: codebase-explorer
description: Deep codebase exploration using Codanna semantic search and relationship mapping. Use when you need to understand the current codebase before editing.
---

# Codebase Explorer Skill (Copilot)

This skill guides Codanna-first codebase exploration in Copilot chat/agent mode.

## When to Use

- You need to understand unfamiliar code before edits.
- You want to map call relationships and ownership.
- You need citations for why a change is safe.

## Search Query Analysis

Codanna semantic search works best with concrete technical terms. Refine vague prompts into specific keywords.

Examples:

1. **Vague**: "that parsing thing" → "language parser implementation"
1. **Question**: "how does parsing work?" → "parsing implementation process"
1. **Conversational**: "the stuff that handles languages" → "language handler processor"
1. **Too broad**: "errors" → "error handling exception management"

**OptimizedQuery**: _{Write your improved query here, then use it below}_

## Workflow

### Step 1: Gather context

Run semantic search:

```bash
codanna mcp semantic_search_with_context query:"$OptimizedQuery" limit:5
```

### Step 2: Analyze and explore

1. Review results (prioritize score > 0.6 when possible).
1. Open referenced files and navigate to the cited line ranges.
   - If Codanna reports `path/to/file.rs:108-120`, read those exact lines.
   - Formula: `lines = end - start + 1`.
1. Follow key relationships:

```bash
codanna retrieve describe <symbol|symbol_id:ID>
codanna mcp get_calls symbol_id:ID
codanna mcp find_callers symbol_id:ID
```

1. Build a concise mental model before making changes.

### Step 3: Summarize and confirm

- Summarize findings with file:line citations.
- Ask for confirmation before edits.

## Tips

- Add `lang:<language>` to narrow multi-language workspaces.
- Follow 1–2 key relationships per result to stay focused.
- Treat this skill as discovery only; switch to an implementer workflow for edits.
