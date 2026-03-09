# AI Global

English · [简体中文](README_CN.md) · [繁體中文](README_TW.md) · [日本語](README_JP.md)· [한국어](README_KR.md)

---

**Unified Configuration Manager for AI Coding Tools.**

Edit one file, sync to all your AI tools.

Works both **System Mode** & **Project Mode**

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

### Automatic Mode Detection

AI Global automatically detects your context:

- **System Mode**: When run from `~` directory, unified configs for system-wide
- **Project Mode**: When run from any project directory (not `~`), unified configs for project-specific

### First run

```bash
ai-global
```

This will:

1. Detect current directory (system or project)
2. Scan for installed AI tools
3. Backup original configs to `.ai-global/backups/`
4. Merge AGENTS.md/skills/agents/rules/commands from detected tools
5. Create symlinks from each tool's config to shared directories

## Commands

| Command                     | Description                            | Context-aware |
| --------------------------- | -------------------------------------- | ------------- |
| `ai-global`                 | Scan, merge, update symlinks (default) | Yes           |
| `ai-global status`          | Show symlinks status                   | Yes           |
| `ai-global list`            | List all supported AI tools            | Yes           |
| `ai-global backups`         | List available backups                 | Yes           |
| `ai-global unlink <key>`    | Restore a tool's original config       | Yes           |
| `ai-global unlink all`      | Restore all tools                      | Yes           |
| `ai-global add <user/repo>` | Add skills from GitHub repository      | Yes           |
| `ai-global upgrade`         | Upgrade to latest version              |               |
| `ai-global uninstall`       | Completely remove ai-global            |               |
| `ai-global version`         | Show version                           |               |
| `ai-global help`            | Show help                              |               |

**Context-aware**: Command behavior depends on current directory (system vs project)

### Add skills

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

Skills will be downloaded and added to your `.ai-global/skills/` directory.

## How it works

### System Mode Structure

```
~/.ai-global/
├── AGENTS.md        <- Shared AGENTS.md (edit this)
├── skills/          <- Shared skills (merged from all tools)
├── agents/          <- Shared agents
├── rules/           <- Shared rules
├── commands/        <- Shared slash commands
└── backups/         <- Original configs (backups)

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (symlink)
├── skills/   -> ~/.ai-global/skills/          (symlink)
└── commands/ -> ~/.ai-global/commands/        (symlink)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (symlink)
└── skills/   -> ~/.ai-global/skills/          (symlink)

... and more tools
```

### Project Mode Structure

```
my-project/
├── .ai-global/          <- Project-specific configs
│   ├── AGENTS.md        <- Project AGENTS.md
│   ├── skills/          <- Project skills
│   ├── agents/          <- Project agents
│   ├── rules/           <- Project rules
│   ├── commands/        <- Project commands
│   └── backups/         <- Project backups
└── .cursor/             <- AI tool config
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (symlink)
    └── skills/   -> ../.ai-global/skills/     (symlink)
```

### Mode Behavior

- **System Mode**: Manages AI configs across your entire system
- **Project Mode**: Manages AI configs for a specific project only
- **Automatic Detection**: No commands needed to switch between modes
- **Context-Aware**: Commands will show which context they're operating in

### Merge behavior

When you run `ai-global`, it merges items from all tools by filename:

- Cursor has skills: `react/`, `typescript/`
- Claude has skills: `typescript/`, `python/`
- Result in `.ai-global/skills/`: `react/`, `typescript/`, `python/`

**Last file wins** (later tools overwrite earlier tools with same filename).

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
