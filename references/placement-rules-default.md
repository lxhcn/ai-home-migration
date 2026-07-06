# Placement Rules Default

Use this file as the shareable default placement policy for `codex-home-migration`.

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
5. if the user still does not provide custom paths, continue with the suggested defaults

Do not silently assume a final storage layout before this step.

## OS-Aware Defaults

### Windows default

- `C:\Users\<user>\ai_tools\skills`
- `C:\Users\<user>\ai_tools\agent-skills`
- `C:\Users\<user>\ai_tools\mcp`
- `C:\Users\<user>\ai_tools\user_plugin`

### macOS default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`

### Linux default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`

These are suggested defaults only. The installed copy should store the final confirmed values in a local placement file.

## First-Run Prompt Template

Use this concise structure:

`I can standardize your user-installed Codex content into long-term folders. Based on your current operating system, my suggested defaults are:`

`- skills: <default-skills-path>`
`- agent-skills: <default-agent-skills-path>`
`- mcp: <default-mcp-path>`
`- user_plugin: <default-user-plugin-path>`

`You can keep these defaults or change any of them. If you do not specify different paths, I will use these defaults and continue.`

## Ongoing Rule

If the user later changes any confirmed category path:

- automatically perform the migration needed to move content into the new location
- recreate or update any required junctions
- refresh the local placement record
