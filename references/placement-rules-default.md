# Placement Rules Default

Use this file as the shareable default placement policy for `ai-home-migration`.

## Purpose

This file describes generic first-run behavior and OS-aware default path suggestions.
It is safe to publish because it does not assume any machine has already confirmed local paths.

## First-Run Rule

On first use:

1. detect the current operating system
2. propose OS-matched default locations
3. tell the user that these defaults can be changed
4. ask the user to confirm the long-term paths for:
   - `skills`
   - `agent-skills`
   - `mcp`
   - `user_plugin`
   - `agent-config`
5. if the user still does not provide custom paths, continue with the suggested defaults

Do not silently assume a final storage layout before this step.

## OS-Aware Defaults

### Windows default

- `C:\Users\<user>\ai_tools\skills`
- `C:\Users\<user>\ai_tools\agent-skills`
- `C:\Users\<user>\ai_tools\mcp`
- `C:\Users\<user>\ai_tools\user_plugin`
- `C:\Users\<user>\ai_tools\agent-config`

### macOS default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`
- `~/ai_tools/agent-config`

### Linux default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`
- `~/ai_tools/agent-config`

These are suggested defaults only. The installed copy should store the final confirmed values in a local placement file.

## Category Content Defaults

- `skills`: callable user skills that should be discovered directly by the agent, normally one folder per skill with `SKILL.md`.
- `agent-skills`: generated skill links, compatibility entry points, Claude-style command or agent folders, and agent-facing launchers.
- `mcp`: MCP servers, bundles, manifests, adapters, and support files controlled by the user.
- `user_plugin`: third-party plugin repositories, self-contained plugin suites, standalone tool homes, marketplace-installed repos after migration, and plugin source trees.
- `agent-config`: user-controlled config files, adapter prompts, routing notes, launcher metadata, and local policy snippets.

## Skill-Linked Plugin Default

Treat a plugin as skill-linked only when it depends on one or more callable skill entries under the confirmed `skills` or `agent-skills` path.

Default placement rule:

- store the real repo under `user_plugin/<tool-name>`
- store only required callable skill entries or links under `skills` or `agent-skills`
- list it in the inventory as a skill-linked plugin only when those external skill entries exist
- list self-contained plugin suites only under `user_plugin`

## Marketplace Install Default

Before using Codex marketplace or another host installer, confirm the final long-term `user_plugin/<tool-name>` path.

Do not leave the real repo inside vendor-managed cache or temp marketplace paths long-term. If the host installs it to a temp marketplace path first, move or copy the real repo into `user_plugin` and keep the old path as a bridge when the host still expects that entry path.

## First-Run Prompt Template

Use this concise structure:

`I can standardize your user-installed AI agent content into long-term folders. Based on your current operating system, my suggested defaults are:`

`- skills: <default-skills-path>`
`- agent-skills: <default-agent-skills-path>`
`- mcp: <default-mcp-path>`
`- user_plugin: <default-user-plugin-path>`
`- agent-config: <default-agent-config-path>`

`You can keep these defaults or change any of them. If you do not specify different paths, I will use these defaults and continue.`

## Ongoing Rule

If the user later changes any confirmed category path:

- automatically perform the migration needed to move content into the new location
- recreate or update any required entry bridges
- refresh the local placement record
- refresh `<confirmed-ai-home-root>/ai-home-inventory.md` as a Chinese-primary bilingual inventory with total and per-category counts

## Bridge Terminology

Use `bridge` as the cross-platform term for preserving old tool entry paths:

- Windows: directory junctions
- macOS/Linux: symbolic links

Do not silently bridge private runtime state. Ask before touching sessions, history, local settings, or project-owned `.claude/` content.
