# Generic OpenAI-Compatible Adapter

Use this adapter for OpenAI-compatible agents, custom assistants, local agent runners, or prompt-based workflows that do not understand Codex `agents/openai.yaml`.

## System Or Developer Prompt Snippet

```text
You have access to a skill folder named ai-home-migration. Read SKILL.md as the canonical workflow. Use it to standardize user-managed AI agent content, including Codex skills, Claude skills or instructions, MCP bundles, OpenAI-compatible agent prompts, plugin repos, and standalone tool homes. Before changing files, confirm long-term category paths, inventory source paths, classify each move by risk, preserve legacy entry paths when needed, and keep machine-specific runtime files out of shared repository files.
```

## Loading Order

1. Read `SKILL.md`.
2. Read `references/placement-rules.md`.
3. Read `references/placement-rules-default.md` when no local placement file exists.
4. Read `references/windows-junction-notes.md` on Windows or when junctions/symlinks are involved.
5. Read `references/agent-compatibility.md` only when adapting the package to another runtime.

## Runtime Requirements

- Use structured filesystem APIs where available.
- Ask before destructive moves.
- Prefer copy-first migration for active repos, locked files, and plugin homes.
- Keep local runtime files local.
