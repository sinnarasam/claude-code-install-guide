# Remote Control 가이드 설계 문서

- 작성일: 2026-05-05
- 작업 브랜치: `add-remote-control-guide`
- 대상 산출물: `remote-control-guide.md` (한글, 시리즈 템플릿 준수)
- 시리즈: Claude Code 강의 실습용 환경 구축 가이드 시리즈

## 1. 배경

이미 `skills-and-remote-control.md` (PR #6) 가 Skills 와 Remote Control 을 한 파일에서 다루지만, Skills 분량이 많아 Remote Control 은 짧은 단일 섹션(섹션 4)으로만 등장한다. 학습자가 "원격 제어"만 빠르게 익히고 싶을 때 진입점이 없는 상태.

본 가이드는 **Remote Control 단독 딥다이브**를 제공한다. 기존 결합 가이드는 그대로 두고, 본 가이드가 더 자세한 셋업 / 표면별 사용법 / 보안 / 트러블슈팅을 담당한다.

## 2. 사실 확인 출처 (claude-code-guide 에이전트 조사)

- 공식 문서: https://code.claude.com/docs/en/remote-control
- CLI 레퍼런스: https://code.claude.com/docs/en/cli-reference
- 보안: https://code.claude.com/docs/en/security
- 인증: https://code.claude.com/docs/en/authentication

핵심 사실:
- 정식 명칭은 "Remote Control" (research preview).
- Pro / Max / Team / Enterprise 에서 사용 가능. **claude.ai OAuth 로그인 필수, API key 미지원.**
- Claude Code v2.1.51+ 필요. VS Code 확장은 v2.1.79+.
- 진입 명령 3가지: `claude remote-control` (서버 모드) / `claude --remote-control` (인터랙티브) / 세션 안에서 `/remote-control`.
- 표면: claude.ai/code 웹, iOS / Android 모바일 앱, VS Code 확장, 로컬 터미널.
- 로컬 전용 명령: `/mcp`, `/plugin`, `/resume`. 그 외 `/compact`, `/clear`, `/context`, `/usage`, `/exit`, `/rename` 등은 원격에서도 가능.
- 보안: outbound HTTPS 만, 단명 자격증명, 코드 실행은 항상 로컬. Bedrock/Vertex 와 함께는 동작 안 함.
- 한계: 로컬 프로세스가 살아있어야 함, 네트워크 끊김 ~10분 허용, Ultraplan 시작 시 Remote Control 연결 해제.
- 푸시 알림은 `/config` 의 "Push when Claude decides" 토글로 제어.

## 3. 가이드 구조 (시리즈 템플릿 준수)

CLAUDE.md 의 13단 슬롯 순서를 그대로 따른다. 본문 번호 섹션은 6개:

1. **1️⃣ Remote Control 이 뭐예요?** — 한 줄 설명, "퇴근하면서도 작업 이어가기" 문제, research preview 표기, SSH / Codespaces / 클라우드 에이전트 와의 비교 표.
2. **2️⃣ 시작 전 체크리스트** — claude.ai 로그인 / 플랜 / 버전 / Team-Enterprise 관리자 토글 / API key 미지원 ⚠️.
3. **3️⃣ 5분 만에 켜보기** — 진입 명령 3가지 비교 표, 🍎🐧🪟 코드 블록, QR 스캔으로 모바일 연결.
4. **4️⃣ 어디서 어떻게 제어할까** — 웹 / iOS / Android / VS Code 표면별 가능/불가, local-only vs remote 명령 비교 표.
5. **5️⃣ 실전 시나리오: 카페에서 빌드 확인하기** — 🎬 점심시간 → 폰으로 테스트 결과 확인 → 승인 → 푸시 알림 의 단일 내러티브.
6. **6️⃣ 보안과 한계** — outbound only, 단명 자격증명, 코드는 로컬 실행, 10분 네트워크 허용, Bedrock/Vertex 미지원, Ultraplan 충돌.

이후 표준 꼬리 섹션:

- 🪞 5분 회고 + 💭 토론거리
- 🆘 자주 막히는 지점 (FAQ 3~5개: QR 스캔 실패 / 노트북 잠금 시 끊김 / Team 토글 미보임 / 버전 미달 / API key 사용)
- 🎯 오늘 배운 핵심 정리 (요약 표 + 💎 takeaway)
- 📚 공식 문서 (위 4개 URL)
- 🎓 다음 단계 (`./skills-and-remote-control.md`, `./effective-prompting-and-claude-md.md`, `./claude_commands-reference.md`)
- 🌱 마무리: Fail Forward 🟢🟡🔴 + 학습노트 fenced 템플릿
- 푸터: `📅 작성일: 2026.05.05` + 시리즈 시그니처

## 4. 분기 / 커밋 / PR 규약

- 분기: `add-remote-control-guide` (이미 생성)
- 커밋 메시지: `remote-control-guide.md 추가` (한글 패턴 준수)
- 커밋 대상: **새 파일만** — `hello.py`, `python-calculator/`, `cli-essentials/`, `claude-pet*.py`, `diary/`, `desktop.ini` 같은 기존 untracked 산출물은 제외.
- 본 설계 문서(`docs/superpowers/specs/2026-05-05-remote-control-guide-design.md`)는 같은 브랜치에 함께 커밋한다 (작업 기록).
- PR 은 직접 만들지 않는다. push 후 GitHub 가 표시하는 PR 생성 URL 을 사용자에게 전달한다.

## 5. 의도적으로 하지 않는 것 (YAGNI)

- 기존 `skills-and-remote-control.md` 본문은 건드리지 않는다 (이미 머지된 PR 내용에 손대지 않기 위함).
- VS Code 확장 설치 가이드는 다루지 않는다 — 별도 IDE 통합 문서(`ide-integration.md`)가 이미 존재.
- 인증/로그인 자체의 깊은 설명은 다루지 않고 `claude_commands-reference.md` 로 링크.
- 자동 스크린샷 / GIF 는 첨부하지 않는다 (시리즈 다른 가이드 관행과 동일).

## 6. 실측 검증 결과 (2026-05-05, claude v2.1.126)

`claude remote-control` 을 실제로 실행해 확인한 사실. 초기 가이드에서 잘못 적었던 부분을 정정해 반영함.

| 항목 | 초기 가이드 | 실측 |
|------|------------|------|
| 이름 지정 진입 | `claude --remote-control "이름"` ❌ (그런 플래그 없음) | `claude remote-control --name "이름"` ✅ |
| 첫 실행 흐름 | 곧장 URL/QR 표시 ❌ | `Enable Remote Control? (y/n)` 동의 프롬프트 1회 |
| 배너 형식 | `Connected. Session URL: ...` ❌ | `·✔︎· Connected · <project> · <branch>` + `Capacity: N/32` + `space to show QR · w to toggle spawn mode` |
| 핫키 | `space` 만 언급 | `space` (QR), `w` (spawn 모드 토글) |
| Spawn 모드 | 미언급 | `same-dir` / `worktree` / `session` 3종, `--capacity` 로 동시 세션 수 |

위 항목을 본 가이드에 모두 반영함.

## 7. 검수 체크리스트

가이드 작성 후 다음을 확인:

- [ ] 13단 슬롯 순서 일치
- [ ] 모든 코드 블록 언어 태그 존재
- [ ] 이모지가 의미 슬롯에서만 사용됨 (✅❌⚠️💡🎯🆘📚🎓🌱🎬🏋️ + 🍎🐧🪟)
- [ ] 존댓말 (~해요/~이에요) 일관 유지
- [ ] 푸터 날짜 `2026.05.05` 와 시그니처 행 정확
- [ ] 외부 링크는 조사 결과의 4개 공식 URL 만 사용
- [ ] `./other-guide.md` 상대 경로로 시리즈 내부 링크
