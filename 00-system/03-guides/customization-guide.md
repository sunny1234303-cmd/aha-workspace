# 내 직군에 맞게 커스터마이징하기

> 지금 채워진 내용은 "예시"이지 "정답"이 아닙니다

## 왜 이 문서가 필요한가

이 워크스페이스를 처음 열어보면 `30-knowledge/32-marketing/`(GA4, SEO/GEO, 캠페인 용어)처럼 마케팅 실무 내용이 이미 채워져 있습니다. 이건 "이렇게 채워서 쓰면 됩니다"를 보여주는 **작동하는 예시**일 뿐, 마케터가 아니면 필요 없는 내용입니다. 구조와 예시 콘텐츠를 구분해서 봐야 헷갈리지 않습니다.

## 구조 vs 콘텐츠

| 구분 | 유지해야 하는 것 | 갈아끼워도 되는 것 |
|------|-----------------|-------------------|
| **폴더 골격** | `00-system`, `10-projects`, `20-operation`, `30-knowledge`, `70-schedule`, `80-resources`, `90-archive` 번호 체계 | 폴더 안에 뭘 채울지 |
| **커맨드 메커니즘** | `/오늘`, `/gather`, `/truth`, `/idea`, `/security-check`의 동작 방식 | (그대로 써도 됩니다 — 아래 참고) |
| **30-knowledge** | 폴더 존재 자체 | `32-marketing/` → 자기 도메인 지식으로 |
| **20-operation** | HR/반복업무 구조 선택 메커니즘 | `_templates/hr/` 서식 내용 |

## 커맨드는 대부분 그대로 써도 됩니다

`/오늘`, `/gather`, `/truth`, `/idea`, `/security-check`는 도메인 중립적으로 설계돼 있어서 직군과 무관하게 그대로 씁니다. "정보 수집 → 이해 확인 → 사실 기반 분석"이라는 사고 흐름은 마케터든 개발자든 똑같이 유용합니다. 손댈 필요가 있는 건 **커맨드가 아니라 30-knowledge와 20-operation 안의 콘텐츠**입니다.

## 30-knowledge 채우기: 직군별 예시

`30-knowledge/README.md`에 이미 "필요 없으면 지우고, 다른 이름의 폴더로 바꿔 써도 됩니다"라고 되어 있습니다. 감이 안 잡히면 아래를 참고하세요.

| 직군 | `32-marketing/` 자리에 들어갈 폴더 예시 |
|------|--------------------------------------|
| 개발자 | `32-engineering/` — 배포 체크리스트, 코드 컨벤션, 인시던트 회고 |
| 디자이너 | `32-design/` — 컴포넌트 가이드, 브랜드 톤앤매너, 리서치 아카이브 |
| 1인 사업자 | `32-business/` — 세무 일정, 거래처 정보, 계약서 템플릿 |
| 대학원생/연구자 | `32-research/` — 논문 노트, 실험 프로토콜, 인용 관리 |

`31-claude-code/`는 직군과 무관하게 Claude Code 자체를 배우는 폴더라 그대로 두면 됩니다.

## 20-operation 채우기

`CLAUDE.md.template`의 "20-operation 용도"에서 HR / 반복업무 / 둘 다 중 고르면, `_templates/hr/`나 `_templates/routines/`의 서식이 복사됩니다. 이 서식들(`입사신고-template.md` 등)은 일반 사무직 기준 예시이니, 직군에 안 맞으면 `/setup-workspace` 이후 자유롭게 내용을 바꾸세요 — 폴더 구조(21-hr, 22-routines)만 유지하면 됩니다.

## CLAUDE.md 채우기

`/setup-workspace`가 대화형으로 `CLAUDE.md.template`을 채워주지만, 직접 채워도 됩니다. 이때 "활용 용도" 항목에 자기 직군과 워크스페이스로 뭘 하고 싶은지 구체적으로 적을수록, Claude가 `30-knowledge`나 `20-operation`을 채울 때 더 정확하게 맞춰줍니다.

## 체크리스트

새로 시작할 때:
- [ ] `/setup-workspace`로 CLAUDE.md 생성 (이름, 역할, 활용 용도)
- [ ] `30-knowledge/32-marketing/`을 지우거나 자기 도메인 폴더로 교체
- [ ] `20-operation` 용도(HR/반복업무) 선택 및 템플릿 내용 조정
- [ ] 커맨드(`/오늘`, `/gather`, `/truth`, `/idea`, `/security-check`)는 그대로 사용

---

*더 고급 활용(Hooks, MCP 외부 연동)은 [[30-knowledge/31-claude-code/04-hooks-mcp|Hooks & MCP 가이드]] 참고.*
