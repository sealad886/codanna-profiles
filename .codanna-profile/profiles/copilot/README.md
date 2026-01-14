# GitHub Copilot (VS Code) Codanna Profile

This profile targets **GitHub Copilot** and **GitHub Copilot Chat** for VS Code.

## Extension IDs

- **GitHub Copilot (inline suggestions):** `GitHub.copilot`
- **GitHub Copilot Chat (chat/agent mode):** `GitHub.copilot-chat`

## What gets installed

- `.github/copilot-instructions.md.codanna` (template) → rename to `.github/copilot-instructions.md` to activate.
- Prompt files:
  - `.github/prompts/codanna-xray.prompt.md`
  - `.github/prompts/codanna-symbol.prompt.md`
- Custom agent:
  - `.github/agents/codanna-implementer.agent.md`

## Quick start

1. Install the profile:
   - `codanna profile install copilot@codanna-profiles`
2. Activate Copilot instructions:
   - Rename `.github/copilot-instructions.md.codanna` → `.github/copilot-instructions.md`
3. Enable instruction files:
   - Set `github.copilot.chat.codeGeneration.useInstructionFiles` to `true`
4. Use prompt files via `/codanna-xray` and `/codanna-symbol` in chat.

> Note: Custom instructions are not applied to inline suggestions. They apply to chat/agent mode only.

## Settings to know

```json
{
  "github.copilot.enable": {
    "*": true
  },
  "github.copilot.nextEditSuggestions.enabled": true,
  "chat.agent.enabled": true,
  "github.copilot.chat.codeGeneration.useInstructionFiles": true
}
```

## Capabilities matrix

See `capabilities.md` for the full matrix.

| Capability | Copilot (native) | Codanna | VS Code commands/settings | MCP tools |
| --- | --- | --- | --- | --- |
| Inline suggestions | ✅ | — | `github.copilot.enable` | — |
| Agent mode & multi-file edits | ✅ | — | Agent picker, `chat.agent.enabled` | — |
| Prompt files (slash commands) | ✅ | — | `.github/prompts/*.prompt.md` | — |
| Custom agents | ✅ | — | `.github/agents/*.agent.md` | — |
| Project instruction files | ✅ | — | `.github/copilot-instructions.md` | — |
| Semantic search & call graph | — | ✅ | — | — |
| Documentation search (RAG) | — | ✅ (indexed docs) | — | — |
| External tools & web data | — | — | — | ✅ (MCP servers like Context7) |

## Suggested workflows

- **Discovery**: Use `/codanna-xray` to run Codanna semantic search before edits.
- **Symbol deep dive**: Use `/codanna-symbol` to explain how a symbol is used.
- **Implementation**: Switch to the *Codanna Implementer* agent for multi-file edits.
- **Validation**: Run existing lint/test commands or explain why they cannot be run.

## Debugging & verbosity guidance

- Always record the exact Codanna command used (query + limit).
- Prefer `--json` output when collecting logs for reproducibility.
- If Codanna results are ambiguous, run `codanna retrieve describe` for the top symbols.

## “Don’t lie” policy

If Copilot lacks a capability, state it explicitly and provide a workaround (for example, using instruction files or prompt files instead of an unsupported action).
