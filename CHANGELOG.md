# Changelog

All notable changes to this project will be documented in this file.

The format is inspired by Keep a Changelog and uses semantic-style version labels for repository releases.

## [Unreleased]

### Added

- Claude adapter instructions in `agents/claude.md`
- Generic OpenAI-compatible prompt wrapper in `agents/generic-openai.md`
- Cross-agent packaging guidance in `references/agent-compatibility.md`
- `agent-config` category for user-controlled adapter prompts and agent metadata

### Changed

- Expanded the skill from Codex-only positioning to a multi-agent migration policy for Codex, Claude, OpenAI-compatible agents, MCP bundles, skills, plugins, and tool repos
- Expanded Claude coverage beyond `~/.claude/skills` to include user settings, project settings, commands, agents, rules, MCP config, and CLAUDE memory files
- Moved the canonical local inventory concept to the AI home root as `ai-home-inventory.md`; the old `installed-skills-cheatsheet.md` path is now only a compatibility pointer

## [1.0.0] - 2026-07-06

### Added

- Initial public repository structure for `ai-home-migration`
- English and Simplified Chinese documentation split into separate README files
- Shareable default placement policy for first-run path confirmation
- Windows-specific junction and migration safety guidance
- GitHub publishing support files including `.gitignore`, `.gitattributes`, `LICENSE`, and repository metadata copy
- Contribution and security guidance for safe repository maintenance

### Changed

- Reframed the project as a reusable policy skill instead of a machine-specific migration note
- Clarified the split between shareable repository files and local runtime-generated files
- Formalized first-run behavior for OS-aware defaults and local path confirmation
- Added explicit install instructions to both README files

### Notes

- Machine-specific files such as `references/placement-rules-local.md` and `references/installed-skills-cheatsheet.md` are intentionally excluded from the public repository baseline
