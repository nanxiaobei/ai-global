# AI Global

[English](README.md) · [简体中文](README_CN.md) · 繁體中文 · [日本語](README_JP.md) · [한국어](README_KR.md)

---

**AI 程式設計助手統一設定管理器。**

編輯一個檔案，同步到所有 AI 工具。

同時支援**系統模式**和**專案模式**！

## 安裝

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

### 自動模式偵測

AI Global 會自動偵測你的上下文：

- **系統模式**：當從 `~` 目錄執行時，為系統範圍統一設定
- **專案模式**：當從任何專案目錄（非 `~`）執行時，為專案特定統一設定

### 首次執行

```bash
ai-global
```

這將會：

1. 偵測當前目錄（系統或專案）
2. 掃描已安裝的 AI 工具
3. 備份原始設定到 `.ai-global/backups/`
4. 合併偵測到的工具的 AGENTS.md/skills/agents/rules/commands
5. 建立從各工具設定到共享目錄的符號連結

### 指令列表

| 指令                        | 說明                             | 上下文感知 |
| --------------------------- | -------------------------------- | ---------- |
| `ai-global`                 | 掃描、合併、更新符號連結（預設） | 是         |
| `ai-global status`          | 顯示符號連結狀態                 | 是         |
| `ai-global list`            | 列出支援的工具                   | 是         |
| `ai-global backups`         | 列出可用的備份                   | 是         |
| `ai-global unlink <key>`    | 還原某個工具的原始設定           | 是         |
| `ai-global unlink all`      | 還原所有工具                     | 是         |
| `ai-global add <user/repo>` | 新增技能                         | 是         |
| `ai-global upgrade`         | 升級到最新版本                   |            |
| `ai-global uninstall`       | 完整解除安裝                     |            |
| `ai-global version`         | 顯示版本號                       |            |
| `ai-global help`            | 顯示說明                         |            |

**上下文感知**：指令行為取決於當前目錄（系統 vs 專案）

### 新增技能

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

技能將被下載並新增到你的 `.ai-global/skills/` 目錄。

## 運作原理

### 系統模式結構

```
~/.ai-global/
├── AGENTS.md        <- 共享 AGENTS.md（編輯這個）
├── skills/          <- 共享技能（從所有工具合併）
├── agents/          <- 共享代理
├── rules/           <- 共享規則
├── commands/        <- 共享斜線指令
└── backups/         <- 原始設定（備份）

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
├── .ai-global/          <- 專案特定設定
│   ├── AGENTS.md        <- 專案 AGENTS.md
│   ├── skills/          <- 專案技能
│   ├── agents/          <- 專案代理
│   ├── rules/           <- 專案規則
│   ├── commands/        <- 專案指令
│   └── backups/         <- 專案備份
└── .cursor/             <- AI 工具設定
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (符號連結)
    └── skills/   -> ../.ai-global/skills/     (符號連結)
```

### 模式行為

- **系統模式**：管理整個系統的 AI 設定
- **專案模式**：僅管理特定專案的 AI 設定
- **自動偵測**：無需指令即可切換模式
- **上下文感知**：指令將顯示它們正在操作的上下文

### 合併行為

執行 `ai-global` 時，會按檔案名稱合併所有工具的內容：

- Cursor 有 skills: `react/`, `typescript/`
- Claude 有 skills: `typescript/`, `python/`
- 合併結果 `.ai-global/skills/`: `react/`, `typescript/`, `python/`

**最後找到的檔案優先**（後找到的工具會覆蓋同名檔案）。

## 支援的工具

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

## 解除安裝

```bash
ai-global uninstall
```

這將會：

1. 還原所有工具的原始設定
2. 刪除 `~/.ai-global` 目錄
3. 移除 `ai-global` 指令

如果透過 npm 安裝：

```bash
ai-global uninstall

npm uninstall -g ai-global
```

## 授權條款

MIT
