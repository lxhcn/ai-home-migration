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
- Standardized the local inventory format as a Chinese-primary bilingual quick reference with Chinese and English purpose fields
- Redesigned the English and Simplified Chinese README files with badges, icon-led sections, navigation links, comparison tables, and clearer installation flow
- Made Simplified Chinese the primary GitHub README, moved English documentation to `README.en.md`, and refreshed GitHub About topic guidance
- Added a prominent post-install first-run section explaining that migration and platform bridge creation require explicit user-triggered execution
- Added cross-platform bridge rules that map Windows directory junctions and macOS/Linux symbolic links into one shared entry-path preservation model
- Clarified that marketplace-installed plugin repos must be moved into the confirmed `user_plugin` path instead of remaining in user-profile, cache, or temporary marketplace locations
- Narrowed the "plugin with skills" inventory rule so self-contained plugin suites stay under `user_plugin`; only plugins that require callable entries under `skills` get a dedicated skill-linked plugin subsection
- Documented what each confirmed category path stores in the Chinese and English README files
- Simplified the standard skill discovery model: all standard callable `SKILL.md` folders now publish to `skills`, while `agent-skills` is treated as a compatibility bridge by default and reserved as a real directory only for non-shared agent-specific adapters
- Added a compact-root cleanup rule: keep the AI home root limited to durable category folders plus `ai-home-inventory.md`, move backup/retention artifacts to a sibling archive, and use direct global entry bridges to the unified `skills` directory
- Required local inventories to keep the existing large categories while adding work-type subgroups and source/upstream project labels for related skills
- Clarified that unknown skill provenance must be labeled `来源待确认 / Source pending` instead of treating the unified storage directory as a source

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
