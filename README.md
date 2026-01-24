# AI Global

[简体中文](README_CN.md) | [繁體中文](README_TW.md) | [日本語](README_JP.md) | [한국어](README_KR.md)

Unified configuration manager for AI coding assistants. Edit one file, sync to all your AI tools.

## Installation

### curl

```bash
curl -fsSL https://raw.githubusercontent.com/nanxiaobei/ai-global/main/install.sh | bash
```

### npm

```bash
npm install -g ai-global
# or
pnpm add -g ai-global
# or
yarn global add ai-global
# or
bun add -g ai-global
```

## Usage

### First run

```bash
ai-global
```

This will:

1. Scan your system for installed AI tools
2. Backup original configs to `~/.ai-global/backups/`
3. Merge AGENTS.md/skills/agents/rules/commands from all tools
4. Create symlinks from each tool's config to shared directories

### Commands

| Command                       | Description                            |
| ----------------------------- | -------------------------------------- |
| `ai-global`                   | Scan, merge, update symlinks (default) |
| `ai-global status`            | Show symlink status                    |
| `ai-global list`              | List supported tools                   |
| `ai-global backups`           | List available backups                 |
| `ai-global unlink <key>`      | Restore a tool's original config       |
| `ai-global unlink all`        | Restore all tools                      |
| `ai-global skill <user/repo>` | Add skills                             |
| `ai-global upgrade`           | Upgrade to latest version              |
| `ai-global uninstall`         | Completely remove ai-global            |
| `ai-global version`           | Show version                           |
| `ai-global help`              | Show help                              |

### Add skills

```bash
ai-global skill user/repo
ai-global skill https://github.com/user/repo
```

## How it works

```
~/.ai-global/
├── AGENTS.md        <- Shared AGENTS.md (edit this)
├── skills/          <- Shared skills (merged from all tools)
├── agents/          <- Shared agents
├── rules/           <- Shared rules
├── commands/        <- Shared slash commands
└── backups/         <- Original configs (backups)

Each AI tool's config directory contains symlinks:

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (symlink)
├── skills/   -> ~/.ai-global/skills/          (symlink)
└── commands/ -> ~/.ai-global/commands/        (symlink)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (symlink)
└── skills/   -> ~/.ai-global/skills/          (symlink)

... and more tools
```

## Merge behavior

When you run `ai-global`, it merges items from all tools by filename:

- Cursor has skills: `react/`, `typescript/`
- Claude has skills: `typescript/`, `python/`
- Result in `~/.ai-global/skills/`: `react/`, `typescript/`, `python/`

The first file found wins (dedup by filename).

## Supported Tools

| Tool           | Key           | AGENTS.md | Rules | Commands | Skills | Agents |
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

## Uninstall

```bash
ai-global uninstall
```

This will:

1. Unlink all tools to original configuration
2. Remove `~/.ai-global` directory
3. Remove `ai-global` command

If installed via npm:

```bash
ai-global uninstall

npm uninstall -g ai-global
```

## License

MIT
