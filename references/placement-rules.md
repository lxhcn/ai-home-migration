# Placement Rules

This folder separates shareable policy from local runtime state.

## Shareable Files

- `placement-rules-default.md`
  Public default behavior. Use this for first-run prompts, OS-aware suggested paths, and generic placement rules.

- `windows-junction-notes.md`
  Windows-specific migration and junction safety notes.

## Local Runtime Files

- `placement-rules-local.md`
  Machine-specific confirmed paths. Read it only if it already exists in the installed copy for the current machine.

- `installed-skills-cheatsheet.md`
  Local quick-reference file for installed skills. Read or update it only after skill installs.

## Usage Rule

When `codex-home-migration` runs:

1. read `placement-rules-local.md` first if it exists
2. otherwise use `placement-rules-default.md` to propose OS-aware defaults
3. ask the user to confirm or change the category paths
4. if the user still does not specify custom paths, proceed with the suggested defaults
5. create or update `placement-rules-local.md` in the installed copy
6. create or update `installed-skills-cheatsheet.md` only when skill installs require it

## Publishing Rule

For a shareable repository:

- keep `placement-rules-default.md`
- keep `placement-rules.md`
- keep `windows-junction-notes.md`
- do not commit machine-specific runtime files unless they are intentionally sanitized examples
