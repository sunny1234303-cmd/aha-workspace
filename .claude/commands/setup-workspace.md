---
description: 대화형으로 CLAUDE.md 자동 생성 + 초기 설정
allowed-tools: Read, Write, Edit, Bash
---

aha-workspace를 처음 사용할 때 실행하는 대화형 설정 도구입니다.
**CLAUDE.md를 자동으로 생성**하여 Claude가 프로젝트 맥락을 이해할 수 있게 합니다.

---

## 실행 흐름

### Step 1: 환영 및 안내

```
안녕하세요! aha-workspace 초기 설정을 시작합니다.

몇 가지 질문을 통해 CLAUDE.md 파일을 자동 생성해드릴게요.
이 파일은 Claude가 당신의 프로젝트 맥락을 이해하는 핵심 파일입니다.

준비되셨으면 진행할게요!
```

---

### Step 2: 사용자 정보 수집 (대화형, 하나씩 질문)

#### Q1. 이름
```
이름이 어떻게 되세요?
```

#### Q2. 역할/직업
```
어떤 일을 하고 계세요? (예: 마케터, 프리랜서, 학생 등)
```

#### Q3. 주요 관심사
```
주로 어떤 분야에 관심이 있으세요? (예: 마케팅, 프로젝트 관리, 글쓰기, 자동화 등)
```

#### Q4. 워크스페이스 용도
```
이 워크스페이스를 어떤 용도로 사용하실 건가요?
(예: 개인 업무 관리, 프로젝트 문서화, 학습 기록, 아이디어 정리 등)
```

#### Q5. 20-operation 용도

```
20-operation 폴더를 어떤 용도로 쓰실 건가요?
1) HR (입사/퇴사 등 인사 업무)
2) 일상 반복 업무 (보고, 콘텐츠 발행 루틴 등)
```

답변에 따라:
- 1번 선택 → `20-operation/_templates/hr/`의 파일들을 `20-operation/21-hr/`로 복사
- 2번 선택 → `20-operation/_templates/routines/`의 파일들을 `20-operation/21-routines/`로 복사

---

### Step 3: CLAUDE.md 자동 생성

`CLAUDE.md.template`을 읽어서, 수집한 정보로 채운 뒤 워크스페이스 루트에 `CLAUDE.md`로 저장합니다. 기존 CLAUDE.md가 있으면 덮어쓸지 먼저 확인하세요.

`CLAUDE.md.template`에서 채울 항목:
- 사용자 프로필 (이름/역할/관심사)
- 워크스페이스 목적
- 20-operation 용도 체크박스 (Step 2의 Q5 답변 반영)

---

### Step 4: 필수 폴더/파일 생성

1. **첫 Daily Note 생성**
   - 경로: `40-schedule/41-daily/{YYYY-MM-DD}.md`
   - 템플릿: `00-system/01-templates/daily-note-template.md` 사용

2. **할 일 파일 확인**
   - 경로: `40-schedule/43-todos/active-todos.md`
   - 이미 빈 템플릿으로 존재 — 없으면 새로 생성

---

### Step 5: 완료 안내

```
설정이 완료되었습니다! 🎉

생성된 파일:
- CLAUDE.md (프로젝트 컨텍스트)
- 40-schedule/41-daily/{오늘날짜}.md (첫 Daily Note)
- 20-operation/21-hr/ 또는 21-routines/ (선택하신 용도)

다음 단계:
1. `/daily-note` - 매일 Daily Note 작성
2. `/thinking-partner` - 생각 정리가 필요할 때
3. README.md - 폴더 구조 자세히 알아보기

궁금한 점이 있으면 언제든 물어보세요!
```

---

## 주의사항

- **하나씩 질문**: 한 번에 여러 질문하지 않기
- **간단하게**: 복잡한 설명 없이 핵심만
- **덮어쓰기 확인**: 기존 CLAUDE.md가 있으면 반드시 확인
- **경로 정확히**: CLAUDE.md는 워크스페이스 루트에 생성

---

## 재실행

언제든 `/setup-workspace`로 다시 실행 가능합니다.
기존 CLAUDE.md가 있으면 덮어쓸지 물어봅니다.
