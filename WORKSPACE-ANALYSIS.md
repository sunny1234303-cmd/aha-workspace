# aha-workspace 분석 문서

> 용도: 워크스페이스 구조 및 기능 설명 (온보딩·참고용)

## 1. 개요

**aha-workspace**는 AI를 처음 써보는 사람을 위한 작업 환경으로, Claude Code와 Johnny Decimal 시스템을 결합한 실전 PKM(Personal Knowledge Management) 워크스페이스입니다.

**핵심 철학**:
1. AI amplifies thinking, not just writing
2. File system = AI memory
3. Structure enables creativity
4. Iteration over perfection
5. Immediate usability

---

## 2. 구조 (9개 카테고리)

```
aha-workspace/
├── .claude/        # 슬래시 커맨드 6개 (+ 최초 1회용 setup-workspace)
├── 00-inbox/       # 메모함 — 생각날 때 바로 텍스트로 적어두는 곳
├── 00-system/      # 템플릿·가이드·데이터베이스
├── 10-projects/    # 진행 중인 프로젝트
├── 20-operation/   # HR / 반복업무 (초기 설정 때 선택, 둘 다 가능)
├── 30-knowledge/   # 용도를 직접 정의하는 레퍼런스 공간
├── 40-schedule/    # 일정관리 (Daily / Weekly / Todo)
├── 50-resources/   # 참고 자료
└── 90-archive/     # 완료된 프로젝트 + 인사이트
```

---

## 3. Slash Commands

### 최초 1회

| 커맨드 | 설명 |
|--------|------|
| `/setup-workspace` | 대화형 초기 설정 — CLAUDE.md 생성 + 데이터베이스 생성 + 20-operation 용도 선택 |

### 실제 쓰는 순서 (5개)

| 커맨드 | 설명 |
|--------|------|
| `/오늘` | 매일 — 오늘 기록 생성/열기 + 할일 캡처·조회·자동 추출 |
| `/gather` | 정보 수집 모드 (구조화된 질문 생성) |
| `/reframe` | 이해 확인 모드 (대화 요약 및 확인) |
| `/truth` | 사실 기반 분석 모드 (객관적 분석) |
| `/idea [카테고리]` | 대화에서 아이디어 추출 후 `30-knowledge/`에 저장 |

### Claude Code 기본 내장

`/compact`(대화 요약), `/clear`(대화 초기화), `/resume`(이전 대화 이어하기), `/help`(도움말)도 자주 씁니다.

---

## 4. Templates

`00-system/01-templates/`에 기본 템플릿(Daily Note, Weekly Review, Project)을 제공합니다.

---

## 5. 핵심 기능 연결도

```
┌─────────────────────────────────────────────────────────────┐
│                    INITIAL SETUP                            │
│  /setup-workspace → 이름/역할/용도 → CLAUDE.md 생성          │
│                   → 데이터베이스 생성 (00-system/09-database/)│
│                   → 20-operation 용도 선택                   │
└─────────────────────────────────────────────────────────────┘
                              │
                              v
┌─────────────────────────────────────────────────────────────┐
│                    DAILY WORKFLOW                            │
│  /오늘 → 41-daily에 자유 기록 (할일 포함)                    │
│       → 기록에서 할일 자동 추출·정리 → 43-todos              │
└─────────────────────────────────────────────────────────────┘
                              │
                              v
┌─────────────────────────────────────────────────────────────┐
│                ORCHESTRATION COMMANDS                        │
│  /gather → 정보 수집 (구조화된 질문)                         │
│  /reframe → 이해 확인 (대화 요약)                            │
│  /truth → 사실 기반 분석 (객관적 평가)                       │
└─────────────────────────────────────────────────────────────┘
                              │
                              v
┌─────────────────────────────────────────────────────────────┐
│                KNOWLEDGE MANAGEMENT                          │
│  /idea → 대화에서 인사이트 추출 → 30-knowledge 저장          │
└─────────────────────────────────────────────────────────────┘
```

---

## 6. 사용자 시작 가이드

### 최초 설정 (5분)
```bash
git clone https://github.com/sunny1234303-cmd/aha-workspace.git
cd aha-workspace

# Claude Code에서 열기
/setup-workspace
```

### 매일 사용
```bash
/오늘                # 오늘 기록 + 할일 확인/추가
```

### 생각 정리가 필요할 때
```bash
/gather              # 정보 수집
/reframe             # 이해 확인
/truth               # 사실 기반 분석
```
