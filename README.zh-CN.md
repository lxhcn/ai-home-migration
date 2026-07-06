# codex-home-migration

[English](README.md) | 简体中文

让 Codex 的自装内容从“越装越乱”变成“长期可维护”。

`codex-home-migration` 是一个 Codex skill，用来统一管理用户自己的 `skills`、`agent-skills`、`mcp` 和 `user_plugin` 内容，把它们放到长期目录中，在需要时保留旧入口路径的 junction，并把一次性的迁移经验沉淀成可复用的安装规则。

## 快速看点

- 首次运行时确认 `skills`、`agent-skills`、`mcp`、`user_plugin` 的长期路径
- 按 Windows、macOS、Linux 自动给出默认建议目录
- 为锁文件仓库、插件目录、旧入口路径提供更稳妥的迁移方式
- 专门考虑 Windows 下 junction、`.git` 占用和原生插件文件锁问题
- 明确区分“可分享的仓库文件”和“本机私有运行文件”
- 后续所有自装内容都能继续沿用同一套目录规则

## 安装方式

把这个仓库安装或复制为名为 `codex-home-migration` 的 Codex skill，并保持仓库结构不变：

```text
codex-home-migration/
  SKILL.md
  agents/openai.yaml
  references/
```

首次使用时，skill 应该先让你确认 `skills`、`agent-skills`、`mcp`、`user_plugin` 四类内容的长期路径。确认后的本机运行文件应写入你自己的安装副本，而不是写进公开仓库默认文件。

## 为什么这个项目值得关注

很多 Codex 环境最后都会变成类似的问题：

- 自装 skills 分散在多个目录
- 插件仓库藏在各种工具目录里
- MCP 内容和其他资源分开管理
- 旧入口路径还不能直接删
- Windows 一旦锁文件，迁移就容易出问题

大多数人会手动解决一次，但下次安装时又重新重复同样的混乱决策。

`codex-home-migration` 的价值，就是把这种一次性的整理经验，变成一套长期可复用的规则。

## 适合谁用

- 经常从 GitHub 安装第三方 Codex skill 的用户
- 想把 Codex 内容迁移到别的磁盘的用户
- 主要在 Windows 上维护 Codex 环境的用户
- 希望以后每次安装都按统一规则落盘的用户
- 长期维护 `skills`、`agent-skills`、MCP 和插件仓库的重度使用者

## 迁移前后对比

迁移前：

- 自装 skills 在 `.codex`
- agent 链接在 `.agents`
- 插件仓库散落在隐藏目录
- MCP 内容在其他地方单独维护
- 以后装新东西没有统一规则

迁移后：

- 有一套已经确认过的长期目录结构
- 四类内容按分类规则统一放置
- 每条路径都能按风险选最稳妥的迁移方式
- 必要时保留旧入口路径
- 以后新装内容自动沿用同一套规则

## 核心能力

### 1. 路径策略统一

为用户自装内容建立一套长期有效的目录归属规则，而不是每次安装都临时判断。

### 2. 首次配置引导

先让用户确认长期路径，再开始迁移或安装，同时保留按系统提供的默认建议。

### 3. 迁移策略选择

根据文件锁和风险情况，在直接移动、先复制后改联接、备份后切换之间做出合适选择。

### 4. 旧入口兼容

当工具仍依赖旧入口路径时，通过 junction 保持兼容，减少迁移带来的断裂。

### 5. 后续持续维护

复用已经确认过的本地路径，在路径变更时自动触发迁移，并让未来安装保持一致。

## 它具体解决哪些常见问题

- “我的 Codex skills 到处都是，不知道该怎么整理。”
- “我想把安装内容迁到别的盘，但又怕旧路径失效。”
- “某个插件还依赖原来的启动目录。”
- “Windows 一直提示文件被占用或者删不掉。”
- “我不想每装一个新 skill 都重新想一遍该放哪里。”
- “我希望以后这套目录规则也能分享给别人使用。”

## 工作流程

1. 识别当前操作系统。
2. 提供默认建议目录。
3. 让用户确认四类长期路径。
4. 盘点当前目录布局。
5. 为每条路径选择最稳妥的迁移策略。
6. 在需要时重建 junction。
7. 保存本地运行状态，供后续复用。

## 首次使用行为

首次安装或首次使用时，skill 应该按下面顺序工作：

1. 判断当前操作系统。
2. 提供按系统匹配的默认目录建议。
3. 明确告诉用户这些默认值可以修改。
4. 让用户确认 `skills`、`agent-skills`、`mcp`、`user_plugin` 的长期路径。
5. 如果用户没有改动，就直接采用默认值继续执行。
6. 将确认后的结果写入本地路径记录文件，供后续复用。

之后再次使用时，如果已经存在本地路径记录，就应该优先使用那份记录，而不是重新退回通用默认值。

## 默认目录规则

Windows 默认建议：

- `C:\Users\<user>\ai_tools\skills`
- `C:\Users\<user>\ai_tools\agent-skills`
- `C:\Users\<user>\ai_tools\mcp`
- `C:\Users\<user>\ai_tools\user_plugin`

macOS / Linux 默认建议：

- `~/ai_tools/skills`
- `~/ai_tools/agent-skills`
- `~/ai_tools/mcp`
- `~/ai_tools/user_plugin`

## 迁移模式

这个 skill 根据风险程度，采用三种迁移模式：

- `Direct move + junction`
  适用于普通目录、未被占用、可直接移动的情况。

- `Copy first + repoint`
  适用于活跃仓库、插件目录、可能被 `.git` 或运行进程占用的情况。

- `Backup + junction`
  适用于已经部分迁移、源目录仍有残留、直接删除存在风险的情况。

Windows 下的具体安全注意事项见 [references/windows-junction-notes.md](references/windows-junction-notes.md)。

## 典型使用场景

- 把分散在多个目录里的自装 skills 统一迁移到长期目录
- 将第三方插件仓库迁移到 `user_plugin`，同时保留原有启动入口
- 在准备分享 Codex 环境前，先统一 `agent-skills` 和 MCP 目录结构
- 把用户自装内容迁移到新的磁盘或根目录，同时尽量不影响旧工具入口
- 把一次成功的本地迁移经验沉淀成未来可复用的统一安装规则

## 快速示例

```text
请用 codex-home-migration 把这个 skill 安装到我的长期 skills 目录，并保留需要兼容的旧路径。
```

```text
请用 codex-home-migration 统一整理我的 Codex 环境，并告诉我哪些该迁移、哪些该保留、哪些该做 junction。
```

## 推荐调用方式

```text
请用 codex-home-migration 安装这个 skill，并按统一目录规则处理。
```

```text
请用 codex-home-migration 检查我现在的 skills、agent-skills、mcp、user_plugin 应该迁移到哪里。
```

```text
请用 codex-home-migration 把这个插件装到 user_plugin，并保留旧入口联接。
```

## 仓库文件与本地文件的区别

这个仓库故意分成两层。

可公开分享的通用文件：

- `SKILL.md`
- `agents/openai.yaml`
- `references/placement-rules.md`
- `references/placement-rules-default.md`
- `references/windows-junction-notes.md`

安装后在本机生成或维护的运行文件：

- `references/placement-rules-local.md`
- `references/installed-skills-cheatsheet.md`

后面这两个文件不应该作为公共默认模板提交出去，因为它们会包含某台机器的实际路径和本机安装状态。

## 仓库结构

```text
codex-home-migration/
  SKILL.md
  README.md
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
  references/
    placement-rules.md
    placement-rules-default.md
    windows-junction-notes.md
```

## 包含文件

- `SKILL.md`
  核心 skill 说明文件。

- `agents/openai.yaml`
  Codex 界面展示元数据。

- `references/placement-rules.md`
  说明默认规则与本地运行文件如何配合。

- `references/placement-rules-default.md`
  可公开分享的默认路径与首次运行规则。

- `references/windows-junction-notes.md`
  Windows 下的迁移与联接安全说明。

- `README.md`
  英文说明首页。

- `CHANGELOG.md`
  对外发布时的版本变更记录。

- `GITHUB_ABOUT.md`
  可直接用于 GitHub 仓库设置的描述文案和 topics 建议。

- `LICENSE`
  仓库许可证。

## 可发现性说明

这个仓库在标题、描述和 README 中故意强调了 `Codex`、`skills`、`agent-skills`、`MCP`、`plugin`、`migration`、`Windows`、`junction` 等关键词，因为这些正是目标用户最可能搜索的问题词。

## 说明

- 这个仓库保存的是“可分享的策略层”。
- 每台机器自己的路径确认结果，应当在安装后本地生成，而不是作为默认值发布出去。
- 如果你要把这个 skill 分享给别人，分享仓库文件即可，首次运行时让对方自己确认长期目录。
