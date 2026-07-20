# aha-workspace

> AI를 처음 써보는 사람을 위한 워크스페이스
> Claude Code와 Johnny Decimal 시스템으로 만든 실전 PKM 환경

---

## 이게 뭔가요?

컴퓨터에 파일 정리하듯, AI와 대화하며 일하고 기록하는 폴더 구조입니다. 코딩을 몰라도 됩니다 — 터미널에 한글로 말하듯 요청하면 Claude가 알아서 정리해줍니다.

**핵심 특징**:
- 폴더 번호만 봐도 뭐가 어디 있는지 알 수 있는 구조 (Johnny Decimal)
- 처음 열면 `/setup-workspace`가 대화로 안내하고, 기본 데이터베이스까지 만들어줌
- 매일 쓰는 루틴이 커맨드 하나로 끝남

## Quick Start (5분)

### 1. Clone
```bash
git clone https://github.com/sunny1234303-cmd/aha-workspace.git
cd aha-workspace
```

### 2. Claude Code에서 열기
터미널에서 `claude` 실행 (또는 VS Code 확장에서 열기)

### 3. 초기 설정
```
/setup-workspace
```
이름, 역할, 활용 용도를 물어보고 `CLAUDE.md`를 자동으로 만들어줍니다. 표로 관리하고 싶은 목록이 있으면 데이터베이스도 같이 만들고, `20-operation`을 HR용으로 쓸지 반복업무용으로 쓸지(또는 둘 다)도 이때 정합니다.

### 4. 사용법이 궁금하면
`00-system/orchestration-commands-guide.md`와 `00-system/03-guides/`에서 각 커맨드를 언제·왜·어떻게 쓰는지 확인하세요.

## Philosophy

1. AI는 글만 대신 써주는 게 아니라 생각을 확장시켜준다
2. 파일 구조 자체가 AI의 기억이다
3. 구조가 있어야 창의성이 나온다
4. 완벽보다 반복 개선
5. 바로 쓸 수 있어야 한다

## 구조

```
aha-workspace/
├── .claude/        # 슬래시 커맨드
├── 00-inbox/       # 빠른 캡처
├── 00-system/      # 템플릿·가이드·데이터베이스
├── 10-projects/    # 진행 중인 프로젝트
├── 20-operation/   # HR / 반복업무 (초기 설정 때 선택)
├── 30-knowledge/   # 용도를 직접 정의하는 레퍼런스 공간
├── 40-schedule/    # 일정관리 (Daily / Weekly / Todo)
├── 50-resources/   # 참고 자료
└── 90-archive/     # 완료된 프로젝트 + 인사이트
```

### Johnny Decimal 네이밍

```
[숫자]-[설명적-이름]

✅ 11-website-redesign
❌ my-project (숫자 없음)
```

## Slash Commands

| 커맨드 | 용도 |
|--------|------|
| `/setup-workspace` | 대화형 초기 설정 (CLAUDE.md + 데이터베이스) |
| `/daily-note` | 오늘 기록 생성/열기 |
| `/todo` | 할일 캡처/조회 |
| `/gather` | 정보 수집 모드 |
| `/reframe` | 이해 확인 모드 |
| `/truth` | 사실 기반 분석 모드 |
| `/idea` | 대화에서 아이디어 추출·저장 |

이 외에 Claude Code 자체 기본 커맨드인 `/compact`(대화 요약), `/clear`(대화 초기화)도 자주 씁니다.

각 커맨드가 언제·왜·어떻게 조합되는지는 `00-system/03-guides/`와 `00-system/orchestration-commands-guide.md`를 참고하세요.

## 실습해보고 싶다면

`00-system/claude-code-practice-guide.md`에서 Claude Code 기본 사용법을 익힐 수 있습니다.

## License

MIT License — 자유롭게 사용하고 수정하세요.

## Support

Issues나 질문이 있으면 GitHub Issues를 활용해주세요.
