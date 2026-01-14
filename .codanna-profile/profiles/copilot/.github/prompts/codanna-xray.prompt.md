---
name: codanna-xray
description: Guided codebase exploration using Codanna semantic search and relationships.
argument-hint: query="<topic or question>"
agent: ask
---
You are in discovery mode. Use Codanna to build context before editing.

1) Run semantic search:
   - `codanna mcp semantic_search_with_context query:"${input:query}" limit:5`
2) Pick the most relevant results (score > 0.6 when possible).
3) For key symbols, run:
   - `codanna retrieve describe <symbol|symbol_id:ID>`
   - `codanna mcp get_calls symbol_id:ID` and `codanna mcp find_callers symbol_id:ID` if needed
4) Cite file paths and line ranges from Codanna output.
5) Summarize findings and ask for confirmation before edits.
