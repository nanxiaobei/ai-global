# AI Global

[English](README.md) · [简体中文](README_CN.md) · [繁體中文](README_TW.md) · 日本語 · [한국어](README_KR.md)

---

**AI プログラミングアシスタント統合設定管理ツール。**

1つのファイルを編集して、すべての AI ツールに同期します。

**システムモード**と**プロジェクトモード**の両方に対応。

## サポートされているツール

| ツール                                                | Key           | AGENTS.md | Rules | Commands | Skills |
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

## インストール

`curl` または `npm` を使用してインストールします：

### curl

```bash
curl -fsSL https://raw.githubusercontent.com/nanxiaobei/ai-global/main/install.sh | bash
```

### npm

```bash
npm install -g ai-global
# または
pnpm add -g ai-global
# または
yarn global add ai-global
# または
bun add -g ai-global
```

## 使い方

実行：

```bash
ai-global
```

これにより：

1. 現在のディレクトリコンテキストを検出（システムまたはプロジェクト）
2. インストールされている AI ツールをスキャン
3. 元の設定を `.ai-global/backups` にバックアップ
4. 検出されたツールの `AGENTS.md` `skills` `rules` `commands` を `.ai-global` 共有設定にマージ
5. 各ツールから `.ai-global` 共有設定へのシンボリックリンクを作成

### コンテキスト

- **システムモード**：`~`ディレクトリから実行時、システム全体の統一設定
- **プロジェクトモード**：任意のプロジェクトディレクトリ（`~`以外）から実行時、プロジェクト固有の統一設定

## コマンド

```bash
ai-global                   # シンボリックリンク更新（デフォルト）
ai-global status            # シンボリックリンク状態を表示
ai-global list              # サポートされているツールを一覧表示
ai-global backups           # 利用可能なバックアップを一覧表示
ai-global unlink <key>      # ツールの元の設定を復元
ai-global unlink all        # すべてのツールを復元
ai-global add <user/repo>   # GitHub から skills を追加
ai-global upgrade           # 最新バージョンにアップグレード
ai-global uninstall         # 完全にアンインストール
ai-global version           # バージョンを表示
ai-global help              # ヘルプを表示
```

**コンテキスト対応**：コマンドの動作は現在のディレクトリ（システムまたはプロジェクト）に依存します

### Skills を追加

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

Skills はあなたの `.ai-global/skills` に追加され、各ツールに自動的に共有されます（シンボリックリンクのため）。

## 動作原理

### システムモード構造

```
~/.ai-global/
├── AGENTS.md        <- システム共有 AGENTS.md
├── skills/          <- システム共有 skills
├── rules/           <- システム共有 rules
├── commands/        <- システム共有 commands
└── backups/         <- 元のツール設定のバックアップ

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (シンボリックリンク)
├── skills/   -> ~/.ai-global/skills/          (シンボリックリンク)
└── commands/ -> ~/.ai-global/commands/        (シンボリックリンク)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (シンボリックリンク)
└── skills/   -> ~/.ai-global/skills/          (シンボリックリンク)

... その他のツール
```

### プロジェクトモード構造

```
my-project/
├── .ai-global/
│   ├── AGENTS.md        <- プロジェクト共有 AGENTS.md
│   ├── skills/          <- プロジェクト共有 skills
│   ├── rules/           <- プロジェクト共有 rules
│   ├── commands/        <- プロジェクト共有 commands
│   └── backups/         <- 元のツール設定のバックアップ
└── .cursor/
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (シンボリックリンク)
    └── skills/   -> ../.ai-global/skills/     (シンボリックリンク)

    ... その他のツール
```

### モード動作

- **システムモード**：システム用の AI ツール設定を管理
- **プロジェクトモード**：プロジェクト用の AI ツール設定を管理
- **自動検出**：切り替えにコマンドは不要
- **コンテキスト対応**：コマンドはどのコンテキストで動作しているかを表示

### マージ動作

`ai-global` を実行すると、ファイル名ですべてのツールの項目をマージします：

- Cursor は skills: `react/`, `typescript/`
- Claude は skills: `typescript/`, `python/`
- 結果 `.ai-global/skills`: `react/`, `typescript/`, `python/`

**最後のファイルが優先**（後のツールが前のツールと同じファイル名を上書きします）。

## アンインストール

```bash
ai-global uninstall
```

これにより：

1. すべてのツールのシンボリックリンクを解除し、元の設定に復元
2. すべての `.ai-global` ディレクトリを削除
3. `ai-global` コマンドを削除

## ライセンス

MIT
