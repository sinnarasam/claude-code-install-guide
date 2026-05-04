# 반려 클로드봇 만들기 🤖

> 터미널 안에서 함께 사는 작은 친구를 만들어요.
> 밥을 주면 행복해하고, 자리를 비우면 배고파지는, 진짜 "반려"하는 코드예요.

## 🎯 학습 목표

- ✅ **클래스(OOP)** 로 상태와 행동을 한 곳에 묶는 방법 익히기
- ✅ **시간 흐름** 을 코드에 반영해 자연스러운 변화 만들기
- ✅ **JSON 파일** 로 상태를 저장·복원해 "살아있는" 느낌 주기
- ✅ Claude Code와 **점진적으로 기능을 키우는** 협업 방식 체득

---

## 📑 목차

- [1️⃣ 무엇을 만들까요?](#1️⃣-무엇을-만들까요)
- [2️⃣ 클래스로 봇 뼈대 잡기](#2️⃣-클래스로-봇-뼈대-잡기)
- [3️⃣ 시간이 흐르게: tick 메서드](#3️⃣-시간이-흐르게-tick-메서드)
- [4️⃣ 표정이 살아나게: 상태 → 얼굴](#4️⃣-표정이-살아나게-상태--얼굴)
- [5️⃣ 행동 만들기: 먹이 · 놀이 · 잠 · 쓰담](#5️⃣-행동-만들기-먹이--놀이--잠--쓰담)
- [6️⃣ 기억하기: JSON으로 저장·복원](#6️⃣-기억하기-json으로-저장복원)
- [7️⃣ 메인 루프와 메뉴](#7️⃣-메인-루프와-메뉴)
- [8️⃣ Claude Code와 함께 키우는 팁](#8️⃣-claude-code와-함께-키우는-팁)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🎯 오늘 배운 핵심 정리](#-오늘-배운-핵심-정리)
- [🎓 다음 단계](#-다음-단계)
- [🌱 마무리: Fail Forward](#-마무리-fail-forward)

---

## 📋 시작하기 전에

| 준비물 | 설명 | 가이드 |
|---|---|---|
| Python 3.8+ | 표준 라이브러리만 사용 | [Python 계산기 만들기](./1-5.python-calculator-tutorial.md) |
| Claude Code | 함께 코딩할 짝꿍 | [설치 가이드](<./1-1. claude-code-install-guide.md>) |
| 프롬프트 감각 | "한 입씩" 요청하는 습관 | [효과적인 프롬프트 & CLAUDE.md](./effective-prompting-and-claude-md.md) |

> 💡 이 가이드는 **계산기 튜토리얼** 다음 단계로 추천드려요. 클래스를 처음 다룬다면 [Python 계산기 만들기](./1-5.python-calculator-tutorial.md)를 먼저 가볍게 훑고 오세요.

---

## 1️⃣ 무엇을 만들까요?

🎬 **시나리오:** 터미널을 열고 `python claude-pet.py`를 입력하면, 작은 클로디(이름은 마음대로)가 깨어나서 우리를 기다려요. 자리를 비우면 배가 고파지고, 놀아주면 행복해지고, 친밀도가 쌓여요.

```
╭──────────────────────────────────╮
│           (◕‿◕✿) 헤헤             │
╰──────────────────────────────────╯
  이름:   클로디    (생일로부터 3일째 🎂)
  배고픔: ███░░░░░░░  30%
  기분:   ████████░░  82%  (행복해요)
  에너지: ██████░░░░  64%
  친밀도: ❤️ ❤️ ❤️ ❤️  (24)
```

### 🧩 어떤 부품들이 필요할까요?

| 부품 | 역할 | 비유 |
|---|---|---|
| **상태(state)** | 배고픔·기분·에너지 등 숫자 | 다마고치의 눈금 |
| **행동(method)** | 먹이주기·놀기·재우기 | 버튼 |
| **시간(tick)** | 자리 비운 만큼 자연 변화 | 시계 |
| **얼굴(face)** | 상태에 따라 바뀌는 표정 | 표정 거울 |
| **저장(save/load)** | JSON 파일에 기억 | 일기장 |

> 💡 **핵심 비유:** 클래스는 **캐릭터 시트**예요. 능력치(필드)와 할 수 있는 행동(메서드)을 한 종이 위에 묶어 두는 거예요. TRPG 캐릭터 시트처럼요.

---

## 2️⃣ 클래스로 봇 뼈대 잡기

먼저 가장 단순한 형태부터 시작해요. 상태 변수 몇 개만 들고 있는 빈 클래스예요.

```python
class ClaudePet:
    def __init__(self, name="클로디"):
        self.name = name
        self.hunger = 30   # 0(배부름) ~ 100(아주 배고픔)
        self.mood = 70     # 0(우울) ~ 100(행복)
        self.energy = 80   # 0(녹초) ~ 100(쌩쌩)
        self.affection = 0 # 친밀도 누적값
```

### ❓ 왜 클래스인가요?

| 클래스 없이 (변수만) | 클래스로 묶기 |
|---|---|
| `hunger = 30`, `mood = 70`, … 흩어짐 | 한 객체 안에 모임 |
| 봇이 2마리면 변수 6개 됨 | `pet1`, `pet2` 따로 만들면 끝 |
| 함수에 매번 모든 값 넘겨줌 | `pet.feed()` 한 줄 |

> 💡 **Claude Code에 이렇게 부탁해보세요:**
> > "Python으로 ClaudePet 클래스를 만들어줘. 필드는 name, hunger, mood, energy, affection이고 모두 적당한 기본값을 가져."

### 🏋️ 작은 실습

방금 만든 클래스로 봇을 하나 만들고, 상태를 직접 출력해보세요.

```python
pet = ClaudePet("뽀삐")
print(pet.name, pet.hunger, pet.mood)
```

---

## 3️⃣ 시간이 흐르게: tick 메서드

진짜 반려동물처럼 느껴지려면, **자리를 비운 동안에도 변해야** 해요. "마지막으로 본 시각"을 저장해두고, 다음에 켤 때 그 차이만큼 상태를 갱신해요.

```python
import time

class ClaudePet:
    def __init__(self, name="클로디"):
        # ... 위와 동일 ...
        self.last_seen = time.time()

    def tick(self):
        elapsed = time.time() - self.last_seen
        minutes = elapsed / 60
        self.hunger = min(100, self.hunger + minutes * 1.5)
        self.energy = max(0, self.energy - minutes * 1.0)
        if self.hunger > 70 or self.energy < 20:
            self.mood = max(0, self.mood - minutes * 1.2)
        self.last_seen = time.time()
```

### ⚠️ 왜 `min`, `max`로 감싸요?

`hunger`가 100을 넘거나 `energy`가 음수가 되면 이상해져요. **상한·하한 클램핑(clamping)** 은 게임 코드의 단골 패턴이에요.

| 안 막으면 | 막으면 |
|---|---|
| `hunger = 250` 같은 값이 나옴 | 항상 0~100 사이 보장 |
| 표시할 때 `200%` 게이지 깨짐 | UI 안전 |
| 다른 로직에서 또 검사해야 함 | 한 곳에서 끝 |

> 💡 **자연스러운 변화는 "비례"가 핵심.** 상수(1.5, 1.0, 1.2)를 조절해서 봇의 성격을 만들 수 있어요. 자주 배고파지는 식탐 봇, 잠이 많은 봇 등.

---

## 4️⃣ 표정이 살아나게: 상태 → 얼굴

얼굴을 그리는 건 **조건문 사다리** 한 줄이면 돼요. 위에서부터 우선순위 높은 상태를 먼저 잡아요.

```python
def face(self):
    if self.energy < 15:
        return "(￣ω￣) zzZ"
    if self.hunger > 80:
        return "(╥﹏╥) 배고파…"
    if self.mood < 25:
        return "(｡•́︿•̀｡)"
    if self.mood > 85 and self.affection > 20:
        return "(◕‿◕✿) 헤헤"
    if self.mood > 70:
        return "(•‿•)"
    return "( ・_・)"
```

### 🎨 우선순위는 왜 중요할까요?

`if/elif`가 아니라 **각각 `if`로 두고 위에서 return** 하는 패턴이에요. **위에 있을수록 더 시급한 상태**라는 뜻을 코드에 담아요.

> 💡 졸리고(에너지<15) 동시에 행복한(기분>85) 상황이라면? → "졸려서 자야 할 때"가 더 중요하니까 zzZ가 우선이에요.

### ❓ ASCII 얼굴은 어떻게 떠올려요?

| 상황 | 추천 표정 |
|---|---|
| 졸림 | `(￣ω￣) zzZ`, `(˘ω˘)ᶻᶻᶻ` |
| 배고픔 | `(╥﹏╥)`, `(>д<)` |
| 행복 | `(◕‿◕✿)`, `(✿◠‿◠)` |
| 시무룩 | `(｡•́︿•̀｡)`, `(´•ω•̥`)` |

> 💡 **Claude Code에 이렇게 부탁해보세요:**
> > "상태(energy/hunger/mood)에 따라 얼굴을 반환하는 face() 메서드를 만들어줘. 우선순위는 졸림 > 배고픔 > 우울 > 행복 > 평온 순서로."

---

## 5️⃣ 행동 만들기: 먹이 · 놀이 · 잠 · 쓰담

행동 메서드는 모두 비슷한 모양이에요: **상태 검사 → 능력치 변화 → 대사 반환**.

```python
def feed(self):
    if self.hunger < 10:
        return f"{self.name}: 으윽 배불러… 🤢"
    self.hunger = max(0, self.hunger - 35)
    self.mood = min(100, self.mood + 5)
    self.affection += 2
    return f"{self.name}: 냠냠! 맛있어요 🍪"

def play(self):
    if self.energy < 20:
        return f"{self.name}: 너무 졸려요… 😴"
    self.mood = min(100, self.mood + 25)
    self.energy = max(0, self.energy - 15)
    self.hunger = min(100, self.hunger + 10)
    self.affection += 3
    return f"{self.name}: 신난다! 같이 놀아요 🎮"
```

### 🎯 모든 행동의 공통 구조

| 단계 | 하는 일 | 예 |
|---|---|---|
| 1. 거부 조건 | "지금은 안 돼요" 상황 차단 | 너무 배부르면 못 먹음 |
| 2. 비용·이득 | 능력치를 +/- 하기 | 놀면 기분↑ 에너지↓ 배고픔↑ |
| 3. 친밀도 | 상호작용은 항상 +affection | 1~3 정도 |
| 4. 대사 반환 | f-string 한 줄 | `f"{self.name}: …"` |

> 💡 **놀이 = 즐겁지만 비용이 있는 행동** 이에요. 한 가지 능력치만 올라가면 게임이 너무 단순해져요. 트레이드오프를 만들면 플레이가 생겨요.

### 🏋️ 직접 추가해보기

다음 행동을 직접 만들어보세요:

- **목욕시키기**: 기분 +10, 에너지 -5
- **칭찬하기**: 친밀도 +5 (단, 하루에 한 번만)
- **공부 시키기**: 기분 -5, "지식" 능력치 +1 (새 필드 필요)

> 💡 **Claude Code 활용법:** 한꺼번에 5개 행동 만들지 말고, "feed 메서드 만들어줘" → 테스트 → "play 추가해줘" → 테스트… 식으로 하나씩이에요.

---

## 6️⃣ 기억하기: JSON으로 저장·복원

지금 상태로는 프로그램을 끄면 봇이 **사라져요.** 진짜 반려가 되려면 **파일에 기억**해야 해요. JSON이 제격이에요.

```python
import json
from pathlib import Path

SAVE_FILE = Path.home() / ".claude-pet.json"

def save(self):
    SAVE_FILE.write_text(
        json.dumps(self.to_dict(), ensure_ascii=False, indent=2),
        encoding="utf-8",
    )

@classmethod
def load(cls):
    if not SAVE_FILE.exists():
        return None
    data = json.loads(SAVE_FILE.read_text(encoding="utf-8"))
    return cls.from_dict(data)
```

`to_dict`/`from_dict`는 객체 ↔ 딕셔너리 변환을 담당해요. 그래야 JSON으로 다룰 수 있어요.

### 📂 왜 홈 디렉터리에 저장해요?

| 저장 위치 | 장단점 |
|---|---|
| 현재 폴더 (`./pet.json`) | ❌ 폴더를 옮기면 봇이 사라짐 |
| 홈 디렉터리 (`~/.claude-pet.json`) | ✅ 어디서 실행해도 같은 봇 |
| OS별 설정 폴더 | ✅✅ 가장 정석. 다만 코드 길어짐 |

> 💡 학습용으로는 홈 디렉터리가 적당해요. 점(`.`)으로 시작해 숨김 파일이 돼요.

### ⚠️ 흔한 함정: `last_seen` 저장하기

저장할 때 `last_seen = time.time()`을 같이 넣어둬야, 다음에 켤 때 "그 사이에 얼마 지났는지" 계산할 수 있어요. 이걸 빼먹으면 자리 비웠는데 봇이 항상 쌩쌩한 이상한 일이 벌어져요.

---

## 7️⃣ 메인 루프와 메뉴

마지막으로, 사용자 입력을 받는 루프를 만들어요. **딕셔너리로 메뉴를 관리**하면 새 명령 추가가 쉬워요.

```python
def main():
    pet = ClaudePet.load() or ClaudePet(input("이름: ") or "클로디")
    pet.tick()
    print(f"{pet.name}이(가) 깨어났어요! {pet.face()}")

    actions = {
        "1": pet.feed,
        "2": pet.play,
        "3": pet.sleep,
        "4": pet.pet,
        "5": pet.chat,
        "6": lambda: pet.status(),
    }

    while True:
        choice = input("> ").strip().lower()
        if choice == "q":
            pet.save()
            break
        action = actions.get(choice)
        if action:
            pet.tick()
            print(action())
            pet.save()
```

### 💡 작은 디테일들

| 패턴 | 왜 좋은가 |
|---|---|
| `pet.save()`를 매 행동 후에 호출 | 갑자기 종료돼도 데이터 안 잃음 |
| `KeyboardInterrupt` 잡기 | Ctrl+C로 끄는 사람도 안전하게 저장 |
| 메뉴를 **dict**로 관리 | if/elif 사다리보다 깔끔, 추가 쉬움 |
| 입력 검증은 `.strip().lower()` | 공백·대소문자 사고 방지 |

---

## 8️⃣ Claude Code와 함께 키우는 팁

이 봇을 만들 때 Claude Code를 어떻게 부리면 좋을까요?

### ✅ 잘 먹히는 프롬프트

| 단계 | 좋은 프롬프트 |
|---|---|
| 뼈대 | "ClaudePet 클래스 만들어줘. 필드는 …, 메서드는 빈 채로 둬도 돼" |
| 한 메서드씩 | "feed 메서드만 추가해줘. 거부 조건도 포함해서" |
| 디버깅 | "방금 만든 tick에서 hunger가 100을 넘는데 왜 그래?" |
| 리팩터 | "actions를 dict로 바꿔줘. 동작은 동일해야 해" |

### ❌ 피하면 좋은 프롬프트

| 안 좋은 프롬프트 | 왜 |
|---|---|
| "다마고치 만들어줘" | 너무 광범위, 결과물 통제 어려움 |
| "다 좋게 고쳐줘" | "좋게"의 기준이 없음 |
| "에러 났어" (메시지 없이) | Claude도 모름. 메시지 붙여주세요 |

> 💡 **핵심 원칙:** **점진적으로**. 50줄짜리 결과를 한 방에 받지 말고, 5~10줄씩 검토하면서 키우세요. [효과적인 프롬프트 가이드](./effective-prompting-and-claude-md.md)의 **Few-shot · CoT** 패턴이 그대로 적용돼요.

### 🎬 실전 흐름 예시

```
나: ClaudePet 클래스 뼈대 만들어줘. 필드는 name, hunger, mood, energy.
Claude: [코드 생성]
나: 이제 tick 메서드 추가해줘. 시간 지나면 hunger 올라가게.
Claude: [tick 추가]
나: 좋아. feed 메서드도 추가. 너무 배부르면 거부하게.
Claude: [feed 추가]
... (반복)
```

---

## 🪞 5분 회고

지금까지 만든 봇을 한 번 켜보고, 아래 질문에 답해보세요.

- 🤔 클래스로 묶으니까 변수만 쓸 때보다 **무엇이 편해졌나요?**
- 🤔 `tick` 메서드 없이 행동만으로 게임을 만들면 **어떤 느낌**이 들까요?
- 🤔 봇의 **성격을 바꾸려면** 어떤 숫자(상수)를 만지면 될까요?
- 🤔 Claude Code에 한 번에 너무 많이 부탁했을 때, **결과가 어땠나요?**

> 💭 **토론거리**
> "좋은 반려봇"의 조건은 무엇일까요? **사용자의 주의를 더 끌게** 만드는 게 정답일까요, 아니면 **적당히 무심해도 살아있는 듯한** 봇이 더 매력적일까요?

---

## 🆘 자주 막히는 지점

### Q1. JSON 저장이 안 돼요. `PermissionError`가 나요.

🅰️ 홈 디렉터리(`Path.home()`)에 쓰기 권한이 있는지 확인하세요. 회사 PC라면 `Documents` 폴더 등으로 경로를 바꿔보세요.

```python
SAVE_FILE = Path.home() / "Documents" / "claude-pet.json"
```

### Q2. 한글 출력이 깨져요 (`UnicodeEncodeError`).

🅰️ `json.dumps`에 `ensure_ascii=False`를 꼭 넣고, 파일 쓸 때 `encoding="utf-8"`을 명시하세요. Windows PowerShell이라면 한 번 `chcp 65001`로 콘솔 인코딩도 바꿔보세요.

### Q3. 봇이 너무 빨리 배고파져요 / 너무 안 졸려요.

🅰️ `tick`의 상수(`1.5`, `1.0`, `1.2`)를 조절하세요. 모든 상수가 봇의 성격을 결정하는 다이얼이에요.

| 다이얼 | 키우면 | 줄이면 |
|---|---|---|
| `hunger * 1.5` | 식탐 봇 | 소식 봇 |
| `energy * 1.0` | 잠꾸러기 봇 | 활동적 봇 |
| `mood * 1.2` | 예민한 봇 | 무던한 봇 |

### Q4. 행동을 추가했는데 메뉴에 안 떠요.

🅰️ 메뉴(`actions` dict)에도 추가했는지 확인하세요. **메서드 정의 + 메뉴 등록**이 한 쌍이에요.

### Q5. Ctrl+C로 끄면 상태가 사라져요.

🅰️ `try/except KeyboardInterrupt`로 감싸고, except 블록에서 `pet.save()`를 호출하세요.

---

## 🎯 오늘 배운 핵심 정리

| 개념 | 이 봇에서의 역할 | 다른 곳에서도 |
|---|---|---|
| **클래스(OOP)** | 상태 + 행동 묶기 | 모든 게임/앱의 기본 |
| **시간 기반 변화** | `tick`으로 자연스러움 | 알림, 캐시 만료 |
| **클램핑** | `min/max`로 범위 보장 | 게임, UI 진행률 바 |
| **JSON 직렬화** | 객체 ↔ 파일 | 설정 저장, API 응답 |
| **메뉴 dict** | if/elif 사다리 대체 | CLI 도구, 라우팅 |
| **점진적 개발** | 한 메서드씩 늘리기 | 모든 협업의 기본 |

> 💎 **오늘의 한 줄:**
> **"좋은 코드는 한 번에 태어나지 않아요. 작은 메서드 하나씩, Claude와 한 입씩 키워가는 거예요."**

---

## 📚 공식 문서

- [Python `dataclasses` (다음 단계 추천)](https://docs.python.org/ko/3/library/dataclasses.html) — to_dict/from_dict를 더 깔끔하게
- [Python `json` 모듈](https://docs.python.org/ko/3/library/json.html)
- [Python `pathlib` 모듈](https://docs.python.org/ko/3/library/pathlib.html)

---

## 🎓 다음 단계

이 봇을 더 키우고 싶다면?

| 다음 도전 | 어떤 걸 배우게 되나 |
|---|---|
| **여러 봇 키우기** | 컬렉션, ID, dict-of-pets |
| **봇끼리 친구 맺기** | 객체 간 관계 |
| **GUI 입히기 (tkinter)** | 이벤트 기반 프로그래밍 |
| **웹으로 확장 (Flask)** | HTTP, REST |
| **AI 대답 붙이기 (Anthropic API)** | LLM 통합, 캐릭터 프롬프트 |

이어서 추천하는 가이드:

- [Skills & Remote Control](./skills-and-remote-control.md) — 봇을 Claude Code의 Skill로 등록해서 어디서든 부르기
- [Spotify 데이터 분석](./spotify-data-analysis.md) — 다른 종류의 실전 응용 (데이터 분석 흐름)

---

## 🌱 마무리: Fail Forward

오늘 작업하면서…

- 🟢 **잘 풀렸다면** → 어떤 메서드를 추가해보고 싶어요? 직접 한 줄 적어두세요.
- 🟡 **반쯤 풀렸다면** → 어디까지 만들었고, 다음에 뭘 이어붙일지 메모해두세요.
- 🔴 **막혔다면** → 어떤 에러가 났는지 메시지 통째로 적어두세요. **그 자체가 다음 학습의 출발점**이에요.

```markdown
## 오늘의 학습 노트

- 작업 일자:
- 만든 봇 이름:
- 추가한 행동:
- Claude Code에 가장 잘 먹힌 프롬프트:
- 막혔던 지점 / 에러 메시지:
- 다음에 시도할 것:
```

> 💎 코드는 **반려봇처럼** 키우는 거예요. 한 번에 완성된 어른이 아니라, 매일 조금씩 자라는 작은 친구로요. 🌱

---

📅 작성일: 2026.05.05
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
