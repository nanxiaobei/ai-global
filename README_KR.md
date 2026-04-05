# AI Global

[English](README.md) · [简体中文](README_CN.md) · [繁體中文](README_TW.md) · [日本語](README_JP.md) · 한국어

---

**AI 프로그래밍 어시스턴트 통합 설정 관리 도구입니다.**

하나의 파일을 편집하여 모든 AI 도구에 동기화하세요.

**시스템 모드**와 **프로젝트 모드**를 모두 지원합니다.

## 지원되는 도구

| 도구                                                  | Key           | AGENTS.md | Rules | Commands | Skills |
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

## 설치

`curl` 또는 `npm`을 사용하여 설치합니다:

### curl

```bash
curl -fsSL https://raw.githubusercontent.com/nanxiaobei/ai-global/main/install.sh | bash
```

### npm

```bash
npm install -g ai-global
# 또는
pnpm add -g ai-global
# 또는
yarn global add ai-global
# 또는
bun add -g ai-global
```

## 사용법

실행:

```bash
ai-global
```

이렇게 하면:

1. 현재 디렉토리 컨텍스트를 감지합니다 (시스템 또는 프로젝트)
2. 설치된 AI 도구를 스캔합니다
3. 원본 설정을 `.ai-global/backups`에 백업합니다
4. 감지된 도구의 `AGENTS.md` `skills` `rules` `commands`를 `.ai-global` 공유 설정으로 병합합니다
5. 각 도구에서 `.ai-global` 공유 설정으로 심볼릭 링크를 생성합니다

### 컨텍스트

- **시스템 모드**: `~` 디렉토리에서 실행 시, 시스템 전체의 통합 설정
- **프로젝트 모드**: 모든 프로젝트 디렉토리(`~` 제외)에서 실행 시, 프로젝트별 통합 설정

## 명령어

```bash
ai-global                   # 심볼릭 링크 업데이트 (기본값)
ai-global status            # 심볼릭 링크 상태 표시
ai-global list              # 지원되는 도구 목록 표시
ai-global backups           # 사용 가능한 백업 목록 표시
ai-global unlink <key>      # 특정 도구의 원본 설정 복원
ai-global unlink all        # 모든 도구 복원
ai-global add <user/repo>   # GitHub 에서 skills 추가
ai-global upgrade           # 최신 버전으로 업그레이드
ai-global uninstall         # 완전히 제거
ai-global version           # 버전 표시
ai-global help              # 도움말 표시
```

**컨텍스트 인지**: 명령어 동작은 현재 디렉토리(시스템 또는 프로젝트)에 따라 달라집니다

### Skills 추가

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

Skills은 당신의 `.ai-global/skills`에 추가되며, 모든 도구에 자동으로 공유됩니다 (심볼릭 링크 때문).

## 작동 원리

### 시스템 모드 구조

```
~/.ai-global/
├── AGENTS.md        <- 시스템 공유 AGENTS.md
├── skills/          <- 시스템 공유 skills
├── rules/           <- 시스템 공유 rules
├── commands/        <- 시스템 공유 commands
└── backups/         <- 원본 도구 설정의 백업

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (심볼릭 링크)
├── skills/   -> ~/.ai-global/skills/          (심볼릭 링크)
└── commands/ -> ~/.ai-global/commands/        (심볼릭 링크)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (심볼릭 링크)
└── skills/   -> ~/.ai-global/skills/          (심볼릭 링크)

... 그 외 더 많은 도구들
```

### 프로젝트 모드 구조

```
my-project/
├── .ai-global/
│   ├── AGENTS.md        <- 프로젝트 공유 AGENTS.md
│   ├── skills/          <- 프로젝트 공유 skills
│   ├── rules/           <- 프로젝트 공유 rules
│   ├── commands/        <- 프로젝트 공유 commands
│   └── backups/         <- 원본 도구 설정의 백업
└── .cursor/
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (심볼릭 링크)
    └── skills/   -> ../.ai-global/skills/     (심볼릭 링크)

    ... 그 외 더 많은 도구들
```

### 모드 동작

- **시스템 모드**: 시스템 AI 도구 설정 관리
- **프로젝트 모드**: 프로젝트 AI 도구 설정 관리
- **자동 감지**: 전환을 위한 명령어 불필요
- **컨텍스트 인지**: 명령어는 어떤 컨텍스트에서 동작하는지 표시

### 병합 동작

`ai-global`을 실행하면, 파일명으로 모든 도구의 항목을 병합합니다:

- Cursor는 skills: `react/`, `typescript/`
- Claude는 skills: `typescript/`, `python/`
- 결과 `.ai-global/skills`: `react/`, `typescript/`, `python/`

**마지막 파일이 우선** (나중 도구가 이전 도구와 동일한 파일명을 덮어쓰니다).

## 제거

```bash
ai-global uninstall
```

이렇게 하면:

1. 모든 도구의 심볼릭 링크를 해제하고 원본 설정으로 복원
2. 모든 `.ai-global` 디렉토리 제거
3. `ai-global` 명령어 제거

## 라이선스

MIT
