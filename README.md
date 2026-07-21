# aha-workspace

> 클로드 코드를 처음 써보는 사람을 위한 워크스페이스
> 번호 붙은 폴더 구조 + 슬래시 커맨드로, 기록부터 정리까지 자동으로 이어집니다

---

## 이게 뭔가요?

컴퓨터에 파일 정리하듯, AI와 대화하며 일하고 기록하는 폴더 구조입니다. 코딩을 몰라도 됩니다 — 터미널에 한글로 말하듯 요청하면 Claude가 알아서 정리해줍니다.

**핵심 특징**:
- 폴더 번호만 봐도 뭐가 어디 있는지 알 수 있는 구조
- 처음 열면 `/setup-workspace`가 대화로 안내하고, 기본 데이터베이스까지 만들어줌
- 매일 쓰는 루틴이 커맨드 하나로 끝남

## Quick Start (5분)

### 0. 준비물: Git

이 워크스페이스는 GitHub라는 곳에 저장되어 있습니다. **Clone**은 그걸 내 컴퓨터로 그대로 복사해오는 것을 말합니다. 터미널(Mac: 터미널 앱 / Windows: PowerShell)을 열고 `git --version`을 쳤을 때 버전이 나오면 준비 완료입니다. 안 나온다면 [00-system/git-setup-guide.md](00-system/git-setup-guide.md)의 "Step 1: Git 설치 확인"부터 보세요.

### 1. Clone (내 컴퓨터로 복사하기)
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
이름, 역할, 활용 용도를 물어보고 `CLAUDE.md`를 자동으로 만들어줍니다 ([[CLAUDE.md.template|템플릿]] 기반). 표로 관리하고 싶은 목록이 있으면 데이터베이스도 같이 만들고, `20-operation`을 HR용으로 쓸지 반복업무용으로 쓸지(또는 둘 다)도 이때 정합니다.

### 4. 사용법이 궁금하면
[[orchestration-commands-guide]]와 `00-system/03-guides/`에서 각 커맨드를 언제·왜·어떻게 쓰는지 확인하세요.

전체 구조를 한눈에 보고 싶다면 [GUIDE.html](./GUIDE.html)을 다운로드해서 브라우저로 열어보세요 (GitHub에서는 소스로만 보여서, 로컬에 받아서 열어야 원래 디자인대로 보입니다).

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
├── 00-system/      # 템플릿·가이드·데이터베이스
├── 10-projects/    # 진행 중인 프로젝트
├── 20-operation/   # HR / 반복업무 (초기 설정 때 선택)
├── 30-knowledge/   # 용도를 직접 정의하는 레퍼런스 공간
├── 70-schedule/    # 일정관리 (Daily / Weekly / Todo)
├── 80-resources/   # 참고 자료
└── 90-archive/     # 완료된 프로젝트 + 인사이트
```

### 폴더 넘버링 규칙

```
[숫자]-[설명적-이름]

✅ 11-website-redesign
❌ my-project (숫자 없음)
```

## Slash Commands

`/setup-workspace`는 최초 1회만 실행하는 설정 커맨드라 아래 목록에서는 뺐습니다. 나머지는 실제로 쓰게 되는 순서대로 정리했습니다.

| 커맨드 | 언제 쓰나 |
|--------|------|
| [[오늘\|/오늘]] | 매일 — 오늘 기록 + 할일 캡처/조회를 한 번에 |
| [[gather\|/gather]] | 생각 정리 시작 — 구조화된 질문으로 모으고, 답변하면 이해 확인까지 자동으로 이어짐 |
| [[truth\|/truth]] | 판단이 필요할 때 — 사실 기반으로 객관적 분석 |
| [[idea\|/idea]] | 대화 중 좋은 생각이 나왔을 때 — [[30-knowledge/README\|30-knowledge]]에 저장 |

Claude Code 자체 기본 커맨드도 자주 씁니다: `/compact`(대화 요약), `/clear`(대화 초기화), `/resume`(이전 대화 이어하기), `/help`(막혔을 때 도움말).

`git push`할 때마다 [[security-check|/security-check]]가 개인정보·시크릿 노출을 자동으로 검사합니다 (필요하면 직접 실행도 가능).

각 커맨드가 언제·왜·어떻게 조합되는지는 `00-system/03-guides/`와 [[orchestration-commands-guide]]를 참고하세요.

## 실습해보고 싶다면

[[claude-code-practice-guide]]에서 Claude Code 기본 사용법을 익힐 수 있습니다.

## Security

개인정보·시크릿 보호 기능이 기본 포함되어 있습니다. 자세한 내용은 [SECURITY.md](./SECURITY.md) 참고.

## License

MIT License — 자유롭게 사용하고 수정하세요.

## Author

Made by **seoni jin**

## Support

Issues나 질문이 있으면 GitHub Issues를 활용해주세요.
