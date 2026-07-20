---
description: 오늘 날짜의 Daily Note 생성 또는 열기 (Google Calendar 연동 시 일정 포함)
allowed-tools: Read, Write, Edit, Bash
---

오늘 날짜의 Daily Note를 생성하거나 열어주세요.

**수행할 작업:**

1. 오늘 날짜 확인 (YYYY-MM-DD 형식)
2. 경로: `./40-schedule/41-daily/YYYY-MM-DD.md`
3. 파일이 없으면:
   - 템플릿 읽기: `./00-system/01-templates/daily-note-template.md`
   - **Google Calendar 연동이 되어 있으면** (`which gcalcli` 확인), 오늘 일정을 가져와 포함:
     ```bash
     gcalcli agenda --tsv
     ```
     TSV 출력을 Markdown 리스트로 변환해 "오늘 일정" 섹션에 추가. 연동 안 되어 있으면 이 섹션은 생략.
   - 변수 치환: `{{date}}`, `{{weekday}}`, `{{yesterday}}`, `{{tomorrow}}`, `{{week}}`
   - 새 파일 생성
4. 파일이 있으면:
   - 현재 내용 표시
   - Google Calendar 연동 시, 일정 업데이트 여부 확인

**참고:**
- 할일도 이 파일에 자유롭게 섞어서 적어도 됩니다 — `/todo` 실행 시 자동으로 찾아 정리합니다.
- Google Calendar 연동은 선택 사항입니다. `gcalcli`를 설치·인증해두면 자동으로 일정을 가져옵니다 (설치 안 했으면 이 부분은 그냥 건너뜁니다).
