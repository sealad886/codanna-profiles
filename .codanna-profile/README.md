# Codanna Profiles for Claude, Codex, and Copilot

Profiles bundle hooks, commands, skills, and settings into a single package you can install across projects. Pack your favorite agentic tools and prompts, then bootstrap new projects with one command instead of copying files around.

This profile pack includes:

- **Claude** (Claude Code) profile with semantic code search, guided exploration workflows, auto-activating skills, read limits, and a lightweight research agent.
- **Codex** (OpenAI Codex VS Code extension) profile with Codanna-first workflows and `AGENTS.md` guidance.
- **Copilot** (GitHub Copilot + Copilot Chat) profile with instruction-file templates and prompt/agent helpers.

## Prerequisites

Install the Codanna CLI:

```bash
# From crates.io
cargo install codanna --locked

# Or download pre-built binaries
# https://github.com/bartolli/codanna/releases
```

## Installation

### From GitHub

```bash
# Initialize codanna in your project
cd your-project
codanna init

# Add the provider
codanna profile provider add bartolli/codanna-profiles

# Install a profile
codanna profile install claude@codanna-profiles
codanna profile install codex@codanna-profiles
codanna profile install copilot@codanna-profiles

# Install hook dependencies
npm --prefix .claude/hooks/codanna install

# Index your codebase (examples)
codanna index                    # Index current directory
codanna index src tests          # Index specific directories
codanna add-dir src              # Add directory to settings for indexing
```

### From URL

```bash
# Initialize codanna in your project
cd your-project
codanna init

# Add the provider via URL (It works with any git provider)
codanna profile provider add https://github.com/bartolli/codanna-profiles.git

# Install the profile
codanna profile install claude@codanna-profiles

# Install hook system
npm --prefix .claude/hooks/codanna install

# Index your codebase (examples)
codanna index                    # Index current directory
codanna index src tests          # Index specific directories
codanna add-dir src              # Add directory to settings for indexing
```

### From Local Directory

Clone the repository and make modifications according to your project needs (customize hooks, commands, or skills).

```bash
# Clone and customize
git clone https://github.com/bartolli/codanna-profiles.git
cd codanna-profiles
# Make your modifications...

# Initialize codanna in your project
cd your-project
codanna init

# Add the local provider (ID auto-derived from directory name)
codanna profile provider add /path/to/your-profiles

# Install the profile
codanna profile install claude@your-profiles

# Install hook dependencies
npm --prefix .claude/hooks/codanna install

# Index your codebase (examples)
codanna index                    # Index current directory
codanna index src tests          # Index specific directories
codanna add-dir src              # Add directory to settings for indexing
```

## Usage

### Codex (VS Code)

After installing the `codex` profile:

- Rename `AGENTS.md.codanna` → `AGENTS.md` to enable Codex project instructions.
- Use Codex commands like `chatgpt.newChat` and `chatgpt.openSidebar` (see profile README for the verified list).

### Copilot (VS Code)

After installing the `copilot` profile:

- Rename `.github/copilot-instructions.md.codanna` → `.github/copilot-instructions.md`.
- Enable instruction files via `github.copilot.chat.codeGeneration.useInstructionFiles`.
- Use prompt files `/codanna-xray` and `/codanna-symbol` for Codanna-first workflows.

**Explore code deeply:**

```text
/codanna:x-ray vector search
/codanna:x-ray error handling
```

Guides Claude to search semantically, read relevant code, follow relationships, and build understanding.

**Look up symbols:**

```text
/codanna:symbol parse_file "how does this work?"
```

Finds the symbol, shows context, and answers your question.

**Auto-suggestions:**
Skills activate automatically when you ask about exploring code, adding languages, or creating skills.

## What's Included

**Commands:**

- `/codanna:x-ray` - Guided code exploration
- `/codanna:symbol` - Symbol lookup with context

**Skills:**

- Auto-activate when exploring code, adding languages, or creating skills

**Hooks:**

- Read limits - Warns at 400 lines, blocks at 600
- Skill suggestions - Shows relevant skills before you start
- Tool logging - Tracks usage in `.claude/hooks/codanna/logs/`

**Agent:**

- Research-Agent (formerly known as codanna-navigator) - Lightweight Haiku agent for code research, creates structured reports

---

## Codex Profile Highlights

- `AGENTS.md` instructions template for Codex discovery and editing rules
- Verified Codex command IDs (see `profiles/codex/README.md`)
- Capabilities matrix distinguishing Codex vs Codanna vs VS Code features

## Copilot Profile Highlights

- `.github/copilot-instructions.md` template (chat-only instructions)
- Prompt files for Codanna discovery and symbol lookup
- Custom agent for Codanna-first implementation workflows
- Capabilities matrix distinguishing Copilot vs Codanna vs VS Code features

## Requirements

- Codanna CLI
- Node.js 18+
- Indexed codebase

## Development

**Test hooks:**

```bash
# From project root
npm --prefix .claude/hooks/codanna run test:all

# Or individual tests
npm --prefix .claude/hooks/codanna run test:read-warn
npm --prefix .claude/hooks/codanna run test:prompt
```

**Enable hooks in local settings:**

The hooks are automatically configured via `.claude/settings.local.codanna.json` when you install the profile. To customize, edit `.claude/settings.local.json` in your project:

```json
{
  "hooks": {
    "UserPromptSubmit": [{
      "hooks": [{
        "type": "command",
        "command": "npm run --prefix \"$CLAUDE_PROJECT_DIR\"/.claude/hooks/codanna hook:prompt"
      }]
    }],
    "PreToolUse": [{
      "matcher": "Read",
      "hooks": [{
        "type": "command",
        "command": "npm run --prefix \"$CLAUDE_PROJECT_DIR\"/.claude/hooks/codanna hook:read"
      }]
    }]
  }
}
```

---

**Version:** 1.0.0
