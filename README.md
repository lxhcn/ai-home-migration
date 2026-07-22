<div align="center">

# 🏠 ai-home-migration

**给 Codex、Claude、OpenAI 兼容 agent、MCP、skills、plugins 和工具仓库用的 AI home 整理器。**

让 AI agent 的自装内容不再越装越乱，而是可迁移、可复用、可长期维护。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Skill](https://img.shields.io/badge/type-agent%20skill-5B8DEF)
![Agents](https://img.shields.io/badge/agents-Codex%20%7C%20Claude%20%7C%20OpenAI-20A67A)
![Bridge](https://img.shields.io/badge/bridge-junction%20%7C%20symlink-0078D4)
![Inventory](https://img.shields.io/badge/inventory-Chinese--primary%20bilingual-F59E0B)

[English](README.en.md) · [安装](#-安装) · [安装后必须做](#-安装后必须做) · [工作方式](#-工作方式) · [本地清单](#-本地清单)

</div>

---

## ✨ 它做什么

`ai-home-migration` 会把散落在不同目录里的 AI agent 自装内容，整理进一套长期稳定的目录规则。

它覆盖：

| 分类 | 管理内容 |
| --- | --- |
| 🧠 Skills | Codex skills、Claude 风格 skills、通用 OpenAI 兼容 skill 包 |
| 🔗 Agent 入口 | 统一指向 `skills` 的兼容入口；`agent-skills` 默认只做旧路径 bridge |
| 🧩 MCP | 用户管理的 MCP bundle、server 和支持目录 |
| 🛠️ 插件 | 第三方插件仓库、独立工具仓库、marketplace 安装后的真实仓库 |
| ⚙️ 配置 | 用户可控的 agent prompt、适配元数据和启动配置 |
| 🧭 旧入口 | 用跨平台 bridge 保留旧工具入口 |

目标很简单：安装时有规则，迁移时更稳妥，旧入口继续可用，以后新增内容沿用同一套目录策略。

## 🚀 安装

把这个仓库安装或复制为名叫 `ai-home-migration` 的 skill 包，并保持结构不变：

```text
ai-home-migration/
  SKILL.md
  agents/openai.yaml
  agents/claude.md
  agents/generic-openai.md
  references/
```

按运行环境选择入口：

| 运行环境 | 入口文件 |
| --- | --- |
| Codex / OpenAI skill 环境 | `SKILL.md` 和 `agents/openai.yaml` |
| Claude 风格环境 | `agents/claude.md`，它会指回核心 `SKILL.md` |
| 通用 OpenAI 兼容 agent | `agents/generic-openai.md` 里的 prompt wrapper |

首次使用时，skill 会让你确认 `skills`、`mcp`、`user_plugin`、`agent-config`，以及是否需要保留 `agent-skills` 兼容 bridge。

## 🗂️ 统一目录分别放什么

| 目录 | 存放内容 |
| --- | --- |
| `skills` | 唯一公共 Skills 目录；所有标准 `SKILL.md`，包括普通 skills 和插件提供的 skill 入口，都发布到这里 |
| `agent-skills` | 默认作为指向 `skills` 的兼容 bridge；只有真正不能通用的 Agent 专用适配器才单独放这里 |
| `mcp` | 用户管理的 MCP server、bundle、manifest、adapter 和支持文件 |
| `user_plugin` | 第三方插件仓库、整套自洽的插件、独立工具仓库、marketplace 安装后迁入的真实仓库 |
| `agent-config` | 用户可控的 agent 配置、adapter prompt、路由说明、启动元数据、本地策略片段 |

### 🧹 根目录保持轻量

迁移和清理完成后的 AI home 根目录应该容易扫一眼看懂。正常稳定状态只保留：

```text
<ai-home-root>/
  skills/
  plugins/
  user_plugin/
  mcp/
  ai-home-inventory.md
```

说明：

- `agent-config` 只有在真的存在用户可控配置、adapter prompt、路由说明或启动元数据时才创建。
- `agent-skills` 默认不再作为根目录常驻；需要兼容旧入口时，让对应 agent 的全局入口直接 bridge 到统一 `skills`。
- 备份、迁移留存、旧路径保护目录和临时 staging 内容，应该移动到相邻的 `<ai-home-root>-archive/<cleanup-id>`，不要长期堆在 AI home 根目录。

## ✅ 安装后必须做

安装这个仓库只代表你的 agent 已经能读取 `ai-home-migration` 的规则。它不会在安装瞬间自动迁移目录、修改配置或创建接引 bridge。

> **默认路径提醒 / Default Path Notice**
> 如果你还没有确认长期路径，`ai-home-migration` 只会提出默认建议，不会静默迁移、创建 bridge 或修改配置。
> 只有当你明确回复“使用默认路径”或提供自定义路径后，agent 才能继续执行写入类操作。
> 如果你确认使用默认路径，后续计划、执行摘要和完成报告都应继续醒目标注“正在使用默认路径”。

安装完成后，请在 Codex、Claude 或其他兼容 agent 中显式运行一次首次整理：

```text
请用 ai-home-migration 检查并整理我的 Codex、Claude、MCP、skills、plugins 路径，把真实内容放到统一 AI home，并为需要兼容的旧入口建立跨平台接引 bridge。
```

首次整理会做这些事：

| 步骤 | 作用 |
| --- | --- |
| 1. 盘点入口 | 检查 `.codex`、`.claude`、`.agents`、MCP、plugins 和工具仓库路径 |
| 2. 确认长期目录 | 让你确认 `skills`、`mcp`、`user_plugin`、`agent-config`，以及 `agent-skills` 是否只保留兼容 bridge |
| 3. 迁移或接引 | 把真实内容放到长期目录，或为旧入口创建对应系统的 bridge |
| 4. 验证路径 | 确认 Codex、Claude 或其他工具仍能从自己熟悉的入口找到内容 |
| 5. 写入清单 | 更新 `<confirmed-ai-home-root>/ai-home-inventory.md` |

为什么不自动静默处理？因为这一步可能涉及移动目录、备份旧内容、修改工具入口、创建平台接引（Windows junction 或 macOS/Linux symlink）。`ai-home-migration` 会引导并执行这些操作，但应该在你明确触发并确认后进行。

如果通过 Codex marketplace 或类似安装器安装插件，也要先确认最终长期位置。即使安装器先把仓库下载到 Windows 的 `C:\Users\<user>`、`.codex` 缓存目录或临时 marketplace 路径，真实仓库也应该迁到统一的 `user_plugin/<tool-name>`，旧入口只作为 bridge 保留。

如果你只想接引 Claude，可以这样说：

```text
请用 ai-home-migration 只检查 Claude 的 skills、commands、agents 和配置入口，告诉我哪些应该接到统一 AI home，哪些应该保留为本机私有状态。
```

### 跨平台接引规则

`ai-home-migration` 对用户统一称为“接引 / bridge”：真实内容放在统一 AI home，旧工具入口继续可用。不同系统底层实现不同：

| 系统 | 默认接引方式 | 典型用途 |
| --- | --- | --- |
| Windows | directory junction | `.codex\skills`、`.claude\skills`、插件旧入口 |
| macOS | symbolic link | `~/.codex/skills`、`~/.claude/skills`、`~/.agents/skills` |
| Linux | symbolic link | `~/.codex/skills`、`~/.claude/skills`、`~/.agents/skills` |

它不会把 sessions、history、shell snapshots、local settings 或项目自己的 `.claude/` 内容一股脑自动接引；这些属于私有状态或项目状态，需要单独确认。

## 🧭 工作方式

```text
识别操作系统
   ↓
给出默认长期目录建议
   ↓
让你确认或修改路径
   ↓
盘点 Codex / Claude / agent / MCP / plugin 相关位置
   ↓
选择直接迁移、先复制再改入口，或备份后建立 bridge
   ↓
刷新 AI home 根目录总清单
```

这个 skill 会把“可公开分享的策略文件”和“某台机器自己的运行状态”分开。仓库保持通用，本机路径和清单留在本机。

## 🧰 核心能力

### 📍 目录策略统一

给用户自装的 AI agent 内容建立长期归属，而不是每次安装都临时判断。

### 🧪 首次配置引导

迁移前先确认长期路径，同时提供按系统匹配的默认建议。

### 🛡️ 更稳妥的迁移方式

根据文件锁和风险，在 `Direct move + bridge`、`Copy first + repoint`、`Backup + bridge` 之间选择。

### 🧭 跨平台接引

把真实内容迁到长期目录，同时用 Windows junction 或 macOS/Linux symlink 保持旧入口可用。

### 🔁 后续持续维护

复用已确认路径，刷新本地清单，让未来安装保持一致。

## 📚 本地清单

规范的本地总清单位于：

```text
<confirmed-ai-home-root>/ai-home-inventory.md
```

例如：

```text
D:\2_file\codex-home\ai-home-inventory.md
```

它是中文为主、中英对照的速查表，包含：

- 受管条目总数
- 各分类数量
- 大类下的工作用途小类
- 同源 GitHub 项目或插件包的 `源头 / Source` 标注；无法确认来源时标为 `来源待确认 / Source pending`
- 中文用途优先，英文用途辅助
- 每个条目的路径
- 适用时提供调用示例
- 被排除的支持目录，例如 `.system`

“带 skill 的插件”只在一种情况下单独列出：插件仓库本身放在 `user_plugin`，同时还需要在 `skills` 里暴露可调用入口。像 `last30days` 这种整套功能都在 plugin 内部自洽的插件，只列在 `user_plugin`，不额外放进“带 skill 的插件”分组。

历史路径 `references/installed-skills-cheatsheet.md` 只作为兼容指针保留。

## 🧩 它解决什么问题

- “我的 Codex 和 Claude skills 到处都是。”
- “我想让同一套迁移规则同时支持 Codex、Claude 和 OpenAI 兼容 agent。”
- “我想把 AI agent 内容迁到别的盘，但又怕旧路径失效。”
- “某个插件还依赖原来的启动目录。”
- “Windows 提示仓库、`.git` 或原生文件被占用。”
- “我不想每装一个新 skill 都重新想放哪。”

## 🏗️ 迁移前后

| 迁移前 | 迁移后 |
| --- | --- |
| 自装 skills 散落在 `.codex`、`.claude`、`.agents` 和临时目录里 | 有一套确认过的长期目录结构 |
| 插件仓库藏在各种工具目录里 | 插件仓库进入 `user_plugin` |
| MCP 内容单独管理 | MCP 内容纳入同一套放置策略 |
| 旧入口路径容易断 | bridge 保持旧入口可用 |
| 没有可复用清单 | 根目录中英对照 `ai-home-inventory.md` |

## 🧭 默认目录建议

Windows 默认建议：

```text
C:\Users\<user>\ai_tools\skills
C:\Users\<user>\ai_tools\agent-skills  # compatibility bridge to skills
C:\Users\<user>\ai_tools\mcp
C:\Users\<user>\ai_tools\user_plugin
C:\Users\<user>\ai_tools\agent-config
```

macOS / Linux 默认建议：

```text
~/ai_tools/skills
~/ai_tools/agent-skills  # compatibility symlink to skills
~/ai_tools/mcp
~/ai_tools/user_plugin
~/ai_tools/agent-config
```

这些只是建议值。安装副本会把最终确认的路径写入 `references/placement-rules-local.md`。

## 💬 调用示例

```text
请用 ai-home-migration 把这个 skill 安装到我的长期 skills 目录，并保留需要兼容的旧路径。
```

```text
请用 ai-home-migration 统一整理我的 Codex、Claude、MCP 和 agent 工具环境。
```

```text
请用 ai-home-migration 把这个插件迁到 user_plugin，并用 bridge 保留旧入口。
```

## 📦 公共文件与本地文件

可公开分享的仓库文件：

- `SKILL.md`
- `agents/openai.yaml`
- `agents/claude.md`
- `agents/generic-openai.md`
- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/agent-compatibility.md`
- `references/cross-platform-bridge-rules.md`
- `references/windows-junction-notes.md`

本机生成或维护的运行文件：

- `references/placement-rules-local.md`
- `<confirmed-ai-home-root>/ai-home-inventory.md`
- `references/installed-skills-cheatsheet.md`，只作为兼容指针

本地运行文件不应该作为公共默认模板提交，因为它们包含某台机器的实际路径和安装状态。

## 🗂️ 仓库结构

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

## 🔎 可发现性说明

这个仓库刻意保留 `Codex`、`Claude`、`OpenAI`、`AI agent`、`skills`、`agent-skills`、`MCP`、`plugin`、`migration`、`Windows`、`junction` 等关键词，因为它们正是用户在整理本地 agent 环境时最可能搜索的问题词。

## 📝 说明

- 本仓库保存的是可分享的策略层。
- 每台机器自己的路径确认结果，应当在安装后本地生成。
- 如果你把这个 skill 分享给别人，分享仓库文件即可，首次运行时让对方确认自己的长期目录。
