<div align="center">

# 🏠 ai-home-migration

**A multi-agent home organizer for Codex, Claude, OpenAI-compatible agents, MCP, skills, plugins, and tool repos.**

Make AI agent installs clean, predictable, portable, and reusable.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Skill](https://img.shields.io/badge/type-agent%20skill-5B8DEF)
![Agents](https://img.shields.io/badge/agents-Codex%20%7C%20Claude%20%7C%20OpenAI-20A67A)
![Bridge](https://img.shields.io/badge/bridge-junction%20%7C%20symlink-0078D4)
![Inventory](https://img.shields.io/badge/inventory-Chinese--primary%20bilingual-F59E0B)

[简体中文](README.md) · [Install](#-install) · [After Install](#-after-install-required-first-run) · [How It Works](#-how-it-works) · [Inventory](#-local-inventory)

</div>

---

## ✨ What It Does

`ai-home-migration` turns scattered AI-agent assets into one durable home layout.

It helps you standardize:

| Area | What Gets Managed |
| --- | --- |
| 🧠 Skills | Codex skills, Claude-style skills, and generic OpenAI-compatible skill packages |
| 🔗 Agent entries | Compatibility entries that point to `skills`; `agent-skills` is normally only a legacy bridge |
| 🧩 MCP | User-managed MCP bundles, servers, and support directories |
| 🛠️ Plugins | Third-party plugin repos, standalone tool homes, and real repos migrated after marketplace installs |
| ⚙️ Config | User-controlled agent prompts, adapter metadata, and launcher config |
| 🧭 Legacy paths | Cross-platform bridges that keep older tool entries working |

The goal is simple: install once, migrate safely, keep old entry paths working, and make future installs follow the same rule.

## 🚀 Install

Install or copy this repository as a skill package named `ai-home-migration`:

```text
ai-home-migration/
  SKILL.md
  agents/openai.yaml
  agents/claude.md
  agents/generic-openai.md
  references/
```

Use the entry point that matches your runtime:

| Runtime | Entry Point |
| --- | --- |
| Codex / OpenAI skill surfaces | `SKILL.md` plus `agents/openai.yaml` |
| Claude-style surfaces | `agents/claude.md`, which points back to `SKILL.md` |
| Generic OpenAI-compatible agents | prompt wrapper in `agents/generic-openai.md` |

On first use, the skill asks you to confirm long-term paths for `skills`, `mcp`, `user_plugin`, `agent-config`, and whether `agent-skills` should remain only as a compatibility bridge.

## 🗂️ What Each Directory Stores

| Directory | Contents |
| --- | --- |
| `skills` | The single shared public Skills directory; all standard `SKILL.md` folders, including normal skills and plugin-provided skill entries, are published here |
| `agent-skills` | Compatibility bridge to `skills` by default; use it as a real separate directory only for truly agent-specific adapters |
| `mcp` | User-managed MCP servers, bundles, manifests, adapters, and support files |
| `user_plugin` | Third-party plugin repos, self-contained plugin suites, standalone tool homes, and real repos migrated after marketplace installs |
| `agent-config` | User-controlled agent config, adapter prompts, routing notes, launcher metadata, and local policy snippets |

### 🧹 Keep the Root Compact

After migration and cleanup, the AI home root should be easy to scan. The normal steady state keeps only:

```text
<ai-home-root>/
  skills/
  plugins/
  user_plugin/
  mcp/
  ai-home-inventory.md
```

Notes:

- Create `agent-config` only when real user-controlled config, adapter prompts, routing notes, or launcher metadata exist.
- Do not keep `agent-skills` as a permanent root folder by default. When legacy compatibility is needed, point each agent's global entry directly to the unified `skills` directory with a bridge.
- Move backups, migration retention folders, old-path protection folders, and temporary staging content to a sibling `<ai-home-root>-archive/<cleanup-id>` instead of leaving them in the AI home root.

## ✅ After Install: Required First Run

Installing this repository only makes the `ai-home-migration` rules available to your agent. It does not silently migrate folders, edit configuration, or create entry bridges at install time.

> **Default Path Notice / 默认路径提醒**
> If you have not confirmed long-term paths yet, `ai-home-migration` only proposes defaults. It must not silently migrate folders, create bridges, or edit configuration.
> The agent may continue with write operations only after you explicitly reply that it should use the defaults or provide custom paths.
> If you confirm the defaults, later plans, action summaries, and final reports should keep prominently saying that default paths are being used.

Keep the confirmation boundary clear: the user confirms long-term paths and high-risk write operations, not a complete migration plan every time. After paths are confirmed, the agent should continue with inventory, classification, validation, and low-risk migration work. It should pause again only for non-empty directory replacement, destructive cleanup, private runtime state, unclear project ownership, or unresolved conflicts.

After installation, explicitly run the first organization pass in Codex, Claude, or another compatible agent:

```text
Use ai-home-migration to inspect and organize my Codex, Claude, MCP, skills, and plugins paths. Put real content under one AI home and create cross-platform bridges for legacy entry paths that must keep working.
```

The first run does five things:

| Step | Purpose |
| --- | --- |
| 1. Inventory entry paths | Check `.codex`, `.claude`, `.agents`, MCP, plugins, and tool repo locations |
| 2. Confirm long-term folders | Ask you to confirm `skills`, `mcp`, `user_plugin`, `agent-config`, and whether `agent-skills` should stay only as a compatibility bridge |
| 3. Migrate or bridge | Move real content into long-term folders, or create the platform-appropriate bridge for legacy entries |
| 4. Validate resolution | Confirm Codex, Claude, or other tools can still find content through their expected entry paths |
| 5. Refresh inventory | Update `<confirmed-ai-home-root>/ai-home-inventory.md` |

Why not do this automatically and silently? Because this step may move directories, preserve backups, repoint tool entries, or create platform bridges such as Windows junctions or macOS/Linux symlinks. `ai-home-migration` can guide and perform that work, but it should happen only after you explicitly trigger and confirm it.

For Codex marketplace or similar host installers, confirm the final long-term location first. Even if the installer downloads a repo into a Windows `C:\Users\<user>` path, `.codex` cache, or temporary marketplace path, the real repo should be migrated into `user_plugin/<tool-name>`, with the old entry path kept only as a bridge when needed.

If you only want to bridge Claude, say:

```text
Use ai-home-migration to inspect only Claude skills, commands, agents, and config entry paths. Tell me what should be bridged into the unified AI home and what should remain private local state.
```

### Cross-Platform Bridge Rules

`ai-home-migration` uses `bridge` as the shared user-facing concept: real content lives in the unified AI home, while old tool entry paths keep working. The operating-system implementation differs:

| Platform | Default bridge | Typical use |
| --- | --- | --- |
| Windows | directory junction | `.codex\skills`, `.claude\skills`, legacy plugin entries |
| macOS | symbolic link | `~/.codex/skills`, `~/.claude/skills`, `~/.agents/skills` |
| Linux | symbolic link | `~/.codex/skills`, `~/.claude/skills`, `~/.agents/skills` |

It does not broadly bridge sessions, history, shell snapshots, local settings, or project-owned `.claude/` content. Those are private or project state and require separate confirmation.

## 🧭 How It Works

```text
Detect OS
   ↓
Suggest default long-term folders
   ↓
Ask you to confirm or change paths
   ↓
Inventory current Codex / Claude / agent / MCP / plugin locations
   ↓
Choose direct move, copy-first repoint, or backup + bridge
   ↓
Refresh the root AI home inventory
```

The skill keeps shareable policy files separate from machine-specific runtime state. That means the repository stays reusable, while each computer keeps its own confirmed paths.

## 🧰 Core Capabilities

### 📍 Placement Policy

Define one durable home for user-managed AI agent content instead of deciding manually on every install.

### 🧪 First-Run Setup

Prompt for long-term paths before migration starts, with sensible OS-aware defaults.

### 🛡️ Safer Migration

Choose between `Direct move + bridge`, `Copy first + repoint`, and `Backup + bridge` based on file locks and risk.

### 🧭 Cross-Platform Bridges

Preserve legacy entry paths with Windows junctions or macOS/Linux symlinks while moving real content to a cleaner long-term location.

### 🔁 Ongoing Maintenance

Reuse confirmed paths, refresh the inventory, and keep future installs consistent.

## 📚 Local Inventory

The canonical local inventory lives at:

```text
<confirmed-ai-home-root>/ai-home-inventory.md
```

For example:

```text
D:\2_file\codex-home\ai-home-inventory.md
```

It is a Chinese-primary bilingual quick reference. It includes:

- total managed entry count
- per-category counts
- work-type subgroups under each large category
- `Source` labels for entries that come from the same GitHub project or plugin bundle, and `Source pending` when local evidence cannot verify the upstream
- Chinese purpose first, English purpose second
- path for every listed entry
- invocation examples when applicable
- excluded support folders such as `.system`

A "plugin with skills" is listed separately only when the plugin repo lives under `user_plugin` and also needs callable entries under `skills`. A self-contained plugin suite such as `last30days` should be listed only under `user_plugin`, not under a separate skill-linked plugin group.

The historical `references/installed-skills-cheatsheet.md` path is kept only as a compatibility pointer.

## 🧩 What It Solves

- "My Codex and Claude skills are scattered everywhere."
- "I want the same migration rule to work in Codex, Claude, and OpenAI-compatible agents."
- "I need to move AI-agent installs to another drive without breaking old paths."
- "A plugin still expects its original launcher folder."
- "Windows says a repo, `.git`, or native file is locked."
- "I do not want to rethink folder placement every time I install a new skill."

## 🏗️ Before / After

| Before | After |
| --- | --- |
| Custom skills scattered across `.codex`, `.claude`, `.agents`, and ad-hoc folders | One confirmed long-term layout |
| Plugin repos hidden inside tool homes | Plugin repos live under `user_plugin` |
| MCP content managed separately | MCP content follows the same placement policy |
| Old entry paths are fragile | Bridges keep legacy entry paths working |
| No reusable inventory | Root-level bilingual `ai-home-inventory.md` |

## 🧭 Default Path Policy

Windows defaults:

```text
C:\Users\<user>\ai_tools\skills
C:\Users\<user>\ai_tools\agent-skills  # compatibility bridge to skills
C:\Users\<user>\ai_tools\mcp
C:\Users\<user>\ai_tools\user_plugin
C:\Users\<user>\ai_tools\agent-config
```

macOS / Linux defaults:

```text
~/ai_tools/skills
~/ai_tools/agent-skills  # compatibility symlink to skills
~/ai_tools/mcp
~/ai_tools/user_plugin
~/ai_tools/agent-config
```

These are suggestions only. The installed copy stores the final confirmed values in `references/placement-rules-local.md`.

## 💬 Example Prompts

```text
Use ai-home-migration to install this skill into my long-term skills directory and keep any expected old path working.
```

```text
Use ai-home-migration to standardize my Codex, Claude, MCP, and agent-tool setup.
```

```text
Use ai-home-migration to move this plugin into user_plugin and keep the old entry path working with a bridge.
```

## 📦 Shareable vs Local Files

Shareable repository files:

- `SKILL.md`
- `agents/openai.yaml`
- `agents/claude.md`
- `agents/generic-openai.md`
- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/agent-compatibility.md`
- `references/cross-platform-bridge-rules.md`
- `references/windows-junction-notes.md`

Machine-specific runtime files:

- `references/placement-rules-local.md`
- `<confirmed-ai-home-root>/ai-home-inventory.md`
- `references/installed-skills-cheatsheet.md` as a compatibility pointer

Local runtime files should not be committed as universal defaults because they contain machine-specific paths and installation state.

## 🗂️ Repository Layout

```text
ai-home-migration/
  SKILL.md
  README.md
  README.en.md
  README.zh-CN.md
  .gitignore
  .gitattributes
  CHANGELOG.md
  CONTRIBUTING.md
  GITHUB_ABOUT.md
  LICENSE
  SECURITY.md
  agents/
    openai.yaml
    claude.md
    generic-openai.md
  references/
    agent-compatibility.md
    cross-platform-bridge-rules.md
    placement-rules.md
    placement-rules-default.md
    windows-junction-notes.md
```

## 🔎 Discoverability

This repository intentionally uses terms such as `Codex`, `Claude`, `OpenAI`, `AI agent`, `skills`, `agent-skills`, `MCP`, `plugin`, `migration`, `Windows`, and `junction`, because those are the practical problems users search for when their local agent setup starts getting hard to maintain.

## 📝 Notes

- This repository contains the shareable policy layer.
- Each machine should generate its own confirmed path record after installation.
- If you distribute this skill, share the repository files and let each user confirm their own long-term paths on first run.
