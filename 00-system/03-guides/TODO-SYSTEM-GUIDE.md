# 🎯 Todo Management System - Quick Start Guide

> `/todo` 하나로 캡처부터 조회까지 끝내는 통합 Todo 관리 시스템

---

## ⚡ 빠른 시작

### 1. Todo 추가하기
```bash
/todo 클라이언트 계약서 검토
/todo [urgent] 세무 신고 마감 확인
/todo [project-a] 랜딩페이지 문구 수정
```

### 2. Todo 확인하기
```bash
/todo              # 전체 보기
/todo today        # 오늘 할 일만
/todo project       # 프로젝트별
/todo overdue       # 오래된 것들
/todo stats         # 통계
```

### 3. 매일 아침 루틴
```bash
/daily-note         # 오늘 기록 시작 (할일도 여기 섞어서 적기)
/daily-review        # 어제-오늘 변경사항 + Todo 상태 체크
```

`/daily-note`에 자유롭게 적은 기록에서 Claude가 할일로 보이는 항목을 자동으로 찾아 `43-todos/active-todos.md`에 정리해줍니다. 굳이 "이건 할일, 이건 기록"으로 나눠 적지 않아도 됩니다.

---

## 🎨 시스템 구조

```
Claude Code Workspace
└── /todo  → 추가 · 조회 · 통계를 한 커맨드로

저장 위치:
40-schedule/43-todos/
├── active-todos.md        # 중앙 저장소 ⭐
├── completed-todos.md     # 완료 아카이브
└── README.md               # 상세 가이드
```

---

## 💡 핵심 기능

### 자동 저장되는 정보
- **추가 시각**: 언제 추가했는지
- **컨텍스트**: 어디서 작업하다 추가했는지
- **우선순위**: urgent/high/normal/low
- **프로젝트**: 어떤 프로젝트와 연결됐는지

### daily 기록에서 자동 추출
`41-daily/`에 하루 기록을 자유롭게 쓰면, `/todo` 실행 시 Claude가 "~해야 함", "~하기" 같은 할일성 문장을 찾아 `active-todos.md`로 옮겨 정리합니다.

---

## 📊 실전 시나리오

### 시나리오 1: 작업 중 Todo 생각남
```
작업 중 "아, 이거 나중에 처리해야지" 싶은 게 생김
→ /todo 계약서 서명 요청 보내기
→ 2초 만에 저장 완료, 계속 작업
```

### 시나리오 2: 매일 아침 체크
```
9:00 AM
→ /daily-review 실행
→ 📋 Todo 상태:
   - 미처리: 7개
   - 오늘 할 일: 3개
   - 지연: 2개 ⚠️
→ 오늘 할 것 선택 → 실행
```

### 시나리오 3: 프로젝트별 정리
```
/todo project
→ project-a 관련 4개 발견
→ 한 번에 모아서 처리
```

---

## 🎯 사용 예시

```bash
# 기본
/todo 클라이언트 미팅 자료 준비

# 우선순위 지정
/todo [urgent] 세무사 자료 제출
/todo [low] 사무실 정리

# 프로젝트 지정
/todo [project-a] 랜딩페이지 문구 수정

# 복합
/todo [urgent] [project-a] 오늘까지 시안 확정
```

```bash
# 전체 보기 (섹션별)
/todo
→ 📥 Inbox / 🎯 Today / ⚠️ Overdue

# 오늘 할 일만
/todo today

# 프로젝트별 그룹화
/todo project

# 오래된 것들
/todo overdue

# 통계
/todo stats
→ 총 15개, High 3 / Normal 10 / Low 2, 완료율 68%
```

---

## 🔧 커스터마이징

### active-todos.md 직접 편집

파일 위치: `40-schedule/43-todos/active-todos.md`

```markdown
## 📥 Inbox (처리 안 한 것들)
- [ ] 계약서 서명 요청 보내기
  - added: 2026-01-15 15:23
  - context: 41-daily/2026-01-15.md
  - priority: high
  - project: project-a

## 🎯 Today (오늘 할 일)
← 매일 아침 여기로 이동

## ⚠️ Overdue (오래된 것들)
← 자동 감지 (1주일 이상)
```

### 체크박스 사용

```markdown
- [x] 완료된 Todo  ← 완료 시 x 입력, completed-todos.md로 아카이빙
```

---

## 💪 활용 팁

1. **컨텍스트 추적**: "이 Todo를 왜 추가했지?" → context 필드에서 어느 daily 기록에서 왔는지 확인
2. **프로젝트 묶음 처리**: `/todo project`로 모아서 한 번에
3. **우선순위 관리**: `/todo today`에서 high → normal → low 순으로
4. **Overdue 주기적 체크**: 주 1회 `/todo overdue`로 방치된 항목 정리

---

## 📚 상세 문서

- [40-schedule/43-todos/README.md](../../40-schedule/43-todos/README.md)
- 커맨드 도움말: `.claude/commands/todo.md`, `.claude/commands/daily-review.md`
