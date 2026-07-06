# Windows Junction Notes

Use these notes when Codex-home migration on Windows does not behave like a simple move.

## Reliable Patterns

- Use `cmd /c rmdir <path>` to remove a junction shell when PowerShell `Remove-Item` throws unexpected errors.
- Use `robocopy <src> <dst> /E` for copy-first migrations when `Move-Item` fails on locked repos or plugin caches.
- Create the destination directory tree before attempting junction swaps.
- Verify `LinkType` and `Target` after each step instead of assuming the swap succeeded.

## Common Failure Modes

### Locked Native Plugin Files

Symptoms:

- `Remove-Item` fails on `.node` files inside plugin caches
- `Rename-Item` on `.codex\plugins` returns access denied

Response:

- Preserve the old directory as-is
- Finish everything else first
- Return later when Codex processes are closed

### Locked Git Metadata

Symptoms:

- `Move-Item` fails on `.git` inside a tool-specific repo

Response:

- Copy the repo to the unified target instead of moving it
- Repoint external entry junctions to the copied target
- Leave the original repo as fallback

### Partial Move Into Precreated Target

Symptoms:

- You precreate the destination directory
- `Move-Item` places content into the destination but leaves the source directory shell behind

Response:

- Inspect both source and destination before continuing
- Do not assume the source is safe to delete
- Prefer backup + junction if the source still contains content

## Validation Checklist

- Original path exists
- Original path is now a junction when migration is complete
- Junction target is correct
- Destination contains expected children
- Tool-specific entry links resolve to the unified target
