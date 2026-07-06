# Contributing

Thanks for improving `codex-home-migration`.

This repository is intentionally small. Contributions should keep the skill focused on one job: standardizing user-managed Codex content paths while preserving compatibility with legacy entry paths.

## Good Contributions

- Clearer first-run behavior
- Safer Windows junction guidance
- Better examples for `skills`, `agent-skills`, `mcp`, and `user_plugin`
- Cross-platform default path improvements
- Documentation fixes that keep local machine paths out of shared files

## Please Avoid

- Committing machine-specific runtime files such as `references/placement-rules-local.md`
- Adding one user's absolute paths as universal defaults
- Moving third-party tools into bundled Codex cache paths
- Recommending destructive cleanup without an inventory and backup path

## Local Runtime Files

The following files are expected to be generated or updated only after installation on a user's machine:

- `references/placement-rules-local.md`
- `references/installed-skills-cheatsheet.md`

They are ignored by default because they may contain local paths and local installation state.
