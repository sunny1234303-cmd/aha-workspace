---
description: 할일 빠른 캡처 + 조회/관리를 한 커맨드로 (daily 기록 자동 추출 포함)
argument-hint: "[내용] 또는 today/project/overdue/stats (비우면 전체 보기)"
allowed-tools: Read, Write, Edit, Bash
---

`/todo`는 할일 추가와 조회를 모두 처리합니다. 저장 위치: `40-schedule/43-todos/active-todos.md`

**인자에 따라 동작 분기:**

## 인자 없음 + 텍스트 내용 (`/todo [내용]`)

Todo를 추가합니다.

1. 우선순위 태그 파싱: `[urgent]`/`[high]` → high, `[low]` → low, 없으면 normal
2. 프로젝트 태그 파싱: `[프로젝트명]`
3. `40-schedule/43-todos/active-todos.md`의 "📥 Inbox" 섹션에 추가:
   ```markdown
   - [ ] [내용]
     - added: YYYY-MM-DD HH:mm
     - context: [현재 작업 파일/디렉토리]
     - priority: [high/normal/low]
     - project: [있으면]
   ```
4. 확인 메시지: "✅ Todo 추가됨: [내용]"

## 인자 없음 (그냥 `/todo`)

`active-todos.md`를 읽어 Inbox/Today/Overdue 섹션별로 요약 출력.

## `/todo today`

Today 섹션을 우선순위(high→normal→low)로 정렬해 출력.

## `/todo project`

`project:` 필드로 그룹화해서 출력.

## `/todo overdue`

`added:` 기준 7일 이상 지난 항목을 오래된 순으로 출력.

## `/todo stats`

전체 개수, 우선순위별/프로젝트별/상태별 통계, 완료율(`completed-todos.md` 대비) 출력.

## daily 기록에서 자동 추출

`40-schedule/41-daily/`의 오늘 기록에 할일로 보이는 문장("~해야 함", "~하기", 체크박스 등)이 있고 아직 `active-todos.md`에 없으면, 실행 시점에 자동으로 찾아서 Inbox에 추가하고 알려주세요: "📌 오늘 기록에서 할일 N개를 찾아 추가했어요."

## 완료 처리

`- [x]`로 체크된 항목은 `completed-todos.md`로 옮겨 아카이빙합니다.
