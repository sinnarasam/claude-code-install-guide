# Kedance Scientific Skill 설치 및 활용 — Claude Code Cowork

> **소요 시간**: 약 30분
> **준비물**: Claude Code 설치, 빈 폴더 하나, 인터넷 연결
> **이 실습을 마치면 할 수 있어요**: Claude Code에 Kedance Scientific Skill을 직접 설치하고, 과학 계산·문헌 정리 같은 작업을 Skill에게 시킬 수 있어요.

## 0. 시작하기 전에

이 실습에서는 **Kedance Scientific Skill**을 Claude Code에 설치하고, 실제로 한 번 써 봅니다. 처음 보는 단어가 나오면 본문에서 풀어서 설명할 테니, 막히면 잠깐 멈추고 그 부분만 다시 읽어 주세요.

> 💡 **이번 시간의 핵심 개념**: Skill은 **부엌에 붙여 둔 요리 레시피 모음**입니다. Claude가 "지금 이거 만들어야 할 것 같은데?" 하고 알아서 그 레시피를 꺼내 봅니다.

---

## 1. Skill이 뭔가요?

Skill은 Claude Code가 **특정 작업을 잘 하도록 미리 적어 둔 안내문**입니다. 예를 들어 "엑셀 파일을 열어서 합계를 계산해 줘" 같은 요청이 오면, Claude는 자기 가방 속에서 `xlsx` Skill이라는 레시피를 꺼내서 그 순서대로 일을 합니다.

수강생이 직접 매번 "이렇게 하고 저렇게 하고…" 알려주지 않아도 되니까, 같은 종류의 작업이 반복될 때 **시간과 토큰을 크게 아낄 수 있어요**.

> **잠깐, "토큰"이란?**
> Claude가 글자를 처리할 때 쓰는 작은 단위예요. 글이 길어질수록 토큰을 많이 씁니다. Skill을 쓰면 매번 긴 설명을 안 해도 되니까 토큰이 절약되는 거예요.

오늘 우리가 설치할 **Kedance Scientific Skill**은 과학·연구 관련 작업(예: 단위 변환, 문헌 정리, 간단한 데이터 분석 보조)을 위한 Skill입니다. 설치하고 나면 Claude가 관련 질문을 받았을 때 자동으로 이 Skill을 꺼내 씁니다.

> 💡 **레시피 비유로 한 번 더**
> - Skill 설치 = 부엌에 새 레시피 카드 한 장을 붙이기
> - Skill 사용 = "오늘 저녁 뭐 해 먹지?" 했을 때 Claude가 알아서 그 카드를 꺼내 보기
> - Skill 제거 = 안 쓰는 레시피 카드를 떼기

---

## 2. 준비 점검

시작 전에 다음이 다 되어 있어야 해요. 안 되어 있어도 괜찮아요 — 어디서 시작해야 하는지 안내해 둘게요.

- [ ] **Claude Code가 설치되어 있다.**
  - 확인 명령어: `claude --version`
  - 결과로 `1.x.x` 같은 숫자가 보이면 OK입니다.
  - 안 보이면 → [claude-code-install-guide](./claude-code-install-guide.md)부터 보고 와 주세요.
- [ ] **터미널(PowerShell 또는 Terminal)을 켤 수 있다.**
  - Windows: 시작 메뉴 → "PowerShell" 검색
  - macOS: Spotlight(⌘+Space) → "터미널" 검색
- [ ] **빈 폴더 하나를 만들어 두었다.**
  - 예: `C:\Users\내이름\claude-skill-test`
  - 아래 명령어로 만들 수도 있어요.

```powershell
# Windows (PowerShell)
mkdir $HOME\claude-skill-test
cd $HOME\claude-skill-test
```

```bash
# macOS / Linux
mkdir ~/claude-skill-test
cd ~/claude-skill-test
```

> **잠깐, `cd`가 뭐예요?**
> "change directory"의 줄임말이에요. 폴더를 그쪽으로 이동한다는 뜻입니다. 마치 탐색기에서 폴더를 더블클릭해서 들어가는 것과 똑같아요.

---

## 3. 따라하기

### 3-1. Claude Code 켜기

방금 만든 폴더 안에서 Claude Code를 실행합니다.

```powershell
claude
```

**이렇게 나와야 정상이에요** (대략 이런 모양):

```
╭─────────────────────────────────────────╮
│  Welcome to Claude Code                 │
│  Working directory: ...claude-skill-test │
╰─────────────────────────────────────────╯

>
```

> `command not found: claude`가 보이면 → Claude Code 설치가 안 됐거나, 터미널이 설치 경로를 못 찾는 거예요. (자세한 건 5번 참고)

---

### 3-2. 현재 설치된 Skill 목록 확인하기

Claude Code 화면(`>` 프롬프트가 깜빡이는 곳)에서 다음을 입력합니다.

```
/plugin
```

> **잠깐, `/`로 시작하는 건 뭐예요?**
> Slash command(슬래시 명령어)예요. Claude에게 메시지를 보내는 게 아니라, **Claude Code 프로그램 자체에게 명령을 내리는 단축키**입니다. 카톡에서 `/`를 입력하면 이모티콘 검색이 뜨는 것과 비슷한 느낌이에요.

`/plugin`을 치면 현재 설치된 플러그인/Skill 목록을 볼 수 있는 화면이 열립니다. 처음 보면 거의 비어 있거나, 기본 예시 몇 개만 있을 거예요.

---

### 3-3. Kedance Scientific Skill 설치하기

Skill을 설치하는 방법은 크게 두 가지예요. 둘 중 **하나만** 골라서 따라 하세요.

#### 방법 A. 플러그인 마켓플레이스에서 설치 (권장)

Claude Code 안에서 다음 슬래시 명령어를 입력합니다.

```
/plugin marketplace add kedance/scientific
```

> 위 명령어의 `kedance/scientific` 부분은 **Skill 제공처에서 알려준 주소**예요. 실제 주소는 Kedance Scientific 공식 안내(README, 배포 페이지)에서 확인해 주세요. 이 자료에서는 예시로 적어 둔 형태입니다.

마켓플레이스가 등록되면, 그 안의 Skill을 골라서 설치합니다.

```
/plugin install kedance-scientific
```

설치가 시작되면 다음과 같은 메시지가 차례로 보여요.

```
Fetching plugin metadata...
Downloading kedance-scientific...
Verifying...
Installed: kedance-scientific (v0.x.x)
```

> 마지막 줄에 `Installed:`가 보이면 성공입니다!

#### 방법 B. 로컬 파일로 직접 설치

이미 누군가에게 Skill 폴더를 통째로 받았거나, 직접 만든 Skill을 쓰고 싶다면 이 방법을 씁니다.

1. Skill 폴더(예: `kedance-scientific/`)를 다음 위치에 복사합니다.

   - Windows: `C:\Users\내이름\.claude\skills\`
   - macOS/Linux: `~/.claude/skills/`

2. 터미널에서 폴더가 잘 들어갔는지 확인합니다.

```powershell
# Windows
ls $HOME\.claude\skills
```

```bash
# macOS / Linux
ls ~/.claude/skills
```

`kedance-scientific`이라는 폴더 이름이 보이면 OK입니다.

3. Claude Code를 한 번 껐다가(`Ctrl+C` 두 번 또는 `/exit`) 다시 켭니다. Skill은 시작할 때 한 번 읽히기 때문이에요.

---

### 3-4. 설치 확인하기

Claude Code 안에서 다시 `/plugin`을 쳐 봅니다. 또는 더 빠르게:

```
/skill list
```

목록에 **`kedance-scientific`** 또는 **Kedance Scientific** 항목이 보이면 설치 완료입니다.

> 💡 슬래시 명령어 이름이 살짝씩 다를 수 있어요. `/plugin`, `/plugins`, `/skill`, `/skills` 중 작동하는 것으로 확인하세요. Tab 키를 누르면 자동완성도 됩니다.

---

### 3-5. 실제로 한 번 써 보기

Skill은 보통 **사용자가 "이거 해 줘" 하고 자연어로 부탁하면 Claude가 알아서 꺼내 씁니다.** 우리가 굳이 "Kedance Skill 써!" 라고 외칠 필요가 없어요.

Claude Code 화면에 다음을 그대로 입력해 보세요.

```
0.45 mol의 NaCl을 그램으로 환산해 줘. 계산 과정도 같이 보여줘.
```

**이렇게 나와야 정상이에요** (예시 — 실제 출력은 약간 다를 수 있어요):

```
Kedance Scientific 레시피를 사용해 계산할게요.

NaCl의 분자량: 22.99 + 35.45 = 58.44 g/mol
0.45 mol × 58.44 g/mol = 26.298 g

답: 약 26.30 g
```

> Claude가 답을 내면서 **"Kedance Scientific Skill을 사용했다"는 식의 표시**가 같이 보일 수 있어요. 정확한 표현은 버전마다 다릅니다. 표시가 없어도 답만 맞다면 정상이에요.

만약 Claude가 평범하게 답하기만 하고 Skill을 꺼내 쓰는 낌새가 없다면, **3-6**으로 가서 강제로 호출해 봅니다.

---

### 3-6. (필요할 때만) Skill 강제 호출하기

Claude가 알아서 안 꺼낼 때는, **자료에서 어떤 Skill을 쓰는 게 좋은지 명시적으로 지시**해 줄 수 있어요.

```
Kedance Scientific Skill을 써서, 다음 표를 SI 단위로 정리해 줘.

거리: 12 마일
무게: 5 파운드
온도: 98.6 화씨
```

이렇게 적으면 Claude가 **Kedance**라는 단어를 봤기 때문에 해당 Skill을 우선적으로 꺼낼 가능성이 훨씬 높아져요.

---

## 4. 직접 해 보기

> **연습 1**: 단위 변환 부탁해 보기
> Claude에게 *"섭씨 25도가 화씨로 몇 도인지, Kedance Skill로 풀어 줘"* 라고 요청해 보세요.
> 💡 힌트: 답만 받지 말고, *"계산식도 같이"* 라고 추가해 보세요. Skill이 어떻게 일하는지 더 잘 보입니다.

> **연습 2**: 작은 분석 부탁해 보기
> 빈 폴더에 `data.txt` 파일 하나를 만들고, 안에 숫자 몇 개를 줄마다 적어 둡니다. 그리고 Claude에게 *"이 파일의 평균과 표준편차를 구해 줘"* 라고 부탁해 보세요.
> 💡 힌트: 파일 경로를 정확히 알려주면 Claude가 더 빨리 찾아요. `./data.txt` 처럼 적으면 됩니다.

> **연습 3**: Skill 끄고 비교해 보기
> 같은 질문을 두 번 해 보세요 — 한 번은 그냥, 한 번은 *"Kedance Skill 쓰지 말고"* 라고 요청. 답의 분위기가 어떻게 달라지는지 관찰해 봅니다.
> 💡 힌트: Skill이 있으면 답이 더 **정형화·구조화**되어 나올 때가 많아요.

---

## 5. 자주 막히는 곳

| 증상 | 원인 | 해결 |
|---|---|---|
| `command not found: claude` | Claude Code 설치 자체가 안 됐거나, 터미널이 경로를 못 찾음 | [Claude Code 설치 가이드](./claude-code-install-guide.md)로 돌아가서 설치 확인 |
| `/plugin install` 했는데 `not found` | 마켓플레이스 주소가 틀렸거나, 인터넷이 끊김 | 주소 다시 확인 + `ping anthropic.com` 으로 네트워크 점검 |
| `/skill list`에 보이긴 하는데, Claude가 안 씀 | Skill 설명(description)이 현재 요청과 매칭 안 됨 | 3-6처럼 *"Kedance Skill로"* 같이 이름을 명시 |
| 설치는 됐는데 답이 이상함 | Skill 버전이 옛것이거나, 입력 형식이 안 맞음 | `/plugin update kedance-scientific` 후 재시도 |
| Windows에서 `mkdir`은 됐는데 `cd`가 안 됨 | 경로에 한글/공백이 있어서 따옴표가 필요함 | `cd "C:\Users\내 이름\폴더"` 처럼 큰따옴표로 감싸기 |
| Claude Code가 갑자기 멈춤 | 너무 큰 파일을 한꺼번에 다루는 중일 수 있음 | `Ctrl+C` 한 번으로 현재 작업만 취소. 두 번 누르면 종료 |

> 💡 위 표에 없는 에러가 보이면, **에러 메시지를 그대로 복사**해서 강사에게 보여주세요. 메시지를 다시 적느라 글자가 바뀌면 원인을 찾기 어려워져요.

---

## 6. 오늘의 정리

오늘 배운 것을 다시 한 번 정리하면:

- [ ] **Skill은 Claude의 레시피 모음**이다. 같은 종류의 일을 반복할 때 시간·토큰을 아낀다.
- [ ] **Kedance Scientific Skill**을 마켓플레이스나 로컬 폴더에 직접 설치할 수 있다.
- [ ] **`/plugin`, `/skill list`** 같은 슬래시 명령어로 설치 상태를 확인한다.
- [ ] Skill은 **자동으로 꺼내** 쓰지만, 안 꺼내면 **이름을 명시**해서 강제 호출할 수 있다.

**한 줄 요약**: Skill은 부엌의 레시피 카드. 한 번 붙여 두면 Claude가 알아서 꺼내 본다.

**다음 시간 예고**: 다음 회차에서는 **나만의 Skill을 직접 만들어** 보고, 팀원에게 공유하는 방법을 배워요. 오늘 설치한 Kedance Skill의 폴더 구조를 살짝 들여다보면 미리보기가 됩니다.

---

> 🙋 막히면? 강사에게 화면을 보여주거나, 에러 메시지를 그대로 복사해서 물어보세요.
> 정상 동작 화면을 캡처해 두면 다음에 비슷한 문제가 생겼을 때 비교하기 좋습니다.

📅 작성일: 2026.05.15
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
