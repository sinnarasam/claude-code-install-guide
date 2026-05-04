# 개발자가 꼭 알아야 할 CLI 필수 용어 🖥️

> 검은 화면이 무서워 보이나요?
> CLI는 **"컴퓨터에게 직접 말 거는 외국어"** 예요. 단어 몇 개만 알면 대화가 시작돼요!

---

## 🎯 학습 목표

이 가이드를 다 읽으면 다음을 할 수 있어요:

- ✅ Shell · Terminal · Prompt **헷갈리는 3대장** 구분하기
- ✅ 명령어의 **해부학** (command · option · argument) 읽기
- ✅ 경로(Path), 파이프, 리다이렉션을 **자유자재로 조합**
- ✅ `sudo`, `chmod`, `$PATH` 같은 **약자·기호의 진짜 의미** 파악
- ✅ Claude Code, Git, npm 같은 도구의 **공식 문서를 막힘없이 읽기**

---

## 📑 목차

- [📋 시작하기 전에](#-시작하기-전에)
- [1. Shell · Terminal · Prompt — 헷갈리는 3대장](#1️⃣-shell--terminal--prompt--헷갈리는-3대장)
- [2. 명령어 해부학 — command · option · argument](#2️⃣-명령어-해부학--command--option--argument)
- [3. 경로(Path) — 절대 vs 상대](#3️⃣-경로path--절대-vs-상대)
- [4. 파일·폴더 다루기](#4️⃣-파일폴더-다루기)
- [5. 파이프 · 리다이렉션 — `|`, `>`, `>>`, `2>&1`](#5️⃣-파이프--리다이렉션---)
- [6. 검색의 기술 — grep · find · which](#6️⃣-검색의-기술--grep--find--which)
- [7. 권한 · 환경변수 — sudo · chmod · `$PATH`](#7️⃣-권한--환경변수--sudo--chmod--path)
- [8. 프로세스 · 단축키 — ps · kill · Tab · Ctrl+C](#8️⃣-프로세스--단축키--ps--kill--tab--ctrlc)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🎯 오늘 배운 핵심 정리](#-오늘-배운-핵심-정리)
- [📚 공식 문서](#-공식-문서)
- [🎓 다음 단계](#-다음-단계)
- [🌱 마무리: Fail Forward](#-마무리-fail-forward)

---

## 📋 시작하기 전에

- ✅ 운영체제 어디서든 OK — 🍎 macOS / 🐧 Linux / 🪟 Windows
- ✅ 터미널 앱이 열리는 상태 (Terminal · iTerm2 · Windows Terminal · WSL 등)
- ✅ Claude Code 설치돼 있으면 더 좋아요 → [설치 가이드](./1-1.%20claude-code-install-guide.md)
- ✅ 마음의 준비: **"오타 한 번 났다고 컴퓨터 안 망가져요"** 🌱

> ⏱ **소요 시간**: 약 30~40분 (한 번에 다 외우려 하지 말고 **북마크**로!)
> 🎯 **추천 활용법**: 막힐 때마다 해당 섹션만 다시 펼쳐 보세요

### 🪟 Windows 사용자에게 한마디

이 가이드는 **Bash 계열 명령어**(macOS · Linux · Git Bash · WSL)를 기준으로 해요.
Windows의 PowerShell·CMD는 명령어가 다르지만, **개념은 100% 동일**해요.

| Bash (이 가이드) | PowerShell |
|------------------|------------|
| `ls` | `Get-ChildItem` (alias: `ls`, `dir`) |
| `pwd` | `Get-Location` (alias: `pwd`) |
| `rm` | `Remove-Item` (alias: `rm`, `del`) |
| `cat` | `Get-Content` (alias: `cat`) |

> 💡 PowerShell도 `ls`, `cat`, `pwd` 같은 alias가 대부분 동작해요. 일단 따라 해보세요!

---

## 1️⃣ Shell · Terminal · Prompt — 헷갈리는 3대장

### 🤔 셋이 뭐가 달라요?

처음 CLI를 만나면 이 단어들이 **다 같은 말** 같지만, 실은 역할이 달라요.

```
[ 모니터에 보이는 검은 창 ]   = Terminal (껍데기)
   ↓
[ 명령어를 해석하는 엔진 ]    = Shell    (두뇌)
   ↓
[ 입력 대기 중 표시 ]         = Prompt   (커서 옆 기호)
```

### 🎬 음식점 비유

| CLI 용어 | 음식점 비유 | 하는 일 |
|----------|-------------|---------|
| 🪟 **Terminal** | 식당 건물 | 손님(나)이 들어가서 주문하는 공간 |
| 🧑‍🍳 **Shell** | 주방장 | 주문서 받아서 실제 요리(명령) 처리 |
| 📋 **Prompt** | "주문하시겠어요?" 멘트 | 다음 주문 받을 준비 완료 신호 |

### 🔍 자주 보는 Shell 종류

| Shell | 어디서? | 특징 |
|-------|---------|------|
| **bash** | Linux 기본, macOS 구버전 | 가장 널리 쓰임 |
| **zsh** | macOS 기본 (Catalina+) | bash 호환 + 자동완성 강력 |
| **fish** | 직접 설치 | 입력 시 실시간 추천 |
| **PowerShell** | 🪟 Windows 기본 | 객체 기반, .NET 통합 |
| **cmd.exe** | 🪟 Windows 구식 | 레거시, 거의 안 씀 |

### 🆔 내가 쓰는 Shell 확인

```bash
echo $SHELL     # 결과 예: /bin/zsh
```

> 💡 **기억할 것**: "Terminal에 명령을 입력하면 → Shell이 해석해서 실행 → Prompt가 다시 입력 받을 준비"

---

## 2️⃣ 명령어 해부학 — command · option · argument

### 🦴 모든 명령은 같은 뼈대를 가져요

```bash
git    commit   -m   "first commit"
└─┬─┘  └──┬──┘  └┬┘  └─────┬─────┘
 명령어 서브명령  옵션      인자
```

### 📚 4가지 구성요소

| 이름 | 영어 | 역할 | 예시 |
|------|------|------|------|
| **명령어** | command | 무엇을 할까? | `git`, `npm`, `ls` |
| **서브명령** | subcommand | 어떤 종류? | `git commit`, `npm install` |
| **옵션 / 플래그** | option / flag | 어떻게 할까? | `-m`, `--verbose` |
| **인자** | argument | 무엇에 대해? | `"first commit"`, `./src` |

### 🎚 옵션의 두 얼굴: 짧은 형태 vs 긴 형태

```bash
ls -a              # 짧은 형태 (한 글자, 대시 1개)
ls --all           # 긴 형태 (단어, 대시 2개)
```

| 형태 | 시작 기호 | 길이 | 예시 |
|------|-----------|------|------|
| 짧은 형태 | `-` (대시 1개) | 한 글자 | `-a`, `-h`, `-v` |
| 긴 형태 | `--` (대시 2개) | 단어 | `--all`, `--help`, `--version` |

> 💡 **꿀팁**: 짧은 형태는 **합쳐 쓰기** 가능. `ls -la` = `ls -l -a`

### 🆘 막힐 땐 무조건 `--help`

```bash
git --help
git commit --help
npm install --help
```

> 💡 거의 모든 CLI 도구가 `--help`(또는 `-h`) 옵션을 제공해요. **Claude한테 물어보기 전에 먼저!**

### 🔬 더 자세히: `man` 명령어 (🍎🐧 Unix 계열)

```bash
man ls         # ls의 매뉴얼 페이지
man git        # git 매뉴얼
# 종료: q
# 검색: /키워드
```

---

## 3️⃣ 경로(Path) — 절대 vs 상대

### 🗺 경로는 "주소"예요

파일이 컴퓨터 어디에 있는지 알려주는 **주소 체계**예요.

### 🏠 절대 경로 vs 상대 경로

| 종류 | 의미 | 예시 |
|------|------|------|
| **절대 경로** (Absolute) | "지구 어디서든 찾아갈 수 있는 전체 주소" | `/Users/nara/claude-code-guide/README.md` |
| **상대 경로** (Relative) | "지금 내 위치 기준 주소" | `./README.md`, `../docs/intro.md` |

### 🔣 꼭 알아야 할 4개 기호

```
~       =  내 홈 폴더 (홈 디렉토리)
.       =  현재 폴더
..      =  바로 위 폴더 (부모 폴더)
/       =  최상위 (루트, root)
```

### 🎬 시각화

```
/                          ← 루트 (모든 것의 시작)
└── Users
    └── nara              ← ~ (홈)
        └── claude-code-guide
            ├── README.md  ← ./README.md
            └── src
                └── main.py ← ./src/main.py
                            ← (src 안에서) ../README.md
```

### 🧭 길 찾기 명령어

```bash
pwd                  # 내 현재 위치 출력 (Print Working Directory)
cd ~                 # 홈으로 이동
cd /                 # 루트로 이동
cd ..                # 한 단계 위로
cd -                 # 직전 위치로 (왔다갔다 토글)
cd ./src             # 현재 폴더의 src로
```

> 💡 **꿀팁**: `cd` 입력 후 **Tab 키**를 누르면 자동완성! 폴더 이름 다 안 외워도 OK.

### 🔗 PATH는 또 다른 이야기

`$PATH`는 "**실행파일을 찾는 주소록**"이에요. 자세한 건 [7번 섹션](#7️⃣-권한--환경변수--sudo--chmod--path)에서!

---

## 4️⃣ 파일·폴더 다루기

### 📦 핵심 명령어 한눈에

| 명령어 | 풀이름 | 하는 일 | 예시 |
|--------|--------|---------|------|
| `pwd` | Print Working Directory | 현재 위치 표시 | `pwd` |
| `ls` | LiSt | 폴더 내용 보기 | `ls -la` |
| `cd` | Change Directory | 폴더 이동 | `cd ./src` |
| `mkdir` | MaKe DIRectory | 폴더 만들기 | `mkdir new-folder` |
| `touch` | (시간 도장 찍기) | 빈 파일 만들기 | `touch hello.txt` |
| `cp` | CoPy | 복사 | `cp a.txt b.txt` |
| `mv` | MoVe | 이동 / 이름 변경 | `mv old.txt new.txt` |
| `rm` | ReMove | 삭제 ⚠️ | `rm file.txt` |
| `cat` | conCATenate | 파일 내용 출력 | `cat README.md` |
| `less` | (more보다 less) | 페이지 단위로 보기 | `less long.log` |
| `head` | (앞부분) | 앞 10줄 보기 | `head -n 5 log.txt` |
| `tail` | (뒷부분) | 뒤 10줄 보기 | `tail -f server.log` |

### 🔍 `ls`의 자주 쓰는 옵션

```bash
ls               # 기본 목록
ls -l            # 자세히 (퍼미션·크기·날짜)
ls -a            # 숨김 파일 포함 (.으로 시작하는 파일)
ls -la           # 둘 다 합치기
ls -lh           # 크기 사람이 읽기 쉽게 (KB, MB)
ls -lt           # 시간 순 정렬 (최신부터)
```

### ⚠️ 위험 명령어 BEST 3

```bash
rm -rf <경로>          # ⚠️ 폴더째 강제 삭제 (휴지통 안 거침!)
rm -rf /              # 🚨 절대 금지! 시스템 전체 파괴
> 파일명               # 파일 내용 즉시 비우기
```

> 🆘 **반드시 기억**:
> - `rm`에는 **휴지통이 없어요**. 한 번 지우면 끝!
> - **항상 `pwd`로 위치 확인** 후 삭제
> - 자신 없으면 `rm -i`로 하나하나 확인하며 삭제

### 🎬 자주 쓰는 시나리오

```bash
# 📁 새 프로젝트 시작
mkdir my-project && cd my-project
touch README.md

# 📋 백업 만들기
cp config.json config.json.bak

# 📦 폴더째 복사
cp -r src/ src-backup/

# 📝 파일 끝에 내용 추가하며 모니터링
tail -f /var/log/system.log
```

---

## 5️⃣ 파이프 · 리다이렉션 — `|`, `>`, `>>`, `2>&1`

### 🚰 비유: 수도관과 호스

CLI의 진짜 힘은 **명령어를 호스로 연결해서** 작은 도구를 합치는 거예요.

### 🔀 4대 리다이렉션 기호

| 기호 | 이름 | 하는 일 | 예시 |
|------|------|---------|------|
| `\|` | **파이프** (pipe) | A의 출력 → B의 입력 | `ls \| grep .md` |
| `>` | **출력 리다이렉트** | 결과를 파일로 (덮어쓰기) | `ls > files.txt` |
| `>>` | **출력 리다이렉트 (추가)** | 결과를 파일 끝에 이어붙이기 | `echo "log" >> app.log` |
| `<` | **입력 리다이렉트** | 파일을 명령의 입력으로 | `wc -l < data.txt` |

### 🎬 시각화

```
[ ls ]  ──── 출력 ────▶  [ grep .md ]  ──── 출력 ────▶  화면
       (파이프 |)                      (파이프 |)
```

### 📺 표준 입출력 3형제 (stdin · stdout · stderr)

| 이름 | 번호 | 역할 |
|------|------|------|
| **stdin** (표준 입력) | `0` | 명령으로 들어가는 입력 (보통 키보드) |
| **stdout** (표준 출력) | `1` | 명령의 정상 결과 (보통 화면) |
| **stderr** (표준 에러) | `2` | 명령의 에러 메시지 |

### 🛠 `2>&1`이라는 마법의 주문

```bash
npm install > install.log 2>&1
```

**해석**: "`npm install`의 결과를 `install.log`로 보내고, **에러도 같은 곳으로 합쳐줘**"

| 부분 | 의미 |
|------|------|
| `> install.log` | stdout(1번)을 파일로 |
| `2>&1` | stderr(2번)도 stdout(1번) 가는 곳으로 합치기 |

### 🎬 자주 쓰는 콤보 패턴

```bash
# 🔍 .md 파일만 찾기
ls -la | grep ".md"

# 🔢 줄 수 세기
cat README.md | wc -l

# 🚮 출력 버리기 (조용히 실행)
npm install > /dev/null 2>&1

# 🔍 에러 로그만 따로 저장
npm run build > build.log 2> error.log

# 🔗 여러 단계 체이닝
cat access.log | grep "404" | sort | uniq -c | sort -rn | head -10
#   파일 출력  → 404만 → 정렬 → 중복 카운트 → 역순 → 상위 10개
```

> 💡 **핵심 철학**: "**작은 도구 하나가 한 가지 일만** 잘 하고, **파이프로 합쳐서** 큰 일을 해낸다" — Unix 철학

---

## 6️⃣ 검색의 기술 — grep · find · which

### 🔎 3대 검색 도구

| 명령어 | 무엇을 찾나? | 예시 |
|--------|--------------|------|
| **`grep`** | **파일 내용** 안에서 텍스트 찾기 | `grep "TODO" *.py` |
| **`find`** | **파일 자체**를 이름·크기·날짜로 찾기 | `find . -name "*.md"` |
| **`which`** | **명령어 실행파일** 위치 찾기 | `which python` |

### 🔍 grep — 텍스트 안에서 사냥

```bash
grep "error" log.txt              # log.txt에서 "error" 포함 줄
grep -i "ERROR" log.txt           # 대소문자 무시
grep -r "TODO" ./src              # 폴더 재귀 검색
grep -n "import" main.py          # 줄 번호 같이 표시
grep -v "DEBUG" log.txt           # "DEBUG"가 **없는** 줄만 (반대)
grep -E "error|warn" log.txt      # 정규식 (or 검색)
```

### 🗂 find — 파일 자체 사냥

```bash
find . -name "*.md"               # 현재 폴더에서 .md 파일 모두
find . -type d -name "test*"      # test로 시작하는 폴더만
find . -size +10M                 # 10MB 넘는 파일
find . -mtime -7                  # 최근 7일 내 수정된 것
find . -name "*.tmp" -delete      # 찾고 바로 삭제 ⚠️
```

### 🛤 which / whereis — 명령어 출처 찾기

```bash
which python          # /usr/bin/python
which node            # /usr/local/bin/node
which claude          # Claude Code 실행파일 위치
```

> 💡 **언제 쓰나요?** "분명히 설치했는데 안 돼요" 할 때 → `which`로 진짜 설치돼 있는지 확인!

### 🌟 보너스: 현대적 도구들

| 전통적 | 현대적 대안 | 차이점 |
|--------|-------------|--------|
| `grep` | **`ripgrep`** (`rg`) | 압도적으로 빠름, `.gitignore` 자동 인식 |
| `find` | **`fd`** | 사용법 간단, 컬러 출력 |
| `cat` | **`bat`** | 문법 하이라이트 |
| `ls` | **`eza`** / `lsd` | 컬러 + 아이콘 |

> 💡 Claude Code 자체도 내부적으로 `ripgrep`을 써요. 빠른 이유가 있죠!

---

## 7️⃣ 권한 · 환경변수 — sudo · chmod · `$PATH`

### 🔐 sudo — "잠깐 관리자 권한 줘"

```bash
sudo apt update              # 관리자 권한으로 실행 (Linux)
sudo npm install -g pkg      # 글로벌 설치 시 자주 등장
```

| 단어 | 의미 |
|------|------|
| **sudo** | **S**uper**U**ser **DO** ("관리자로 실행해") |
| **root** | 최고 권한 사용자 (윈도우의 Administrator와 비슷) |

> ⚠️ **주의**: `sudo`는 진짜 필요할 때만! 무지성 `sudo`는 시스템을 위험에 빠뜨려요.

### 🛡 chmod — 파일 권한 바꾸기

```bash
chmod +x script.sh          # 실행 권한 추가
chmod 755 script.sh         # rwxr-xr-x로 설정
chmod -R 644 ./docs         # 폴더 전체 재귀 적용
```

#### 📊 권한 숫자 해석법

```
   r   w   x        rwx의 값
   4 + 2 + 1   =    7   (전부)
   4 + 2 + 0   =    6   (읽기+쓰기)
   4 + 0 + 1   =    5   (읽기+실행)
   4 + 0 + 0   =    4   (읽기만)
   0 + 0 + 0   =    0   (없음)
```

```
chmod 755 file
       │││
       ││└─ 다른 사람 (other)   = 5 = r-x
       │└── 그룹 (group)         = 5 = r-x
       └─── 소유자 (owner)       = 7 = rwx
```

### 🌍 환경변수 (Environment Variable)

**한마디로**: 시스템·터미널이 공유하는 **전역 변수**

```bash
echo $HOME              # 내 홈 경로
echo $USER              # 내 사용자명
echo $PATH              # 명령어 검색 경로
env                     # 모든 환경변수 보기
```

#### 🛤 `$PATH`의 정체

`$PATH`는 **":"로 구분된 폴더 목록**이에요. 명령어를 입력하면 **이 목록 순서대로** 실행파일을 찾아요.

```bash
echo $PATH
# /usr/local/bin:/usr/bin:/bin:/Users/nara/.local/bin
#  └─────┬─────┘ └──┬───┘ └─┬─┘ └──────────┬─────────┘
#        1번         2번    3번         4번 (홈 아래)
```

### ⚙️ 환경변수 설정 (셸별 차이)

| Shell | 설정 파일 | 적용 명령 |
|-------|-----------|-----------|
| bash | `~/.bashrc` (또는 `~/.bash_profile`) | `source ~/.bashrc` |
| zsh | `~/.zshrc` | `source ~/.zshrc` |
| fish | `~/.config/fish/config.fish` | `source ~/.config/fish/config.fish` |
| 🪟 PowerShell | `$PROFILE` | `. $PROFILE` |

#### 📝 일시적 vs 영구적

```bash
# 일시적 (현재 세션만)
export API_KEY="abc123"

# 영구적 (~/.zshrc에 추가)
echo 'export API_KEY="abc123"' >> ~/.zshrc
source ~/.zshrc
```

> 💡 **팁**: API 키처럼 민감한 값은 `~/.zshrc`에 직접 쓰지 말고 `.env` 파일에 두고 dotenv로 불러오세요!

---

## 8️⃣ 프로세스 · 단축키 — ps · kill · Tab · Ctrl+C

### 👀 프로세스 들여다보기

| 명령어 | 하는 일 | 예시 |
|--------|---------|------|
| `ps` | 현재 프로세스 목록 | `ps aux` |
| `top` / `htop` | 실시간 모니터 (작업 관리자) | `top` |
| `kill` | 프로세스 종료 | `kill 1234` |
| `kill -9` | 강제 종료 (최후의 수단) | `kill -9 1234` |
| `pkill` | 이름으로 죽이기 | `pkill node` |

### 🚦 백그라운드 / 포어그라운드

```bash
node server.js &       # 백그라운드 실행 (& 붙이기)
jobs                   # 현재 실행 중인 백그라운드 작업
fg                     # 가장 최근 백그라운드 작업 → 포어그라운드
fg %1                  # 1번 작업 가져오기
bg                     # 멈춘 작업 백그라운드로 보내기
```

### ⌨️ 터미널 필수 단축키

| 단축키 | 의미 | 언제 쓰나요? |
|--------|------|-------------|
| **Tab** | 자동완성 | 파일·명령어·폴더 이름 완성 |
| **Tab Tab** | 가능한 후보 모두 보기 | 선택지 궁금할 때 |
| **↑ / ↓** | 이전 명령 불러오기 | 방금 명령 다시 실행 |
| **Ctrl + C** | 현재 명령 취소 | 무한 루프, 멈췄을 때 |
| **Ctrl + D** | 입력 종료 / 로그아웃 | REPL, 셸 종료 |
| **Ctrl + Z** | 일시정지 (백그라운드로) | 작업 잠깐 멈추고 다른 일 |
| **Ctrl + L** | 화면 지우기 (`clear`와 동일) | 깔끔하게 보고 싶을 때 |
| **Ctrl + R** | 명령 히스토리 검색 | 옛날 쓴 명령 찾기 |
| **Ctrl + A** | 줄 처음으로 | 긴 명령 앞으로 이동 |
| **Ctrl + E** | 줄 끝으로 | 긴 명령 끝으로 이동 |
| **Ctrl + U** | 커서 앞 모두 삭제 | 비밀번호 잘못 쳤을 때 |
| **Ctrl + W** | 단어 하나 삭제 | 오타 빠르게 수정 |

### 📜 history — 내가 쳤던 명령들

```bash
history                # 전체 히스토리
history | tail -20     # 최근 20개
history | grep git     # git 들어간 명령만
!42                    # 42번 명령 다시 실행
!!                     # 직전 명령 다시 실행
sudo !!                # 직전 명령에 sudo 붙여 재실행 ✨
!$                     # 직전 명령의 마지막 인자
```

### 🎯 실전 시나리오

```bash
# 시나리오 1: 무한 루프 / 멈춘 명령 끝내기
^C   (Ctrl+C)

# 시나리오 2: 8080 포트 점유한 프로세스 죽이기
lsof -i :8080          # PID 찾기
kill -9 <PID>          # 강제 종료

# 시나리오 3: 30초 전에 친 긴 명령 다시 쓰기
^R   (Ctrl+R)
# → 검색어 입력 → Enter
```

---

## 🪞 5분 회고

여기까지 따라왔다면 정말 훌륭해요! 잠시 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 가장 오래 헷갈렸던 용어는?**
- Shell vs Terminal vs Prompt?
- 절대경로 vs 상대경로?
- stdout vs stderr?

**2. 오늘 알게 된 약자 풀이 중 가장 인상 깊은 것은?**
- `cd` = Change Directory
- `cat` = conCATenate
- `sudo` = SuperUser DO
- `grep` = **G**lobal **R**egular **E**xpression **P**rint

**3. 평소 무지성으로 쓰던 명령은 뭐였나요?**

### 💭 토론거리

> "GUI(클릭)와 CLI(타이핑) 중 **어느 쪽이 더 빠르다**는 건 사실일까요? 어떤 작업에서?"
> "AI 시대에 CLI는 **사라질까요, 더 중요해질까요**?"

---

## 🆘 자주 막히는 지점

### Q1. `command not found` 에러가 떠요

**A.** 셋 중 하나예요:

```bash
# 1) 아예 설치 안 됨
which <명령어>          # 결과 없으면 설치 필요

# 2) 설치는 됐는데 PATH에 없음
echo $PATH | tr ':' '\n'   # PATH 보기 좋게
# 설치된 폴더가 보이는지 확인

# 3) 새 셸을 안 열었음
source ~/.zshrc          # 설정 다시 로드
```

### Q2. `permission denied` — 권한 거부

**A.** 두 가지 경우로 나눠요:

| 상황 | 해결 |
|------|------|
| **시스템 폴더** (`/usr/local`, `/etc`) | `sudo` 붙이기 |
| **내 파일인데** 실행 안 됨 | `chmod +x 파일명` |

> ⚠️ **무지성 sudo는 위험!** 정말 시스템 영역인지 한 번 더 확인하세요.

### Q3. 한 번에 너무 많은 결과가 쏟아져요

**A.** **파이프로 잘라서 보세요**:

```bash
ls -la | head -20            # 앞 20줄만
git log | less               # 페이지 넘기며 (q로 종료)
npm ls | grep react          # 필요한 것만 추출
```

### Q4. 실수로 `rm -rf`로 중요한 폴더를 지웠어요

**A.** **휴지통이 없어요**. Git으로 버전 관리되는 파일이라면:

```bash
git status              # 삭제된 파일 보임
git checkout HEAD -- <파일>   # 마지막 커밋으로 복구
```

> 💡 **예방법**: `alias rm='rm -i'`로 매번 확인 받기 / 중요 폴더는 항상 Git 관리.

### Q5. `cd ..`을 너무 많이 쳐야 해요

**A.** 점프 도구를 익히세요!

```bash
cd ../../..            # 너무 길어요
# 대안 1
cd ~                   # 홈으로
# 대안 2 (z 같은 도구)
z my-project           # 자주 가는 폴더로 점프
```

### Q6. 따옴표 `'`, `"`, `` ` ``는 뭐가 다른가요?

| 따옴표 | 변수 치환? | 명령 실행? | 예시 |
|--------|-----------|-----------|------|
| `'홑따옴표'` | ❌ 안 함 | ❌ | `echo '$HOME'` → `$HOME` 그대로 |
| `"쌍따옴표"` | ✅ 함 | ❌ | `echo "$HOME"` → `/Users/nara` |
| `` `백틱` `` | — | ✅ 실행 | `` echo `date` `` → 현재 날짜 |
| `$(...)` | — | ✅ 실행 (권장) | `echo $(date)` |

### Q7. Claude Code 안에서도 이 명령들 다 쓸 수 있나요?

**A.** ✅ **네!** Claude Code의 `Bash` 도구가 이 모든 명령을 실행할 수 있어요. 그리고 결과를 자동으로 분석해서 다음 단계를 추천해줘요. 이게 **CLI를 알수록 Claude Code를 잘 쓰는** 진짜 이유예요.

---

## 🎯 오늘 배운 핵심 정리

| 카테고리 | 한 줄 요약 |
|----------|-----------|
| 🪟 Terminal · Shell · Prompt | 화면 / 두뇌 / 입력 신호의 3단 구조 |
| 🦴 명령어 해부 | `command [option] <argument>` |
| 🗺 경로 | `~`(홈) `.`(현재) `..`(부모) `/`(루트) |
| 📦 파일 다루기 | `ls cd cp mv rm cat` 6개면 90% 해결 |
| 🚰 파이프 | `\|`로 작은 도구 합쳐 큰 일 처리 |
| 🔄 리다이렉션 | `>` 덮기 / `>>` 추가 / `2>&1` 에러도 합치기 |
| 🔎 검색 | `grep`(내용) / `find`(파일) / `which`(명령) |
| 🔐 권한 | `sudo`(관리자) / `chmod 755`(rwxr-xr-x) |
| 🌍 환경변수 | `$PATH`는 명령 검색 경로 / `export`로 설정 |
| ⌨️ 단축키 | `Tab`(자동완성) `↑`(이전) `Ctrl+C`(취소) `Ctrl+R`(검색) |

### 💎 가장 중요한 교훈

> **"Unix 철학: 작은 도구 하나가 한 가지 일만 잘 한다.**
> **그리고 파이프로 합치면 못 할 게 없다."**
>
> **"CLI는 외워서 쓰는 게 아니라 `--help`로 찾아 쓰는 거예요."**

---

## 📚 공식 문서

- 🐧 [GNU Coreutils 매뉴얼](https://www.gnu.org/software/coreutils/manual/coreutils.html) — `ls`, `cp`, `mv` 등 표준 명령어
- 🍎 [macOS Terminal 사용자 가이드](https://support.apple.com/guide/terminal/welcome/mac)
- 🪟 [Microsoft Learn — Windows Terminal](https://learn.microsoft.com/windows/terminal/)
- 📘 [Bash 공식 매뉴얼](https://www.gnu.org/software/bash/manual/)
- 📕 [Zsh 공식 문서](https://zsh.sourceforge.io/Doc/)
- 🌐 [explainshell.com](https://explainshell.com/) — 명령어 한 줄 붙여넣으면 옵션마다 해설!

---

## 🎓 다음 단계

축하해요! 🎉 이제 검은 화면이 **무서운 곳**이 아니라 **파워풀한 작업장**으로 보일 거예요.

**바로 적용해볼 만한 것:**

1. 📜 **`history`로 본인이 자주 쓰는 명령 TOP 10** 뽑아보기
2. 🪄 자주 치는 긴 명령은 **alias로 단축**:
   ```bash
   alias gs='git status'
   alias ll='ls -la'
   ```
3. 🔍 `--help`와 `man`을 **검색보다 먼저** 시도해보기
4. 🚰 **파이프 체인 1개 만들기** — 예: `ls | wc -l` (현재 폴더 파일 개수)
5. 📝 본인의 `~/.zshrc` (또는 `~/.bashrc`) **한 번 열어보기**

**더 깊이 배우고 싶다면:**

- 📦 **[Git 입문 (택배 비유)](./git-basics-easy.md)** — 가장 많이 쓰는 CLI 도구
- 🛠 **[Git 명령어 정리](./git-commands.md)** — 빠른 참조 치트시트
- 🩺 **[/status 가이드](./status-reading-guide.md)** — Claude Code 환경 점검
- ✍️ **[효과적인 프롬프트 & CLAUDE.md](./effective-prompting-and-claude-md.md)** — Claude에게 CLI 작업 잘 시키기

---

## 🌱 마무리: Fail Forward

이 가이드를 다 읽고:

> 🟢 **모든 용어가 술술 들어왔다면** — 진짜 명령을 직접 쳐보면서 손에 익혀요!
> 🟡 **반쯤 알고 반쯤 헷갈린다면** — 정상이에요. 책갈피 해두고 막힐 때마다 펼쳐 보세요.
> 🔴 **여전히 검은 화면이 무섭다면** — 괜찮아요. `pwd` 한 번, `ls` 한 번 치는 것부터 시작해도 충분해요.

학습 노트에 적어보세요:

```
✏️ 가장 처음 외울 명령어 5개: ___
🔥 평소 무지성으로 쓰던 명령: ___
💡 alias로 단축할 만한 긴 명령: ___
🪄 다음에 시도해볼 파이프 조합: ___
```

CLI는 **하루에 하나씩** 익혀도 충분해요. 한 달 뒤면 완전히 다른 사람이 되어 있을 거예요. 🌱

---

📅 작성일: 2026.05.04
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
