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
   - `agent-skills` compatibility bridge, if needed
   - `mcp`
   - `user_plugin`
   - `agent-config`
5. require explicit confirmation before write operations:
   - if the user says to use the defaults, continue and record the local placement status as `confirmed-default`
   - if the user provides custom paths, continue and record the local placement status as `user-custom`
   - if the user does not confirm either option, stop before migration, install, bridge creation, or config changes

Do not silently assume a final storage layout before this step. Installation alone must not cause migration or default-path adoption.

## Confirmation Boundary Default

The first-run requirement is path confirmation, not full migration-plan approval.

Ask for confirmation before high-risk writes: replacing, moving, or bridging a non-empty real directory; destructive cleanup; private runtime state; project-owned Claude files; or unresolved conflicts.

Do not ask the user to approve a complete migration plan by default. After the user confirms default or custom paths, proceed with read-only inventory and routine low-risk actions under the documented migration rules.

## OS-Aware Defaults

### Windows default

- `C:\Users\<user>\ai_tools\skills`
- `C:\Users\<user>\ai_tools\agent-skills` as a compatibility bridge to `skills`
- `C:\Users\<user>\ai_tools\mcp`
- `C:\Users\<user>\ai_tools\user_plugin`
- `C:\Users\<user>\ai_tools\agent-config`

### macOS default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills` as a compatibility symlink to `skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`
- `~/ai_tools/agent-config`

### Linux default

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills` as a compatibility symlink to `skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`
- `~/ai_tools/agent-config`

These are suggested defaults only. The installed copy should store the final confirmed values in a local placement file.

## Default Path Notice Requirement

When no local placement file exists, or when the local placement file records `confirmed-default`, every agent response that proposes, installs, migrates, bridges, or summarizes managed paths must include a prominent notice near the top:

> **默认路径提醒 / Default Path Notice**
> 当前尚未使用自定义长期路径，或正在使用已确认的默认路径。
> Current status: default AI home paths are being proposed or used.
> Change them now if you want another drive or directory.

Use this notice in Codex, Claude, and generic OpenAI-compatible adapters. Do not hide default-path status inside prose.

## Category Content Defaults

- `skills`: the single shared public discovery directory for all standard callable `SKILL.md` folders, including normal skills and plugin-provided skill entries.
- `agent-skills`: compatibility bridge to `skills` by default; use as a real separate directory only for truly agent-specific adapters that cannot be shared through `skills`.
- `mcp`: MCP servers, bundles, manifests, adapters, and support files controlled by the user.
- `user_plugin`: third-party plugin repositories, self-contained plugin suites, standalone tool homes, marketplace-installed repos after migration, and plugin source trees.
- `agent-config`: user-controlled config files, adapter prompts, routing notes, launcher metadata, and local policy snippets.

## Compact Root Default

The confirmed AI home root should stay compact after migration and cleanup.

Default steady-state root contents:

- `skills`
- `plugins`, when a user-visible host plugin cache or bundle root belongs under the confirmed AI home
- `user_plugin`
- `mcp`
- `ai-home-inventory.md`

Create `agent-config` only when the machine actually has user-controlled adapter prompts, launcher metadata, routing notes, or local policy snippets to store.

Keep `agent-skills` as a compatibility bridge when an old entry path needs it. Do not keep it as a normal root folder unless the user confirms a real non-shared adapter directory is required.

Move backup, retention, and cleanup artifacts to a sibling archive root such as `<confirmed-ai-home-root>-archive`, not inside the AI home root.

## Skill-Linked Plugin Default

Treat a plugin as skill-linked only when it depends on one or more callable skill entries under the confirmed `skills` path.

Default placement rule:

- store the real repo under `user_plugin/<tool-name>`
- store only required callable skill entries or links under `skills`
- list it in the inventory as a skill-linked plugin only when those external skill entries exist
- list self-contained plugin suites only under `user_plugin`

## Marketplace Install Default

Before using Codex marketplace or another host installer, confirm the final long-term `user_plugin/<tool-name>` path.

Do not leave the real repo inside vendor-managed cache or temp marketplace paths long-term. If the host installs it to a temp marketplace path first, move or copy the real repo into `user_plugin` and keep the old path as a bridge when the host still expects that entry path.

## First-Run Prompt Template

Use this concise structure:

`I can standardize your user-installed AI agent content into long-term folders. Based on your current operating system, my suggested defaults are:`

`- skills: <default-skills-path>`
`- agent-skills: <default-agent-skills-compat-bridge-path>`
`- mcp: <default-mcp-path>`
`- user_plugin: <default-user-plugin-path>`
`- agent-config: <default-agent-config-path>`

`Please reply with "use defaults" to confirm these paths, or provide custom paths. If you do not confirm either option, I will stop before moving files, creating bridges, or changing configuration.`

## Ongoing Rule

If the user later changes any confirmed category path:

- automatically perform the migration needed to move content into the new location
- recreate or update any required entry bridges
- refresh the local placement record
- refresh `<confirmed-ai-home-root>/ai-home-inventory.md` as a Chinese-primary bilingual inventory with total counts, per-category counts, second-level work-type subgroups, source/upstream project labels for verified related skills or plugin entries, and `来源待确认 / Source pending` for entries whose upstream cannot be verified locally

## Bridge Terminology

Use `bridge` as the cross-platform term for preserving old tool entry paths:

- Windows: directory junctions
- macOS/Linux: symbolic links

Do not silently bridge private runtime state. Ask before touching sessions, history, local settings, or project-owned `.claude/` content.
