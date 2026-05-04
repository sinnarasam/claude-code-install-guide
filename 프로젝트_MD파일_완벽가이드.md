# 📚 프로젝트 MD 파일 완벽 가이드

> 실제 프로젝트 샘플로 배우는 마크다운 문서의 모든 것

---

## 📖 먼저, MD 파일이 뭔가요?

**MD = Markdown(마크다운)** 의 줄임말이에요.
- **mark** = "표시하다"
- **down** = "아래로, 단순하게"

→ **"간단한 표시만으로 글을 예쁘게 꾸미는 문서 형식"** 이라는 뜻이에요.

`# 제목`, `**굵게**`, `- 목록` 이런 간단한 기호로 문서를 작성할 수 있어요. HTML보다 훨씬 쉽죠!

GitHub, Notion, Slack 등 거의 모든 개발 도구가 마크다운을 지원해요. 그래서 개발 문서는 거의 다 .md 파일이에요. 📝

---

## 🗂️ 프로젝트에서 자주 만나는 MD 파일들

크게 **5개 카테고리**로 나눠서 설명드릴게요.

### 📘 카테고리 1: 프로젝트 소개용 (필수)

| 파일명 | 역할 | 누가 읽나? |
|--------|------|-----------|
| **README.md** | 프로젝트 첫인상, 소개서 | 모두 (필수!) |
| **CHANGELOG.md** | 버전별 변경 이력 | 사용자, 개발자 |
| **LICENSE.md** | 사용 권한, 라이선스 | 사용자, 법무팀 |

### 🤝 카테고리 2: 협업/기여용

| 파일명 | 역할 | 누가 읽나? |
|--------|------|-----------|
| **CONTRIBUTING.md** | 기여하는 방법 안내 | 외부 기여자 |
| **CODE_OF_CONDUCT.md** | 행동 강령 (예의 규칙) | 커뮤니티 멤버 |
| **PULL_REQUEST_TEMPLATE.md** | PR 작성 양식 | 코드 제출자 |
| **ISSUE_TEMPLATE.md** | 이슈 작성 양식 | 버그 신고자 |

### 🔒 카테고리 3: 보안/정책용

| 파일명 | 역할 |
|--------|------|
| **SECURITY.md** | 보안 취약점 신고 방법 |
| **PRIVACY.md** | 개인정보 처리 방침 |

### 🤖 카테고리 4: AI/도구용

| 파일명 | 역할 |
|--------|------|
| **CLAUDE.md** | Claude Code용 프로젝트 매뉴얼 |
| **HANDOFF.md** | 작업 인수인계 메모 (비공식) |
| **.cursorrules / CURSOR.md** | Cursor AI용 규칙 |
| **AGENTS.md** | AI 에이전트용 지침 |

### 📂 카테고리 5: 기술 문서용 (`/docs` 폴더 안)

| 파일명 | 역할 |
|--------|------|
| **ARCHITECTURE.md** | 시스템 구조 설명 |
| **API.md** | API 명세서 |
| **DEPLOYMENT.md** | 배포 방법 |
| **SETUP.md / INSTALL.md** | 설치 방법 |
| **TROUBLESHOOTING.md** | 자주 나오는 에러 해결법 |
| **ROADMAP.md** | 향후 개발 계획 |
| **FAQ.md** | 자주 묻는 질문 |

---

## 🏪 실제 프로젝트 샘플로 보기

가상의 프로젝트로 설명할게요. **"맛집 추천 웹앱(YumYum)"** 을 만든다고 가정해봅시다! 🍔

### 프로젝트 폴더 구조

```
yumyum/
├── README.md                    ← 1. 프로젝트 소개
├── CHANGELOG.md                 ← 2. 변경 이력
├── LICENSE.md                   ← 3. 라이선스
├── CONTRIBUTING.md              ← 4. 기여 방법
├── CODE_OF_CONDUCT.md           ← 5. 행동 강령
├── SECURITY.md                  ← 6. 보안 정책
├── CLAUDE.md                    ← 7. Claude용 매뉴얼
├── HANDOFF.md                   ← 8. 작업 인수인계
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md ← 9. PR 템플릿
│   └── ISSUE_TEMPLATE.md        ← 10. 이슈 템플릿
├── docs/
│   ├── ARCHITECTURE.md          ← 11. 시스템 구조
│   ├── API.md                   ← 12. API 명세서
│   ├── DEPLOYMENT.md            ← 13. 배포 방법
│   ├── SETUP.md                 ← 14. 설치 방법
│   └── TROUBLESHOOTING.md       ← 15. 문제 해결
└── src/
    └── ... (실제 코드)
```

---

## 1️⃣ README.md — 프로젝트의 얼굴 😎

**가장 중요한 파일!** GitHub에 올리면 첫 화면에 보여요. 사람이 처음 보는 정보.

````markdown
# 🍔 YumYum - 맛집 추천 웹앱

> 위치 기반으로 주변 맛집을 추천해주는 서비스

![License](https://img.shields.io/badge/license-MIT-blue)
![Version](https://img.shields.io/badge/version-1.2.0-green)

## ✨ 주요 기능
- 📍 GPS 기반 주변 맛집 검색
- ⭐ 사용자 리뷰 및 평점
- 🔖 즐겨찾기 저장
- 🗺️ 카카오맵 연동

## 🚀 빠른 시작

```bash
git clone https://github.com/myteam/yumyum.git
cd yumyum
npm install
npm run dev
```

서버가 http://localhost:3000 에서 실행됩니다.

## 📸 스크린샷
![메인 화면](./docs/images/main.png)

## 🛠️ 기술 스택
- Frontend: React, TypeScript, TailwindCSS
- Backend: Node.js, Express, PostgreSQL
- Deploy: Vercel, AWS

## 📖 자세한 문서
- [설치 가이드](./docs/SETUP.md)
- [API 문서](./docs/API.md)
- [기여 방법](./CONTRIBUTING.md)

## 📝 라이선스
MIT License - 자세한 내용은 [LICENSE](./LICENSE.md) 참고
````

> 💡 **README의 핵심**: "이게 뭔지", "어떻게 쓰는지", "어디서 더 알 수 있는지" 3가지!

---

## 2️⃣ CHANGELOG.md — 변경 이력 📜

**버전마다 뭐가 바뀌었는지** 기록해요. 사용자가 업데이트할 때 참고해요.

```markdown
# 변경 이력

## [1.2.0] - 2026-05-01
### ✨ 추가
- 즐겨찾기 폴더 분류 기능
- 다크 모드 지원

### 🐛 수정
- 검색 결과 중복 표시 버그 수정
- iOS Safari에서 지도 안 보이는 문제 해결

### 🗑️ 제거
- 사용하지 않던 레거시 API 제거

## [1.1.0] - 2026-04-15
### ✨ 추가
- 카카오 로그인 지원

## [1.0.0] - 2026-03-01
### 🎉 첫 출시
- 기본 맛집 검색 기능
- 리뷰 작성 기능
```

> 💡 **꿀팁**: [keep a changelog](https://keepachangelog.com) 라는 표준 양식을 따르는 게 일반적이에요. 카테고리는 `Added`, `Changed`, `Deprecated`, `Removed`, `Fixed`, `Security` 6가지를 써요.

---

## 3️⃣ LICENSE.md — 라이선스 ⚖️

**이 코드를 누가 어떻게 쓸 수 있는지** 정하는 법적 문서예요.

```markdown
MIT License

Copyright (c) 2026 YumYum Team

이 소프트웨어는 누구나 자유롭게 사용, 복사, 수정, 배포할 수 있습니다.
단, 저작권 표시는 유지해야 합니다.
```

> 💡 **자주 쓰는 라이선스**:
> - **MIT** — "마음대로 쓰세요" (가장 자유로움) 👍
> - **Apache 2.0** — MIT + 특허 보호
> - **GPL** — "쓴 것도 오픈소스로 공개해야 함" (전염성)
> - **Proprietary** — "회사 내부 전용, 외부 사용 금지"

---

## 4️⃣ CONTRIBUTING.md — 기여 방법 🤝

**외부 개발자가 코드를 보내고 싶을 때** 따라야 할 규칙을 적어요.

```markdown
# 기여 가이드

YumYum에 관심 가져주셔서 감사합니다! 🎉

## 🐛 버그를 발견했어요
1. Issues에서 중복 확인
2. 새 이슈 작성 (템플릿 사용)
3. 재현 방법, 예상 동작, 실제 동작 명시

## 💡 새 기능을 제안하고 싶어요
1. 먼저 Discussions에 글을 올려 의견 수렴
2. 합의되면 이슈 생성 후 PR 작성

## 🔧 코드 기여 절차
1. 저장소 Fork
2. 새 브랜치 생성: `git checkout -b feature/내기능`
3. 변경사항 커밋
4. PR 생성 (템플릿 작성 필수)

## 📐 코드 규칙
- ESLint, Prettier 설정 따르기
- 커밋 메시지: Conventional Commits 형식
  - `feat: 새 기능`
  - `fix: 버그 수정`
  - `docs: 문서 수정`
- 테스트 코드 필수
```

---

## 5️⃣ CODE_OF_CONDUCT.md — 행동 강령 🙏

**커뮤니티에서 지켜야 할 예의**를 정해요.

```markdown
# 행동 강령

## 우리의 약속
모든 참여자가 존중받는 환경을 만들기 위해 노력합니다.

## 권장 행동
- ✅ 친절하고 포용적인 언어 사용
- ✅ 다른 의견 존중
- ✅ 건설적인 비판 받아들이기

## 금지 행동
- ❌ 성적인 발언 또는 이미지
- ❌ 인신공격, 모욕
- ❌ 차별 발언 (성별, 인종, 종교 등)
- ❌ 사적인 정보 무단 공개

## 신고
violation@yumyum.com 으로 신고해주세요.
```

> 💡 보통 [Contributor Covenant](https://www.contributor-covenant.org/)라는 표준 양식을 그대로 가져다 써요.

---

## 6️⃣ SECURITY.md — 보안 정책 🔒

**보안 취약점을 발견했을 때 어떻게 신고하는지** 안내해요.

```markdown
# 보안 정책

## 지원 버전
| 버전 | 보안 업데이트 |
| ---- | ------------ |
| 1.2.x | ✅ 지원 |
| 1.1.x | ✅ 지원 |
| 1.0.x | ❌ 미지원 |

## 취약점 신고
보안 이슈는 **공개 이슈로 올리지 마세요!**

📧 security@yumyum.com 로 비공개 신고해주세요.

24시간 내 응답, 7일 내 패치를 목표로 합니다.
```

---

## 7️⃣ CLAUDE.md — Claude 전용 매뉴얼 🤖

**Claude Code가 자동으로 읽는 파일**! 프로젝트 규칙을 알려줘요.

```markdown
# YumYum 프로젝트 가이드 (Claude용)

## 프로젝트 개요
위치 기반 맛집 추천 웹앱. React + Node.js 풀스택.

## 기술 스택
- Frontend: React 18, TypeScript, TailwindCSS, Vite
- Backend: Node.js 20, Express, Prisma
- DB: PostgreSQL 15
- 패키지 매니저: pnpm

## 명령어
- `pnpm dev`: 개발 서버 (프론트+백엔드 동시 실행)
- `pnpm test`: 테스트 실행
- `pnpm lint`: 린트 검사
- `pnpm db:migrate`: DB 마이그레이션

## 코딩 규칙
- 함수명: camelCase
- 컴포넌트명: PascalCase
- 상수: UPPER_SNAKE_CASE
- 들여쓰기: 스페이스 2칸
- 세미콜론: 사용

## 금지사항
- main 브랜치 직접 push 금지
- console.log 커밋 금지
- any 타입 사용 금지
```

---

## 8️⃣ HANDOFF.md — 작업 인수인계 📝

**오늘 작업한 내용을 다음 세션에 넘기는 메모**예요.

```markdown
# 작업 인수인계 (2026-05-05)

## 🎯 현재 작업
즐겨찾기 폴더 분류 기능 구현

## ✅ 완료
- [x] DB 스키마 추가 (FavoriteFolder 모델)
- [x] POST /folders API 구현
- [x] 폴더 생성 UI 컴포넌트

## 🚧 진행 중
- [ ] 폴더 이동 드래그앤드롭 (70%)
  - react-dnd 라이브러리 적용 중
  - 모바일 터치 이벤트 처리 막힘

## 📋 다음 할 일
1. 모바일 드래그 처리
2. 폴더별 색상 지정 기능
3. 통합 테스트 작성
```

---

## 9️⃣ PULL_REQUEST_TEMPLATE.md — PR 템플릿

**Pull Request(PR)** 작성할 때 자동으로 채워지는 양식이에요.

> 💡 **PR이란?** "내가 짠 코드 합쳐주세요!" 라고 요청하는 거예요.

```markdown
## 📌 변경 내용
<!-- 어떤 변경을 했는지 간단히 설명 -->

## 🎯 관련 이슈
Closes #이슈번호

## 🧪 테스트 방법
1. 
2. 

## ✅ 체크리스트
- [ ] 테스트 통과 확인
- [ ] 린트 에러 없음
- [ ] CHANGELOG 업데이트
- [ ] 문서 업데이트 (필요 시)
```

---

## 🔟 ISSUE_TEMPLATE.md — 이슈 템플릿

```markdown
## 🐛 버그 설명
<!-- 무엇이 잘못됐는지 -->

## 🔄 재현 단계
1. 
2. 
3. 

## ✅ 예상 동작
## ❌ 실제 동작

## 🖥️ 환경
- OS: [예: macOS 14.0]
- 브라우저: [예: Chrome 120]
- 버전: [예: 1.2.0]
```

---

## 1️⃣1️⃣ ARCHITECTURE.md — 시스템 구조 🏗️

```markdown
# 시스템 아키텍처

## 전체 구조
[사용자] → [Vercel Frontend] → [AWS EC2 Backend] → [AWS RDS PostgreSQL]
                                       ↓
                                   [Redis 캐시]

## 주요 컴포넌트

### Frontend (React)
- Pages: 라우팅 단위
- Components: 재사용 UI
- Hooks: 비즈니스 로직

### Backend (Express)
- Routes: API 엔드포인트
- Services: 비즈니스 로직
- Models: DB 모델 (Prisma)
```

---

## 1️⃣2️⃣ API.md — API 명세서 📡

````markdown
# API 문서

## 인증

### POST /api/auth/login
로그인하고 토큰 받기

**요청:**
```json
{
  "email": "user@example.com",
  "password": "비밀번호"
}
```

**응답 (200):**
```json
{
  "token": "eyJhbGc...",
  "user": { "id": 1, "name": "홍길동" }
}
```
````

> 💡 요즘은 **Swagger/OpenAPI** 같은 자동 생성 도구를 많이 써요.

---

## 1️⃣3️⃣ DEPLOYMENT.md — 배포 방법 🚀

````markdown
# 배포 가이드

## Frontend 배포 (Vercel)
1. Vercel에 GitHub 저장소 연결
2. 환경변수 설정
3. main 브랜치에 push하면 자동 배포

## Backend 배포 (AWS EC2)
1. EC2 인스턴스 생성
2. SSH 접속 후 Node.js 설치
3. PM2로 실행:
```bash
pm2 start npm --name yumyum -- start
```
````

---

## 1️⃣4️⃣ SETUP.md — 설치 방법 ⚙️

````markdown
# 개발 환경 세팅

## 필수 프로그램
- Node.js 20 이상
- pnpm 8 이상
- PostgreSQL 15
- Git

## 설치 단계

### 1. 저장소 클론
```bash
git clone https://github.com/myteam/yumyum.git
cd yumyum
```

### 2. 의존성 설치
```bash
pnpm install
```

### 3. 환경변수 설정
```bash
cp .env.example .env
```

### 4. 개발 서버 실행
```bash
pnpm dev
```
````

---

## 1️⃣5️⃣ TROUBLESHOOTING.md — 문제 해결 🔧

````markdown
# 문제 해결

## ❌ "DATABASE_URL is not defined"
**원인**: 환경변수가 설정되지 않음
**해결**: `.env` 파일 확인

## ❌ "Port 3000 already in use"
**해결**:
```bash
lsof -i :3000
kill -9 [PID]
```
````

---

## 🎯 실전 적용 가이드

### 프로젝트 규모에 따라 다르게!

**🌱 작은 개인 프로젝트 (필수만)**
```
├── README.md       ← 이거 하나면 충분!
└── LICENSE.md      ← 오픈소스라면
```

**🌳 중간 규모 팀 프로젝트**
```
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── LICENSE.md
├── CLAUDE.md
└── docs/
    ├── SETUP.md
    └── API.md
```

**🌲 대규모 오픈소스 / 회사 프로덕트**
```
├── README.md
├── CHANGELOG.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── LICENSE.md
├── CLAUDE.md
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── ISSUE_TEMPLATE/
└── docs/
    ├── ARCHITECTURE.md
    ├── API.md
    ├── DEPLOYMENT.md
    ├── SETUP.md
    └── TROUBLESHOOTING.md
```

---

## 💡 실무 꿀팁 모음

### 1. 우선순위는 README → SETUP → API 순
처음 문서 만들 땐 욕심내지 말고 **README부터 잘 쓰세요**.

### 2. 마크다운 작성 단축키 (VS Code)
- 미리보기: `Ctrl + Shift + V`
- 마크다운 린터 추천: `markdownlint`

### 3. 이모지 활용
```
✨ 기능   🐛 버그   📝 문서   🚀 배포
🔒 보안   ⚡ 성능   🎨 디자인   🧪 테스트
```

### 4. Badge(뱃지) 활용
[shields.io](https://shields.io)에서 예쁜 뱃지 만들 수 있어요.

### 5. 다이어그램은 Mermaid로
GitHub은 마크다운 안에서 Mermaid 다이어그램을 자동 렌더링해줘요.

### 6. 한국어 vs 영어
- 국내 팀: 한국어 OK
- 오픈소스: 영어 권장

---

## 📋 체크리스트: 새 프로젝트 시작할 때

- [ ] README.md 작성 (필수)
- [ ] LICENSE 선택
- [ ] .gitignore 설정
- [ ] CLAUDE.md 작성 (AI 협업 시)
- [ ] 1주일 후: SETUP.md, CONTRIBUTING.md 추가 검토
- [ ] 1.0 출시 전: CHANGELOG.md, API.md 작성
- [ ] 오픈소스 공개 전: SECURITY.md, CODE_OF_CONDUCT.md 추가

---

## 🎁 보너스: README.md 작성 황금 공식

좋은 README는 이 순서를 따라요:

1. **제목 + 한 줄 설명** (5초 안에 파악되게)
2. **뱃지** (빌드 상태, 버전 등)
3. **데모/스크린샷**
4. **주요 기능** (불릿 포인트)
5. **빠른 시작** (3-5줄 명령어)
6. **상세 문서 링크**
7. **기여 / 라이선스 / 연락처**

---

## 📌 마무리

**MD 파일은 "글로 된 설계도이자 매뉴얼"** 이에요.

코드만 있으면 다른 사람(미래의 나 포함!)이 못 알아봐요.
**좋은 문서는 좋은 코드만큼 가치 있어요.** 📚✨

---

> 작성: 2026-05-05  
> 작성자: 친절한 개발자 과외 선생님 (with Claude)
