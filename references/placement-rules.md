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
  Local quick-reference file for installed skills. Read or update it only after skill installs.

## Usage Rule

When `ai-home-migration` runs:

1. read `placement-rules-local.md` first if it exists
2. otherwise use `placement-rules-default.md` to propose OS-aware defaults
3. ask the user to confirm or change the category paths
4. if the user still does not specify custom paths, proceed with the suggested defaults
5. create or update `placement-rules-local.md` in the installed copy
6. create or update `installed-skills-cheatsheet.md` only when skill installs require it

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
