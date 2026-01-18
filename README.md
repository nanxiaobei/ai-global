# AI Config

[中文文档](README_CN.md)

Unified configuration manager for AI coding assistants. Edit one file, sync to all your AI tools.

## Supported Tools

| Tool              | Instructions | Skills | Agents | Rules | Commands | Prompts |
| ----------------- | :----------: | :----: | :----: | :---: | :------: | :-----: |
| Claude Code       |      ✓       |   ✓    |        |       |    ✓     |         |
| Cursor            |      ✓       |   ✓    |        |       |          |    ✓    |
| GitHub Copilot    |      ✓       |        |        |       |          |         |
| Factory Droid     |      ✓       |        |        |       |          |         |
| Gemini CLI        |      ✓       |   ✓    |        |       |    ✓     |         |
| Windsurf          |      ✓       |   ✓    |   ✓    |   ✓   |          |         |
| Kiro              |      ✓       |        |   ✓    |       |          |         |
| Qodo              |      ✓       |        |   ✓    |       |          |         |
| Antigravity       |      ✓       |   ✓    |        |       |    ✓     |         |
| Continue          |      ✓       |        |        |   ✓   |          |    ✓    |
| Cline             |      ✓       |        |        |   ✓   |          |    ✓    |
| Roo Code          |      ✓       |        |        |   ✓   |          |         |
| Sourcegraph Cody  |      ✓       |        |        |       |    ✓     |         |
| CodeGPT           |      ✓       |        |        |       |          |    ✓    |
| GPT Engineer      |      ✓       |        |        |       |          |    ✓    |
| Smol Developer    |      ✓       |        |        |       |          |    ✓    |
| Amp               |      ✓       |        |        |       |          |         |
| Trae              |      ✓       |        |        |       |          |         |
| OpenCode          |      ✓       |        |        |       |          |         |
| OpenAI Codex      |      ✓       |        |        |       |          |         |
| Aider             |      ✓       |        |        |       |          |         |
| Codeium           |      ✓       |        |        |       |          |         |
| TabNine           |      ✓       |        |        |       |          |         |
| Zed               |      ✓       |        |        |       |          |         |
| Aide              |      ✓       |        |        |       |          |         |
| PearAI            |      ✓       |        |        |       |          |         |
| Supermaven        |      ✓       |        |        |       |          |         |
| CodeStory         |      ✓       |        |        |       |          |         |
| Double            |      ✓       |        |        |       |          |         |
| Blackbox AI       |      ✓       |        |        |       |          |         |
| Amazon Q          |      ✓       |        |        |       |          |         |
| Copilot Workspace |      ✓       |        |        |       |          |         |
| Goose AI          |      ✓       |        |        |       |          |         |
| Mentat            |      ✓       |        |        |       |          |         |
| Melty             |      ✓       |        |        |       |          |         |
| Void              |      ✓       |        |        |       |          |         |
| Qoder             |      ✓       |        |        |       |          |         |

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
3. Merge instructions/skills/agents/rules/commands/prompts from all tools
4. Create symlinks from each tool's config to shared directories

### Edit instructions

```
~/.ai-global/instructions.md
```

Changes take effect immediately - all tools read the same file via symlinks.

### Commands

| Command                      | Description                               |
| ---------------------------- | ----------------------------------------- |
| `ai-global`                  | Scan, merge and update symlinks (default) |
| `ai-global status`           | Show symlink status                       |
| `ai-global list`             | List supported tools                      |
| `ai-global backups`          | List available backups                    |
| `ai-global unlink <tool>`    | Unlink a tool's original config           |
| `ai-global unlink all`       | Unlink all tools                          |
| `ai-global skill <source>`   | Add a skill (file or GitHub repo)         |
| `ai-global agent <source>`   | Add an agent                              |
| `ai-global rule <source>`    | Add a rule                                |
| `ai-global command <source>` | Add a command                             |
| `ai-global prompt <source>`  | Add a prompt                              |
| `ai-global upgrade`          | Upgrade to latest version                 |
| `ai-global uninstall`        | Completely remove ai-global               |
| `ai-global version`          | Show version                              |
| `ai-global help`             | Show help                                 |

### Add skill/agent/rule/command/prompt

```bash
# From local file
ai-global skill react.md
ai-global agent coder.md

# From GitHub repo (clone all .md files)
ai-global skill user/repo
ai-global skill https://github.com/user/repo

# From GitHub subdirectory
ai-global skill user/repo/skills

# From GitHub single file
ai-global skill user/repo/skills/react.md
```

## How it works

```
~/.ai-global/
├── instructions.md  <- Shared instructions (edit this)
├── skills/          <- Shared skills (merged from all tools)
├── agents/          <- Shared agents
├── rules/           <- Shared rules
├── commands/        <- Shared slash commands
├── prompts/         <- Shared prompt templates
└── backups/         <- Original configs (backup)

Each AI tool's config directory contains symlinks:

~/.claude/
├── CLAUDE.md -> ~/.ai-global/instructions.md  (symlink)
├── skills/   -> ~/.ai-global/skills/          (symlink)
└── commands/ -> ~/.ai-global/commands/        (symlink)

~/.cursor/
├── rules/global.md -> ~/.ai-global/instructions.md (symlink)
├── skills/         -> ~/.ai-global/skills/         (symlink)
└── prompts/        -> ~/.ai-global/prompts/        (symlink)

... and more tools
```

## Merge behavior

When you run `ai-global`, it merges items from all tools by filename:

- Cursor has skills: `react.md`, `typescript.md`
- Claude has skills: `typescript.md`, `python.md`
- Result in `~/.ai-global/skills/`: `react.md`, `typescript.md`, `python.md`

The first file found wins (dedup by filename).

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

## Example instructions.md

```markdown
# AI Assistant Instructions

- Use pnpm as the package manager
- Reply in English
- Follow existing code style
- Use TypeScript with `type` for type definitions
```

## License

MIT
