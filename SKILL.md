---
name: codex-home-migration
description: Standardize user-installed Codex content into user-confirmed long-term directories, recreate legacy entry paths as junctions when needed, and maintain local reference files such as the installed-skills cheat sheet. Use when installing, migrating, reorganizing, or cleaning up user-managed `skills`, `agent-skills`, `mcp`, or `user_plugin` content, especially when content is scattered across `~/.codex`, `~/.agents`, third-party tool homes, or ad-hoc folders and the user wants one consistent install policy plus reusable first-run path selection rules.
---

# Codex Home Migration

Use this skill as the standing install and migration policy for user-managed Codex content.

It covers the full lifecycle:

- choose long-term install locations
- migrate existing content into those locations
- recreate original entry paths as junctions when needed
- install new content into the correct category path
- maintain local helper files such as the installed-skills cheat sheet

This skill is intentionally split into:

- shareable default policy files that are safe to publish
- local runtime files that should be created or updated after installation on each machine

## Read These References

Always read these files before acting:

- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/windows-junction-notes.md`

Read `references/placement-rules-local.md` only if it already exists in the installed copy for the current machine.

Read `references/installed-skills-cheatsheet.md` only when updating the local cheat sheet after a skill install.

If either local file does not exist yet, create it during the workflow instead of treating that as an error.

## Category Scope

Confirm and manage these user-owned categories:

- `skills`
- `agent-skills`
- `mcp`
- `user_plugin`

Use them like this:

- `skills`: normal Codex skill folders containing `SKILL.md`
- `agent-skills`: agent-facing skill links or tool-generated skill entry points
- `mcp`: user-managed MCP bundles or support directories
- `user_plugin`: third-party plugin repos or standalone tool homes

Do not mix user-installed third-party tools into Codex bundled cache paths unless the user explicitly asks for that.

## First-Run Behavior

On the first install or first use on a machine:

1. detect the current operating system
2. propose OS-appropriate default locations from `references/placement-rules-default.md`
3. ask the user to confirm the long-term paths for all four categories
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
   - `references/installed-skills-cheatsheet.md`

## Inventory Rules

Check common source or entry paths such as:

- `C:\Users\<user>\.codex\skills`
- `C:\Users\<user>\.codex\plugins`
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

Do not assume everything lives under `~/.codex`. Third-party tools may use `~/.agents` or their own hidden home directories.

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

If a tool creates both a repo home and a separate launcher path, store the real repo under `user_plugin/<tool-name>` and recreate the launcher path as a junction.

## Local File Rules

### `references/placement-rules-local.md`

This file is machine-specific and should be created or updated only in the installed copy.

Required behavior:

- create it after the user confirms category paths
- reuse it on later runs
- update it if the user changes the confirmed locations
- do not treat it as a shareable default file

### `references/installed-skills-cheatsheet.md`

This file is a local quick-reference list for installed skills.

Required behavior after a new skill install:

1. check whether the file exists
2. if it does not exist, create it first
3. add the new skill name
4. add a short Chinese usage hint
5. keep it concise and easy to copy from

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
