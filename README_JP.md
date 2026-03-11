# AI Global

[English](README.md) · [简体中文](README_CN.md) · [繁體中文](README_TW.md) · 日本語 · [한국어](README_KR.md)

---

**AI プログラミングアシスタント統合設定管理ツール。**

1つのファイルを編集して、すべての AI ツールに同期します。

**システムモード**と**プロジェクトモード**の両方に対応

## インストール

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

### 自動モード検出

AI Globalは自動的にコンテキストを検出します：

- **システムモード**：`~`ディレクトリから実行時、システム全体の統一設定
- **プロジェクトモード**：任意のプロジェクトディレクトリ（`~`以外）から実行時、プロジェクト固有の統一設定

### 初回実行

```bash
ai-global
```

これにより：

1. 現在のディレクトリを検出（システムまたはプロジェクト）
2. インストールされている AI ツールをスキャン
3. 元の設定を `.ai-global/backups/` にバックアップ
4. 検出されたツールの AGENTS.md/skills/agents/rules/commands をマージ
5. 各ツールの設定から共有ディレクトリへのシンボリックリンクを作成

注意: AI Global が処理するのは、すでに存在するツールディレクトリだけです。`.github`、`.kiro`、`.cursor` のようなディレクトリは自動作成されません。

### コマンド一覧

| コマンド                    | 説明                                                   | コンテキスト対応 |
| --------------------------- | ------------------------------------------------------ | ---------------- |
| `ai-global`                 | スキャン、マージ、シンボリックリンク更新（デフォルト） | はい             |
| `ai-global status`          | シンボリックリンクの状態を表示                         | はい             |
| `ai-global list`            | サポートされているツールを一覧表示                     | はい             |
| `ai-global backups`         | 利用可能なバックアップを一覧表示                       | はい             |
| `ai-global unlink <key>`    | 特定のツールの元の設定を復元                           | はい             |
| `ai-global unlink all`      | すべてのツールを復元                                   | はい             |
| `ai-global add <user/repo>` | スキルを追加                                           | はい             |
| `ai-global upgrade`         | 最新バージョンにアップグレード                         |                  |
| `ai-global uninstall`       | 完全にアンインストール                                 |                  |
| `ai-global version`         | バージョン番号を表示                                   |                  |
| `ai-global help`            | ヘルプを表示                                           |                  |

**コンテキスト対応**：コマンドの動作は現在のディレクトリ（システム vs プロジェクト）に依存します

### スキルを追加

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

スキルはダウンロードされ、あなたの `.ai-global/skills/` ディレクトリに追加されます。

## 動作原理

### システムモード構造

```
~/.ai-global/
├── AGENTS.md        <- 共有 AGENTS.md（これを編集）
├── skills/          <- 共有スキル（すべてのツールからマージ）
├── agents/          <- 共有エージェント
├── rules/           <- 共有ルール
├── commands/        <- 共有スラッシュコマンド
└── backups/         <- 元の設定（バックアップ）

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
├── .ai-global/          <- プロジェクト固有の設定
│   ├── AGENTS.md        <- プロジェクト AGENTS.md
│   ├── skills/          <- プロジェクトスキル
│   ├── agents/          <- プロジェクトエージェント
│   ├── rules/           <- プロジェクトルール
│   ├── commands/        <- プロジェクトコマンド
│   └── backups/         <- プロジェクトバックアップ
└── .cursor/             <- AIツール設定
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (シンボリックリンク)
    └── skills/   -> ../.ai-global/skills/     (シンボリックリンク)
```

### モードの動作

- **システムモード**：システム全体の AI 設定を管理
- **プロジェクトモード**：特定のプロジェクトの AI 設定のみを管理
- **自動検出**：コマンドなしでモードを切り替え可能
- **コンテキスト対応**：コマンドが操作中のコンテキストを表示

### マージ動作

`ai-global` を実行すると、ファイル名に基づいてすべてのツールの内容をマージします：

- Cursor のスキル: `react/`, `typescript/`
- Claude のスキル: `typescript/`, `python/`
- マージ結果 `.ai-global/skills/`: `react/`, `typescript/`, `python/`

**最後に見つかったファイルが優先されます**（後のツールが同名ファイルを上書きします）。

## サポートされているツール

| ツール         | Key           | AGENTS.md | Rules | Commands | Skills | Agents |
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

## アンインストール

```bash
ai-global uninstall
```

これにより：

1. すべてのツールの元の設定を復元
2. `~/.ai-global` ディレクトリを削除
3. `ai-global` コマンドを削除

npm でインストールした場合：

```bash
ai-global uninstall

npm uninstall -g ai-global
```

## ライセンス

MIT
