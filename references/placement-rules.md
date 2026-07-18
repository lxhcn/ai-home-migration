# Placement Rules

This folder separates shareable policy from local runtime state.

## Shareable Files

- `placement-rules-default.md`
  Public default behavior. Use this for first-run prompts, OS-aware suggested paths, and generic placement rules.

- `agent-compatibility.md`
  Cross-agent packaging guidance for Codex, Claude, and generic OpenAI-compatible agents.

- `windows-junction-notes.md`
  Windows-specific migration and junction safety notes.

- `cross-platform-bridge-rules.md`
  Shared bridge policy for Windows junctions and macOS/Linux symbolic links.

## Local Runtime Files

- `placement-rules-local.md`
  Machine-specific confirmed paths. Read it only if it already exists in the installed copy for the current machine.

- `installed-skills-cheatsheet.md`
  Backward-compatible pointer only. The canonical inventory belongs at the confirmed AI home root as `ai-home-inventory.md`.

- `<confirmed-ai-home-root>/ai-home-inventory.md`
  Canonical local AI home inventory. This file lives at the root of the user's confirmed AI home, not under a single skill folder.

## Usage Rule

When `ai-home-migration` runs:

1. read `placement-rules-local.md` first if it exists
2. otherwise use `placement-rules-default.md` to propose OS-aware defaults
3. ask the user to confirm or change the category paths
4. if the user still does not specify custom paths, proceed with the suggested defaults
5. create or update `placement-rules-local.md` in the installed copy
6. create or update `<confirmed-ai-home-root>/ai-home-inventory.md` after skill installs, plugin installs, MCP changes, category migrations, renames, cleanup, or local inventory corrections
7. if `references/installed-skills-cheatsheet.md` exists, keep it as a pointer to the root inventory instead of a second source of truth
8. use `cross-platform-bridge-rules.md` when old entry paths must keep working after real content moves into the confirmed AI home

## Root Inventory Rule

`<confirmed-ai-home-root>/ai-home-inventory.md` must be a Chinese-primary bilingual quick reference and include:

- total managed entry count
- per-category counts for `skills`, `mcp`, `user_plugin`, `agent-config`, and any `agent-skills` compatibility bridge
- second-level work-type subgroups inside each large category so the file is scannable by purpose, not only by name
- source or upstream project labels for skills that can be verified as belonging to the same GitHub repository, plugin bundle, marketplace source, or local project
- a source summary showing how many entries came from each known source
- a dedicated subsection for skill-linked plugins only when a plugin repo also needs callable entries under `skills`
- plugin cache roots or plugin bundles when they are user-visible under the confirmed home
- backup directories and legacy entry bridges created during migration
- concise Chinese purpose hints first, with English purpose notes as secondary context
- path and invocation example fields where applicable

Use concise labels such as `源头 / Source: coreyhaines31/marketingskills` or `源头 / Source: OpenAI curated plugin cache`. The label can appear in the table row, entry heading, or a dedicated field; prefer the shape that keeps the inventory readable.

If local evidence cannot verify the upstream source, use `来源待确认 / Source pending`. Do not use a storage location such as `skills` or `local unified skills` as if it were a real upstream source.

When multiple skills belong to the same upstream project, mark every affected skill. For example, if `a1` and `b1` are both published from the `AB` GitHub project, show `源头 / Source: AB` for both entries and include `AB` in the source summary.

## Category Content Rule

- `skills`: the single shared public discovery directory for all standard callable `SKILL.md` folders, including normal skills and plugin-provided skill entries.
- `agent-skills`: compatibility bridge to `skills` by default; use as a real separate directory only for truly agent-specific adapters that cannot be shared through `skills`.
- `mcp`: MCP servers, bundles, manifests, adapters, and support files controlled by the user.
- `user_plugin`: third-party plugin repositories, self-contained plugin suites, standalone tool homes, marketplace-installed repos after migration, and plugin source trees.
- `agent-config`: user-controlled config files, adapter prompts, routing notes, launcher metadata, and local policy snippets.

## Compact Root Rule

Keep the confirmed AI home root easy to scan. In the normal steady state, it should contain only:

- `skills`
- `plugins`, when a user-visible host plugin cache or bundle root belongs under the confirmed AI home
- `user_plugin`
- `mcp`
- `ai-home-inventory.md`

Create `agent-config` only when real user-controlled config, adapter prompt, routing, or launcher metadata files exist.

Do not keep backup folders, old migration retention folders, temporary marketplace staging folders, or legacy compatibility directories in the AI home root after validation. Move those items to a sibling archive such as `<confirmed-ai-home-root>-archive/<cleanup-id>`.

Do not keep `agent-skills` as a visible root folder in the compact steady state unless it is a real, confirmed, non-shared adapter directory. Prefer direct global entry bridges from each agent's expected path to the shared `skills` directory.

For example, after cleanup a Windows root may intentionally contain only:

```text
D:\2_file\codex-home\
  skills\
  plugins\
  user_plugin\
  mcp\
  ai-home-inventory.md
```

## Skill-Linked Plugin Inventory Rule

Treat a plugin as skill-linked only when it depends on one or more callable skill entries under the confirmed `skills` path.

Do not create a separate "plugin with skills" inventory section merely because a plugin repo contains internal `skills/`, `SKILL.md`, `.codex-plugin/`, `.claude-plugin/`, `mcp/`, or `hooks/` paths. If the whole tool is self-contained inside the plugin, list it only under `user_plugin`.

If a plugin does need external callable skill entries:

1. store the real plugin repo under `user_plugin/<tool-name>`
2. store only the required callable skill entry folders or links under `skills`
3. keep the root inventory entry under a dedicated skill-linked plugin subsection
4. show both the plugin repo path and the skill entry path in the inventory

## Marketplace Install Rule

Before using Codex marketplace or another host installer, confirm the final long-term `user_plugin/<tool-name>` path.

If Codex marketplace installs a repo under a cache or temp path such as `~/.codex/.tmp/marketplaces/<tool-name>` or `C:\Users\<user>\.codex\...`, then:

1. treat the temp path as an entry path only
2. move or copy the real repo into `user_plugin/<tool-name>`
3. recreate the old marketplace path as a bridge to the unified `user_plugin` location
4. list it as a normal plugin unless it also needs callable entries under `skills`

Do not count system folders without `SKILL.md` as skills. For example, a `.system` directory can be present under `skills` but should be reported as excluded system support content, not as a callable skill.

The legacy `references/installed-skills-cheatsheet.md` path must not contain a divergent copy of the inventory. It should point readers to the root-level inventory file.

## Claude Coverage Rule

When inventorying Claude-related content, include both user-level and project-level paths:

- user-level: `~/.claude/`, `~/.claude.json`, `~/.claude/settings.json`, `~/.claude/skills/`, `~/.claude/commands/`, `~/.claude/agents/`
- project-level: `.claude/settings.json`, `.claude/settings.local.json`, `.claude/skills/`, `.claude/commands/`, `.claude/agents/`, `.claude/rules/`, `.mcp.json`, `CLAUDE.md`, `.claude/CLAUDE.md`, `CLAUDE.local.md`

Treat `settings.local.json`, `CLAUDE.local.md`, and user-level state as local/private unless the user explicitly asks to migrate or back them up.

## Publishing Rule

For a shareable repository:

- keep `placement-rules-default.md`
- keep `placement-rules.md`
- keep `windows-junction-notes.md`
- do not commit machine-specific runtime files unless they are intentionally sanitized examples
