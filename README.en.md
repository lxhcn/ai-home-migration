<div align="center">

# 🏠 ai-home-migration

**A multi-agent home organizer for Codex, Claude, OpenAI-compatible agents, MCP, skills, plugins, and tool repos.**

Make AI agent installs clean, predictable, portable, and reusable.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Skill](https://img.shields.io/badge/type-agent%20skill-5B8DEF)
![Agents](https://img.shields.io/badge/agents-Codex%20%7C%20Claude%20%7C%20OpenAI-20A67A)
![Windows](https://img.shields.io/badge/Windows-junction%20aware-0078D4)
![Inventory](https://img.shields.io/badge/inventory-Chinese--primary%20bilingual-F59E0B)

[简体中文](README.md) · [Install](#-install) · [How It Works](#-how-it-works) · [Inventory](#-local-inventory) · [Repository Layout](#-repository-layout)

</div>

---

## ✨ What It Does

`ai-home-migration` turns scattered AI-agent assets into one durable home layout.

It helps you standardize:

| Area | What Gets Managed |
| --- | --- |
| 🧠 Skills | Codex skills, Claude-style skills, and generic OpenAI-compatible skill packages |
| 🔗 Agent entries | `agent-skills` links and tool-generated agent entry points |
| 🧩 MCP | User-managed MCP bundles, servers, and support directories |
| 🛠️ Plugins | Third-party plugin repos and standalone tool homes |
| ⚙️ Config | User-controlled agent prompts, adapter metadata, and launcher config |
| 🧭 Legacy paths | Junctions or compatibility paths that keep older tools working |

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

On first use, the skill asks you to confirm long-term paths for `skills`, `agent-skills`, `mcp`, `user_plugin`, and `agent-config`.

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
Choose direct move, copy-first repoint, or backup + junction
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

Choose between `Direct move + junction`, `Copy first + repoint`, and `Backup + junction` based on file locks and risk.

### 🪟 Windows-Aware Junctions

Preserve legacy entry paths while moving real content to a cleaner long-term location.

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
- Chinese purpose first, English purpose second
- path for every listed entry
- invocation examples when applicable
- excluded support folders such as `.system`

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
| Old entry paths are fragile | Junctions keep legacy entry paths working |
| No reusable inventory | Root-level bilingual `ai-home-inventory.md` |

## 🧭 Default Path Policy

Windows defaults:

```text
C:\Users\<user>\ai_tools\skills
C:\Users\<user>\ai_tools\agent-skills
C:\Users\<user>\ai_tools\mcp
C:\Users\<user>\ai_tools\user_plugin
C:\Users\<user>\ai_tools\agent-config
```

macOS / Linux defaults:

```text
~/ai_tools/skills
~/ai_tools/agent-skills
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
Use ai-home-migration to move this plugin into user_plugin and keep the old entry path working with a junction.
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
