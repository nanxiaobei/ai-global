# AI Global

[English](README.md) · 简体中文 · [繁體中文](README_TW.md) · [日本語](README_JP.md) · [한국어](README_KR.md)

---

**AI 编程工具统一配置管理器。**

编辑一个文件，同步到所有 AI 工具。

同时支持**系统模式**和**项目模式**

## 安装

### curl

```bash
curl -fsSL https://raw.githubusercontent.com/nanxiaobei/ai-global/main/install.sh | bash
```

### npm

```bash
npm install -g ai-global
# 或
pnpm add -g ai-global
# 或
yarn global add ai-global
# 或
bun add -g ai-global
```

## 使用方法

### 自动模式检测

AI Global 会自动检测你的上下文：

- **系统模式**：当从 `~` 目录运行时，为系统范围统一配置
- **项目模式**：当从任何项目目录（非 `~`）运行时，为项目特定统一配置

### 首次运行

```bash
ai-global
```

这将会：

1. 检测当前目录（系统或项目）
2. 扫描已安装的 AI 工具
3. 备份原始配置到 `.ai-global/backups/`
4. 合并检测到的工具的 AGENTS.md/skills/agents/rules/commands
5. 创建从各工具配置到共享目录的软链

注意：AI Global 只会处理已经存在的工具目录，不会帮你创建 `.github`、`.kiro`、`.cursor` 这类目录。

### 命令列表

| 命令                        | 说明                         | 上下文感知 |
| --------------------------- | ---------------------------- | ---------- |
| `ai-global`                 | 扫描、合并、更新软链（默认） | 是         |
| `ai-global status`          | 显示软链状态                 | 是         |
| `ai-global list`            | 列出支持的工具               | 是         |
| `ai-global backups`         | 列出可用的备份               | 是         |
| `ai-global unlink <key>`    | 恢复某个工具的原始配置       | 是         |
| `ai-global unlink all`      | 恢复所有工具                 | 是         |
| `ai-global add <user/repo>` | 添加技能                     | 是         |
| `ai-global upgrade`         | 升级到最新版本               |            |
| `ai-global uninstall`       | 彻底卸载                     |            |
| `ai-global version`         | 显示版本号                   |            |
| `ai-global help`            | 显示帮助                     |            |

**上下文感知**：命令行为取决于当前目录（系统 vs 项目）

### 添加技能

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

技能将被下载并添加到你的 `.ai-global/skills/` 目录。

## 工作原理

### 系统模式结构

```
~/.ai-global/
├── AGENTS.md        <- 共享 AGENTS.md（编辑这个）
├── skills/          <- 共享技能（从所有工具合并）
├── agents/          <- 共享代理
├── rules/           <- 共享规则
├── commands/        <- 共享斜杠命令
└── backups/         <- 原始配置（备份）

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (软链)
├── skills/   -> ~/.ai-global/skills/          (软链)
└── commands/ -> ~/.ai-global/commands/        (软链)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (软链)
└── skills/   -> ~/.ai-global/skills/          (软链)

... 以及更多工具
```

### 项目模式结构

```
my-project/
├── .ai-global/          <- 项目特定配置
│   ├── AGENTS.md        <- 项目 AGENTS.md
│   ├── skills/          <- 项目技能
│   ├── agents/          <- 项目代理
│   ├── rules/           <- 项目规则
│   ├── commands/        <- 项目命令
│   └── backups/         <- 项目备份
└── .cursor/             <- AI 工具配置
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (软链)
    └── skills/   -> ../.ai-global/skills/     (软链)
```

### 模式行为

- **系统模式**：管理整个系统的 AI 配置
- **项目模式**：仅管理特定项目的 AI 配置
- **自动检测**：无需命令即可切换模式
- **上下文感知**：命令将显示它们正在操作的上下文

### 合并行为

运行 `ai-global` 时，会按文件名合并所有工具的内容：

- Cursor 有 skills: `react/`, `typescript/`
- Claude 有 skills: `typescript/`, `python/`
- 合并结果 `.ai-global/skills/`: `react/`, `typescript/`, `python/`

**最后找到的优先**（后找到的会覆盖同名文件夹）。

## 支持的工具

| 工具           | Key           | AGENTS.md | Rules | Commands | Skills | Agents |
| -------------- | ------------- | :-------: | :---: | :------: | :----: | :----: |
| Claude Code    | `claude`      |     ✓     |       |    ✓     |   ✓    |   ✓    |
| OpenAI Codex   | `codex`       |     ✓     |   ✓   |          |   ✓    |   ✓    |
| Cursor         | `cursor`      |     ✓     |   ✓   |    ✓     |   ✓    |   ✓    |
| Factory Droid  | `droid`       |     ✓     |   ✓   |    ✓     |   ✓    |   ✓    |
| Amp            | `amp`         |     ✓     |   ✓   |    ✓     |   ✓    |        |
| Antigravity    | `antigravity` |     ✓     |       |          |   ✓    |        |
| Gemini CLI     | `gemini`      |     ✓     |       |          |   ✓    |        |
| Kiro CLI       | `kiro`        |     ✓     |   ✓   |          |   ✓    |   ✓    |
| OpenCode       | `opencode`    |     ✓     |       |    ✓     |   ✓    |   ✓    |
| Qoder          | `qoder`       |     ✓     |   ✓   |    ✓     |   ✓    |   ✓    |
| Qodo           | `qodo`        |     ✓     |       |          |        |   ✓    |
| GitHub Copilot | `copilot`     |     ✓     |       |          |   ✓    |   ✓    |
| Continue       | `continue`    |     ✓     |   ✓   |          |        |        |
| Windsurf       | `windsurf`    |     ✓     |   ✓   |          |   ✓    |        |
| Roo Code       | `roo`         |     ✓     |   ✓   |    ✓     |   ✓    |        |
| Cline          | `cline`       |     ✓     |   ✓   |          |   ✓    |        |
| Blackbox AI    | `blackbox`    |           |       |          |   ✓    |        |
| Goose AI       | `goose`       |     ✓     |       |          |   ✓    |        |
| Augment        | `augment`     |     ✓     |   ✓   |    ✓     |        |   ✓    |
| Clawdbot Code  | `clawdbot`    |     ✓     |       |          |   ✓    |   ✓    |
| Command Code   | `commandcode` |     ✓     |       |    ✓     |   ✓    |        |
| Kilo Code      | `kilocode`    |     ✓     |   ✓   |    ✓     |   ✓    |        |
| Neovate        | `neovate`     |     ✓     |       |    ✓     |   ✓    |   ✓    |
| OpenHands      | `openhands`   |     ✓     |       |          |   ✓    |        |
| TRAE           | `trae`        |     ✓     |   ✓   |          |   ✓    |        |
| Zencoder       | `zencoder`    |     ✓     |   ✓   |          |   ✓    |        |
| GitHub         | `github`      |           |       |          |   ✓    |   ✓    |

## 卸载

```bash
ai-global uninstall
```

这将会：

1. 恢复所有工具的原始配置
2. 删除 `~/.ai-global` 目录
3. 移除 `ai-global` 命令

如果通过 npm 安装：

```bash
ai-global uninstall

npm uninstall -g ai-global
```

## 许可证

MIT
