# Claude Adapter

Use this adapter when a Claude environment can read a skill folder or when a user asks Claude to apply this repository manually.

## Canonical File

Read `../SKILL.md` first. Treat it as the source of truth.

Then read only the references required by the task:

- `../references/placement-rules.md`
- `../references/placement-rules-default.md`
- `../references/windows-junction-notes.md` on Windows or when junctions/symlinks are involved
- `../references/agent-compatibility.md` when packaging this skill for another agent runtime

## Suggested Claude Prompt

```text
Use the ai-home-migration skill from this folder. Read SKILL.md as the canonical workflow, then standardize my user-managed AI agent content across Codex, Claude, MCP, OpenAI-compatible agents, and plugin/tool repos. Confirm long-term category paths and high-risk writes, inventory first, preserve legacy entry paths when needed, and avoid publishing machine-specific local files. Do not require approval of the whole migration plan unless I ask for that review. If only default paths are available or confirmed, show the highlighted Default Path Notice near the top of every plan, action summary, and final response.
```

## Claude-Specific Notes

- Treat Claude skills, project instructions, and local launcher metadata as user-managed agent content.
- Inventory both user-level Claude paths, such as `~/.claude/skills/`, `~/.claude/agents/`, `~/.claude/settings.json`, `~/.claude/CLAUDE.md`, and `~/.claude.json`, and project-level paths, such as `.claude/skills/`, `.claude/commands/`, `.claude/agents/`, `.claude/rules/`, `.claude/settings.json`, `.claude/settings.local.json`, `.mcp.json`, `CLAUDE.md`, `.claude/CLAUDE.md`, and `CLAUDE.local.md`.
- Treat `.claude/settings.local.json`, `CLAUDE.local.md`, and `~/.claude.json` as local/private state by default.
- Treat project `.claude/skills/`, `.claude/commands/`, `.claude/agents/`, `.claude/rules/`, `.claude/settings.json`, `.mcp.json`, `CLAUDE.md`, and `.claude/CLAUDE.md` as potentially shareable repository content only after confirming the user's intent.
- Do not move vendor-managed caches or application bundles unless the user explicitly asks.
- Preserve local files such as `placement-rules-local.md` as machine-specific state.
- When a Claude installation expects a particular entry path, keep that path working with a junction or symlink only after validating the target.
- Do not silently adopt default paths. If no local placement file exists, ask the user to confirm defaults or provide custom paths before migration, bridge creation, or config writes.
- After paths are confirmed, proceed with routine low-risk migration steps and ask again only before replacing non-empty directories, destructive cleanup, private runtime state, project-owned content, or unresolved conflicts.
