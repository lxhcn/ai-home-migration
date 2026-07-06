# Cross-Platform Bridge Rules

Use these rules whenever `ai-home-migration` needs to keep an old tool entry path working while storing real content in the confirmed AI home.

## Unified Concept

Use the word `bridge` for the cross-platform behavior:

- the real content lives in the confirmed AI home
- the old tool-specific entry path remains available
- the operating system redirects the old entry path to the real content

The implementation differs by operating system, but the user-facing intent is the same.

## Platform Mapping

| Platform | Preferred bridge | Typical command | Use for |
| --- | --- | --- | --- |
| Windows | directory junction | `mklink /J <entry> <target>` | local directory entry paths such as `.codex\skills` or `.claude\skills` |
| macOS | symbolic link | `ln -s <target> <entry>` | directory entry paths under `~/.codex`, `~/.claude`, or `~/.agents` |
| Linux | symbolic link | `ln -s <target> <entry>` | directory entry paths under `~/.codex`, `~/.claude`, or `~/.agents` |

Use platform-native path syntax in user-facing plans.

## Safety Rules

- Do not silently replace a non-empty real directory with a bridge.
- If the old entry path contains content, inventory it first.
- If the target is absent, create and validate it before creating the bridge.
- If the old path is already a bridge, verify its target instead of recreating it.
- Keep private runtime state such as sessions, history, shell snapshots, and local settings out of broad automatic bridging.
- Prefer bridging only well-known entry folders such as `skills`, `commands`, `agents`, plugin launchers, and tool-specific entry directories.
- For project-local `.claude/` content, confirm whether it belongs to that project before moving or bridging it.

## First-Run Bridge Flow

1. Detect the operating system.
2. Inventory common Codex, Claude, OpenAI-compatible agent, MCP, plugin, and tool entry paths.
3. Classify each path as:
   - empty entry path
   - normal directory with content
   - existing bridge
   - private runtime state
   - project-owned content
4. Ask for confirmation before migrating or replacing any path that contains content.
5. Move or copy real content into the confirmed AI home when appropriate.
6. Create the platform-specific bridge for the old entry path.
7. Verify that the old path resolves to the intended target.
8. Refresh the root inventory.
