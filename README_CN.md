# AI Global

[English](README.md)

AI 编程助手统一配置管理器。编辑一个文件，同步到所有 AI 工具。

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

### 首次运行

```bash
ai-global
```

这将会：

1. 扫描系统中已安装的 AI 工具
2. 备份原始配置到 `~/.ai-global/backups/`
3. 合并所有工具的 AGENTS.md/skills/agents/rules/commands
4. 创建从各工具配置到共享目录的软链

### 命令列表

| 命令                          | 说明                         |
| ----------------------------- | ---------------------------- |
| `ai-global`                   | 扫描、合并、更新软链（默认） |
| `ai-global status`            | 显示软链状态                 |
| `ai-global list`              | 列出支持的工具               |
| `ai-global backups`           | 列出可用的备份               |
| `ai-global unlink <key>`      | 恢复某个工具的原始配置       |
| `ai-global unlink all`        | 恢复所有工具                 |
| `ai-global skill <user/repo>` | 添加技能                     |
| `ai-global upgrade`           | 升级到最新版本               |
| `ai-global uninstall`         | 彻底卸载                     |
| `ai-global version`           | 显示版本号                   |
| `ai-global help`              | 显示帮助                     |

### 添加 skills

```bash
ai-global skill user/repo
ai-global skill https://github.com/user/repo
```

## 工作原理

```
~/.ai-global/
├── AGENTS.md        <- 共享指令（编辑这个）
├── skills/          <- 共享技能（从所有工具合并）
├── agents/          <- 共享代理
├── rules/           <- 共享规则
├── commands/        <- 共享斜杠命令
└── backups/         <- 原始配置（备份）

各 AI 工具的配置目录中存放软链：

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (软链)
├── skills/   -> ~/.ai-global/skills/          (软链)
└── commands/ -> ~/.ai-global/commands/        (软链)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (软链)
└── skills/   -> ~/.ai-global/skills/          (软链)

... 以及更多工具
```

## 合并行为

运行 `ai-global` 时，会按文件名合并所有工具的内容：

- Cursor 有 skills: `react/`, `typescript/`
- Claude 有 skills: `typescript/`, `python/`
- 合并结果 `~/.ai-global/skills/`: `react/`, `typescript/`, `python/`

先发现的文件优先（按文件名去重）。

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
