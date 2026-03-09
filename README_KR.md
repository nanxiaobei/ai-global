# AI Global

[English](README.md) · [简体中文](README_CN.md) · [繁體中文](README_TW.md) · [日本語](README_JP.md) · 한국어

---

**AI 프로그래밍 어시스턴트 통합 설정 관리 도구입니다.**

하나의 파일을 편집하여 모든 AI 도구에 동기화하세요.

**시스템 모드**와 **프로젝트 모드**를 모두 지원합니다

## 설치

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

### 자동 모드 감지

AI Global은 자동으로 컨텍스트를 감지합니다:

- **시스템 모드**: `~` 디렉토리에서 실행 시, 시스템 전체의 통합 설정
- **프로젝트 모드**: 모든 프로젝트 디렉토리(`~` 제외)에서 실행 시, 프로젝트별 통합 설정

### 첫 실행

```bash
ai-global
```

실행 시:

1. 현재 디렉토리를 감지합니다 (시스템 또는 프로젝트)
2. 설치된 AI 도구를 스캔합니다
3. 원본 설정을 `.ai-global/backups/`에 백업합니다
4. 감지된 도구의 AGENTS.md/skills/agents/rules/commands를 병합합니다
5. 각 도구의 설정에서 공유 디렉토리로 심볼릭 링크를 생성합니다

### 명령어 목록

| 명령어                      | 설명                                    | 컨텍스트 인식 |
| --------------------------- | --------------------------------------- | ------------- |
| `ai-global`                 | 스캔, 병합, 심볼릭 링크 업데이트 (기본) | 예            |
| `ai-global status`          | 심볼릭 링크 상태 표시                   | 예            |
| `ai-global list`            | 지원되는 도구 목록 표시                 | 예            |
| `ai-global backups`         | 사용 가능한 백업 목록 표시              | 예            |
| `ai-global unlink <key>`    | 특정 도구의 원본 설정 복원              | 예            |
| `ai-global unlink all`      | 모든 도구 복원                          | 예            |
| `ai-global add <user/repo>` | 스킬 추가                               | 예            |
| `ai-global upgrade`         | 최신 버전으로 업그레이드                |               |
| `ai-global uninstall`       | 완전히 제거                             |               |
| `ai-global version`         | 버전 번호 표시                          |               |
| `ai-global help`            | 도움말 표시                             |               |

**컨텍스트 인식**: 명령어 동작은 현재 디렉토리(시스템 vs 프로젝트)에 따라 달라집니다

### 스킬 추가

```bash
ai-global add user/repo
ai-global add https://github.com/user/repo
```

스킬이 다운로드되어 `.ai-global/skills/` 디렉토리에 추가됩니다.

## 작동 원리

### 시스템 모드 구조

```
~/.ai-global/
├── AGENTS.md        <- 공유 AGENTS.md (이 파일을 편집하세요)
├── skills/          <- 공유 스킬 (모든 도구에서 병합됨)
├── agents/          <- 공유 에이전트
├── rules/           <- 공유 규칙
├── commands/        <- 공유 슬래시 명령어
└── backups/         <- 원본 설정 (백업)

~/.claude/
├── CLAUDE.md -> ~/.ai-global/AGENTS.md        (심볼릭 링크)
├── skills/   -> ~/.ai-global/skills/          (심볼릭 링크)
└── commands/ -> ~/.ai-global/commands/        (심볼릭 링크)

~/.cursor/
├── AGENTS.md -> ~/.ai-global/AGENTS.md        (심볼릭 링크)
└── skills/   -> ~/.ai-global/skills/          (심볼릭 링크)

... 기타 도구들
```

### 프로젝트 모드 구조

```
my-project/
├── .ai-global/          <- 프로젝트별 설정
│   ├── AGENTS.md        <- 프로젝트 AGENTS.md
│   ├── skills/          <- 프로젝트 스킬
│   ├── agents/          <- 프로젝트 에이전트
│   ├── rules/           <- 프로젝트 규칙
│   ├── commands/        <- 프로젝트 명령어
│   └── backups/         <- 프로젝트 백업
└── .cursor/             <- AI 도구 설정
    ├── AGENTS.md -> ../.ai-global/AGENTS.md   (심볼릭 링크)
    └── skills/   -> ../.ai-global/skills/     (심볼릭 링크)
```

### 모드 동작

- **시스템 모드**: 시스템 전체의 AI 설정을 관리합니다
- **프로젝트 모드**: 특정 프로젝트의 AI 설정만 관리합니다
- **자동 감지**: 명령어 없이 모드를 전환할 수 있습니다
- **컨텍스트 인식**: 명령어가 작동 중인 컨텍스트를 표시합니다

### 병합 동작

`ai-global`을 실행하면 파일 이름을 기준으로 모든 도구의 내용을 병합합니다:

- Cursor의 스킬: `react/`, `typescript/`
- Claude의 스킬: `typescript/`, `python/`
- 병합 결과 `.ai-global/skills/`: `react/`, `typescript/`, `python/`

**나중에 발견된 파일이 우선됩니다** (나중에 발견된 도구가 동일한 이름의 파일을 덮어씁니다).

## 지원되는 도구

| 도구           | Key           | AGENTS.md | Rules | Commands | Skills | Agents |
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

## 제거

```bash
ai-global uninstall
```

실행 시:

1. 모든 도구의 원본 설정을 복원합니다
2. `~/.ai-global` 디렉토리를 삭제합니다
3. `ai-global` 명령어를 제거합니다

npm으로 설치한 경우:

```bash
ai-global uninstall

npm uninstall -g ai-global
```

## 라이선스

MIT
