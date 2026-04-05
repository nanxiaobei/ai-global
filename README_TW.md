# AI Global

[English](README.md) · [简体中文](README_CN.md) · 繁體中文 · [日本語](README_JP.md) · [한국어](README_KR.md)

---

**AI 程式設計助手統一設定管理器。**

編輯一個檔案，同步到所有 AI 工具。

同時支援**系統模式**和**專案模式**。

## 支援的工具

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

## 安裝

使用 `curl` 或 `npm` 安裝：

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

執行：

```bash
ai-global
```

這將會：

1. 偵測當前目錄上下文（系統或專案）
2. 掃描已安裝的 AI 工具
3. 備份原始設定到 `.ai-global/backups`
4. 將偵測到的工具的 `AGENTS.md` `skills` `rules` `commands` 合併到 `.ai-global` 共享設定
5. 建立從各工具到 `.ai-global` 共享設定的符號連結

### 上下文

- **系統模式**：當從 `~` 目錄執行時，為系統範圍統一設定
- **專案模式**：當從任何專案目錄（非 `~`）執行時，為專案特定統一設定

## 指令

```bash
ai-global                   # 更新符號連結（預設）
ai-global status            # 顯示符號連結狀態
ai-global list              # 列出支援的工具
ai-global backups           # 列出可用的備份
ai-global unlink <key>      # 還原某個工具的原始設定
ai-global unlink all        # 還原所有工具
ai-global add <user/repo>   # 從 GitHub 新增 skills
ai-global upgrade           # 升級到最新版本
ai-global uninstall         # 完整移除 ai-global
ai-global version           # 顯示版本
ai-global help              # 顯示說明
```

**上下文感知**：指令行為取決於當前目錄（系統或專案）

### 新增 Skills

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

Skills 將被新增到你的 `.ai-global/skills`，並自動共享到每個工具（因為符號連結）。

## 工作原理

### 系統模式結構

```
~/.ai-global/
├── AGENTS.md        <- 系統共享 AGENTS.md
├── skills/          <- 系統共享 skills
├── rules/           <- 系統共享 rules
├── commands/        <- 系統共享 commands
└── backups/         <- 原始工具設定的備份

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (符號連結)
├── skills/   -> ~/.ai-global/skills/          (符號連結)
└── commands/ -> ~/.ai-global/commands/        (符號連結)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (符號連結)
└── skills/   -> ~/.ai-global/skills/          (符號連結)

... 以及更多工具
```

### 專案模式結構

```
my-project/
├── .ai-global/
│   ├── AGENTS.md        <- 專案共享 AGENTS.md
│   ├── skills/          <- 專案共享 skills
│   ├── rules/           <- 專案共享 rules
│   ├── commands/        <- 專案共享 commands
│   └── backups/         <- 原始工具設定的備份
└── .cursor/
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (符號連結)
    └── skills/   -> ../.ai-global/skills/     (符號連結)

    ... 以及更多工具
```

### 模式行為

- **系統模式**：管理系統 AI 工具設定
- **專案模式**：管理專案 AI 工具設定
- **自動偵測**：無需指令即可切換
- **上下文感知**：指令將顯示它們正在操作的上下文

### 合併行為

當你執行 `ai-global` 時，它會按檔案名合併所有工具的項目：

- Cursor 有 skills: `react/`, `typescript/`
- Claude 有 skills: `typescript/`, `python/`
- 結果在 `.ai-global/skills`: `react/`, `typescript/`, `python/`

**最後檔案獲勝**（後面的工具會覆蓋與前面工具同名的檔案）。

## 解除安裝

```bash
ai-global uninstall
```

這將會：

1. 取消所有工具的符號連結，恢復到它們的原始設定
2. 刪除所有 `.ai-global` 目錄
3. 移除 `ai-global` 指令

## 授權

MIT
