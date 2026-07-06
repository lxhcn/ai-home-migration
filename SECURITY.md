# Security Policy

`codex-home-migration` is an operational policy skill. It can guide file moves, junction creation, and path cleanup, so changes should be conservative and easy to audit.

## Reporting Issues

If you find a risky instruction, unsafe migration pattern, or path-handling problem, please open a GitHub issue with:

- the operating system
- the affected source and destination path pattern
- whether junctions, symlinks, or locked files were involved
- the safest reproduction steps you can share

Do not include private absolute paths, tokens, API keys, or machine-specific configuration unless you have sanitized them first.

## Safety Expectations

- Inventory before moving files.
- Preserve backups when deletion or replacement is risky.
- Treat local runtime files as private machine state.
- Do not publish `references/placement-rules-local.md` from a real machine.
- Prefer copy-first migration for active repos, plugin homes, and locked paths.
