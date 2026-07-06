---
name: ai-home-migration
description: Standardize user-installed AI agent content into user-confirmed long-term directories, recreate legacy entry paths as junctions when needed, and maintain local reference files. Use when installing, migrating, reorganizing, or cleaning up user-managed Codex, Claude, OpenAI-compatible agent, MCP, skill, plugin, or tool content, especially when content is scattered across `~/.codex`, `~/.claude`, `~/.agents`, third-party tool homes, or ad-hoc folders and the user wants one consistent install policy plus reusable first-run path selection rules.
---

# AI Home Migration

Use this skill as the standing install and migration policy for user-managed AI agent content across Codex, Claude, OpenAI-compatible agents, MCP bundles, and third-party tool repos.

It covers the full lifecycle:

- choose long-term install locations
- migrate existing content into those locations
- recreate original entry paths as junctions when needed
- install new content into the correct category path
- maintain local helper files such as the root-level AI home inventory

This skill is intentionally split into:

- shareable default policy files that are safe to publish
- local runtime files that should be created or updated after installation on each machine
- agent-specific adapter files that explain how Codex, Claude, and generic OpenAI-style agents should invoke the same core workflow

## Agent Compatibility

Treat `SKILL.md` as the canonical execution contract for every agent.

Use adapter files only to help a specific agent load or invoke the skill:

- `agents/openai.yaml`: Codex/OpenAI UI metadata.
- `agents/claude.md`: Claude-oriented usage and installation notes.
- `agents/generic-openai.md`: Plain prompt wrapper for generic OpenAI-compatible agents.
- `references/agent-compatibility.md`: Packaging guidance for maintainers adapting this skill to another agent runtime.

Do not fork the migration rules per agent. If a behavior changes, update the core rule here or in `references/`, then keep adapter files thin.

## Read These References

Always read these files before acting:

- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/windows-junction-notes.md`

Read `references/placement-rules-local.md` only if it already exists in the installed copy for the current machine.

Read the root-level local inventory file only when updating the machine inventory after an install, migration, rename, or cleanup.

The canonical local inventory path is `<confirmed-ai-home-root>/ai-home-inventory.md`, for example `D:\2_file\codex-home\ai-home-inventory.md`.

Keep `references/installed-skills-cheatsheet.md` only as a backward-compatible pointer when an older workflow expects that file.

If either local file does not exist yet, create it during the workflow instead of treating that as an error.

## Category Scope

Confirm and manage these user-owned categories:

- `skills`
- `agent-skills`
- `mcp`
- `user_plugin`
- `agent-config`

Use them like this:

- `skills`: normal Codex skill folders containing `SKILL.md`
- `agent-skills`: agent-facing skill links or tool-generated skill entry points, including Claude-style or OpenAI-style skill entry folders when applicable
- `mcp`: user-managed MCP bundles or support directories
- `user_plugin`: third-party plugin repos or standalone tool homes
- `agent-config`: user-controlled agent configuration files, adapter prompts, or launcher metadata that must stay separate from bundled vendor caches

Do not mix user-installed third-party tools into Codex bundled cache paths unless the user explicitly asks for that.

## First-Run Behavior

On the first install or first use on a machine:

1. detect the current operating system
2. propose OS-appropriate default locations from `references/placement-rules-default.md`
3. ask the user to confirm the long-term paths for all managed categories
4. if the user still does not specify custom paths, proceed with the proposed defaults
5. write the confirmed result into `references/placement-rules-local.md` in the installed copy

If a confirmed local rules file already exists, reuse it and do not override it with generic defaults unless the user explicitly changes paths.

If the user later changes any confirmed path, automatically perform the needed migration and junction updates.

## Quick Start Workflow

1. Confirm whether a local placement file already exists.
2. If no local placement file exists, propose OS-aware defaults and ask the user to confirm or change them.
3. Inventory the current state before changing anything.
4. Classify each source path as direct-move, copy-first, backup-plus-junction, or already-done.
5. Create or verify destination directories.
6. Migrate or install content into the correct category path.
7. Recreate expected original paths as junctions when needed.
8. Validate junction targets and destination contents.
9. Create or update local helper files:
   - `references/placement-rules-local.md`
   - `<confirmed-ai-home-root>/ai-home-inventory.md`
   - optional compatibility pointer at `references/installed-skills-cheatsheet.md`

## Inventory Rules

Check common source or entry paths such as:

- `C:\Users\<user>\.codex\skills`
- `C:\Users\<user>\.codex\plugins`
- `C:\Users\<user>\.claude`
- `C:\Users\<user>\.claude.json`
- `C:\Users\<user>\.claude\settings.json`
- `C:\Users\<user>\.claude\CLAUDE.md`
- `C:\Users\<user>\.claude\skills`
- `C:\Users\<user>\.claude\commands`
- `C:\Users\<user>\.claude\agents`
- project `.claude\settings.json`
- project `.claude\settings.local.json`
- project `.claude\skills`
- project `.claude\commands`
- project `.claude\agents`
- project `.claude\rules`
- project `CLAUDE.md`
- project `.claude\CLAUDE.md`
- project `CLAUDE.local.md`
- project `.mcp.json`
- `C:\Users\<user>\.agents\skills`
- `C:\Users\<user>\.codex\mcp`
- `C:\Users\<user>\.codex\mcp_servers`
- tool-specific homes like `C:\Users\<user>\.understand-anything`
- plugin entry paths like `C:\Users\<user>\.understand-anything-plugin`
- user-created ad-hoc folders such as `D:\2_file\.skills`

Record for each path:

- whether it exists
- whether it is already a junction
- child count
- junction target when present
- whether it appears to be actively referenced

Do not assume everything lives under `~/.codex`. Claude-related content may live in both user-level `~/.claude*` paths and project-level `.claude/`, `CLAUDE.md`, `CLAUDE.local.md`, and `.mcp.json` paths. Third-party tools may use `~/.agents` or their own hidden home directories.

## Migration Strategy Rules

### Direct Move + Junction

Use when:

- the source is a normal directory
- the destination is empty or absent
- the directory is not actively locked

Steps:

1. move the real directory to the destination category path
2. create a junction at the original path if that entry path must keep working
3. verify child counts and target resolution

### Copy First + Repoint Entry Links

Use when:

- the source repo is active
- `.git` or native binaries appear locked
- only the user-managed tool repo needs to be consolidated

Steps:

1. copy the repo into the correct category path
2. point launcher or plugin entry paths to the new copy
3. keep the original repo as fallback if needed

This is the preferred safe pattern for active third-party tool repos.

### Backup + Junction

Use when:

- partial migration already happened
- the source still contains leftover content
- deleting or renaming the live path is risky

Steps:

1. preserve the old directory as a backup under the unified root
2. create the intended junction only after confirming the new target is valid
3. tell the user the backup still exists

## New Install Rule

For future user-managed installs:

- install normal skills into the confirmed `skills` path
- install agent-facing linked skills into the confirmed `agent-skills` path
- install custom MCP content into the confirmed `mcp` path
- install third-party plugin repos or standalone tool homes into the confirmed `user_plugin` path
- install user-controlled adapter prompts or agent config snippets into the confirmed `agent-config` path

For Claude-specific installs:

- put personal Claude skills under the confirmed `skills` path and keep `~/.claude/skills/<skill-name>` working when Claude expects that entry path
- put project Claude skills under the relevant repository `.claude/skills/` only when they are intentionally project-shared
- treat `.claude/settings.local.json`, `CLAUDE.local.md`, and user `~/.claude.json` as local/private state unless the user explicitly asks to migrate or back them up
- treat `.claude/settings.json`, `.claude/agents/`, `.claude/commands/`, `.claude/rules/`, `CLAUDE.md`, `.claude/CLAUDE.md`, and `.mcp.json` as project-shareable only after confirming they belong to that repository

If a tool creates both a repo home and a separate launcher path, store the real repo under `user_plugin/<tool-name>` and recreate the launcher path as a junction.

## Local File Rules

### `references/placement-rules-local.md`

This file is machine-specific and should be created or updated only in the installed copy.

Required behavior:

- create it after the user confirms category paths
- reuse it on later runs
- update it if the user changes the confirmed locations
- do not treat it as a shareable default file

### `<confirmed-ai-home-root>/ai-home-inventory.md`

This is the canonical local AI home inventory file.

Place it at the confirmed AI home root, not under one skill's `references/` folder. For example, if the confirmed root is `D:\2_file\codex-home`, write `D:\2_file\codex-home\ai-home-inventory.md`.

It must summarize every confirmed category, not only normal skills:

- `skills`
- `agent-skills`
- `mcp`
- `user_plugin`
- `agent-config`
- plugin cache roots or plugin bundles when they are user-visible under the confirmed home
- backup directories and legacy entry junctions created by this migration policy

Required behavior after any install, migration, rename, or cleanup:

1. check whether the file exists
2. if it does not exist, create it first
3. rescan all confirmed category directories
4. write a summary with:
   - total managed entry count
   - per-category counts
   - excluded system or empty directories
5. write the inventory as a Chinese-primary bilingual quick reference:
   - Chinese headings and purpose hints should come first
   - English headings and purpose notes should follow as secondary context
   - each listed entry should include Chinese purpose, English purpose, path, and a short invocation example when applicable
6. keep local/private runtime files out of shareable repository files

### `references/installed-skills-cheatsheet.md`

This historical file path is kept only for backward compatibility.

If it exists, replace its full inventory content with a short pointer to the canonical root-level inventory file. Do not maintain two independent inventories.

## Tool-Specific Guidance

### Understand-Anything

Common structure:

- repo home at `C:\Users\<user>\.understand-anything`
- plugin entry path at `C:\Users\<user>\.understand-anything-plugin`
- `understand-*` skill links under `C:\Users\<user>\.agents\skills`

Preferred handling:

1. keep `understand-*` links if `agent-skills` is already standardized
2. copy the repo to `user_plugin/understand-anything`
3. point the plugin entry path to the repo copy
4. keep the original repo if `.git` locks prevent a clean move

### Global Plugin Cache

For `C:\Users\<user>\.codex\plugins`, be conservative.

If native binaries or caches are locked:

- do not hard-delete the old directory
- do not assume a partial move can be resumed blindly
- preserve backups where appropriate
- finish the final swap only when the user confirms Codex is fully closed

## Communication

Always tell the user which state each category ended in:

- fully migrated and junctioned
- copied and repointed, original retained
- partially prepared, waiting on process locks
- backed up for later cleanup
- newly installed and recorded in local helper files
