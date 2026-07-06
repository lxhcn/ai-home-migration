# Placement Rules

This folder separates shareable policy from local runtime state.

## Shareable Files

- `placement-rules-default.md`
  Public default behavior. Use this for first-run prompts, OS-aware suggested paths, and generic placement rules.

- `agent-compatibility.md`
  Cross-agent packaging guidance for Codex, Claude, and generic OpenAI-compatible agents.

- `windows-junction-notes.md`
  Windows-specific migration and junction safety notes.

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

## Root Inventory Rule

`<confirmed-ai-home-root>/ai-home-inventory.md` must be a Chinese-primary bilingual quick reference and include:

- total managed entry count
- per-category counts for `skills`, `agent-skills`, `mcp`, `user_plugin`, and `agent-config`
- plugin cache roots or plugin bundles when they are user-visible under the confirmed home
- backup directories and legacy entry junctions created during migration
- concise Chinese purpose hints first, with English purpose notes as secondary context
- path and invocation example fields where applicable

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
