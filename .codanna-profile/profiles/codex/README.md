# Codex (VS Code) Codanna Profile

This profile targets the **Codex – OpenAI’s coding agent** VS Code extension (`openai.chatgpt`). It adds Codanna-centric workflow guidance and a project-level instruction template for Codex.

## What gets installed

- `AGENTS.md.codanna` (template) → rename to `AGENTS.md` to activate Codex project instructions.
- This README for setup, commands, and workflow guidance.

## Extension IDs

- **Codex VS Code extension:** `openai.chatgpt`

## Quick start

1. Install the profile:
   - `codanna profile install codex@codanna-profiles`
2. Activate project instructions:
   - Rename `AGENTS.md.codanna` → `AGENTS.md`
3. Use Codex in the VS Code sidebar and follow the workflows below.

## Recommended command IDs (verified)

Codex exposes these VS Code command IDs:

| Command ID | Description |
| --- | --- |
| `chatgpt.newChat` | Create a new thread |
| `chatgpt.addToThread` | Add selected text range as context for the current thread |
| `chatgpt.implementTodo` | Ask Codex to address the selected TODO comment |
| `chatgpt.newCodexPanel` | Create a new Codex panel |
| `chatgpt.openSidebar` | Open the Codex sidebar panel |

## Built-in slash commands (Codex chat)

- `/auto-context` – toggle auto context
- `/cloud` – switch to cloud mode
- `/cloud-environment` – select cloud environment
- `/feedback` – send feedback
- `/local` – switch to local mode
- `/review` – review uncommitted changes or compare against a base branch
- `/status` – show thread ID, context usage, and rate limits

## Instruction file conventions

Codex reads project instructions from `AGENTS.md` (and optional `AGENTS.override.md`) along the directory tree. Use `AGENTS.md` to encode Codanna-specific expectations such as running `codanna mcp semantic_search_with_context` before edits and logging the queries used.

> Note: Codex also supports global instructions under `~/.codex/AGENTS.md`. If you use this profile across multiple repos, keep shared rules there and place repo-specific rules in `AGENTS.md`.

## Settings to know

These settings are specific to the Codex VS Code extension:

```json
{
  "chatgpt.commentCodeLensEnabled": true,
  "chatgpt.openOnStartup": false,
  "chatgpt.runCodexInWindowsSubsystemForLinux": true
}
```

Codex behavior (model, approvals, sandbox) is primarily controlled via `~/.codex/config.toml` (shared by the CLI and the IDE extension).

## Capabilities matrix

See `capabilities.md` for the full matrix.

| Capability | Codex (native) | Codanna | VS Code commands/settings | MCP tools |
| --- | --- | --- | --- | --- |
| Chat + multi-file edits | ✅ | — | Agent mode UI | — |
| Cloud delegation & follow-ups | ✅ | — | `/cloud`, `/cloud-environment` | — |
| Project instruction layering | ✅ (`AGENTS.md`) | — | — | — |
| Semantic search & relationship graph | — | ✅ | — | — |
| Documentation search (RAG) | — | ✅ (indexed docs) | — | — |
| Command palette actions | — | — | ✅ (`chatgpt.*`) | — |
| External tools & web data | — | — | — | ✅ (MCP servers like Context7) |

## Suggested Codanna-first workflow

1. **Discover**: run Codanna semantic search before edits.
2. **Trace**: use Codanna call graph queries to understand impact.
3. **Edit**: apply Codex edits in Agent mode with atomic commits.
4. **Validate**: run repo lint/test commands when available.

## Limitations & non-goals

- Custom Codex prompts live under `~/.codex/prompts` (not in the repo). This profile does not attempt to install those prompts.
- Do not invent command IDs or settings. If uncertain, state the gap and provide a safer alternative.
