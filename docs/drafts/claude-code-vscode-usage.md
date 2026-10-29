# 클로드 코드 VS Code 사용법 3단계

> 💡 **한 줄 요약:** 클로드 코드 VS Code 사용법은 확장 설치,
> 파일 지정 요청, 수정 검토의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 VS Code 사용법 3단계 대표 이미지]

"터미널은 낯설고, 늘 쓰던 VS Code 안에서 쓰고 싶어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, 확장을 설치해 패널을 열고,
`@`로 파일을 짚어 요청한 뒤, 나란히 보기 화면에서
수정 내용을 검토하는 것까지가 전부입니다.

클로드 코드 VS Code 확장은 터미널 대신 편집기 옆 패널에서
대화하듯 일을 맡기는 그래픽 도구입니다.
오늘 이 글 하나만 끝까지 읽으시면 설치부터 첫 수정 검토까지
혼자 해 보실 수 있습니다.
설치 조건과 단축키는 [Claude Code 공식 문서](https://code.claude.com/docs/en/vs-code)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** VS Code 1.94.0 이상, 유료 Claude 요금제
* **소요 시간:** 확장 설치와 로그인까지 금방 끝납니다
* **난이도:** 초급, VS Code에서 파일을 열어 봤다면 충분합니다

API 키는 따로 준비하지 않아도 됩니다.
공식 문서에 따르면 Pro, Max, Team, Enterprise 요금제나
Claude Console 계정으로 처음 패널을 열 때 로그인하면 되죠.
VS Code 버전은 메뉴의 **Help > About**에서 확인할 수 있습니다.

---

## Step 1. 클로드 코드 VS Code 확장은 어떻게 설치할까?

설치는 확장 보기에서 이름만 검색하면 됩니다.
아래 순서대로 차근차근 따라와 주세요.

1. `Cmd+Shift+X`(Windows는 `Ctrl+Shift+X`)로 확장 보기를 엽니다.
2. "Claude Code"를 검색하고 **Install**을 누릅니다.
3. 파일 하나를 연 뒤, 편집기 오른쪽 위 Spark 아이콘을 누릅니다.
4. 로그인 화면에서 **Sign in**을 누르고 브라우저에서 허용합니다.

처음 열 때 가장 많이 막히는 부분은 바로 이 Spark 아이콘입니다.
저도 처음엔 폴더만 열어 둔 채 아이콘을 한참 찾았어요.
이 아이콘은 파일이 하나라도 열려 있어야 보이거든요.

[IMAGE: 다이어그램 | 설명: 클로드 코드 VS Code 확장 설치부터 패널 열기, 로그인까지 3단계 흐름]

아이콘이 안 보여도 패널을 여는 길은 더 있습니다.
왼쪽 활동 표시줄(Activity Bar)의 Spark 아이콘은 늘 보이고,
창 오른쪽 아래 상태 표시줄의 **Claude Code**를 눌러도 열립니다.
`Cmd+Shift+P`(명령 팔레트)에 "Claude Code"를 입력해
**Open in New Tab**을 골라도 되죠.

그래도 안 보인다면 명령 팔레트에서
**Developer: Reload Window**를 실행해 창을 다시 불러오세요.
작업 폴더를 신뢰하지 않은 제한 모드(Restricted Mode)에서는
확장이 동작하지 않으니 이것도 함께 확인해 보세요.

### 로그인 화면이 계속 뜰 때는 어떻게 할까?

셸에 `ANTHROPIC_API_KEY`를 설정해 뒀는데도
로그인 화면이 계속 뜬다는 분이 많더라고요.
VS Code가 셸의 환경 변수를 물려받지 못해서 생기는 일인데요.
터미널에서 `code .`로 VS Code를 열거나,
Claude 계정으로 로그인하면 해결됩니다.

> 📌 **전문가 Tip:** 확장의 버전 번호는 안에 든 클로드 코드 버전과 같습니다.
> 문서에 "v2.1.275 이상"처럼 적힌 기능은
> 확장 보기에서 버전 번호를 보고 쓸 수 있는지 판단하세요.

---

## Step 2. 파일을 짚어서 요청하려면 어떻게 할까?

기본이 끝났다면 이제 실제로 일을 맡겨 볼 차례입니다.
클로드는 지금 열려 있는 파일과 선택한 글자를 자동으로 봅니다.
그래서 코드를 복사해 붙여 넣지 않아도
"이 부분 설명해줘"라고 물으면 되죠.

다른 파일까지 함께 보게 하려면 `@`를 씁니다.
입력창에 `@`와 파일 이름 일부만 쳐도 후보가 뜨고,
폴더는 이름 끝에 `/`를 붙이면 됩니다.

* **파일 지정:** `@auth`처럼 이름 일부만 써도 찾아 줍니다
* **폴더 지정:** `@src/components/`처럼 끝에 `/`를 붙입니다
* **줄 범위 지정:** 코드를 선택하고 `Option+K`(Windows는 `Alt+K`)
* **터미널 출력:** `@terminal:이름`으로 터미널 결과를 붙입니다

`Option+K`를 누르면 `@app.ts#5-10`처럼
파일 이름과 줄 번호가 입력창에 들어갑니다.
이 단축키는 커서가 편집기에 있을 때만 동작하니,
안 될 때는 코드 쪽을 한 번 클릭해 보세요.

```
@src/auth.js 의 로그인 함수가 하는 일을 쉽게 설명해줘
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 VS Code에서 @로 파일, 폴더, 줄 범위를 지정하는 방법]

### 자주 쓰는 단축키는 무엇일까?

손이 키보드에서 떠나지 않게 해 주는 단축키도 알아 두면 편합니다.
많은 분들이 궁금해하시는 것만 표로 정리했습니다.

| 기능 | Mac | Windows |
| :--- | :--- | :--- |
| **편집기와 입력창 오가기** | `Cmd+Esc` | `Ctrl+Esc` |
| **@멘션 넣기** | `Option+K` | `Alt+K` |
| **새 탭에서 대화 열기** | `Cmd+Shift+Esc` | `Ctrl+Shift+Esc` |
| **닫은 대화 다시 열기** | `Cmd+Shift+T` | `Ctrl+Shift+T` |

macOS Tahoe 이후 버전에서는 시스템의 게임 오버레이 단축키가
`Cmd+Esc`를 먼저 가로챌 수 있습니다.
이때는 시스템 설정의 키보드 단축키에서 게임 오버레이를 끄거나,
VS Code에서 **Claude Code: Focus input** 단축키를 바꾸면 됩니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 VS Code 확장에서 자주 쓰는 단축키 3가지]

---

## Step 3. 수정 내용은 어디서 검토할까?

클로드가 파일을 고칠 때 어떻게 움직일지는
입력창 아래에 표시된 권한 모드가 정합니다.
표시를 누르면 모드를 바꿀 수 있는데요,
처음이라면 하나씩 확인하는 **Manual** 모드로 시작해 보세요.

| 모드 | 동작 👍 | 주의할 점 👎 |
| :--- | :--- | :--- |
| **Manual** | 수정과 대부분의 명령 전에 허락을 묻습니다 | 확인 요청이 자주 뜹니다 |
| **Plan** | 계획을 먼저 보여 주고 승인을 기다립니다 | 승인 전에는 수정하지 않습니다 |
| **Auto** | 판별기가 대부분의 동작을 대신 검토합니다 | 대부분 묻지 않고 진행합니다 |
| **Edit automatically** | 묻지 않고 바로 수정합니다 | 결과는 직접 챙겨 봐야 합니다 |

Manual 모드에서는 클로드가 파일을 고치려 할 때
원본과 수정안을 나란히 보여 주고 허락을 묻습니다.
받아들이거나 거절할 수도 있고, 다르게 해 달라고 말할 수도 있죠.

바뀐 곳이 여러 군데라면 부분마다 붙는
**Accept this change**, **Reject this change** 버튼으로 하나씩 고르면 됩니다.
이 기능은 클로드 코드 v2.1.275 이상에서 동작하고,
바뀐 곳이 100개를 넘으면 파일 전체 단위로만 검토할 수 있습니다.

Plan 모드에서는 계획이 마크다운 문서로 열려
읽으면서 중간중간 의견을 달 수 있습니다.
입력창에 `/plan`을 입력해도 바로 바꿀 수 있는데,
이 명령은 v2.1.280 이상에서 동작합니다.

[IMAGE: 비교표 | 설명: 클로드 코드 VS Code 권한 모드 Manual, Plan, Auto, Edit automatically 비교]

### 터미널에서 claude 명령이 안 될 때는?

저도 확장만 설치해 놓고 VS Code 터미널에 `claude`를 쳤다가
명령을 찾을 수 없다는 메시지를 보고 당황했어요.
확장 안에는 채팅 패널용 클로드 코드가 따로 들어 있지만,
터미널의 `claude` 명령까지 깔아 주지는 않거든요.

터미널에서도 쓰려면 공식 설치 안내대로 CLI를 한 번 따로 설치하면 됩니다.
CLI와 확장은 대화 기록을 함께 쓰기 때문에
터미널에서 `claude --resume`으로 확장의 대화를 이어 갈 수도 있습니다.

하지만 중요한 건 도구를 어디서 여느냐가 아니라
**수정 내용을 내 눈으로 확인하는 습관**이겠죠.
처음 몇 번은 Manual 모드에서 나란히 보기 화면을 꼼꼼히 살펴보세요.

---

## 4. 마무리

오늘은 클로드 코드 VS Code 사용법을
설치, 파일 지정 요청, 수정 검토의 3단계로 알아보았습니다.
Spark 아이콘이 안 보이면 파일부터 열고,
처음 맡길 때는 Manual 모드로 하나씩 확인해 보세요.

손에 익은 편집기에서 시작하면 새 도구도 훨씬 덜 낯설기 마련이죠!
다음 글에서는 브라우저와 휴대폰에서 쓰는
클로드 코드 웹·모바일 사용법을 정리해 보겠습니다.

여러분은 VS Code에서 어떤 작업부터 맡겨 보고 싶으신가요?
막히는 부분이 있다면 편하게 댓글로 알려주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 VS Code 사용법 3단계 요약과 다음 글 웹·모바일 사용법 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드VSCode #VSCode확장 #VSCode사용법 #클로드코드사용법 #AI코딩도구 #바이브코딩`

<!-- 공식 출처 (2026-10-29 확인)
- VS Code 1.94.0 이상, 유료 요금제·Console 계정, API 키 불필요, 설치 방법, Spark 아이콘(파일을 열어야 보임), 활동 표시줄·상태 표시줄·명령 팔레트, Sign in, ANTHROPIC_API_KEY와 code ., 확장 버전 = 클로드 코드 버전: https://code.claude.com/docs/en/vs-code
- 선택 자동 인식, @ 퍼지 매칭, 폴더 끝 /, Option+K/Alt+K(편집기 포커스 필요), @terminal:이름, 단축키 표, macOS Tahoe 게임 오버레이: 같은 문서
- 권한 모드 Manual/Plan/Auto/Edit automatically, 나란히 보기 diff, Accept/Reject this change(v2.1.275 이상, 100개 초과 시 파일 단위), /plan(v2.1.280 이상): 같은 문서
- 확장은 claude를 PATH에 넣지 않음, CLI 별도 설치, claude --resume 대화 기록 공유, Restricted Mode, Developer: Reload Window: 같은 문서
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "폴더만 열어 둔 채 Spark 아이콘을 한참 찾았다": https://code.claude.com/docs/en/vs-code (Spark icon not visible) , https://claudeissues.com/issue/14317-bug-claude-code-for-vs-code-extension-not-shown-anymore-in-activity-bar , https://claudeissues.com/issue/15104-bug-claude-icon-disappeared-after-vs-code-update , https://clauder-navi.com/vscode-claude/?setlang=en
- Step 1 "API 키를 설정했는데도 로그인 화면이 계속 뜬다는 분이 많다": https://code.claude.com/docs/en/vs-code , https://wikidocs.net/blog/@openwiki/32664/
- Step 3 "확장만 설치하고 터미널에 claude를 쳤다가 명령을 찾을 수 없다는 메시지를 봤다": https://inventivehq.com/knowledge-base/claude/zsh-command-not-found-claude , https://inventivehq.com/knowledge-base/claude/could-not-locate-the-claude-cli-on-path , https://www.developersdigest.tech/errors/claude-code/command-not-found-claude
-->
