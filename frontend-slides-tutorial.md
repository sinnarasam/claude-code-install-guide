# Frontend Slides — 코드 한 줄 없이 멋진 프리젠테이션 만들기 🎨📽️

> CSS·JS 몰라도 괜찮아요. **Claude에게 "느낌"을 보여주고 고르기**만 하면 돼요.
> PPT를 웹으로, 아이디어를 슬라이드로 — **Vibe Coding 식 발표 자료 만들기** 시작!

---

## 🎯 학습 목표

이 실습을 마치면 다음을 할 수 있어요:

- ✅ **frontend-slides Skill** 의 동작 원리·철학 이해
- ✅ Plugin Marketplace로 Skill **설치·확인**
- ✅ 빈 화면에서 **프리젠테이션 1개를 처음부터** 생성
- ✅ 기존 **PPT/PPTX 파일을 웹 슬라이드로 변환**
- ✅ 결과물을 **Vercel 배포 / PDF 추출** 로 공유

---

## 📑 목차

- [시작하기 전에](#-시작하기-전에)
- [1. frontend-slides가 뭐예요?](#1️⃣-frontend-slides가-뭐예요)
- [2. 설치 — Plugin Marketplace](#2️⃣-설치--plugin-marketplace)
- [3. 실습 ①: 처음부터 슬라이드 만들기](#3️⃣-실습--처음부터-슬라이드-만들기)
- [4. 실습 ②: PPT 파일을 웹으로 변환](#4️⃣-실습--ppt-파일을-웹으로-변환)
- [5. 결과물 공유 — 배포 & PDF](#5️⃣-결과물-공유--배포--pdf)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🎯 오늘 배운 핵심 정리](#-오늘-배운-핵심-정리)
- [📚 공식 문서](#-공식-문서)
- [🎓 다음 단계](#-다음-단계)

---

## 📋 시작하기 전에

- ✅ Claude Code 설치 완료 → [설치 가이드](<./1-1. claude-code-install-guide.md>)
- ✅ [Skills & Remote Control 실습](./skills-and-remote-control.md) 완료 — Skill의 개념을 먼저 잡고 오면 100배 수월해요
- ✅ Claude.ai **Pro / Max / Team / Enterprise** 구독 (Plugin Marketplace 사용 권장)
- ✅ Node.js 설치 (배포·PDF 추출 시) — `node --version` 으로 확인
- ✅ Python + `python-pptx` 라이브러리 (PPT 변환 시)

> ⏱ **소요 시간**: 약 60~90분
> 🎯 **권장 모드**: 일반 모드 (창작 중심이라 Plan 모드까진 불필요)

### 작업 폴더 준비

```powershell
mkdir slides-practice
cd slides-practice
claude
```

---

## 1️⃣ frontend-slides가 뭐예요?

### 🤔 한마디로

**디자이너가 아니어도** Claude에게 "이런 느낌으로!" 라고 말만 하면, **단일 HTML 파일** 형태의 프리젠테이션을 뚝딱 만들어주는 Skill이에요.

### 비유로 이해하기

| 익숙한 것 | frontend-slides |
|----------|-----------------|
| 🍱 도시락 메뉴판 | 12가지 비주얼 프리셋 중에서 **눈으로 보고** 골라요 |
| 🎨 옷 가게 시착 | "어울리는 거 입어보고" 결정 — 말로 설명 안 해도 OK |
| 📦 IKEA 가구 | 의존성 없는 **단일 파일** — 박스 하나 풀면 끝 |

### 📐 다른 슬라이드 도구와 비교

| 도구 | 단점 | frontend-slides |
|------|------|-----------------|
| **PowerPoint** | 무겁고 협업 어려움 | 단일 HTML, 브라우저면 OK |
| **Reveal.js** | 코드 직접 작성 필요 | Claude가 다 써줌 |
| **Gamma·Tome** | 결과물이 비슷비슷 (AI 슬롭) | 12개 큐레이션된 **차별화 스타일** |
| **Google Slides** | 디자인 자유도 낮음 | CSS 기반 — 무한 커스텀 |

### 🧱 핵심 철학 4가지

1. 🪶 **Zero Dependencies** — npm, 빌드 도구 없음. HTML 파일 하나로 동작
2. 👀 **Show, don't tell** — "미니멀하게 해줘" 말로 헤매지 말고, 시안 보고 고르기
3. 🚫 **Anti-AI-Slop** — 흔한 보라색 그라데이션 회피, 큐레이션된 스타일만
4. 📜 **Comments are kindness** — 생성된 코드는 **나중의 나도 읽을 수 있게** 주석 충실

### 📁 Skill의 구성 (Progressive Disclosure)

```
frontend-slides/
├── SKILL.md              ← 메인 워크플로 (~180줄, 항상 로드)
├── STYLE_PRESETS.md      ← 12개 비주얼 프리셋 (스타일 선택 시)
├── viewport-base.css     ← 반응형 기본 CSS (생성 시)
├── html-template.md      ← HTML 구조 + JS 기능 (생성 시)
├── animation-patterns.md ← 애니메이션 레퍼런스 (생성 시)
└── scripts/
    ├── extract-pptx.py   ← PPT 변환용 (변환 시만)
    ├── deploy.sh         ← Vercel 배포 (공유 시만)
    └── export-pdf.sh     ← PDF 추출 (공유 시만)
```

> 💡 **핵심**: SKILL.md는 "지도", 나머지는 "필요할 때만 펴보는 페이지". OpenAI의 *harness engineering* 원칙 — "1,000페이지 매뉴얼이 아니라 지도를 줘라" 그대로예요.

---

## 2️⃣ 설치 — Plugin Marketplace

### 🛒 방법 1: Plugin Marketplace (권장)

Claude Code 안에서 **두 줄**로 끝나요.

```
/plugin marketplace add sinnarasam/frontend-slides
/plugin install frontend-slides@frontend-slides
```

> 💡 원본 저자 저장소를 쓰고 싶다면 `zarazhangrui/frontend-slides` 로 대체 가능해요. 둘 다 동일한 Skill 코드예요.

### 🛠 방법 2: 수동 설치

Plugin Marketplace를 못 쓰는 환경이라면 직접 복사하세요.

```bash
# Skill 디렉토리 생성
mkdir -p ~/.claude/skills/frontend-slides/scripts

# 저장소 클론
git clone https://github.com/sinnarasam/frontend-slides.git

# 파일 복사
cp frontend-slides/SKILL.md \
   frontend-slides/STYLE_PRESETS.md \
   frontend-slides/viewport-base.css \
   frontend-slides/html-template.md \
   frontend-slides/animation-patterns.md \
   ~/.claude/skills/frontend-slides/

cp frontend-slides/scripts/*.py \
   frontend-slides/scripts/*.sh \
   ~/.claude/skills/frontend-slides/scripts/
```

### ✅ 설치 확인

```
/help
```

목록에 `frontend-slides` 가 보이면 성공! 또는 직접 호출:

```
/frontend-slides
```

> ⚠️ Plugin이 안 보이면 세션을 재시작하세요. `/exit` → `claude` 다시 실행.

---

## 3️⃣ 실습 ①: 처음부터 슬라이드 만들기

### 🎬 시나리오

**주제**: "Claude Code를 5분 만에 소개하기" 라는 발표 자료를 만들어요.

### Step 1. Skill 호출

```
/frontend-slides

"Claude Code 5분 소개" 라는 제목으로 5장짜리 발표 자료 만들어줘.
청중은 처음 듣는 비개발자이고, 실제 활용 사례 중심으로 가벼운 톤.
```

### Step 2. Claude의 첫 응답 — 콘텐츠 확인

Claude는 먼저 **슬라이드별 개요**를 보여줘요.

```
Slide 1: Hook — "코드를 못 짜도 코딩이 가능하다고요?"
Slide 2: Claude Code란? (한 줄 정의 + 비유)
Slide 3: 5분 만에 할 수 있는 것 3가지
Slide 4: 실제 사례 (스크린샷 자리)
Slide 5: 시작하는 법 (QR + URL)

이대로 진행할까요? 수정할 부분 있나요?
```

→ 이 단계에서 **순서 변경, 내용 추가, 톤 조정** 을 자유롭게 요청하세요.

### Step 3. 비주얼 스타일 선택

콘텐츠가 확정되면, Claude가 **여러 스타일 시안**을 보여줘요. 12개 프리셋 중 어울리는 톤을 추천해 줘요.

| 카테고리 | 스타일 | 어울리는 발표 |
|---------|--------|--------------|
| 🌑 **Dark** | Bold Signal | 강렬한 메시지, 키노트 |
| 🌑 **Dark** | Electric Studio | 깔끔한 프로페셔널, B2B |
| 🌑 **Dark** | Creative Voltage | 레트로 + 네온, 크리에이티브 |
| 🌑 **Dark** | Dark Botanical | 우아한 따뜻함, 브랜딩 |
| ☀️ **Light** | Notebook Tabs | 에디토리얼, 정리된 느낌 |
| ☀️ **Light** | Pastel Geometry | 친근하고 부드러움 |
| ☀️ **Light** | Split Pastel | 발랄, 모던 |
| ☀️ **Light** | Vintage Editorial | 위트, 개성 |
| ✨ **Specialty** | Neon Cyber | SF, 게임, 미래적 |
| ✨ **Specialty** | Terminal Green | 개발자, 해커 미감 |
| ✨ **Specialty** | Swiss Modern | 미니멀, 바우하우스 |
| ✨ **Specialty** | Paper & Ink | 문학적, 인쇄물 느낌 |

> 💡 **선택을 못 하겠으면**: "비개발자 청중에 부드러운 느낌이면 좋겠어" 라고 말하면 Claude가 **2~3개로 좁혀** 추천해줘요.

### Step 4. HTML 생성 & 미리보기

스타일을 고르면 Claude가 `presentation.html` 같은 파일을 생성해요. 브라우저에서 바로 열어보세요.

```powershell
start presentation.html
```

🍎 macOS:

```bash
open presentation.html
```

🐧 Linux:

```bash
xdg-open presentation.html
```

### Step 5. 반복 수정

```
3번 슬라이드 폰트가 너무 큰 것 같아. 한 단계 줄여줘.
4번 슬라이드에 실제 스크린샷 넣을 자리에 placeholder 만들어줘.
```

→ Claude가 HTML을 직접 수정. **새로고침** 만 하면 바로 확인 가능!

### 🏋️ 실습 미션

```
1. /frontend-slides 호출
2. 본인 자기소개 3장 슬라이드 요청
3. 라이트 테마 1개, 다크 테마 1개로 각각 만들어보기
4. 어느 쪽이 본인에게 어울리는지 회고
```

---

## 4️⃣ 실습 ②: PPT 파일을 웹으로 변환

### 🎬 시나리오

**상황**: 회사에서 받은 `.pptx` 파일이 있는데, 노트북·폰 어디서든 보고 싶고 링크로도 공유하고 싶어요.

### 📋 사전 요구사항

```bash
# python-pptx 설치
pip install python-pptx
```

> 🪟 Windows에서 `pip` 명령이 안 되면 `python -m pip install python-pptx`

### Step 1. 파일을 작업 폴더에 두기

```
slides-practice/
└── original.pptx     ← 변환할 원본
```

### Step 2. Skill에 변환 요청

```
/frontend-slides

original.pptx 파일을 웹 프리젠테이션으로 변환해줘.
이미지는 그대로 살리고, 스타일은 Electric Studio로.
```

### Step 3. Claude의 작업 흐름

```
1️⃣ scripts/extract-pptx.py 실행 → 텍스트·이미지 추출
2️⃣ 슬라이드별 콘텐츠 미리보기 → "이대로 변환할까요?"
3️⃣ Electric Studio 스타일 적용 → HTML 생성
4️⃣ 추출된 이미지를 같은 폴더에 보존
```

### Step 4. 결과 확인

```
my-deck/
├── index.html          ← 메인 슬라이드
├── images/             ← 원본 PPT의 이미지들
│   ├── slide1-img.png
│   └── slide3-chart.jpg
└── ...
```

브라우저에서 `index.html` 열어서 확인.

### ⚠️ PPT 변환의 한계

| 변환되는 것 | 변환되지 않는 것 |
|-----------|----------------|
| ✅ 텍스트, 제목 | ❌ 슬라이드 마스터 디자인 |
| ✅ 이미지 (원본 보존) | ❌ 복잡한 도형·차트 (텍스트로 대체) |
| ✅ 슬라이드 순서 | ❌ 슬라이드 전환 효과 |
| ✅ 글머리 기호 | ❌ 애니메이션 |

> 💡 **팁**: 변환 후 "이 슬라이드의 차트를 텍스트 표로 만들어줘" 같은 후속 요청으로 다듬으세요.

---

## 5️⃣ 결과물 공유 — 배포 & PDF

### 🌐 방법 ①: Vercel로 배포 (URL 공유)

영구적인 URL이 생겨서 **카톡·슬랙으로 링크만 던지면** 누구나 볼 수 있어요.

```bash
bash scripts/deploy.sh ./my-deck/
# 또는 단일 HTML
bash scripts/deploy.sh ./presentation.html
```

처음이면 Vercel 가입·로그인을 안내해줘요. 무료 플랜으로 충분.

```
🚀 Deploying...
✅ Deployed!
   URL: https://my-deck-abc123.vercel.app
```

> ⚠️ **민감한 자료 주의**: Vercel 무료 플랜은 **공개 URL** 이에요. 사내 정보가 담긴 슬라이드라면 비공개 옵션을 쓰거나, PDF로만 공유하세요.

### 📄 방법 ②: PDF 추출 (이메일·인쇄)

```bash
bash scripts/export-pdf.sh ./my-deck/index.html
# 출력 경로 지정
bash scripts/export-pdf.sh ./presentation.html ./output.pdf
```

내부적으로 [Playwright](https://playwright.dev) 가 각 슬라이드를 1920×1080 으로 스크린샷 → PDF 결합.

| 장점 | 단점 |
|------|------|
| ✅ 첨부 파일로 공유 | ❌ 애니메이션 사라짐 (정적 스냅샷) |
| ✅ 인쇄 가능 | ❌ 인터랙티브 요소 사라짐 |
| ✅ 오프라인 | ❌ 동영상 사라짐 |

### 🎯 어떤 걸 언제 쓰나요?

| 상황 | 추천 |
|------|------|
| 발표 중 노트북에서 시연 | 🌐 그냥 HTML 파일 열기 |
| 원격 청중에게 공유 | 🌐 Vercel 배포 |
| 이메일로 첨부 | 📄 PDF 추출 |
| 사내 보안 자료 | 📄 PDF (배포 X) |

---

## 🪞 5분 회고

여기까지 따라왔다면 정말 멋져요! 잠시 멈추고 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 이번에 만들어 본 슬라이드 중 가장 마음에 든 스타일은?**
- 왜 그게 마음에 들었나요? — 본인의 미감을 발견하는 순간이에요

**2. PPT 변환과 처음부터 만들기, 어느 쪽이 더 효율적이었나요?**

**3. "코드 한 줄도 안 짰는데 슬라이드가 나왔다" — 이 경험이 본인 일에 어떻게 적용될 수 있을까요?**

### 💭 토론거리

> "AI로 만든 슬라이드 vs. 디자이너가 만든 슬라이드 — 청중은 차이를 느낄까요?"
> "Vibe Coding 이 일반화되면, 디자이너의 역할은 어떻게 바뀔까요?"

---

## 🆘 자주 막히는 지점

### Q1. `/frontend-slides` 가 자동완성에 안 떠요

**A.** Skill이 제대로 설치 안 됐을 가능성. 점검 순서:

```
/help                              # 목록에서 보이는지
!ls ~/.claude/skills/              # 디렉토리 존재 확인
```

세션 재시작:

```
/exit
claude
```

### Q2. PPT 변환할 때 "python-pptx not found" 에러

**A.** 라이브러리 설치 필요:

```bash
pip install python-pptx
# 또는
python -m pip install python-pptx
```

가상환경 사용 중이면 활성화 후 설치:

```powershell
.\venv\Scripts\Activate.ps1
pip install python-pptx
```

### Q3. Vercel 배포 시 "command not found: vercel"

**A.** Node.js가 없거나 PATH가 안 잡혔어요.

```powershell
# Node.js 확인
node --version
npm --version

# Vercel CLI 수동 설치
npm install -g vercel
```

### Q4. PDF 추출이 시작은 되는데 안 끝나요

**A.** Playwright가 처음 실행될 때 **Chromium 다운로드** (~150MB) 가 필요해요. 첫 실행은 5~10분 걸릴 수 있어요. 진행 로그를 확인하세요.

```bash
# Playwright 수동 설치
npx playwright install chromium
```

### Q5. 슬라이드 비율이 화면에 안 맞아요

**A.** frontend-slides는 **반응형** 으로 만들어져요. 그래도 안 맞으면:

```
지금 슬라이드가 16:9 인데, 4:3 으로 바꿔줘.
viewport 설정도 같이 수정해줘.
```

→ Claude가 `viewport-base.css` 의 비율 설정을 조정.

### Q6. 회사 PPT 템플릿 디자인을 그대로 쓰고 싶어요

**A.** frontend-slides는 12개 프리셋 중심이라 회사 템플릿 그대로 재현은 어려워요. 대안:

1. 변환 후 "회사 색상 #1A2B3C 와 폰트 'Pretendard' 로 변경해줘" 식으로 후처리
2. 또는 STYLE_PRESETS.md 에 새 프리셋을 직접 추가 (고급)

---

## 🎯 오늘 배운 핵심 정리

| 개념 | 한 줄 요약 |
|------|-----------|
| 🎨 frontend-slides | 비개발자용 웹 프리젠테이션 생성 Skill |
| 🪶 Zero Dependencies | 단일 HTML 파일, 빌드·npm 불필요 |
| 👀 Show, don't tell | 말 대신 시안으로 스타일 선택 |
| 📁 Progressive Disclosure | SKILL.md는 지도, 상세는 필요 시 로드 |
| 🛒 Plugin Marketplace | `/plugin marketplace add` + `/plugin install` |
| 🎬 워크플로 | 콘텐츠 확정 → 스타일 선택 → 생성 → 반복 수정 |
| 📦 PPT 변환 | `python-pptx` 필요, 텍스트·이미지 보존 |
| 🌐 Vercel 배포 | 무료 URL, 단 공개됨에 주의 |
| 📄 PDF 추출 | Playwright 기반, 애니메이션은 사라짐 |

### 💎 가장 중요한 교훈

> **"디자인을 못 한다"는 건 사실이 아니에요. 단지 "시안 없이 말로 설명하기 힘들 뿐"이에요.**
> **frontend-slides는 그 격차를 메워주는 도구예요 — 보고, 고르고, 다듬으세요.**

---

## 📚 공식 문서

- [frontend-slides GitHub 저장소 (sinnarasam fork)](https://github.com/sinnarasam/frontend-slides)
- [frontend-slides 원본 저장소 (zarazhangrui)](https://github.com/zarazhangrui/frontend-slides)
- [Claude Code Skills 공식 문서](https://code.claude.com/docs/en/skills)
- [Claude Code Plugin Marketplace](https://code.claude.com/docs/en/plugins)
- [Vercel 공식 문서](https://vercel.com/docs)
- [Playwright 공식 문서](https://playwright.dev)

---

## 🎓 다음 단계

축하해요! 🎉 이제 **슬라이드를 코드처럼 만들고 공유** 할 수 있어요.

**바로 적용해볼 만한 것:**

1. 🎤 다음 사내 발표를 frontend-slides로 만들어보기
2. 📚 본인의 강의·튜토리얼 자료를 PPT → 웹으로 변환
3. 🔗 만든 슬라이드를 Vercel 배포 후 **링크 공유** 시도
4. 🎨 12개 프리셋을 모두 한 번씩 시도해보고 본인 미감 발견
5. 🛠 자주 쓰는 회사 색상·로고를 추가한 **커스텀 프리셋** 만들기

**더 깊이 배우고 싶다면:**

- 🛠 **[Skills & Remote Control](./skills-and-remote-control.md)** — Skill 작성 원리·보안
- ✍️ **[효과적인 프롬프트 & CLAUDE.md](./effective-prompting-and-claude-md.md)** — Claude에게 잘 부탁하는 법
- 📊 **[Spotify 데이터 분석](./spotify-data-analysis.md)** — Vibe Coding 실전 응용

---

## 🌱 마무리: Fail Forward

이 실습에서:

> 🟢 **첫 슬라이드가 한 번에 마음에 들었다면** — 본인의 미감과 잘 맞는 프리셋을 발견한 거예요. 그걸 본인 시그니처로!
> 🟡 **여러 번 수정 요청한 끝에 나왔다면** — 그게 진짜 학습이에요. "수정 요청법"이 곧 프롬프트 실력
> 🔴 **결과물이 영 안 들었다면** — 콘텐츠 단계에서 톤·청중을 더 구체적으로 적어주세요. 시안은 콘텐츠를 따라가요

학습 노트에 적어보세요:

```
✏️ 가장 마음에 든 스타일: ___
🎨 본인의 미감 키워드 3개: ___
📦 다음에 변환해보고 싶은 PPT: ___
🔗 만든 슬라이드를 누구에게 공유했나요?: ___
```

📅 작성일: 2026.05.03
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
