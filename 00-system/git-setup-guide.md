# Git 연동 설정 가이드

> Claude Code 워크스페이스를 Git으로 버전 관리하기

---

## 왜 Git을 쓰나요?

| 상황 | Git 없이 | Git 사용 |
|------|----------|----------|
| 실수로 파일 삭제 | 복구 불가 | `git checkout`으로 복구 |
| 이전 버전 필요 | 찾을 수 없음 | `git log`로 히스토리 확인 |
| 다른 PC에서 작업 | 파일 복사 필요 | `git pull`로 동기화 |

---

## Step 1: Git 설치 확인

터미널에서 실행:
```bash
git --version
```

**결과 예시**: `git version 2.39.0`

설치 안 되어 있으면:
- **Mac**: `xcode-select --install`
- **Windows**: https://git-scm.com/download/win 에서 다운로드

---

## Step 2: Git 사용자 설정

최초 1회만 설정:
```bash
git config --global user.name "내 이름"
git config --global user.email "내이메일@example.com"
```

**확인**:
```bash
git config --global --list
```

---

## Step 3: 워크스페이스 Git 초기화

### 3-1. 현재 폴더에서 Git 시작

```bash
cd /path/to/aha-workspace
git init
```

### 3-2. .gitignore 확인

이 워크스페이스는 `.gitignore`가 이미 준비되어 있습니다 (`.env`, `CLAUDE.md`, `.DS_Store` 등 자동 제외). 필요하면 패턴을 추가하세요.

### 3-3. 첫 번째 커밋

```bash
git add .
git commit -m "Initial commit: 워크스페이스 초기 설정"
```

---

## Step 4: GitHub 연동 (선택)

### 4-1. GitHub에서 새 저장소 생성

1. https://github.com/new 접속
2. Repository name 입력 (예: `my-workspace`)
3. **Private** 선택 (개인 작업용 — 개인정보가 쌓이는 워크스페이스라면 특히 권장)
4. "Create repository" 클릭

### 4-2. 로컬과 GitHub 연결

GitHub에서 제공하는 명령어 복사해서 실행:
```bash
git remote add origin https://github.com/내계정/my-workspace.git
git branch -M main
git push -u origin main
```

---

## 일상적인 사용법

### 변경사항 저장 (커밋)

```bash
# 변경된 파일 확인
git status

# 모든 변경사항 추가
git add .

# 커밋 (설명 메시지와 함께)
git commit -m "오늘 작업 내용 설명"
```

### GitHub에 업로드

```bash
git push
```

### 다른 PC에서 가져오기

```bash
git pull
```

---

## Claude Code와 함께 사용하기

Claude에게 직접 요청할 수 있습니다:

```
"현재 변경사항 커밋해줘"
"오늘 작업 내용으로 커밋 메시지 만들어서 커밋해줘"
"git status 확인해줘"
```

---

## 자주 쓰는 명령어 요약

| 명령어 | 설명 |
|--------|------|
| `git status` | 현재 상태 확인 |
| `git add .` | 모든 변경사항 스테이징 |
| `git commit -m "메시지"` | 커밋 생성 |
| `git push` | GitHub에 업로드 |
| `git pull` | GitHub에서 다운로드 |
| `git log --oneline` | 커밋 히스토리 간단히 보기 |
| `git diff` | 변경 내용 확인 |

---

## 문제 해결

### "Please tell me who you are" 오류
→ Step 2의 사용자 설정 실행

### "rejected" 오류 (push 실패)
```bash
git pull --rebase
git push
```

### 실수로 커밋한 파일 되돌리기
```bash
git checkout -- 파일명
```

---

## 보안 주의사항

- `.env` 파일은 절대 커밋하지 않기 (API 키 포함)
- `.gitignore`에 민감한 파일 패턴 추가
- 개인 기록·자소서·연락처 등이 쌓이는 폴더(`40-schedule`, `20-operation` 등)를 다루는 저장소는 **Private**로 시작하고, Public으로 공유할 파일만 별도로 골라 옮기세요
- Public 저장소로 전환하기 전에는 `git log`에 남은 과거 커밋에도 민감한 내용이 없는지 확인하세요 (파일만 지운다고 히스토리에서 사라지지 않습니다)

### 자동 보안 점검 (pre-push 훅)

이 워크스페이스는 `git push`할 때마다 개인정보·시크릿 패턴을 자동으로 검사하는 훅(`.githooks/pre-push`)이 포함되어 있습니다. `/setup-workspace`를 실행하면 자동으로 설치되지만, 직접 clone만 했다면 최초 1회 아래 명령을 실행하세요:

```bash
git config core.hooksPath .githooks
```

이후 push할 때 의심 패턴이 발견되면 push가 막히고 안내 메시지가 뜹니다. Claude Code에서 `/security-check`로 확인·조치한 뒤 다시 push하면 됩니다. Public으로 처음 전환하기 전에는 `/security-check history`로 커밋 히스토리까지 검사하세요.

---

*버전 관리는 실수 방지와 협업의 기본입니다.*
