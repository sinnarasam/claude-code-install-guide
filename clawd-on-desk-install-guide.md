# Clawd on Desk 설치 가이드 🦀

> **AI 코딩 에이전트의 활동을 실시간으로 감시하는 데스크톱 펫**, Clawd on Desk를 설치해요.
> Claude Code가 생각하면 같이 생각하고, 권한이 필요하면 말풍선으로 물어봐요. 이제 터미널만 노려보지 않아도 돼요.

## 🎯 학습 목표

- ✅ **Clawd on Desk** 가 무엇이고 어떤 문제를 해결하는지 이해하기
- ✅ Windows / macOS / Linux 별 **설치 방법** 익히기
- ✅ Claude Code와의 **자동 연동(hook)** 작동 원리 이해
- ✅ **권한 말풍선 · 미니 모드 · DnD** 같은 핵심 기능 활용
- ✅ 다중 세션을 굴릴 때 **누가 입력을 기다리는지** 시각적으로 관리하기

---

## 📑 목차

- [1️⃣ Clawd on Desk가 뭐예요?](#1️⃣-clawd-on-desk가-뭐예요)
- [2️⃣ 설치하기 (Windows / macOS / Linux)](#2️⃣-설치하기-windows--macos--linux)
- [3️⃣ 첫 실행과 기본 사용](#3️⃣-첫-실행과-기본-사용)
- [4️⃣ Claude Code와 자동 연동](#4️⃣-claude-code와-자동-연동)
- [5️⃣ 12가지 애니메이션 상태와 화면 구성](#5️⃣-12가지-애니메이션-상태와-화면-구성)
- [6️⃣ 설정과 커스터마이징](#6️⃣-설정과-커스터마이징)
- [7️⃣ 다중 세션 대시보드](#7️⃣-다중-세션-대시보드)
- [8️⃣ 단축키와 권한 말풍선](#8️⃣-단축키와-권한-말풍선)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🎯 오늘 배운 핵심 정리](#-오늘-배운-핵심-정리)
- [🎓 다음 단계](#-다음-단계)
- [🌱 마무리: Fail Forward](#-마무리-fail-forward)

---

## 📋 시작하기 전에

| 준비물 | 설명 | 가이드 |
|---|---|---|
| Claude Code | 설치되어 있어야 hook이 등록돼요 | [설치 가이드](<./1-1. claude-code-install-guide.md>) |
| OS | 🪟 Windows 11 / 🍎 macOS / 🐧 Ubuntu | — |
| (선택) Node.js | 소스 빌드용 (LTS 권장) | [nodejs.org](https://nodejs.org/) |
| 디스크 여유 | 약 200~300MB | — |

> 💡 **이 가이드는 [Claude HUD 설치 가이드](./1-6.claude-hud-install-guide.md)와 짝이에요.** HUD가 **상태바**에 정보를 띄운다면, Clawd는 **데스크톱 위 캐릭터**로 보여줘요. 둘 다 켜두면 시야 두 군데로 정보가 분산돼서 더 편해요.

---

## 1️⃣ Clawd on Desk가 뭐예요?

🎬 **시나리오:** Claude Code에 긴 작업을 시키고 슬랙을 보러 잠깐 자리를 떴어요. 다시 돌아왔는데 — 진짜 끝난 건지, 권한을 물어보고 멈춰있는 건지, 에러로 죽은 건지 한눈에 안 보여요. 터미널을 일일이 들춰봐야 해요.

**Clawd on Desk** 는 데스크톱 위에 작은 캐릭터(기본은 픽셀 게 🦀)를 띄워서, AI 에이전트가 **지금 무슨 상태인지** 실시간 애니메이션으로 보여줘요.

### 🎯 무엇이 다른가요?

| 특징 | 일반 데스크톱 펫 | **Clawd on Desk** |
|---|---|---|
| 목적 | 귀여움, 동반감 | **AI 에이전트 모니터링** |
| 반응 | 미리 정해진 패턴 | Claude Code 등 **실제 활동에 반응** |
| 권한 처리 | — | **말풍선으로 Allow/Deny** (터미널 안 봐도 됨) |
| 다중 세션 | — | 여러 에이전트 **동시 추적** |
| 알림 | 사운드 위주 | **시각적** (사무실 친화) |

> 💡 **핵심 비유:** Claude Code가 **요리사**라면, Clawd는 **주방 너머에서 주문 진행도를 알려주는 모니터** 예요. 주방 안 들여다봐도 음식이 익는지, 양념을 추가할지 물어보는지 보여요.

### 🤝 지원하는 AI 에이전트

자동 hook 등록(앱 시작 시):

| 에이전트 | 자동 등록 | 권한 말풍선 |
|---|---|---|
| **Claude Code** | ✅ | ✅ |
| Codex CLI | ✅ | — |
| Gemini CLI | ✅ | — |
| Cursor Agent | ✅ | — |
| CodeBuddy | ✅ | ✅ |
| opencode | ✅ | ✅ |
| Kiro CLI / Kimi Code CLI | ✅ | — |
| Copilot CLI | ⚠️ 수동 설정 필요 | — |

---

## 2️⃣ 설치하기 (Windows / macOS / Linux)

### 🪟 Windows (권장 방식)

1. **GitHub Releases** 페이지로 이동: <https://github.com/sinnarasam/clawd-on-desk/releases>
   - 페이지가 비어 있으면 업스트림 [원작 릴리스](https://github.com/rullerzhou-afk/clawd-on-desk/releases/latest)에서 받으세요.
2. 본인 PC 아키텍처에 맞는 인스톨러 다운로드:
   - 일반 PC: `Clawd-on-Desk-Setup-<버전>-x64.exe`
   - ARM 노트북 (Surface Pro X 등): `...-arm64.exe`
3. 인스톨러 실행 → 안내대로 진행 (관리자 권한 불필요)
4. 시작 메뉴에서 **Clawd on Desk** 검색 → 실행

### 🍎 macOS

1. Releases에서 `Clawd-on-Desk-<버전>.dmg` 다운로드
2. `.dmg` 더블클릭 → Clawd 아이콘을 **Applications** 로 드래그
3. Launchpad나 Spotlight에서 실행

> ⚠️ 첫 실행 시 "확인되지 않은 개발자" 경고가 뜨면 **시스템 설정 → 개인정보 보호 및 보안** 에서 "그래도 열기" 클릭.

### 🐧 Linux (Ubuntu 기준)

```bash
# AppImage 방식 (가장 단순)
chmod +x Clawd-on-Desk-<버전>.AppImage
./Clawd-on-Desk-<버전>.AppImage

# .deb 패키지 방식
sudo dpkg -i clawd-on-desk_<버전>_amd64.deb
clawd-on-desk
```

### 🛠️ 소스에서 빌드 (전 OS 공통, 개발자용)

```bash
git clone https://github.com/sinnarasam/clawd-on-desk.git
cd clawd-on-desk
npm install
npm start
```

> 💡 소스 빌드는 **Node.js LTS** 가 필요해요. `npm install` 단계에서 Electron 툴체인을 같이 받아서 첫 실행은 시간이 좀 걸려요 (수백 MB).

### 🔍 어떤 방식을 골라야 하나요?

| 방식 | 장점 | 단점 | 추천 대상 |
|---|---|---|---|
| **인스톨러** | 자동 업데이트, 한 번에 끝 | OS 종속 | 일반 사용자 ✅ |
| **AppImage** | sudo 불필요, 휴대 가능 | Linux 전용 | Linux 사용자 |
| **소스 빌드** | 코드 수정/테마 개발 가능 | 빌드 환경 구성 필요 | 기여자 / 개발자 |

---

## 3️⃣ 첫 실행과 기본 사용

실행하면 화면 어딘가에 작은 게가 나타나서 두리번거려요. 마우스를 움직이면 **눈동자가 따라와요** (eye tracking).

### 🖱️ 기본 인터랙션

| 동작 | 결과 |
|---|---|
| **드래그** | 원하는 위치로 옮기기 |
| **더블 클릭** | poke 애니메이션 (찌르기) |
| **연속 4번 클릭** | flail 애니메이션 (호들갑) |
| **우클릭** | 메뉴 (설정 / 크기 / DnD / 종료) |
| **화면 가장자리로 드래그** | 미니 모드 진입 (화면 모서리에 숨음) |
| **60초 무활동** | 슬립 모드 → 마우스 움직이면 깨어남 |

> 💡 처음엔 **그냥 두고 작업** 해보세요. Claude Code를 띄우고 어떤 명령을 시키면, 게가 그 활동에 맞춰 동작이 바뀌어요. 이게 핵심 가치예요.

---

## 4️⃣ Claude Code와 자동 연동

### 🪝 Hook 자동 등록 — 사용자가 할 일 없음

Clawd가 처음 실행될 때 Claude Code 설정에 **hook** 을 자동으로 추가해요. 그래서 따로 설정할 게 없어요.

```
Clawd 실행
   ↓
Claude Code의 ~/.claude/settings.json 같은 곳에 hook 등록
   ↓
이후 Claude Code가 동작하면 → Clawd가 이벤트를 받아 → 게가 반응
```

### 🔍 어떤 이벤트를 잡아요?

| Claude Code 활동 | Clawd 반응 |
|---|---|
| 프롬프트 처리 중 | thinking 🤔 |
| 도구 실행 중 (Bash, Edit 등) | typing ⌨️ |
| 빌드 / 테스트 돌리는 중 | building 🔨 |
| 1개 서브에이전트 동작 | juggling 🤹 |
| 2개 이상 서브에이전트 | conducting 🎼 |
| 에러 발생 | error 😱 |
| 작업 완료 | happy 🎉 |
| 사용자 입력 대기 | notification 🔔 |

> 💡 **Claude Code의 어떤 명령이 어떤 상태로 매핑되는지** 알면 봇만 봐도 진행 단계가 읽혀요. 처음 며칠은 의식적으로 봇과 터미널을 같이 보면서 매핑을 익히면 좋아요.

---

## 5️⃣ 12가지 애니메이션 상태와 화면 구성

### 🎭 12가지 상태 한눈에

| 상태 | 의미 |
|---|---|
| **idle** | 아무 일 없음 (눈만 굴림) |
| **thinking** | 모델이 생각 중 |
| **typing** | 도구 호출 중 |
| **building** | 빌드/실행 중 |
| **juggling** | 서브에이전트 1개 |
| **conducting** | 서브에이전트 2개 이상 |
| **error** | 에러 발생 |
| **happy** | 작업 완료 |
| **notification** | 사용자 입력 대기 ⭐ |
| **sweeping** | 정리 작업 |
| **carrying** | 파일 이동 |
| **sleeping** | 60초 무활동 |

> 💡 **가장 중요한 건 `notification`** 이에요. 이게 뜨면 → 터미널 가서 답해줘야 한다는 뜻. 슬랙 보다가도 시야 끝에서 깜빡이면 바로 알아채요.

### 👀 Eye Tracking

idle 상태에서 마우스 커서를 따라 눈동자가 굴러요. 몸이 살짝 기울고 그림자도 따라 움직여서 **살아있는 느낌** 이 강해요.

### 📦 Mini Mode

화면 가장자리로 드래그하거나 우클릭 → Mini Mode를 켜면, 평소엔 화면 모서리에 숨어 있다가 마우스를 갖다 대면 살짝 보여요. **공간을 거의 안 차지** 해요.

---

## 6️⃣ 설정과 커스터마이징

### ⚙️ 우클릭 / 시스템 트레이 메뉴

| 항목 | 설명 |
|---|---|
| **Resize** | S / M / L 크기 조절 |
| **Do Not Disturb** | 알림 사운드 음소거 + 알림 애니메이션 억제 |
| **Language** | 영어 · 中文 · 한국어 · 日本語 |
| **Auto-start** | 부팅 시 자동 실행 |
| **Check for updates** | 수동 업데이트 확인 |
| **Settings…** | 에이전트별 권한 말풍선 토글, 테마 변경 |

### 🎨 커스텀 테마 만들기

기본 테마: **Clawd** (픽셀 게), **Calico** (삼색묘 三花猫), **Cloudling** (구름 云宝).

직접 만들고 싶으면:

```bash
npm run create-theme -- my-theme
```

**최소 요구 에셋:**

| 파일 | 용도 |
|---|---|
| `idle.svg` | 평소 상태 (눈동자 추적용 SVG) |
| 7개 GIF/APNG | thinking, working, error, happy, notification, sleeping, waking |

검증:

```bash
node scripts/validate-theme.js path/to/your-theme
```

> 💡 SVG로 idle을 만드는 이유는 **눈동자만 따로 움직여야** 해서예요. GIF는 통째 움직이지만 SVG는 일부 그룹만 변환할 수 있어요.

### 🔊 사운드 효과

- 알림 사운드 있음
- **10초 쿨다운** 으로 너무 자주 안 울려요
- DnD 모드에서는 자동 음소거

---

## 7️⃣ 다중 세션 대시보드

여러 개의 Claude Code (또는 다른 에이전트) 세션을 동시에 돌리는 분께 가장 강력한 기능이에요.

### 🗂️ 대시보드 열기

우클릭 → **Dashboard** (또는 시스템 트레이)

### 📊 보이는 정보

| 영역 | 내용 |
|---|---|
| **활성 세션 목록** | 지금 살아있는 모든 에이전트 세션 |
| **최근 이벤트** | 어느 세션에서 무슨 일이 일어났는지 |
| **터미널 바로가기** | 각 세션의 실제 터미널 창으로 점프 |

> 💡 **핵심 워크플로우:** Clawd가 `notification` 으로 깜빡인다 → 대시보드 열기 → 어느 세션이 답을 기다리는지 보고 → 클릭하면 그 터미널로 점프 → 답 입력. 터미널 헤매는 시간이 사라져요.

---

## 8️⃣ 단축키와 권한 말풍선

### 💬 권한 말풍선 (Permission Bubble)

Claude Code · CodeBuddy · opencode가 권한을 물어볼 때, **터미널에 갇히지 않고** 화면 어딘가에 떠있는 말풍선으로 와요.

| 단축키 | 동작 |
|---|---|
| `Ctrl+Shift+Y` | Allow ✅ |
| `Ctrl+Shift+N` | Deny ❌ |

> ⚠️ 단축키는 **글로벌** 이에요. 다른 앱 쓰고 있어도 작동해요. 충돌나면 다른 앱의 단축키와 겹치는지 확인하세요.

### 🤔 권한 말풍선이 좋은 이유

| 기존 방식 (터미널) | Clawd 권한 말풍선 |
|---|---|
| 터미널 창을 활성화해야 함 | 어디서나 단축키로 즉답 |
| 여러 세션 중 어느 게 물어보는지 헷갈림 | 말풍선에 출처 명시 |
| 슬랙 보다가 놓치기 쉬움 | 시야 끝 알림 |

---

## 🪞 5분 회고

설치 후 30분쯤 써보고 답해보세요.

- 🤔 봇의 어떤 **상태가 가장 정보성** 이었나요? (notification? error?)
- 🤔 권한 말풍선이 떴을 때, **터미널로 안 가도 처리되는 흐름** 이 어떻게 느껴졌나요?
- 🤔 Clawd가 **방해된다** 고 느낀 순간이 있었나요? 그럼 어떻게 줄일 수 있을까요? (DnD, Mini Mode, 크기)
- 🤔 다중 세션을 안 쓴다면, 이 도구가 **여전히 가치 있을지** 어떻게 생각하나요?

> 💭 **토론거리**
> AI 에이전트가 점점 **백그라운드에서 오래 도는 작업** 을 하게 될 텐데, "지금 뭘 하고 있는가"를 알려주는 **시각적 대시보드** 의 가치는 더 커질까요, 작아질까요?

---

## 🆘 자주 막히는 지점

### Q1. Claude Code에 hook이 자동으로 안 등록돼요.

🅰️ Clawd를 한 번 종료하고 다시 켜보세요. 그래도 안 되면:
- `~/.claude/settings.json` (Mac/Linux) 또는 `%USERPROFILE%\.claude\settings.json` (Windows)을 열어서 hook이 들어갔는지 확인
- Claude Code가 설치 안 된 상태에서 Clawd를 먼저 띄웠다면, Claude Code 설치 후 Clawd 재시작

### Q2. 봇이 너무 커요 / 너무 작아요.

🅰️ 우클릭 → Resize → S / M / L. 모니터가 4K라면 L이 적당해요.

### Q3. 사운드가 안 나요.

🅰️ DnD가 켜져 있는지 확인. 또 일부 OS는 시스템 알림 권한이 따로 필요해요.

### Q4. 권한 단축키 `Ctrl+Shift+Y`가 다른 앱과 겹쳐요.

🅰️ 현재 버전은 단축키 변경 UI가 제한적이에요. 충돌하는 다른 앱의 단축키를 바꾸는 게 빠를 수 있어요. 또는 GitHub Issue에 요청.

### Q5. 빌드에서 `npm install`이 실패해요.

🅰️ Node.js 버전 확인 (LTS 권장, v18 이상). Windows라면 **Visual Studio Build Tools** 가 필요할 수 있어요. Electron이 네이티브 모듈을 컴파일하기도 해요.

### Q6. macOS에서 "확인되지 않은 개발자" 경고.

🅰️ 시스템 설정 → 개인정보 보호 및 보안 → "그래도 열기". 한 번만 하면 다음부턴 안 떠요.

### Q7. 다중 모니터에서 봇이 어디 있는지 못 찾겠어요.

🅰️ 우클릭 메뉴에 보통 "Center" 또는 "Reset Position" 옵션이 있어요. 없으면 시스템 트레이 아이콘에서 같은 메뉴.

---

## 🎯 오늘 배운 핵심 정리

| 개념 | Clawd에서의 역할 | 의미 |
|---|---|---|
| **자동 hook 등록** | Claude Code 설정에 자동 주입 | 사용자가 할 일 없음 |
| **상태 매핑** | 12가지 애니메이션 ↔ 에이전트 활동 | 봇만 봐도 진행 상황 파악 |
| **권한 말풍선** | 터미널 안 봐도 Allow/Deny | 컨텍스트 스위칭 비용 ↓ |
| **다중 세션 대시보드** | 모든 세션 + 이벤트 통합 뷰 | 여러 에이전트 동시 운영 |
| **Mini Mode + DnD** | 방해 최소화 | 사무실/집중 모드 친화 |
| **테마 시스템** | SVG + GIF 조합 | 본인 캐릭터로 커스터마이즈 |

> 💎 **오늘의 한 줄:**
> **"봇은 장식이 아니에요. 시야 끝에서 깜빡이는 작은 신호 하나가, 5분의 헛된 터미널 응시를 막아줘요."**

---

## 📚 공식 문서

- 🦀 [Clawd on Desk (sinnarasam fork)](https://github.com/sinnarasam/clawd-on-desk)
- 🌊 [업스트림 원작 (rullerzhou-afk)](https://github.com/rullerzhou-afk/clawd-on-desk)
- 🐛 [에이전트별 알려진 제약](https://github.com/rullerzhou-afk/clawd-on-desk/blob/main/docs/guides/known-limitations.md)
- 🐧 [Codex + WSL 안내](https://github.com/rullerzhou-afk/clawd-on-desk/blob/main/docs/guides/codex-wsl-clarification.md)
- 📜 라이선스: AGPL-3.0 (소스), 캐릭터 아트는 별도 권리 (Anthropic 비공식 팬 프로젝트)

---

## 🎓 다음 단계

| 다음 도전 | 어떤 걸 배우게 되나 |
|---|---|
| **권한 말풍선만으로 워크플로 운영** | 컨텍스트 스위칭 절감 측정 |
| **본인 캐릭터로 테마 만들기** | SVG · GIF 애니메이션 제작 |
| **여러 에이전트 동시 운영** | Claude + Codex + Cursor 비교 |
| **Auto-start로 부팅 시 자동 띄우기** | 일상 루틴에 통합 |
| **소스 빌드해서 기능 추가** | Electron · IPC · hook 시스템 |

이어서 추천하는 가이드:

- [Claude HUD 설치 가이드](./1-6.claude-hud-install-guide.md) — 상태바 버전, Clawd와 같이 켜두면 시너지 ✨
- [데스크톱 클로드봇 만들기](./claude-pet-desktop-tutorial.md) — 직접 Python으로 데스크톱 펫을 만들어보고 싶다면
- [Skills & Remote Control](./skills-and-remote-control.md) — Claude Code를 더 자동화하는 다른 방법

---

## 🌱 마무리: Fail Forward

설치 후 며칠 써보면서…

- 🟢 **잘 풀렸다면** → 어떤 상태가 가장 도움이 됐는지 한 줄 적어두세요. ("notification 덕분에 슬랙 보다가도 안 놓침")
- 🟡 **반쯤 풀렸다면** → hook 등록은 됐는데 어떤 동작에서 잘못된 상태가 떴는지 메모. GitHub Issue 거리예요.
- 🔴 **막혔다면** → 설치 단계에서 막혔는지, 실행 후 hook 연동에서 막혔는지 분리해서 적어두세요. **에러 메시지 통째로** 가 핵심.

```markdown
## 오늘의 학습 노트

- 작업 일자:
- 설치한 OS / 방식:
- Clawd가 처음 보여준 상태:
- 가장 도움이 된 상태:
- 거슬렸던 점 / 끄고 싶은 기능:
- 다음에 시도할 것 (테마? 단축키 변경?):
```

> 💎 도구는 **나에게 맞춰 길들이는** 거예요. 처음엔 거슬리던 봇이, 며칠 지나면 시야 끝의 든든한 동료가 돼요. 며칠 써보고 판단하세요. 🌱

---

📅 작성일: 2026.05.05
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
