# Agent Compatibility

This file explains how to package `ai-home-migration` for multiple AI agent runtimes without duplicating the migration policy.

## Compatibility Model

Use one canonical workflow:

- `SKILL.md` contains the operational policy.
- `references/` contains detailed rules loaded as needed.
- `agents/` contains thin adapters for specific agent surfaces.

Do not maintain separate migration logic for Codex, Claude, and generic OpenAI-style agents. Divergent rules make path migration risky.

## Supported Surfaces

### Codex / OpenAI Skill Surfaces

Use:

- `SKILL.md`
- `agents/openai.yaml`
- `references/*.md`

Codex should trigger from the `SKILL.md` frontmatter and show UI metadata from `agents/openai.yaml`.

### Claude-Style Surfaces

Use:

- `SKILL.md` as the canonical instruction file
- `agents/claude.md` as the Claude-oriented prompt wrapper
- `references/*.md` as supporting policy files

If the Claude environment requires a different manifest, create that manifest as an adapter that points back to `SKILL.md`.

### Generic OpenAI-Compatible Agents

Use:

- `agents/generic-openai.md` as the prompt wrapper
- `SKILL.md` as the canonical workflow
- `references/*.md` as task-specific supporting context

For hosted assistants or local agent runners, paste the prompt snippet from `agents/generic-openai.md` into the agent's system or developer instructions and attach or mount this repository as readable context.

## Packaging Checklist

- Keep `SKILL.md` at the repository root.
- Keep `agents/openai.yaml` for Codex/OpenAI UI metadata.
- Keep `agents/claude.md` for Claude-oriented usage.
- Keep `agents/generic-openai.md` for prompt-only agents.
- Keep local runtime files ignored:
  - `references/placement-rules-local.md`
  - `references/installed-skills-cheatsheet.md`
- Add new runtime manifests only if they are thin pointers to the canonical workflow.

## Naming Guidance

The repository should be named `ai-home-migration`, and public descriptions should mention AI agent content, Claude, OpenAI-compatible agents, MCP, skills, plugins, and path migration.
