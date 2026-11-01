# 클로드 코드 단축키 총정리, 상황별 4가지

> 💡 **한 줄 요약:** 멈출 땐 `Esc`, 줄바꿈은 `\` + `Enter`,
> 모드 전환은 `Shift+Tab`, 빠른 입력은 `/`·`!`·`@`만 기억하세요.

[IMAGE: 썸네일 | 설명: 클로드 코드 단축키 총정리 상황별 4가지 대표 이미지]

결론부터 말씀드리면, **클로드 코드 단축키**는
멈추기, 입력 편집, 모드 전환, 빠른 입력의
네 가지 상황으로 나눠 외우면 훨씬 쉽습니다.
"Enter만 눌렀는데 질문이 반쯤 쓴 채로 보내졌어요"
하시는 분들을 위해 준비했습니다.

단축키는 많아 보여도 매일 쓰는 건 손에 꼽을 정도인데요.
오늘 이 글 하나만 끝까지 읽으시면
마우스 없이도 대화를 멈추고, 고치고, 바꾸실 수 있습니다.
내용은 [Claude Code 공식 문서](https://code.claude.com/docs/en/interactive-mode)를
2026년 11월 1일에 확인해 정리했습니다.

---

## 1. 클로드 코드 단축키, 멈추고 나갈 때는?

가장 먼저 익혀야 할 키는 멈추는 키입니다.
클로드가 엉뚱한 방향으로 작업을 시작했을 때
바로 끊을 수 있어야 마음 편히 맡길 수 있으니까요.
비슷해 보이는 네 가지를 표로 정리했습니다.

| 단축키 | 하는 일 | 알아 둘 점 |
| :--- | :--- | :--- |
| `Esc` | 지금 응답이나<br>작업 중단 | 해 둔 작업은 남고<br>방향만 다시 지시 |
| `Esc` 두 번 | 입력 지우기<br>또는 되감기 | 입력창이 비어 있으면<br>되감기 메뉴가 열림 |
| `Ctrl+C` | 실행 중인<br>작업 중단 | 아무것도 안 돌 때<br>두 번 누르면 종료 |
| `Ctrl+D` | 클로드 코드 종료 | 두 번 눌러야 종료,<br>입력이 있으면 글자 삭제 |

[IMAGE: 비교표 | 설명: 클로드 코드 단축키 Esc, Esc 두 번, Ctrl+C, Ctrl+D 차이 비교]

여기서 많이들 헷갈리시는 키가 `Esc` 두 번입니다.
저도 처음엔 이전 질문을 다시 불러오는 키인 줄 알고 눌렀다가
되감기 화면이 떠서 잠깐 멈칫했어요.
같은 착각을 했다는 이야기가 커뮤니티에 꽤 보이더라고요.

입력창이 비어 있을 때 `Esc`를 두 번 누르면
`/rewind`와 같은 되감기 메뉴가 열립니다.
이전 질문을 다시 쓰고 싶다면 위쪽 방향키나 `Ctrl+R`이 맞는 키예요.

> 📌 **전문가 Tip:** 작업을 멈출 때는 `Ctrl+C`보다 `Esc`가 안전합니다.
> `Ctrl+C`는 아무것도 실행 중이 아닐 때 두 번 누르면
> 클로드 코드가 그대로 종료되기 때문입니다.

---

## 2. 줄바꿈과 입력 편집은 어떻게 할까?

클로드 코드에서 `Enter`는 바로 보내기입니다.
그래서 여러 줄로 요청을 쓰려면 줄바꿈 키를 따로 알아야 하죠.
어느 터미널에서나 통하는 방법은 아래 두 가지입니다.

* **`\` + `Enter`:** 줄 끝에 역슬래시를 치고 Enter
* **`Ctrl+J`:** 설정 없이 모든 터미널에서 줄바꿈

`Shift+Enter`는 iTerm2, Ghostty, Windows Terminal 같은
터미널에서는 설정 없이 바로 됩니다.
VS Code와 Cursor의 내장 터미널은 클로드 코드 안에서
`/terminal-setup`을 한 번 실행해야 쓸 수 있습니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 줄바꿈 단축키 역슬래시 Enter, Ctrl+J, Shift+Enter 정리]

저도 처음엔 `Shift+Enter`를 눌렀는데 줄이 안 바뀌고
반쯤 쓴 질문이 그대로 보내져서 당황했어요.
이 문제로 질문 글과 깃허브 이슈가 정말 많이 올라오더라고요.
대부분 터미널이 두 키를 같은 신호로 보내서 생기는 일이라,
위의 두 방법을 먼저 손에 익혀 두시면 편합니다.

줄바꿈 다음으로 자주 쓰는 편집 키는 아래와 같습니다.

* **위/아래 방향키:** 이전에 보낸 입력 다시 불러오기
* **`Ctrl+R`:** 이전 입력을 검색해서 찾기
* **`Ctrl+G`:** 기본 텍스트 편집기에서 길게 쓰기
* **`Ctrl+S`:** 쓰던 입력을 잠시 보관, 다시 누르면 복원
* **`Ctrl+V`:** 클립보드의 이미지를 붙여 넣기

[IMAGE: 포인트카드 | 설명: 클로드 코드 입력 편집 단축키 방향키, Ctrl+R, Ctrl+G, Ctrl+S 정리]

이미지 붙여넣기는 운영체제마다 키가 조금 다릅니다.
맥의 iTerm2에서는 `Cmd+V`, 윈도우와 WSL에서는 `Alt+V`를 씁니다.
긴 요청을 다듬을 때는 `Ctrl+G`로 편집기를 열면
메모장처럼 편하게 고친 뒤 저장만 하면 돼요.

---

## 3. 권한 모드와 화면은 어떤 키로 바꿀까?

기본이 끝났다면 이제 작업 방식을 바꾸는 키를 볼 차례입니다.
가장 많이 쓰는 키는 `Shift+Tab`입니다.
누를 때마다 권한 모드가 차례로 바뀌는데요.
화면에 Manual로 표시되는 기본 모드에서 시작해
편집 자동 허용(`acceptEdits`), 계획 모드(`plan`) 순으로 돌아갑니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 Shift+Tab 권한 모드 전환 순서 Manual, acceptEdits, plan]

권한 건너뛰기 모드나 자동 모드를 쓸 수 있는 환경이라면
그 모드도 순서에 함께 들어갑니다.
권한 모드 말고도 화면을 바꾸는 키가 몇 가지 더 있습니다.

* **`Option+P` / `Alt+P`:** 쓰던 입력을 지우지 않고 모델 바꾸기
* **`Ctrl+O`:** 도구 사용 내역을 자세히 보는 기록 화면
* **`Ctrl+B`:** 실행 중인 명령을 백그라운드로 보내기
* **`Ctrl+T`:** 클로드의 할 일 목록 보이기·숨기기
* **`Ctrl+L`:** 화면이 깨졌을 때 다시 그리기

맥에서는 `Option+P`가 안 먹는다는 분이 많더라고요.
저도 눌렀는데 모델은 그대로이고
입력창에 π 기호만 찍혀서 한참 고개를 갸웃했어요.
맥 터미널은 기본값으로 Option 키를 단축키 신호로 보내지 않아서
터미널마다 설정을 하나 켜 줘야 합니다.

* **기본 터미널:** 설정 → 프로필 → 키보드에서
  "Use Option as Meta Key" 체크
* **iTerm2:** Profiles → Keys → General에서
  왼쪽·오른쪽 Option 키를 "Esc+"로 변경
* **VS Code:** 설정에 `terminal.integrated.macOptionIsMeta` 켜기

다만 이 설정을 켜면 Option 키로 입력하던
특수 문자가 잘 안 쳐질 수 있습니다.
특수 문자를 Option으로 자주 입력하신다면
켜기 전에 한 번 생각해 보세요.

---

## 4. 기호 하나로 여는 빠른 입력은?

입력창 맨 앞에 기호 하나만 쳐도 기능이 바로 열립니다.
많은 분들이 궁금해하시는 부분이라 하나씩 짚어볼게요.

1. `/`: 명령어와 스킬 목록 열기 (예: `/model`, `/rewind`)
2. `!`: 셸 모드, 터미널 명령을 바로 실행
3. `@`: 파일 경로 자동 완성으로 파일 지정
4. `?`: 빈 입력창에서 누르면 단축키 도움말 열기

[IMAGE: 포인트카드 | 설명: 클로드 코드 빠른 입력 기호 /, !, @, ? 쓰임 정리]

그렇다면 단축키가 손에 안 맞을 땐 어떻게 할까요?
`/keybindings`를 입력하면 `~/.claude/keybindings.json` 파일이
만들어지거나 열리고, 여기서 키를 원하는 대로 바꿀 수 있습니다.
저장하면 클로드 코드를 다시 켜지 않아도 바로 적용돼요.

하지만 중요한 건 단축키를 전부 외우는 것이 아니라
**자주 쓰는 몇 개를 손에 익히는 것**이겠죠.
`Ctrl+C`와 `Ctrl+D`는 바꿀 수 없는 고정 키라는 점도 함께 기억해 두세요.

---

## 5. 마무리

오늘은 클로드 코드 단축키를 멈추기, 입력 편집,
모드 전환, 빠른 입력의 네 가지 상황으로 알아보았습니다.
`Esc`, `\` + `Enter`, `Shift+Tab`, `/` 이 네 개만 먼저 써 봐도
작업 속도가 눈에 띄게 달라집니다.

처음에는 빈 입력창에서 `?`를 눌러 도움말을 띄워 보세요.
작은 습관 하나가 반복 작업을 훨씬 가볍게 만드는 법이죠!
다음 글에서는 클로드 코드 설치 오류 해결법 5가지를 정리해 보겠습니다.

여러분은 어떤 단축키를 가장 자주 쓰시나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 단축키 상황별 4가지 요약과 다음 글 설치 오류 해결 5가지 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드단축키 #클로드코드사용법 #단축키정리 #AI코딩도구 #바이브코딩`

<!-- 글 유형: A 정보·리뷰형 / 메인 키워드: 클로드 코드 단축키
검색 의도: 클로드 코드를 터미널에서 쓰는 사람이 작업 중단, 줄바꿈, 모드 전환, 빠른 입력에 쓰는 단축키를 한 번에 확인하고 싶다.

경험 문장 근거 (style-guide 10장)
- 1장 "Esc 두 번을 이전 질문 불러오기로 알고 눌렀다가 되감기 화면이 떴다 / 같은 착각이 커뮤니티에 보인다":
  https://www.gpters.org/news/post/claudes-code-shortcut-esc-8dxfTogqDriTQFd , https://claudelog.com/faqs/what-is-rewind-in-claude-code/ , https://dev.to/rajeshroyal/your-time-machine-for-code-double-esc-to-rewind-when-things-go-wrong-53pa
- 2장 "Shift+Enter를 눌렀는데 반쯤 쓴 질문이 보내졌다 / 질문 글과 이슈가 많다":
  https://github.com/anthropics/claude-code/issues/2054 , https://claudeissues.com/issue/1114-bug-shift-enter-is-sending-the-mesage-instead-adding-a-new-line , https://claudeissues.com/issue/27465-bug-shift-enter-sends-new-message-instead-of-adding-newline , https://www.inflearn.com/community/questions/1845499
- 3장 "맥에서 Option+P를 눌렀더니 π 기호만 찍혔다 / 안 먹는다는 분이 많다":
  https://claudeissues.com/issue/14322-bug-new-shortcut-option-p-doesnt-work-on-macos , https://claudeissues.com/issue/11522-bug-option-based-key-input-on-macos-not-working-in-terminal-client , https://claudeissues.com/issue/18221-alt-option-keyboard-shortcuts-break-international-keyboard-layouts
- 사실 확인(단축키 표, 줄바꿈 방법과 터미널별 Shift+Enter, Option as Meta 설정, /keybindings, 고정 키):
  https://code.claude.com/docs/en/interactive-mode , https://code.claude.com/docs/en/terminal-config , https://code.claude.com/docs/en/keybindings (2026-11-01 확인)
-->
