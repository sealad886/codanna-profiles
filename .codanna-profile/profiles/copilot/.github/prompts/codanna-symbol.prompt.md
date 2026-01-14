---
name: codanna-symbol
description: Look up a symbol with Codanna and explain how it is used.
argument-hint: symbol="<name or symbol_id:ID>" question="<optional>"
agent: ask
---
Use Codanna to locate the symbol and answer the question.

1) `codanna retrieve describe ${input:symbol}`
2) If needed, follow relationships:
   - `codanna mcp get_calls ${input:symbol}`
   - `codanna mcp find_callers ${input:symbol}`
3) Cite file paths and line ranges from the output.
4) Answer: ${input:question:optional}
