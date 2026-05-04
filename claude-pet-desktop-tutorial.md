# 데스크톱 클로드봇 만들기 🪟🤖

> 화면 위를 자유롭게 돌아다니는 작은 친구를 만들어요.
> 드래그로 잡고, 우클릭으로 먹이도 주는, **눈에 보이는 반려봇** 이에요.

## 🎯 학습 목표

- ✅ **tkinter** 로 GUI 창을 만들고 모양·동작을 제어하기
- ✅ **투명 창 · 항상 위 · 타이틀바 제거** — 데스크톱 위젯의 3종 세트
- ✅ `after()` 로 만드는 **게임 루프** 와 부드러운 애니메이션
- ✅ **마우스 이벤트** 로 드래그·우클릭 메뉴 같은 인터랙션 붙이기
- ✅ **상태 머신** 패턴으로 봇의 행동을 깔끔하게 관리

---

## 📑 목차

- [1️⃣ 무엇을 만들까요?](#1️⃣-무엇을-만들까요)
- [2️⃣ 투명한 창 띄우기](#2️⃣-투명한-창-띄우기)
- [3️⃣ 봇 본체 그리기](#3️⃣-봇-본체-그리기)
- [4️⃣ 움직이게 하기: after() 게임 루프](#4️⃣-움직이게-하기-after-게임-루프)
- [5️⃣ 산책시키기: 목표점 패턴](#5️⃣-산책시키기-목표점-패턴)
- [6️⃣ 상태 머신: walking · idle · sleeping · dragged](#6️⃣-상태-머신-walking--idle--sleeping--dragged)
- [7️⃣ 마우스 이벤트: 드래그와 우클릭 메뉴](#7️⃣-마우스-이벤트-드래그와-우클릭-메뉴)
- [8️⃣ 말풍선과 터미널 봇 연동](#8️⃣-말풍선과-터미널-봇-연동)
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
| 터미널 반려봇 (선택) | 친밀도·이름 공유용 | [반려 클로드봇 만들기](./claude-pet-tutorial.md) |
| Claude Code | 짝꿍 코딩 | [설치 가이드](<./1-1. claude-code-install-guide.md>) |
| OS | 🪟 Windows 권장 (투명색 지원) | macOS/Linux도 동작은 함 |

> 💡 [반려 클로드봇 만들기](./claude-pet-tutorial.md)에서 만든 `~/.claude-pet.json`을 그대로 읽어와 친밀도와 이름을 공유해요. **터미널 봇이 자란 만큼 데스크톱 봇도 친해진** 상태로 깨어나요.

---

## 1️⃣ 무엇을 만들까요?

🎬 **시나리오:** `python claude-pet-desktop.py`를 실행하면 화면 어딘가에 작은 봇이 나타나서 천천히 산책을 시작해요. 어떤 창 위에서도 보이고, 마우스로 잡아 옮길 수 있고, 우클릭하면 먹이/말 걸기 메뉴가 떠요.

```
다른 창들 위에 둥둥 떠다니는…
   (•‿•)>           이쪽으로 걸어가는 중
            (>﹏<)~  잡혀서 끌려가는 중
   (￣ω￣) zzZ      도착해서 졸고 있음
```

### 🧩 GUI 봇의 핵심 구성

| 부품 | 역할 | tkinter에서 |
|---|---|---|
| **창(window)** | 봇이 사는 공간 | `tk.Tk()` |
| **모양(face)** | 보여줄 ASCII 얼굴 | `tk.Label` |
| **타이밍(loop)** | 매 프레임 갱신 | `root.after()` |
| **이벤트(event)** | 클릭·드래그·키 입력 | `widget.bind(...)` |
| **상태(state)** | walking/idle/… | 그냥 문자열 변수 |

> 💡 **핵심 비유:** GUI는 **연극 무대**예요. 창=무대, 위젯=배우, `after()`=초시계, 이벤트=관객의 콜. 각자 역할이 또렷해서 분리하면 코드가 깔끔해져요.

---

## 2️⃣ 투명한 창 띄우기

데스크톱 위젯의 트레이드마크 3종 세트예요. 이거만 알면 절반은 끝났어요.

```python
import tkinter as tk

root = tk.Tk()
root.overrideredirect(True)               # ① 타이틀바·테두리 제거
root.attributes("-topmost", True)         # ② 항상 다른 창 위에
root.attributes("-transparentcolor",      # ③ 이 색은 투명하게
                "magenta")
root.geometry("+500+300")                  # 위치 (x, y)
root.mainloop()
```

### 🧪 세 줄이 하는 일

| 옵션 | 효과 | 이게 없으면 |
|---|---|---|
| `overrideredirect(True)` | 타이틀바/X버튼 사라짐 | 못생긴 창이 둥둥 떠다님 |
| `-topmost True` | 항상 맨 위에 | 다른 창에 가려짐 |
| `-transparentcolor "magenta"` | 마젠타 배경 = 투명 | 사각형 박스가 보임 |

### ⚠️ 플랫폼 차이

| OS | `-transparentcolor` | 결과 |
|---|---|---|
| 🪟 Windows | ✅ 지원 | 봇만 떠다님 |
| 🍎 macOS | ❌ 미지원 | 마젠타 사각형이 보임 |
| 🐧 Linux | ❌ 대부분 미지원 | 마젠타 사각형이 보임 |

> 💡 **타 플랫폼 대안:** macOS는 `-alpha 0.95` (반투명)로, Linux는 `pyglet`/`PyQt`로 우회. 학습 목적이면 그냥 마젠타 박스 두고 진행해도 OK.

```python
try:
    root.attributes("-transparentcolor", "magenta")
except tk.TclError:
    pass  # 지원 안 하는 OS면 조용히 넘어가기
```

> 💡 **Claude Code에 이렇게 부탁해보세요:**
> > "tkinter로 타이틀바 없고, 항상 위에 뜨고, 배경이 투명한 작은 창 만들어줘. Windows 기준."

---

## 3️⃣ 봇 본체 그리기

봇의 몸은 **`Label` 위젯 하나**예요. ASCII 얼굴을 텍스트로 넣고, 배경을 투명색으로 맞춰요.

```python
TRANSPARENT_KEY = "magenta"

label = tk.Label(
    root,
    text="(•‿•)",
    font=("Consolas", 28, "bold"),
    fg="#7B3FF2",          # 보라색 글씨
    bg=TRANSPARENT_KEY,    # ← 배경을 투명색과 맞춤!
)
label.pack()
```

### 🎨 얼굴의 진행 방향 표현

오른쪽으로 갈 때 `(•‿•)>`, 왼쪽으로 갈 때 `<(•‿•)`. **꼬리 한 글자**만으로도 방향이 살아요.

```python
def face(self):
    if self.state == "sleeping":
        return "(￣ω￣) zzZ"
    if self.state == "dragged":
        return "(>﹏<)~"
    return "(•‿•)>" if self.facing_right else "<(•‿•)"
```

### ❓ 왜 Canvas가 아니라 Label?

| 선택 | 장단점 |
|---|---|
| **Label** (텍스트) | ✅ 단순, 폰트만 바꿔도 표현 풍부 / ❌ 진짜 그림은 못 그림 |
| **Canvas** (그림) | ✅ 도형·이미지 자유 / ❌ 코드 길어짐 |
| **이미지 PNG** | ✅ 진짜 캐릭터 / ❌ 에셋 관리 필요 |

> 💡 **학습용은 텍스트가 최고.** 한 글자만 바꿔도 표정이 바뀌어서, 코드가 어떻게 보이는지 즉각 피드백돼요.

---

## 4️⃣ 움직이게 하기: `after()` 게임 루프

GUI에서 **`while True:` 루프는 절대 금지** 예요. 창이 멈춰버려요. 대신 **`root.after(ms, fn)`** 으로 일정 간격마다 함수가 호출되게 해요.

```python
TICK_MS = 50  # 50ms = 초당 20프레임

def tick():
    # ① 상태 업데이트 (위치 변경 등)
    self.x += 2
    # ② 화면 반영
    self.root.geometry(f"+{int(self.x)}+{int(self.y)}")
    # ③ 다음 호출 예약
    self.root.after(TICK_MS, tick)

tick()  # 첫 호출
```

### ⚖️ `while` vs `after()`

| 방식 | GUI 반응성 | 사용처 |
|---|---|---|
| `while True: …` | ❌ 창 멈춤 (이벤트 처리 못 함) | 콘솔 프로그램 |
| `root.after()` | ✅ 클릭·드래그 다 받음 | GUI 게임 루프 |
| `threading` | ⚠️ tkinter는 스레드 안전 X | 복잡, 비추 |

> 💡 **`after()`는 자기 자신을 다시 예약하는 패턴.** 끝에서 다시 `after()`를 안 부르면 한 번 돌고 끝나요. 끝없이 도는 듯 보이지만 사실은 50ms마다 새 약속을 잡는 거예요.

### 🧪 부드러움 vs CPU 사용량

| `TICK_MS` | 프레임 | 체감 | CPU |
|---|---|---|---|
| 16 | ~60fps | 매우 부드러움 | ↑↑ |
| 50 | 20fps | 충분히 자연스러움 | 적당 ✅ |
| 100 | 10fps | 약간 끊김 | 가벼움 |

> 💡 50ms가 데스크톱 펫의 **스위트 스팟** 이에요. 정신없이 빠르지도, 끊겨 보이지도 않아요.

---

## 5️⃣ 산책시키기: 목표점 패턴

랜덤하게 비틀거리는 것보다, **목표점을 정하고 그쪽으로 걸어가는** 패턴이 훨씬 자연스러워요.

```python
import random

SPEED = 2.5

def pick_target(self):
    margin = 80
    self.target_x = random.randint(margin, self.sw - margin)
    self.target_y = random.randint(margin, self.sh - margin)

def walk(self):
    dx = self.target_x - self.x
    dy = self.target_y - self.y
    dist = (dx * dx + dy * dy) ** 0.5
    if dist < SPEED * 1.5:
        # 도착!
        self.state = "idle"
        return
    # 정규화된 방향 벡터 × 속도
    self.x += SPEED * dx / dist
    self.y += SPEED * dy / dist
    self.facing_right = dx >= 0
```

### 🧮 왜 `dx / dist` 인가요?

| 식 | 의미 |
|---|---|
| `dx, dy` | 목표까지 남은 거리 (성분별) |
| `dist` | 직선 거리 (피타고라스) |
| `dx / dist` | -1 ~ 1 사이의 **방향 비율** |
| `SPEED * dx / dist` | 매 tick에 정확히 SPEED 픽셀씩 이동 |

> 💡 단순히 `self.x += dx` 하면 가까울수록 느려져요(Zeno의 역설처럼). **정규화 후 속도를 곱하기** 가 등속 운동의 정석이에요.

### 🏋️ 작은 실습

- `SPEED`를 5로 올려보세요. 봇이 더 활기차져요.
- `pick_target` 안에서 화면 끝 가까이만 고르게 바꿔보세요. 봇이 가장자리만 어슬렁거려요.

---

## 6️⃣ 상태 머신: walking · idle · sleeping · dragged

봇은 4가지 상태 중 **하나만** 가질 수 있어요. 이걸 깔끔히 나누면 코드가 폭발하지 않아요.

```python
def tick(self):
    if self.state == "walking":
        self._walk_step()
    elif self.state == "idle":
        self.timer -= 1
        if self.timer <= 0:
            self.state = "walking"
            self.pick_target()
    elif self.state == "sleeping":
        self.timer -= 1
        if self.timer <= 0:
            self.state = "walking"
            self.pick_target()
    # dragged 상태는 _on_drag가 처리하니까 tick에서는 가만히
    self._apply_position()
    self.root.after(TICK_MS, self.tick)
```

### 🗺️ 상태 전이도

| 현재 상태 | 다음 상태 | 트리거 |
|---|---|---|
| walking | idle | 목표점 도착 (85%) |
| walking | sleeping | 목표점 도착 (15%) |
| idle | walking | 타이머 끝 |
| sleeping | walking | 타이머 끝 |
| any | dragged | 마우스 클릭 |
| dragged | walking | 마우스 뗌 |

> 💡 **상태 머신 = "지금 이 모드에서는 무슨 일이 가능한가?"** 를 명시적으로 적는 거예요. `if/elif` 사다리가 길어 보여도, 미래의 본인이 코드 읽을 때 훨씬 편해요.

### ⚠️ 흔한 함정

| 실수 | 증상 | 해결 |
|---|---|---|
| 상태 전이 직후 `_apply_position` 안 부름 | 한 프레임 늦게 반영 | 항상 마지막에 호출 |
| 여러 if를 elif 없이 쓰기 | 한 tick에 여러 상태 처리 | `elif` 또는 early return |
| `dragged` 상태에서 walking 로직도 돌림 | 마우스 따라 + 자동 이동 동시에 | 상태 분기 명확히 |

---

## 7️⃣ 마우스 이벤트: 드래그와 우클릭 메뉴

GUI는 **이벤트 기반(event-driven)** 이에요. "마우스가 이런 행동을 하면 → 이 함수를 불러줘" 라고 등록만 해 두면 돼요.

### 🖱️ 드래그로 잡기

```python
def _on_press(self, e):
    self._drag_dx = e.x          # 라벨 안에서 클릭한 위치 기억
    self._drag_dy = e.y
    self.state = "dragged"
    self._refresh_face()

def _on_drag(self, e):
    # 마우스 절대좌표 - 라벨 내 클릭 위치 = 새 창 위치
    self.x = self.root.winfo_pointerx() - self._drag_dx
    self.y = self.root.winfo_pointery() - self._drag_dy
    self._apply_position()

def _on_release(self, e):
    self.state = "walking"
    self.pick_target()

label.bind("<Button-1>",        self._on_press)   # 좌클릭 누름
label.bind("<B1-Motion>",       self._on_drag)    # 누른 채 이동
label.bind("<ButtonRelease-1>", self._on_release) # 뗌
```

### 🎯 왜 `e.x` 를 빼요?

| 빼지 않으면 | 빼면 |
|---|---|
| 잡을 때마다 봇이 마우스 끝점으로 점프 | 잡은 그 자리 그대로 따라옴 ✅ |

`e.x`는 **라벨 내부 좌표**예요. "라벨 왼쪽 위로부터 몇 픽셀에서 잡았는지"를 기억해 둬야 자연스러워요.

### 🍽️ 우클릭 메뉴 띄우기

```python
def _show_menu(self, e):
    menu = tk.Menu(self.root, tearoff=0)
    menu.add_command(label="🍪 먹이주기", command=self._feed)
    menu.add_command(label="💬 말 걸기",  command=self._chat)
    menu.add_separator()
    menu.add_command(label="👋 잘 가",    command=self.root.destroy)
    try:
        menu.tk_popup(e.x_root, e.y_root)
    finally:
        menu.grab_release()

label.bind("<Button-3>", self._show_menu)  # 우클릭
```

| 알아둘 것 | 설명 |
|---|---|
| `tearoff=0` | 메뉴 위 점선 "떼어내기" 비활성화 (보기 흉함) |
| `e.x_root, e.y_root` | **화면 절대좌표** (창 안 좌표 아님!) |
| `try/finally + grab_release` | 메뉴 후 마우스 잠김 방지 (정석 패턴) |

---

## 8️⃣ 말풍선과 터미널 봇 연동

### 💬 말풍선 = 작은 Toplevel 창

봇 위에 잠깐 떴다 사라지는 노란 라벨이에요.

```python
def show_speech(self, text):
    bubble = tk.Toplevel(self.root)
    bubble.overrideredirect(True)
    bubble.attributes("-topmost", True)
    tk.Label(bubble, text=text, bg="#FFF8C5", padx=10, pady=6,
             relief="solid", borderwidth=1).pack()
    bubble.geometry(f"+{int(self.x) - 30}+{int(self.y) - 36}")
    self.root.after(2200, bubble.destroy)  # 2.2초 후 자동 닫힘
```

> 💡 `Toplevel`은 **새로운 창**을 만드는 위젯이에요. 메인 창과 독립적이라서, `destroy()`해도 봇 본체는 멀쩡해요.

### 🔗 터미널 봇과 친밀도 공유하기

[반려 클로드봇 만들기](./claude-pet-tutorial.md)에서 만든 `~/.claude-pet.json`을 그냥 읽어오면 끝이에요.

```python
import json
from pathlib import Path

SAVE_FILE = Path.home() / ".claude-pet.json"

def load_state():
    if not SAVE_FILE.exists():
        return None
    try:
        return json.loads(SAVE_FILE.read_text(encoding="utf-8"))
    except Exception:
        return None

# 사용
saved = load_state()
if saved:
    self.affection = saved.get("affection", 0)
    self.name = saved.get("name", "클로디")
```

이러면:
- 터미널에서 키운 친밀도 → 데스크톱 봇 시작값
- 친밀도가 일정 이상이면 얼굴이 `(◕‿◕)`로 바뀜
- 우클릭 메뉴에 이름·❤️ 카운트 표시

> 💡 **느슨한 결합(loose coupling).** 두 프로그램은 서로 모르고, **JSON 파일을 통해서만 대화** 해요. 한쪽이 죽어도 다른 쪽은 멀쩡해요. 이게 마이크로서비스의 발상이에요.

> 💡 **Claude Code에 이렇게 부탁해보세요:**
> > "터미널 봇이 만든 ~/.claude-pet.json을 읽어서 affection과 name을 가져오는 함수를 만들어줘. 파일이 없거나 깨졌으면 None을 반환해."

---

## 🪞 5분 회고

데스크톱 봇을 띄워놓고, 5분만 다른 작업을 해보세요. 그러고 답해주세요.

- 🤔 **`while` 대신 `after()`** 를 써야 하는 이유를 한 줄로 설명할 수 있나요?
- 🤔 봇이 **너무 빠르거나 너무 느려서** 거슬렸다면 어디 숫자를 만질까요?
- 🤔 상태가 `dragged`인데 동시에 `walking` 로직이 돌면 **어떤 사고**가 날까요?
- 🤔 터미널 봇과 **JSON 파일 공유**는 어떤 점이 마음에 들고, 어떤 점이 위험해 보이나요?

> 💭 **토론거리**
> "데스크톱 펫이 작업에 도움이 되는가, 방해가 되는가?" — 시각적 동반자(가시성)가 주는 위안과 주의 산만의 비용을 어떻게 균형 잡을까요?

---

## 🆘 자주 막히는 지점

### Q1. 봇이 마젠타 사각형 박스로 보여요.

🅰️ macOS/Linux에서는 `-transparentcolor`가 동작하지 않아요. 대안:
- macOS: `root.attributes("-alpha", 0.95)` 같은 반투명
- Linux: `Tk` 배경을 데스크톱 색과 비슷하게 맞춤
- 또는 그냥 **사각 박스 봇** 으로 진행 — 학습 목적이면 충분

### Q2. 우클릭 메뉴가 안 떠요 / 두 번째부터 안 떠요.

🅰️ `tk_popup` 호출 후 `grab_release()`를 꼭 부르세요. 안 부르면 마우스 입력이 메뉴에 잠긴 채로 남아요.

```python
try:
    menu.tk_popup(e.x_root, e.y_root)
finally:
    menu.grab_release()
```

### Q3. 드래그할 때 봇이 마우스 끝점으로 순간이동해요.

🅰️ `_on_press`에서 `e.x, e.y`를 안 저장하고 `_on_drag`에서 마우스 위치만 쓰면 그래요. **잡은 위치(offset)** 를 기억해야 자연스러워요. (위 7번 섹션 참고)

### Q4. CPU 사용률이 너무 높아요.

🅰️ `TICK_MS`를 16 → 50 → 100으로 키우세요. 50ms (20fps)가 데스크톱 펫의 스위트 스팟이에요.

### Q5. 봇이 다른 모니터로 안 가요.

🅰️ `winfo_screenwidth()`는 **주 모니터** 만 알아요. 다중 모니터는 `winfo_vrootwidth()` 또는 `pyautogui`/`screeninfo` 같은 라이브러리가 필요해요.

### Q6. Esc로 안 꺼져요.

🅰️ `root.bind("<Escape>", lambda e: root.destroy())`를 등록했는지 확인. 봇 라벨이 포커스를 안 받으면 키 이벤트가 메인 창으로 가요.

---

## 🎯 오늘 배운 핵심 정리

| 개념 | 이 봇에서의 역할 | 다른 곳에서도 |
|---|---|---|
| **`overrideredirect`** | 타이틀바 제거 | 스플래시 화면, 위젯 |
| **`-topmost` / `-transparentcolor`** | 항상 위 + 투명 배경 | 데스크톱 알림, 오버레이 |
| **`after()` 게임 루프** | GUI를 안 멈추고 반복 | 모든 GUI 애니메이션 |
| **이벤트 바인딩** | 클릭·드래그·키 처리 | 버튼, 폼, 게임 입력 |
| **상태 머신** | walking/idle/… 분리 | 게임 캐릭터, UI 모드 |
| **JSON 파일로 느슨한 연동** | 터미널 봇 ↔ 데스크톱 봇 | 마이크로서비스, 설정 공유 |

> 💎 **오늘의 한 줄:**
> **"GUI는 무대고, `after()`는 초시계예요. 배우(위젯)에게 가만히 서있으라 명령하고, 시간만 흘려보내면 알아서 인생이 펼쳐져요."**

---

## 📚 공식 문서

- [Python tkinter 공식 문서](https://docs.python.org/ko/3/library/tkinter.html)
- [Tkinter 8.5 reference (New Mexico Tech)](https://tkdocs.com/tutorial/index.html) — 가장 잘 정리된 비공식 튜토리얼
- [tkinter `after` 메서드 설명](https://docs.python.org/ko/3/library/tkinter.html#tkinter.Misc.after)

---

## 🎓 다음 단계

| 다음 도전 | 어떤 걸 배우게 되나 |
|---|---|
| **PNG 이미지로 봇 그리기** | `tk.PhotoImage`, 알파 채널, 애니메이션 프레임 |
| **여러 마리 동시에** | 객체 컬렉션, 충돌 검사 |
| **시스템 트레이 아이콘** | `pystray` 라이브러리 |
| **커서를 따라다니기** | `winfo_pointerxy()` 추적 |
| **시계·날씨 위젯으로 변형** | 같은 기법, 다른 콘텐츠 |
| **봇 ↔ Claude API 대화** | LLM 통합, 비동기 호출 |

이어서 추천하는 가이드:

- [반려 클로드봇 만들기](./claude-pet-tutorial.md) — 터미널 버전 (이 봇과 친밀도 공유!)
- [Skills & Remote Control](./skills-and-remote-control.md) — 봇을 Claude Code Skill로 등록하기
- [효과적인 프롬프트 & CLAUDE.md](./effective-prompting-and-claude-md.md) — 더 까다로운 GUI 코드를 Claude에게 잘 시키기

---

## 🌱 마무리: Fail Forward

오늘 작업하면서…

- 🟢 **잘 풀렸다면** → 봇에게 어떤 새 행동을 추가하고 싶나요? "춤추기"? "마우스 따라오기"?
- 🟡 **반쯤 풀렸다면** → 어디서 막혔는지, 다음에 무엇부터 다시 볼지 적어두세요.
- 🔴 **막혔다면** → 에러 메시지를 통째로 적어두세요. **GUI 에러는 특히 검색 키워드가 중요** 해요 ("tkinter `_tkinter.TclError: bad option ...`" 식으로).

```markdown
## 오늘의 학습 노트

- 작업 일자:
- 봇이 사는 위치 (어느 화면 모서리):
- 가장 마음에 드는 동작:
- 추가하고 싶은 기능:
- 막혔던 지점 / 에러 메시지:
- 다음에 시도할 것:
```

> 💎 GUI는 처음엔 어렵게 느껴져요. 근데 한 번 봇이 화면 위를 걸어다니는 걸 보면, **"내가 만든 작은 생명체"** 라는 묘한 기쁨이 와요. 그게 GUI를 계속 만들게 하는 연료예요. 🌱

---

📅 작성일: 2026.05.05
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
