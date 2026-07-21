# Hooks & MCP 심화 가이드

> Claude가 알아서 하게 두는 걸 넘어서, 규칙을 강제하고 외부 도구까지 연결하기

## 이 문서는 누구를 위한 건가요?

[[01-subagents]]·[[02-skills-commands]]·[[03-best-practices]]로 서브에이전트·스킬·커맨드에 익숙해졌다면, 다음 단계는 이 둘입니다.

| 개념 | 쉬운 설명 | 예시 |
|------|----------|------|
| **Hooks** | 특정 순간에 무조건 실행되는 규칙 (Claude의 판단을 거치지 않음) | 위험한 명령 자동 차단, 파일 수정 후 자동 린트 |
| **MCP** | Claude Code를 외부 시스템에 연결하는 표준 규격 | Notion, GitHub, 사내 DB, Slack 연동 |

**핵심 차이**: 서브에이전트·스킬은 Claude가 "판단해서" 쓰는 것이고, Hooks는 Claude 판단과 무관하게 "무조건" 실행됩니다. MCP는 Claude가 쓸 수 있는 도구 자체를 늘려주는 것이고요.

---

# Part 1: Hooks

## 왜 필요한가?

`CLAUDE.md`에 "rm -rf 쓰지 마"라고 적어둬도, Claude가 매번 100% 지킨다는 보장은 없습니다. Hooks는 **Claude의 의지와 무관하게 스크립트가 강제로 검사·차단**하게 만듭니다. 이미 이 워크스페이스의 [[01-subagents]] 예제 4(읽기 전용 DB 쿼리 실행자)에서 한 번 다뤘던 개념을, 여기서 전체 이벤트 종류와 다른 활용법까지 넓혀봅니다.

## 자주 쓰는 이벤트

전체 이벤트는 20개 이상이지만, 실무에서 자주 쓰는 것만 추리면 이 정도입니다.

| 이벤트 | 언제 실행되나 | 대표 용도 |
|--------|-------------|----------|
| `SessionStart` | 세션 시작/재개 시 | 프로젝트 컨텍스트 자동 로드 |
| `UserPromptSubmit` | 프롬프트 제출 직후, Claude가 읽기 전 | 프롬프트에 추가 정보 주입 |
| `PreToolUse` | 도구 실행 직전 | 위험한 명령 차단, 자동 승인 |
| `PostToolUse` | 도구 실행 성공 직후 | 파일 수정 후 자동 린트/포맷 |
| `Stop` | Claude가 응답을 끝낼 때 | 완료 알림 |
| `SubagentStop` | 서브에이전트 작업 종료 시 | 서브에이전트 결과 로깅 |
| `PreCompact` | 컨텍스트 압축 직전 | 압축 전 스냅샷 저장 |

## 설정 위치

```
~/.claude/settings.json          # 모든 프로젝트 (공유 안 됨)
.claude/settings.json            # 이 프로젝트 (Git 공유 가능)
.claude/settings.local.json      # 이 프로젝트, 나만 (Git 공유 안 됨)
```

## 기본 구조

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/check.sh",
            "timeout": 30
          }
        ]
      }
    ]
  }
}
```

| 필드 | 설명 |
|------|------|
| `matcher` | 어떤 도구에 반응할지 (`"Bash"`, `"Edit\|Write"`, `"*"` 전체, 정규식도 가능) |
| `type` | `command`(스크립트 실행)가 기본. `http`, `mcp_tool`, `prompt`도 있음 |
| `command` | 실행할 스크립트 경로. `${CLAUDE_PROJECT_DIR}`로 프로젝트 루트 참조 |
| `timeout` | 초 단위 제한 시간 |

## 스크립트가 받는 입력 (stdin)

```json
{
  "hook_event_name": "PreToolUse",
  "tool_name": "Bash",
  "tool_input": { "command": "npm test" },
  "cwd": "/Users/me/project"
}
```

## Exit Code로 동작 제어

| Exit Code | 의미 |
|-----------|------|
| `0` | 정상 — 필요하면 stdout에 JSON을 출력해 세밀 제어 |
| `2` | 차단 — stderr 내용이 Claude에게 "왜 막혔는지"로 전달됨 |
| 그 외 | 경고만 하고 계속 진행 |

## 실전 예제: 파일 수정 후 자동 린트

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/lint-check.sh",
            "timeout": 30
          }
        ]
      }
    ]
  }
}
```

`lint-check.sh`:
```bash
#!/bin/bash
FILE=$(jq -r '.tool_input.file_path // empty' < /dev/stdin)
if [[ "$FILE" == *.js || "$FILE" == *.ts ]]; then
  npx eslint "$FILE" || echo "린트 경고 있음 — 확인해주세요" >&2
fi
exit 0
```

## 실전 예제: 세션 시작 시 컨텍스트 자동 로드

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup",
        "hooks": [
          { "type": "command", "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/load-context.sh" }
        ]
      }
    ]
  }
}
```

세션이 열릴 때마다 `git status`, 최근 커밋, 진행 중 TODO를 자동으로 Claude에게 보여주는 식으로 활용할 수 있습니다.

---

# Part 2: MCP (Model Context Protocol)

## 왜 필요한가?

Claude Code 기본 도구(Read, Bash, Edit 등)로는 로컬 파일만 다룹니다. Notion, GitHub 이슈, 사내 DB, 구글 캘린더 같은 **외부 시스템**에 직접 접근하려면 MCP 서버를 연결해야 합니다. 이 워크스페이스의 `notion-handler`, `google-calendar` 스킬도 실제로는 연결된 MCP 서버 위에서 동작합니다.

## 서버 추가하기

전송 방식이 3가지입니다. 서버 제공자가 안내하는 방식을 그대로 쓰면 됩니다.

### 1) HTTP (원격 서버, 가장 흔함)

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

### 2) SSE (원격 서버, 실시간 이벤트용)

```bash
claude mcp add --transport sse asana https://mcp.asana.com/sse
```

### 3) stdio (로컬에서 직접 실행하는 서버)

```bash
claude mcp add --env API_KEY=your-key --transport stdio airtable \
  -- npx -y airtable-mcp-server
```

`--`(더블 대시) 뒤는 서버를 실행하는 명령어 그대로 전달됩니다.

## 어디에 저장되나 (Scope)

| Scope | 저장 위치 | 범위 | 팀 공유 |
|-------|----------|------|---------|
| `local` (기본값) | `~/.claude.json` | 이 프로젝트, 나만 | ❌ |
| `project` | `.mcp.json` (프로젝트 루트) | 이 프로젝트, 전체 팀 | ✅ (Git 커밋) |
| `user` | `~/.claude.json` | 내 모든 프로젝트 | ❌ |

팀 전체가 같은 MCP 서버를 쓰게 하려면 `--scope project`로 추가하고 `.mcp.json`을 Git에 커밋하세요.

```bash
claude mcp add --transport http paypal --scope project https://mcp.paypal.com/mcp
```

`.mcp.json` 예시:
```json
{
  "mcpServers": {
    "paypal": {
      "type": "http",
      "url": "https://mcp.paypal.com/mcp"
    }
  }
}
```

## 관리 명령어

```bash
claude mcp list              # 연결된 서버 전체 확인
claude mcp get <name>        # 특정 서버 상세
claude mcp remove <name>     # 제거
```

## 연결된 도구는 이렇게 보입니다

MCP 서버의 도구는 `mcp__서버이름__도구이름` 형식으로 나타납니다. 예를 들어 GitHub MCP를 연결하면:

```
mcp__github__list_prs
mcp__github__create_issue
```

이 이름은 [[03-best-practices|권한 설정]]에서 특정 도구만 허용/차단할 때도 그대로 씁니다 (예: `mcp__github__.*`).

## 실무 팁

1. **자격 증명은 stdio 서버의 `--env`나 http 서버의 `--header`로** — CLAUDE.md나 커밋되는 파일에 직접 적지 않기
2. **project scope는 팀 전체가 승인 절차를 거침** — `.mcp.json`에 있는 서버는 처음 실행 시 Claude Code가 승인을 물어봄
3. **필요한 서버만 연결** — 서버가 많아질수록 Claude가 고를 도구 목록도 늘어나므로, 실제로 쓰는 것만 유지

## 참고 링크

- [Claude Code Hooks 공식 문서](https://code.claude.com/docs/en/hooks)
- [Claude Code MCP 공식 문서](https://code.claude.com/docs/en/mcp)

---

*이전: [베스트 프랙티스](03-best-practices.md)*
