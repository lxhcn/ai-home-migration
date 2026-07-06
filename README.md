# ai-home-migration

English | [Simplified Chinese](README.zh-CN.md)

Make AI agent installs clean, predictable, and reusable.

`ai-home-migration` is a multi-agent skill package for standardizing user-installed Codex, Claude, OpenAI-compatible agent, MCP, skill, and plugin assets into long-term directories, preserving legacy entry paths with junctions, and turning one-off cleanup into a repeatable install policy.

## At a Glance

- First-run path confirmation for `skills`, `agent-skills`, `mcp`, `user_plugin`, and `agent-config`
- Adapter files for Codex/OpenAI, Claude, and generic OpenAI-compatible agents
- Local inventory cheat sheet with total and per-category counts across skills, agent-skills, MCP, plugins, user plugin repos, agent config, backups, and legacy entry links
- OS-aware default paths for Windows, macOS, and Linux
- Safer migration patterns for locked repos, plugin homes, and legacy launcher paths
- Windows-aware handling for junctions, `.git` locks, and native plugin binaries
- Clear split between shareable repository files and machine-specific runtime files
- Reusable install policy for every future user-managed AI agent asset

## Install

Install or copy this repository as a skill package named `ai-home-migration`, keeping the repository layout intact:

```text
ai-home-migration/
  SKILL.md
  agents/openai.yaml
  agents/claude.md
  agents/generic-openai.md
  references/
```

Use the entry point that matches your runtime:

- Codex / OpenAI skill surfaces: use `SKILL.md` plus `agents/openai.yaml`
- Claude-style surfaces: read `agents/claude.md`, which points back to `SKILL.md`
- Generic OpenAI-compatible agents: use the prompt wrapper in `agents/generic-openai.md`

On first use, the skill should ask you to confirm the long-term paths for `skills`, `agent-skills`, `mcp`, `user_plugin`, and `agent-config`. It should then create local runtime files in your installed copy, not in the shared repository baseline.

## Why This Project Matters

Many AI agent environments slowly become difficult to manage:

- custom Codex or Claude skills are scattered across multiple folders
- Claude Code user and project configuration can span `~/.claude`, `~/.claude.json`, `.claude/`, `.mcp.json`, and `CLAUDE.md` files
- plugin repos live inside hidden tool homes
- MCP bundles are stored separately from the rest of the setup
- generic agent prompts and adapter files land in ad-hoc locations
- old entry paths still need to work
- Windows file locks make cleanup risky

Most users solve this once, manually, and then repeat the same messy decisions later.

`ai-home-migration` exists to turn that chaos into a durable operating policy.

## Who This Is For

- Codex, Claude, and OpenAI-compatible agent users installing third-party skills from GitHub
- Users moving AI agent assets off the system drive
- Windows-heavy setups dealing with junctions and locked files
- Users who want future installs to follow one clean directory policy
- Power users maintaining `skills`, `agent-skills`, MCP assets, agent prompts, and plugin repos over time

## Before / After

Before:

- custom skills in `.codex`
- Claude or generic agent instructions in separate hidden folders
- agent links in `.agents`
- plugin repos in hidden folders
- MCP content in separate locations
- no durable rule for future installs

After:

- one confirmed long-term layout
- category-based install rules
- thin adapters for Codex, Claude, and generic OpenAI-compatible agents
- one local inventory cheat sheet covering all managed categories, not only skills
- safer migration choices per path
- legacy entry paths preserved when needed
- future installs follow the same structure automatically

## Core Capabilities

### 1. Placement Policy

Define one durable home for user-managed AI agent content instead of solving every install case manually.

### 2. First-Run Setup

Prompt the user to confirm long-term paths before migration starts, while still providing sensible OS-aware defaults.

### 3. Migration Strategy

Choose between direct move, copy-first repointing, or backup-first migration depending on file locks and operational risk.

### 4. Legacy Compatibility

Keep old tool entry paths usable with junctions when tools still depend on them.

### 5. Ongoing Maintenance

Reuse previously confirmed local paths, regenerate local runtime files when needed, and keep future installs consistent.

## Common Problems It Solves

- "My Codex skills are scattered across too many places."
- "I want the same migration skill to work in Claude and OpenAI-compatible agents."
- "I want to move installs to another drive without breaking old paths."
- "A plugin still depends on its original launcher folder."
- "Windows says the repo or native file is locked."
- "I do not want to rethink placement rules for every new skill."
- "I want a setup I can keep clean and share with others."

## How It Works

1. Detect the current operating system.
2. Propose sensible default locations.
3. Ask the user to confirm long-term paths for each category.
4. Inventory the current layout.
5. Choose the safest migration pattern for each path.
6. Recreate junctions when legacy entry points must keep working.
7. Save local runtime state for future reuse.

## First-Run Behavior

On the first install or first use, the skill should:

1. Detect the operating system.
2. Propose OS-aware default paths.
3. Tell the user those defaults can be changed.
4. Ask the user to confirm paths for `skills`, `agent-skills`, `mcp`, `user_plugin`, and `agent-config`.
5. If the user does not override them, continue with the proposed defaults.
6. Save the confirmed result into a local placement file for later reuse.

On later runs, if a local placement file already exists, the skill should reuse it unless the user explicitly changes the layout.

## Default Path Policy

Windows defaults:

- `C:\Users\<user>\ai_tools\skills`
- `C:\Users\<user>\ai_tools\agent-skills`
- `C:\Users\<user>\ai_tools\mcp`
- `C:\Users\<user>\ai_tools\user_plugin`
- `C:\Users\<user>\ai_tools\agent-config`

macOS / Linux defaults:

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`
- `~/ai_tools/agent-config`

## Migration Model

The skill uses three migration patterns depending on risk:

- `Direct move + junction`
  Best for plain directories that are not locked.

- `Copy first + repoint`
  Best for active repos, plugin homes, or anything that may be locked by `.git`, native binaries, or running processes.

- `Backup + junction`
  Best for partial migrations or cases where deleting the source would be unsafe.

Windows-specific safety rules live in [references/windows-junction-notes.md](references/windows-junction-notes.md).

## Example Use Cases

- Consolidate custom skills from multiple folders into one long-term skills directory
- Inventory Claude Code user and project paths, including `~/.claude/skills`, `.claude/skills`, `.claude/commands`, `.claude/agents`, `.claude/settings*.json`, `.mcp.json`, and `CLAUDE.md`
- Package the same migration policy for Codex, Claude, and generic OpenAI-compatible agents
- Move a third-party plugin repo into `user_plugin` without breaking the tool's launcher path
- Standardize `agent-skills` and MCP bundles before sharing a Codex setup with teammates
- Re-home user-managed assets to another drive while preserving old entry points
- Turn one successful local migration into a repeatable install policy for all future additions

## Quick Examples

```text
Use ai-home-migration to install this skill into my long-term skills directory and keep any expected old path working.
```

```text
Use ai-home-migration to standardize my Codex, Claude, MCP, and agent-tool setup and tell me what should move, what should stay, and what should become a junction.
```

## Recommended Prompts

```text
Use ai-home-migration to install this skill and place it using the unified directory policy.
```

```text
Use ai-home-migration to inspect my current skills, agent-skills, mcp, user_plugin, and agent-config layout and tell me what should be migrated.
```

```text
Use ai-home-migration to move this plugin into user_plugin and keep the old entry path working with a junction.
```

## Shareable Files vs Local Runtime Files

This repository is intentionally split into two layers.

Shareable files:

- `SKILL.md`
- `agents/openai.yaml`
- `agents/claude.md`
- `agents/generic-openai.md`
- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/agent-compatibility.md`
- `references/windows-junction-notes.md`

Local runtime files created after installation:

- `references/placement-rules-local.md`
- `references/installed-skills-cheatsheet.md`

Those local runtime files should not be committed as universal defaults because they contain machine-specific paths and local installation state.

## Repository Layout

```text
ai-home-migration/
  SKILL.md
  README.md
  README.zh-CN.md
  .gitignore
  .gitattributes
  CHANGELOG.md
  CONTRIBUTING.md
  GITHUB_ABOUT.md
  LICENSE
  SECURITY.md
  agents/
    openai.yaml
    claude.md
    generic-openai.md
  references/
    agent-compatibility.md
    placement-rules.md
    placement-rules-default.md
    windows-junction-notes.md
```

## Included Files

- `SKILL.md`
  Main operational skill instructions.

- `agents/openai.yaml`
  UI metadata for Codex.

- `agents/claude.md`
  Claude-oriented prompt wrapper and usage notes.

- `agents/generic-openai.md`
  Prompt wrapper for generic OpenAI-compatible agents.

- `references/agent-compatibility.md`
  Cross-agent packaging guidance for Codex, Claude, and generic OpenAI-compatible runtimes.

- `references/placement-rules.md`
  Explains how default rules and local runtime files work together.

- `references/placement-rules-default.md`
  Shareable first-run and default path policy.

- `references/windows-junction-notes.md`
  Windows-specific migration safety notes.

- `README.zh-CN.md`
  Chinese documentation.

- `CHANGELOG.md`
  Release history for the public repository.

- `CONTRIBUTING.md`
  Contribution guidance for keeping the skill focused and safe.

- `GITHUB_ABOUT.md`
  Suggested GitHub repository description, tagline, and topics.

- `LICENSE`
  Repository license.

- `SECURITY.md`
  Safety expectations and issue reporting guidance for migration-related risks.

## Discoverability Notes

This repository intentionally emphasizes search-friendly terms such as `Codex`, `Claude`, `OpenAI`, `AI agent`, `skills`, `agent-skills`, `MCP`, `plugin`, `migration`, `Windows`, and `junction`, because those are the exact problems users usually search for when they need this workflow.

## Notes

- This repository contains the shareable policy layer.
- Machine-specific path confirmations should be generated after installation, not published as defaults.
- If you distribute this skill, share the repository files and let each user confirm their own long-term paths on first run.
