# 🎯 Todo Management System - Quick Start Guide

> `/오늘` 하나로 오늘 기록부터 할일 캡처·조회까지 끝내는 통합 시스템

---

## ⚡ 빠른 시작

### 1. 하루 시작 (기록 + 할일 자동 정리)
```bash
/오늘
```
오늘 기록을 열고, 그 안에서 할일로 보이는 문장을 자동으로 찾아 정리하고, 지금 할일 상태를 요약해서 보여줍니다.

### 2. 할일만 빠르게 추가
```bash
/오늘 클라이언트 계약서 검토
/오늘 [urgent] 세무 신고 마감 확인
/오늘 [project-a] 랜딩페이지 문구 수정
```

### 3. 할일 조회
```bash
/오늘 today          # 오늘 할 일만
/오늘 project        # 프로젝트별
/오늘 overdue        # 오래된 것들
/오늘 stats          # 통계
```

기록과 할일을 따로 나눠 적을 필요 없습니다 — `71-daily/`에 자유롭게 쓴 내용에서 Claude가 알아서 할일을 찾아 `73-todos/active-todos.md`로 정리합니다.

---

## 🎨 시스템 구조

```
Claude Code Workspace
└── /오늘  → 오늘 기록 + 할일 추가·조회·통계를 한 커맨드로

저장 위치:
70-schedule/
├── 71-daily/YYYY-MM-DD.md   # 오늘 기록
└── 73-todos/
    ├── active-todos.md       # 할일 중앙 저장소 ⭐
    └── completed-todos.md    # 완료 아카이브
```

---

## 💡 핵심 기능

### 자동 저장되는 정보
- **추가 시각**: 언제 추가했는지
- **컨텍스트**: 어디서 작업하다 추가했는지
- **우선순위**: urgent/high/normal/low
- **프로젝트**: 어떤 프로젝트와 연결됐는지

### daily 기록에서 자동 추출
`71-daily/`에 하루 기록을 자유롭게 쓰면, `/오늘` 실행 시 Claude가 "~해야 함", "~하기" 같은 할일성 문장을 찾아 `active-todos.md`로 옮겨 정리합니다.

---

## 📊 실전 시나리오

### 시나리오 1: 작업 중 할일 생각남
```
작업 중 "아, 이거 나중에 처리해야지" 싶은 게 생김
→ /오늘 계약서 서명 요청 보내기
→ 2초 만에 저장 완료, 계속 작업
```

### 시나리오 2: 매일 아침 체크
```
9:00 AM
→ /오늘 실행
→ 오늘 기록 열림 + 📋 할일 상태:
   - 미처리: 7개
   - 오늘 할 일: 3개
   - 지연: 2개 ⚠️
→ 오늘 할 것 선택 → 실행
```

### 시나리오 3: 프로젝트별 정리
```
/오늘 project
→ project-a 관련 4개 발견
→ 한 번에 모아서 처리
```

---

## 🎯 사용 예시

```bash
# 할일 추가
/오늘 클라이언트 미팅 자료 준비
/오늘 [urgent] 세무사 자료 제출
/오늘 [low] 사무실 정리
/오늘 [project-a] 랜딩페이지 문구 수정
/오늘 [urgent] [project-a] 오늘까지 시안 확정
```

```bash
# 조회
/오늘                # 오늘 기록 + 할일 요약
/오늘 today          # 오늘 할 일만
/오늘 project        # 프로젝트별 그룹화
/오늘 overdue        # 오래된 것들
/오늘 stats          # 통계 (예: 총 15개, High 3 / Normal 10 / Low 2, 완료율 68%)
```

---

## 🔧 커스터마이징

### active-todos.md 직접 편집

파일 위치: `70-schedule/73-todos/active-todos.md`

```markdown
## 📥 Inbox (처리 안 한 것들)
- [ ] 계약서 서명 요청 보내기
  - added: 2026-01-15 15:23
  - context: 71-daily/2026-01-15.md
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

1. **컨텍스트 추적**: "이 할일을 왜 추가했지?" → context 필드에서 어느 daily 기록에서 왔는지 확인
2. **프로젝트 묶음 처리**: `/오늘 project`로 모아서 한 번에
3. **우선순위 관리**: `/오늘 today`에서 high → normal → low 순으로
4. **Overdue 주기적 체크**: 주 1회 `/오늘 overdue`로 방치된 항목 정리

---

## 📚 상세 문서

- [70-schedule/73-todos/README.md](../../70-schedule/73-todos/README.md)
- 커맨드 도움말: `.claude/commands/오늘.md`
