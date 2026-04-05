# AI Global

[English](README.md) · 简体中文 · [繁體中文](README_TW.md) · [日本語](README_JP.md) · [한국어](README_KR.md)

---

**AI 编程工具统一配置管理器。**

编辑一个文件，同步到所有 AI 工具。

同时支持**系统模式**和**项目模式**。

## 支持的工具

| 工具                                                  | Key           | AGENTS.md | Rules | Commands | Skills |
| ----------------------------------------------------- | ------------- | :-------: | :---: | :------: | :----: |
| [Claude Code](https://claude.com/product/claude-code) | `claude`      |     ✓     |       |    ✓     |   ✓    |
| [OpenAI Codex](https://openai.com/codex/)             | `codex`       |     ✓     |   ✓   |          |   ✓    |
| [Cursor](https://cursor.com/)                         | `cursor`      |     ✓     |   ✓   |    ✓     |   ✓    |
| [Factory Droid](https://factory.ai/)                  | `droid`       |     ✓     |   ✓   |    ✓     |   ✓    |
| [Amp](https://ampcode.com/)                           | `amp`         |     ✓     |   ✓   |    ✓     |   ✓    |
| [Antigravity](https://antigravity.google/)            | `antigravity` |     ✓     |       |          |   ✓    |
| [Gemini CLI](https://geminicli.com/)                  | `gemini`      |     ✓     |       |          |   ✓    |
| [Kiro](https://kiro.dev/)                             | `kiro`        |     ✓     |   ✓   |          |   ✓    |
| [OpenCode](https://opencode.ai/)                      | `opencode`    |     ✓     |       |    ✓     |   ✓    |
| [Qoder](https://qoder.com/)                           | `qoder`       |     ✓     |   ✓   |    ✓     |   ✓    |
| [Qodo](https://www.qodo.ai/)                          | `qodo`        |     ✓     |       |          |        |
| [GitHub Copilot](https://github.com/features/copilot) | `copilot`     |     ✓     |       |          |   ✓    |
| [Continue](https://www.continue.dev/)                 | `continue`    |     ✓     |   ✓   |          |        |
| [Windsurf](https://windsurf.com/)                     | `windsurf`    |     ✓     |   ✓   |          |   ✓    |
| [Roo Code](https://roocode.com/)                      | `roo`         |     ✓     |   ✓   |    ✓     |   ✓    |
| [Cline](https://cline.bot/)                           | `cline`       |     ✓     |   ✓   |          |   ✓    |
| [Blackbox AI](https://www.blackbox.ai/)               | `blackbox`    |           |       |          |   ✓    |
| [Goose AI](https://goose.ai/)                         | `goose`       |     ✓     |       |          |   ✓    |
| [Augment](https://www.augmentcode.com/)               | `augment`     |     ✓     |   ✓   |    ✓     |        |
| [OpenClaw](https://openclaw.ai/)                      | `openclaw`    |     ✓     |       |          |   ✓    |
| [Command Code](https://commandcode.ai/)               | `commandcode` |     ✓     |       |    ✓     |   ✓    |
| [Kilo Code](https://kilo.ai/)                         | `kilocode`    |     ✓     |   ✓   |    ✓     |   ✓    |
| [Neovate](https://neovateai.dev/)                     | `neovate`     |     ✓     |       |    ✓     |   ✓    |
| [OpenHands](https://openhands.dev/)                   | `openhands`   |     ✓     |       |          |   ✓    |
| [TRAE](https://www.trae.ai/)                          | `trae`        |     ✓     |   ✓   |          |   ✓    |
| [Zencoder](https://zencoder.ai/)                      | `zencoder`    |     ✓     |   ✓   |          |   ✓    |

## 安装

使用 `curl` 或 `npm` 安装：

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

运行：

```bash
ai-global
```

这将会：

1. 检测当前目录上下文（系统或项目）
2. 扫描已安装的 AI 工具
3. 备份原始配置到 `.ai-global/backups`
4. 将检测到的工具的 `AGENTS.md` `skills` `rules` `commands` 合并到 `.ai-global` 共享配置
5. 创建从各工具到 `.ai-global` 共享配置的软链

### 上下文

- **系统模式**：当从 `~` 目录运行时，为系统范围统一配置
- **项目模式**：当从任何项目目录（非 `~`）运行时，为项目特定统一配置

## 命令

```bash
ai-global                   # 更新软链（默认）
ai-global status            # 显示软链状态
ai-global list              # 列出支持的工具
ai-global backups           # 列出可用的备份
ai-global unlink <key>      # 恢复某个工具的原始配置
ai-global unlink all        # 恢复所有工具
ai-global add <user/repo>   # 从 GitHub 添加 skills
ai-global upgrade           # 升级到最新版本
ai-global uninstall         # 彻底移除 ai-global
ai-global version           # 显示版本
ai-global help              # 显示帮助
```

**上下文感知**：命令行为取决于当前目录（系统或项目）

### 添加 Skills

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

Skills 将被添加到你的 `.ai-global/skills`，并自动共享到每个工具（因为软链）。

## 工作原理

### 系统模式结构

```
~/.ai-global/
├── AGENTS.md        <- 系统共享 AGENTS.md
├── skills/          <- 系统共享 skills
├── rules/           <- 系统共享 rules
├── commands/        <- 系统共享 commands
└── backups/         <- 原始工具配置的备份

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
├── .ai-global/
│   ├── AGENTS.md        <- 项目共享 AGENTS.md
│   ├── skills/          <- 项目共享 skills
│   ├── rules/           <- 项目共享 rules
│   ├── commands/        <- 项目共享 commands
│   └── backups/         <- 原始工具配置的备份
└── .cursor/
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (软链)
    └── skills/   -> ../.ai-global/skills/     (软链)

    ... 以及更多工具
```

### 模式行为

- **系统模式**：管理系统 AI 工具配置
- **项目模式**：管理项目 AI 工具配置
- **自动检测**：无需命令即可切换
- **上下文感知**：命令将显示它们正在操作的上下文

### 合并行为

当你运行 `ai-global` 时，它会按文件名合并所有工具的项目：

- Cursor 有 skills: `react/`, `typescript/`
- Claude 有 skills: `typescript/`, `python/`
- 结果在 `.ai-global/skills`: `react/`, `typescript/`, `python/`

**最后文件获胜**（后面的工具会覆盖与前面工具同名的文件）。

## 卸载

```bash
ai-global uninstall
```

这将会：

1. 取消所有工具的软链，恢复到它们的原始配置
2. 删除所有 `.ai-global` 目录
3. 移除 `ai-global` 命令

## 许可证

MIT
