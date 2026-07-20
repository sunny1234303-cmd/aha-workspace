# aha-workspace

> AI를 처음 써보는 사람을 위한 워크스페이스
> Claude Code와 Johnny Decimal 시스템으로 만든 실전 PKM 환경

---

## 이게 뭔가요?

컴퓨터에 파일 정리하듯, AI와 대화하며 일하고 기록하는 폴더 구조입니다. 코딩을 몰라도 됩니다 — 터미널에 한글로 말하듯 요청하면 Claude가 알아서 정리해줍니다.

**핵심 특징**:
- 폴더 번호만 봐도 뭐가 어디 있는지 알 수 있는 구조 (Johnny Decimal)
- 처음 열면 `/setup-workspace`가 대화로 안내
- 매일 쓰는 루틴(오늘 기록, 할일, 주간정리)이 커맨드 하나로 끝남

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
이름, 역할, 관심사를 순서대로 물어보고 `CLAUDE.md`를 자동으로 만들어줍니다. `20-operation` 폴더를 HR용으로 쓸지, 반복업무용으로 쓸지도 이때 정합니다.

### 4. 오늘부터 바로 사용
```
/daily-note     # 오늘 기록 시작 (할일도 여기 같이 적으면 됨)
/todo           # 할일만 따로 보고 싶을 때
```

## Philosophy

1. AI는 글만 대신 써주는 게 아니라 생각을 확장시켜준다
2. 파일 구조 자체가 AI의 기억이다
3. 구조가 있어야 창의성이 나온다
4. 완벽보다 반복 개선
5. 바로 쓸 수 있어야 한다

## 폴더 구조

```
aha-workspace/
├── 00-inbox/       # 빠른 캡처 — 생각나는 대로 적고 Claude에게 정리를 맡기세요
├── 00-system/      # 템플릿·가이드·자동화 스크립트
├── 10-projects/    # 시작일·종료일이 있는 프로젝트
├── 20-operation/   # HR 또는 반복업무 (초기 설정 때 하나만 선택)
├── 30-knowledge/   # 검증된 지식·가이드 아카이브
├── 40-schedule/    # 일정관리 (Daily / Weekly / Todo)
├── 50-resources/   # 참고 자료
└── 90-archive/     # 완료·중단된 프로젝트
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
| `/setup-workspace` | 대화형 초기 설정 (최초 1회) |
| `/setup-google-calendar` | Google Calendar 연동 (선택) |
| `/daily-note` | 오늘 기록 생성/열기 |
| `/daily-review` | 어제-오늘 변경사항 정리 |
| `/todo` | 할일 캡처/조회 |
| `/thinking-partner` | 생각 정리 파트너 (소크라테스식 질문) |
| `/gather` | 정보 수집 모드 |
| `/reframe` | 이해 확인 모드 |
| `/truth` | 사실 기반 분석 모드 |
| `/idea` | 대화에서 아이디어 추출·저장 |
| `/create-command` | 커스텀 커맨드 만들기 |

각 커맨드가 언제·왜·어떻게 조합되는지는 `00-system/03-guides/`와 `00-system/orchestration-commands-guide.md`를 참고하세요.

## 실습해보고 싶다면

`00-system/claude-code-practice-guide.md`에서 Claude Code 기본 사용법을 익힐 수 있습니다.

## 원본 대조

기존 imi-workspace에서 가져오면서 내용을 새로 쓴 문서들은, 수정 전 원본이 `00-system/_originals/`에 그대로 남아있습니다.

## Credits

원본 구조: [Rhim80/imi-workspace](https://github.com/Rhim80/imi-workspace) (이림/hovoo)

## License

MIT License — 자유롭게 사용하고 수정하세요.

## Support

Issues나 질문이 있으면 GitHub Issues를 활용해주세요.
