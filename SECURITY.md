# Security

이 워크스페이스는 개인 기록·업무 자료가 쌓이는 곳이라 보안 기능을 기본으로 포함합니다.

## 포함된 기능

- **[[security-check|/security-check]]** — 개인정보(주민등록번호·전화번호·이메일 등)와 시크릿(API 키, 토큰, private key)이 저장소에 남아있는지 점검합니다. `history` 인자를 붙이면 커밋 히스토리까지 검사합니다.
- **`.githooks/pre-push`** — `git push`할 때마다 위 패턴을 자동으로 검사하고, 발견되면 push를 막습니다. [[setup-workspace|/setup-workspace]]를 실행하면 자동 설치되고, 직접 clone만 했다면 `git config core.hooksPath .githooks`로 최초 1회 설치하세요.
- 두 기능 모두 **발견만 하고 자동으로 고치지 않습니다** — 조치 전에 항상 확인을 거칩니다.

## Public으로 공개하기 전에

1. [[security-check|/security-check]] history로 커밋 히스토리까지 검사하세요 — 파일을 지워도 과거 커밋에는 내용이 남아있습니다.
2. `.env` 파일이 실수로 추적되고 있지 않은지 `git ls-files | grep .env`로 확인하세요.
3. 제3자(가족, 동료, 고객 등)의 개인정보가 포함된 파일은 정규식으로 못 잡을 수 있으니 직접 훑어보세요.

## 한계

패턴 기반 점검이라 완벽하지 않습니다. 확신이 안 서면 Private 저장소로 유지하거나, 공개 전 사람이 직접 한 번 더 확인하세요.
