# Setup Google Calendar - 대화형 설정 마법사 (선택 사항)

Google Calendar를 gcalcli로 연결해서, `/daily-note`가 오늘 일정을 자동으로 가져오게 합니다.

## 🎯 수행 작업

### Phase 1: 자동 설치 (Claude가 실행)
1. ✅ pipx 설치 확인 및 설치 (필요 시)
2. ✅ gcalcli 설치
3. ✅ PATH 설정 확인 및 추가 (필요 시)
4. ✅ 설치 확인 테스트

### Phase 2: OAuth 인증 (사용자 필요)
1. 🔐 OAuth 인증 실행 안내
2. 🌐 브라우저 로그인 가이드
3. ✅ 인증 완료 확인

### Phase 3: 테스트 및 완료
1. 📋 캘린더 목록 조회
2. 🎉 완료 메시지

---

## 📋 실행 순서

### Step 1: 환영 메시지

```
안녕하세요! Google Calendar 설정을 시작합니다. 🎉

**소요 시간:** 약 5분
**필요한 것:** Google 계정

이 과정에서 대부분은 자동으로 진행되고,
OAuth 인증만 직접 해주시면 됩니다.

준비되셨으면 'start' 또는 '시작'이라고 입력해주세요.
```

---

### Step 2: 자동 설치 시작

**2-1. pipx 확인:**
```bash
which pipx
```
없으면 자동 설치:

**macOS (Homebrew):**
```bash
which brew
brew install pipx
pipx ensurepath
```

**Linux/WSL:**
```bash
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

설치 후 현재 세션에 PATH 적용:
```bash
export PATH="$HOME/.local/bin:$PATH"
pipx --version
```

---

### Step 3: gcalcli 설치

```bash
which gcalcli
```
없으면:
```bash
pipx install gcalcli
gcalcli --version
```

---

### Step 4: PATH 설정 확인 및 추가

```bash
echo $PATH | grep -q "$HOME/.local/bin" && echo "YES" || echo "NO"
echo $SHELL
```

**zsh 사용자:**
```bash
grep -q 'export PATH="$HOME/.local/bin:$PATH"' ~/.zshrc || echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
export PATH="$HOME/.local/bin:$PATH"
source ~/.zshrc
```

**bash 사용자:**
```bash
grep -q 'export PATH="$HOME/.local/bin:$PATH"' ~/.bashrc || echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
export PATH="$HOME/.local/bin:$PATH"
source ~/.bashrc
```

---

### Step 5: OAuth 인증 안내 (사용자 직접)

```
✅ 자동 설치가 완료되었습니다!

이제 OAuth 인증이 필요합니다. 다음 명령어를 터미널에 복사해서 실행해주세요:

gcalcli init

1. 브라우저가 자동으로 열립니다
2. Google 계정을 선택하세요
3. "허용" 버튼을 클릭하세요
4. "Authentication successful!" 메시지가 나타나면 완료!

브라우저가 자동으로 열리지 않으면 터미널에 표시된 URL을 복사해서 브라우저에 붙여넣으세요.

OAuth 인증을 완료하셨으면 '완료' 또는 'done'이라고 입력해주세요.
```

---

### Step 6: 인증 확인 및 테스트

```bash
ls -la ~/.gcalcli_oauth
```
파일이 있으면 인증 완료. 캘린더 목록 조회 테스트:
```bash
gcalcli list
```

---

### Step 7: 완료 및 안내

```
🎉 Google Calendar 설정이 완료되었습니다!

이제 사용 가능한 기능:

1. Daily Note 자동 통합
   - /daily-note 실행 시 자동으로 오늘 일정 포함

2. 직접 요청
   - "오늘 일정 뭐 있어?"
   - "이번 주 스케줄 알려줘"
   - "내일 오후 3시에 미팅 잡아줘"

3. gcalcli 직접 사용
   gcalcli agenda    # 오늘 일정
   gcalcli calw      # 주간 캘린더
   gcalcli calm      # 월간 캘린더

**테스트해보세요:** "오늘 일정 뭐 있어?"
```

캘린더가 여러 개(업무용/개인용 등)라면, `gcalcli agenda --calendar "캘린더명"`처럼 이름을 지정할 수 있습니다. 자주 쓰는 캘린더 이름을 CLAUDE.md에 적어두면 Claude가 매번 기억합니다.

---

## ⚠️ 오류 처리

### OAuth 인증 실패
```bash
rm ~/.gcalcli_oauth
gcalcli init
```

### "command not found: gcalcli"
```bash
export PATH="$HOME/.local/bin:$PATH"
pipx install --force gcalcli
```

### pipx 설치 실패
```bash
# macOS
brew install python3
# Linux/WSL
sudo apt-get install python3 python3-pip
```

### 브라우저가 열리지 않음
터미널에 표시된 URL을 복사해서 브라우저에 수동으로 붙여넣고 로그인하세요.

---

## 🔄 재실행

```bash
rm ~/.gcalcli_oauth
/setup-google-calendar
```
