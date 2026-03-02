# 응급처치 디버깅 센터 (Troubleshooting Guide)

"뭐야 이거 안 되잖아!" 할 때 찾아보는 빨간약 가이드입니다.

---

## 초기 셋업(설치) 지옥 벗어나기

### 현상: "command not found: claude" (명령어를 못 찾겠대요)

**상황:**

```bash
$ claude
zsh: command not found: claude
```

**왜 이래요?**

- 글로벌(-g 옵션)로 제대로 안 깔았을 때.
- 설치하고 터미널을 안 껐다 다시 켰을 때.
- npm 전역 폴더가 내 맥/리눅스 환경변수(PATH)에 안 잡혔을 때.

**응급 처방:**

**처방 1: 글로벌 설치 강타**

```bash
npm install -g claude-code
```

**처방 2: 터미널 껐다 켜기 (재부팅의 마법)**
터미널 창(혹은 iTerm2) 끄고 쌩으로 다시 켜보세요.

**처방 3: npm 경로 PATH 등록 멱살 잡기**

```bash
npm config get prefix
```

이걸 치면 나오는 경로의 `/bin`을 구경하신 다음, 당신의 `~/.bashrc` 혹은 `~/.zshrc` 맨 아래에 이걸 때려 넣으세요:

```bash
export PATH="$PATH:$(npm config get prefix)/bin"
```

그리고 터미널 껐다 켜거나 `source ~/.zshrc` 때리세요.

---

### 현상: 설치할 때 "Permission denied" (권한 없다고 내쫓김)

**상황:**

```bash
npm install -g claude-code
# Error: EACCES: permission denied
```

**응급 처방:**

**처방 1: npx 로 숟가락만 얹기 (가장 안전)**
설치 에러 나면 스트레스 받지 말고 매번 이걸로 부팅시키세요:

```bash
npx @anthropic-ai/claude-code
```

**처방 2: npm 폴더 주인 권한 내 걸로 뺏기**

```bash
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
export PATH=~/.npm-global/bin:$PATH
```

저 마지막 `export` 줄을 쉘 파일(`~/.zshrc` 등)에 넣어서 저장시키세요.

**(※ 경고: 처방 3 `sudo npm install -g ...` 같은 무지성 sudo는 웬만하면 쓰지 마세요. 나중에 권한 죄다 다 꼬여서 피눈물 납니다.)**

---

### 현상: Node.js 버전 틀딱 에러

**상황:**

```
Error: Claude Code requires Node.js 18 or higher
```

**응급 처방:**
노드 버전이 선사시대 유물입니다. 18버전 이상을 깔아야 해요.

**nvm 쓰세요 (무조건 추천):**

```bash
# nvm 설치 안 되어 있으면:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# 최신 쌩쌩한 노드 다운받아 꽂아넣기:
nvm install node
nvm use node
```

아니면 걍 [nodejs.org](https://nodejs.org) 가서 LTS 버튼 클릭해서 다운받아 까셔도 됩니다.

---

## API 키 관련 절망

### 현상: API 키를 도대체 찾을 수가 없대 (Not found)

**상황:**

```
Error: ANTHROPIC_API_KEY environment variable not set
```

**응급 처방:**
내 지갑(API 통장)을 연동 안 한 겁니다.

**처방 1: 이번 한 번만(일회용) 적용**

```bash
export ANTHROPIC_API_KEY="sk-ant-...내키값..."
```

**처방 2: 터미널 프로필에 영구 문신 박기**
`~/.zshrc` (또는 `~/.bashrc`)를 열어서:

```bash
export ANTHROPIC_API_KEY="sk-ant-...내키값..."
```

저장 후 빠져나와서 `source ~/.zshrc` 치기!

**처방 3: Claude 자체 Config 금고에다 맡기기**

```bash
claude config set apiKey "sk-ant-...내키값..."
```

---

### 현상: 님 API 키 구라래요 (Invalid API key)

**상황:**

```
Error: Invalid API key
```

**응급 처방:**

- 오타 났거나,
- 복붙할 때 앞뒤 공백(Space) 같이 복사했거나,
- 정지 먹었거나.

해결: [console.anthropic.com](https://console.anthropic.com) 접속해서 싹 지우고 "Create Key" 새삥 발급받아서 붙여넣으세요. 무조건 `sk-ant-` 로 시작해야 합니다!

---

### 현상: 앵꼬 났습니다 (Insufficient credits)

**상황:**

```
Error: Insufficient credits in your account
```

**응급 처방:**
돈이 터졌습니다. (클로드 코드는 프로(Pro) 구독과 완전 별개로 쓴 만큼 요금 내는 종량제 지갑입니다. [console.anthropic.com] 가서 카드 등록해서 5달러라도 선불 충전하세요. 아니면 빌드 제한 걸립니다.)

---

## 한창 런타임 중에 클로드가 뻗을 때 (Freezes/Hangs)

### 현상: 클로드가 아무 말도 안 하고 걍 대뇌가 멈춤

**상황:**
엔터 쳤는데 커서도 안 깜빡이고 3분간 응답도 없음. 아 미치겠네.

**응급 처방:**

**처방 1: 와이파이 벽돌됐는지 확인**

```bash
ping anthropic.com
```

**처방 2: 인내심 게이지 확장**
덩치가 큰 코드면 생각하는데 오래 걸립니다. 타임아웃 길게 부팅하세요.

```bash
claude --timeout 300
```

**처방 3: 그냥 모가지 비틀고 재부팅**
`Ctrl + C` 누르면 백그라운드로 도망갑니다. 종료 후 껐다 켜세요.

**처방 4: 귀신 들린 백그라운드 잡(Job) 죽이기**

```bash
/tasks
# 리스트 띄우고 지가 혼자 좀비처럼 도는 애들 모조리 폭파시키세요.
```

---

### 현상: "Rate limit exceeded" (호출 속도 제한 걸림)

**상황:**

```
Error: Rate limit exceeded. Please try again later.
```

**응급 처방:**
앤스로픽 서버에서 "너 너무 많이 쏴대서 방어벽 쳤어" 하는 겁니다.

- **해결책 1:** 60초간 커피 마시고 진정하세요.
- **해결책 2:** 짜잘하게 10번 프롬프트 쏘지 말고 메모장에 장황하게 10줄 묶어서 거대하고 뚱뚱한 프롬프트 한 덩어리로 던지세요.

---

### 현상: "아 툴이 안 돌아간다고!!!" (Tool execution failed)

**상황:**
Bash 명령어나 파일 Edit 수술 툴이 에러를 뿜으며 뒤짐.

**응급 처방 (파일 툴):**

- 파일 위치가 꼬인 겁니다. "상대경로" 말고 리눅스 최상단부터 시작하는 "절대경로(/Users/.../project)"를 던져주세요.

**응급 처방 (터미널 Bash 툴):**

- 명령어 오타 치고 뻗은 겁니다.
- `이 터미널 명령어 네가 날려먹은 거 도대체 뭐가 에러냐 설명 좀 해`
- 아니면 직접 클로드 앱 잠깐 끄고 내 터미널에서 그 명령어 직접 쳐보고 뭐가 에러인지 눈으로 확인하세요.

---

## 깃(Git) 연동 붕괴 사태

### 현상: Git 어쩌고저쩌고 뻑남

**상황:**

```
Error: fatal: not a git repository
```

**응급 처방:**
Git 관리 소속이 아닌 그냥 깡통 폴더에서 뻘짓하는 겁니다.

```
여기에 git init 초기화 구동시켜 줘!
```

또는 수동으로 `git init`.

### 현상: 커밋(Commit)이 안 먹어요 (Please tell me who you are)

**상황:**

```
Error: Please tell me who you are
```

**응급 처방:**
깃허브 로그인(아이디/비번) 연동을 내 로컬 환경에 안 박아놓은 초보자 실수입니다.

```bash
git config --global user.name "내 깃헙 닉네임"
git config --global user.email "가입한내@이메일.com"
```

명령어 치고 나면 커밋 잘 됩니다.

---

## 🐶 무적의 사소한 꿀팁 (Prevention & Get More Help)

1. **깃은 생명줄입니다:** 클로드한테 거대한 파일 수정 메스 맡기기 직전엔 **무.조.건.** 깃 커밋(Commit '방금까지멀쩡했던본진') 박아두고 지시 내리세요. 수정하다 말아먹으면 5분 전 커밋 백업본 가져오면 그만입니다.
2. **에러 나면 무조건 문맹(Blind) 탈출:** 터미널 에러 안 읽고 그냥 '에러 나는데?' 던지지 마시고, 콘솔창 메시지를 드래그 복사해서 "이 에러가 뭔 소린지 초딩에게 알려주듯 한글로 번역 통역해 봐" 라고 윽박지르면 100% 자기가 짠 코드에서 무슨 짓을 해서 터진 건지 잡아냅니다.
3. **그래도 뻗으면 직접 GitHub 포럼 가기:** [Claude Code GitHub Issues](https://github.com/anthropics/claude-code/issues) 여기가 본진 수리센터입니다. 당신이 겪는 에러는 무조건 지구상 다른 누군가가 여기다 영어로 질문해 놨습니다. 가서 구글번역기 돌려보고 따라 하세요.
