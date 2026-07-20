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

## 2. 폴더 구조 (Johnny Decimal 시스템)

```
aha-workspace/
├── .claude/
│   └── commands/          # 슬래시 커맨드 (11개)
├── 00-inbox/              # 빠른 캡처 공간
├── 00-system/             # 시스템 설정 및 템플릿
│   ├── 01-templates/      # 재사용 템플릿
│   ├── 02-automation-scripts/  # 자동화 스크립트
│   ├── 03-guides/         # 가이드 문서
│   └── _originals/        # 업그레이드 전 원본 보존 (원문 대조용)
├── 10-projects/           # 활성 프로젝트 (시한부)
├── 20-operation/          # 운영 업무 — HR용 또는 반복업무용, 초기 설정 시 택1
├── 30-knowledge/          # 지식 아카이브
│   ├── 31-claude-code/    # Claude Code 활용 가이드
│   └── 32-marketing/      # 마케팅 실무 가이드
├── 40-schedule/           # 일정관리
│   ├── 41-daily/          # 일별 기록 (할일 포함, 자유롭게 작성)
│   ├── 42-weekly/         # 주간 리뷰
│   └── 43-todos/          # 할일 자동 정리 (daily 기록에서 Claude가 추출)
├── 50-resources/          # 참고 자료
└── 90-archive/            # 완료/중단 항목
```

`.claude/skills/`, `.claude/agents/`는 기본 제공하지 않습니다 — 필요할 때 직접 만들어 쓰는 확장 영역입니다.

---

## 3. Slash Commands (11개)

### 초기 설정
| 커맨드 | 설명 |
|--------|------|
| `/setup-workspace` | 대화형 CLAUDE.md 자동 생성 + 초기 설정 (20-operation 용도도 이때 선택) |
| `/setup-google-calendar` | Google Calendar 연결 (OAuth, 선택) |

### Daily Workflow
| 커맨드 | 설명 |
|--------|------|
| `/daily-note` | 오늘 Daily Note 생성/열기 |
| `/daily-review` | 어제/오늘 변경사항 분석 |
| `/todo` | 할일 빠른 캡처 + 목록 조회/관리 (daily 기록에서 자동 추출도 겸함) |

### AI 활용 (Orchestration)
| 커맨드 | 설명 |
|--------|------|
| `/thinking-partner` | AI와 대화하며 생각 발전 (소크라테스식 질문) |
| `/gather` | 정보 수집 모드 (구조화된 질문 생성) |
| `/reframe` | 이해 확인 모드 (대화 요약 및 확인) |
| `/truth` | 사실 기반 분석 모드 (객관적 분석) |

### 지식 관리 / 시스템
| 커맨드 | 설명 |
|--------|------|
| `/idea [카테고리]` | 대화에서 아이디어 추출 후 `30-knowledge/`에 저장 |
| `/create-command` | 커스텀 슬래시 커맨드 생성 |

---

## 4. Templates

`00-system/01-templates/`에 기본 템플릿(Daily/Weekly/Project)과, 오피스원 주식회사 가상 시나리오 기반 업종별 분석 프레임워크 6종(고객분석/직원만족도/경영보고/재고분석/마케팅ROI/매출분석)을 제공합니다.

---

## 5. 핵심 기능 연결도

```
┌─────────────────────────────────────────────────────────────┐
│                    INITIAL SETUP                            │
│  /setup-workspace → 대화형 정보 수집 → CLAUDE.md 자동 생성  │
│                   → 20-operation 용도(HR/반복업무) 선택      │
└─────────────────────────────────────────────────────────────┘
                              │
                              v
┌─────────────────────────────────────────────────────────────┐
│                    DAILY WORKFLOW                            │
│  /daily-note → 41-daily에 자유 기록 (할일 포함)              │
│  /todo → 기록에서 할일 자동 추출·정리 → 43-todos             │
│  /daily-review → 변경사항 분석 → 우선순위 제안               │
└─────────────────────────────────────────────────────────────┘
                              │
                              v
┌─────────────────────────────────────────────────────────────┐
│                ORCHESTRATION COMMANDS                        │
│  /gather → 정보 수집 (구조화된 질문)                         │
│  /reframe → 이해 확인 (대화 요약)                            │
│  /truth → 사실 기반 분석 (객관적 평가)                       │
│  /thinking-partner → 소크라테스식 대화                       │
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
/daily-note          # 아침: 오늘 계획
/todo                # 오늘 할 일 확인/추가
/daily-review        # 저녁: 하루 정리
```

### 생각 정리가 필요할 때
```bash
/thinking-partner    # 소크라테스식 대화
/gather              # 정보 수집
/reframe             # 이해 확인
/truth               # 사실 기반 분석
```

---

## 7. 원본 대조 (`_originals/`)

`00-system/_originals/`에는 이 워크스페이스가 원본 imi-workspace에서 파생될 때 내용을 고쳐 쓴 문서들의 수정 전 버전이, 원래 상대 경로 그대로 보존되어 있습니다. 무엇이 왜 바뀌었는지 대조하고 싶을 때 참고하세요.

---

## 8. Credits

원본 구조는 [Rhim80/imi-workspace](https://github.com/Rhim80/imi-workspace) (이림/hovoo)에서 파생되었습니다.

**Made with Claude Code**
