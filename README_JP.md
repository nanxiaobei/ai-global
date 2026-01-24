# AI Global

[English](README.md) | [简体中文](README_CN.md) | [繁體中文](README_TW.md) | [한국어](README_KR.md)

AI プログラミングアシスタント統合設定管理ツール。1つのファイルを編集して、すべての AI ツールに同期します。

## インストール

### curl

```bash
curl -fsSL https://raw.githubusercontent.com/lazyjerry/ai-global/main/install.sh | bash
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

### 初回実行

```bash
ai-global
```

これにより：

1. システムにインストールされている AI ツールをスキャン
2. 元の設定を `~/.ai-global/backups/` にバックアップ
3. すべてのツールの AGENTS.md/skills/agents/rules/commands をマージ
4. 各ツールの設定から共有ディレクトリへのシンボリックリンクを作成

### コマンド一覧

| コマンド                      | 説明                                 |
| ----------------------------- | ------------------------------------ |
| `ai-global`                   | スキャン、マージ、シンボリックリンク更新（デフォルト） |
| `ai-global status`            | シンボリックリンクの状態を表示       |
| `ai-global list`              | サポートされているツールを一覧表示   |
| `ai-global backups`           | 利用可能なバックアップを一覧表示     |
| `ai-global unlink <key>`      | 特定のツールの元の設定を復元         |
| `ai-global unlink all`        | すべてのツールを復元                 |
| `ai-global skill <user/repo>` | スキルを追加                         |
| `ai-global upgrade`           | 最新バージョンにアップグレード       |
| `ai-global uninstall`         | 完全にアンインストール               |
| `ai-global version`           | バージョン番号を表示                 |
| `ai-global help`              | ヘルプを表示                         |

### スキルを追加

```bash
ai-global skill user/repo
ai-global skill https://github.com/user/repo
```

## 動作原理

```
~/.ai-global/
├── AGENTS.md        <- 共有プロンプト（これを編集）
├── skills/          <- 共有スキル（すべてのツールからマージ）
├── agents/          <- 共有エージェント
├── rules/           <- 共有ルール
├── commands/        <- 共有スラッシュコマンド
└── backups/         <- 元の設定（バックアップ）

各 AI ツールの設定ディレクトリにシンボリックリンクを配置：

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (シンボリックリンク)
├── skills/   -> ~/.ai-global/skills/          (シンボリックリンク)
└── commands/ -> ~/.ai-global/commands/        (シンボリックリンク)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (シンボリックリンク)
└── skills/   -> ~/.ai-global/skills/          (シンボリックリンク)

... その他のツール
```

## マージ動作

`ai-global` を実行すると、ファイル名に基づいてすべてのツールの内容をマージします：

- Cursor のスキル: `react/`, `typescript/`
- Claude のスキル: `typescript/`, `python/`
- マージ結果 `~/.ai-global/skills/`: `react/`, `typescript/`, `python/`

最初に見つかったファイルが優先されます（ファイル名で重複を除去）。

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
