# 클로드 코드 인텔리제이 사용법 3단계

> 💡 **한 줄 요약:** 클로드 코드 인텔리제이 사용법은 설치,
> 연결, 활용의 3단계면 충분합니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 인텔리제이 사용법 3단계 대표 이미지]

"인텔리제이에서도 클로드 코드를 쓸 수 있나요?"
궁금하셨던 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 인텔리제이 사용법**은
CLI와 플러그인을 설치하고, IDE 터미널에서 연결한 뒤,
diff 보기와 파일 참조를 활용하면 됩니다.

인텔리제이 안에서 바로 쓰면 수정안을 IDE의 diff 화면으로 보고,
지금 보고 있는 코드를 그대로 넘겨 물어볼 수 있는데요.
오늘 이 글 하나만 끝까지 읽으시면 설치부터 첫 요청까지
혼자 해 보실 수 있습니다.

설치 방법과 메뉴 이름은
[Claude Code 공식 문서](https://code.claude.com/docs/en/jetbrains)를
2026년 10월 30일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 인텔리제이 등 JetBrains IDE, Claude 유료 구독
* **소요 시간:** 설치 두 번과 로그인 한 번이면 끝납니다
* **난이도:** 초급, 터미널에 명령을 입력해 봤다면 충분합니다

공식 문서는 IntelliJ IDEA, PyCharm, Android Studio,
WebStorm, PhpStorm, GoLand 같은
대부분의 JetBrains IDE에서 플러그인이 동작한다고 안내합니다.
계정은 Pro, Max, Team, Enterprise 구독이나
Claude Console 계정이면 되고, API 키는 필요 없습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 인텔리제이 사용 흐름 3단계: 설치, 연결, 활용]

---

## Step 1. 클로드 코드는 무엇부터 설치할까?

처음에 가장 많이 놓치는 부분은 설치할 것이 두 가지라는 점입니다.
플러그인은 IDE 터미널에서 `claude` 명령을 실행해 연결하는 방식이라,
클로드 코드 CLI가 따로 설치돼 있어야 하죠.

아래 순서대로 차근차근 따라와 주세요.

1. 터미널에서 운영체제에 맞는 설치 명령을 실행합니다.
2. 새 터미널을 열고 `claude --version`으로 설치를 확인합니다.
3. 마켓플레이스에서 **Claude Code [Beta]** 플러그인을 설치합니다.
4. IDE를 다시 시작합니다.

```bash
# macOS, Linux, WSL
curl -fsSL https://claude.ai/install.sh | bash

# Windows PowerShell
irm https://claude.ai/install.ps1 | iex
```

설치 명령은 내려받는 동안 진행 상황을 보여 주지 않으니
멈춘 것처럼 보여도 조금 기다려 주세요.
`claude --version`을 입력했을 때 버전 번호가 나오면 성공이고,
명령을 찾을 수 없다고 나오면 PATH 설정을 확인해야 합니다.

플러그인은
[JetBrains 마켓플레이스](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-)에서
설치할 수 있습니다.
CLI 없이 플러그인만 설치하면 "Cannot launch Claude Code" 알림이 뜨니,
순서를 꼭 지켜 주세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 설치 순서: CLI 설치, 설치 확인, 플러그인 설치, 재시작]

> 📌 **전문가 Tip:** `claude`를 IDE가 못 찾는 위치에 설치했다면
> **Settings → Tools → Claude Code [Beta]**의
> **Claude command** 칸에 전체 경로를 적어 주세요.
> WSL이라면 `wsl -d Ubuntu -- bash -lic "claude"`처럼 적고,
> `Ubuntu`는 쓰는 배포판 이름으로 바꾸면 됩니다.

---

## Step 2. 인텔리제이와는 어떻게 연결할까?

기본이 끝났다면 이제 IDE와 연결할 차례입니다.
가장 쉬운 방법은 IDE 내장 터미널에서 `claude`를 실행하는 것인데요,
이렇게 하면 연동 기능이 모두 켜집니다.

에디터에서 바로 열고 싶다면 Mac은 `Cmd+Esc`,
Windows와 Linux는 `Ctrl+Esc`를 누르면 됩니다.
평소 쓰던 외부 터미널에서 실행했다면
`claude`를 켠 뒤 `/ide`를 입력해 연결하면 되죠.

| 실행 위치 | 연결 방법 | 확인할 점 |
| :--- | :--- | :--- |
| **IDE 내장 터미널** | `claude` 실행 | 별도 명령 없이 연결 |
| **외부 터미널** | `claude` 실행 후 `/ide` | 연결 메시지가 뜨는지 확인 |
| **단축키** | `Cmd+Esc` / `Ctrl+Esc` | 에디터에서 바로 열기 |

연결에 성공하면 `Connected to IntelliJ IDEA.` 같은 메시지가 나옵니다.
이때 IDE에서 연 프로젝트 루트 폴더에서 `claude`를 실행해야
클로드 코드가 IDE와 같은 파일을 볼 수 있습니다.

[IMAGE: 비교표 | 설명: 클로드 코드 인텔리제이 연결 방법 비교: 내장 터미널, 외부 터미널, 단축키]

### 연결이 안 될 때는 어떻게 할까?

`/ide`를 입력했는데 "No available IDEs detected"가 뜨는
경우가 가장 흔합니다.
저도 처음엔 프로젝트가 아닌 다른 폴더에서 `claude`를 켜 놓고
왜 IDE를 못 찾는지 한참 헤맸어요.

공식 문서가 안내하는 점검 순서는 아래와 같습니다.

1. 플러그인이 설치돼 있고 켜져 있는지 확인합니다.
2. IDE를 완전히 종료했다가 다시 켭니다. (여러 번 필요할 수 있어요)
3. IDE 내장 터미널의 프로젝트 루트에서 `claude`를 실행합니다.

ESC를 눌러도 작업이 멈추지 않는다면 IDE 설정 문제일 수 있습니다.
ESC가 안 먹혀서 결국 `Ctrl+C`로 끊었다는 분이 꽤 많더라고요.
**Settings → Tools → Terminal**에서
"Move focus to the editor with Escape"를 끄면 됩니다.

[IMAGE: 비교표 | 설명: 클로드 코드 인텔리제이 연결 문제 증상별 해결 방법]

---

## Step 3. 연결하면 무엇을 할 수 있을까?

연결이 끝나면 인텔리제이와 클로드 코드가 정보를 주고받습니다.
공식 문서에 나온 주요 기능은 네 가지입니다.

* **diff 보기:** 수정안이 IDE의 diff 뷰어에 열립니다
* **선택 영역 공유:** 지금 선택한 코드와 탭이 자동으로 전달됩니다
* **파일 참조:** `Cmd+Option+K`(Windows·Linux는 `Alt+Ctrl+K`)
* **진단 공유:** IDE의 lint·문법 오류를 읽을 수 있습니다

파일 참조 단축키를 누르면 `@src/auth.ts#L1-99`처럼
파일과 줄 범위가 입력창에 들어갑니다.
다만 진단은 수정할 때마다 자동으로 확인하지 않으니,
필요하면 오류를 확인해 달라고 직접 요청해 보세요.

diff가 IDE가 아닌 터미널에만 나온다면
`/config`의 **Diff tool**이 `auto`로 되어 있는지 확인하세요.
이 항목은 IDE와 연결된 상태에서만 보입니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 연결 후 쓸 수 있는 기능 4가지]

> 📌 **전문가 Tip:** 공식 문서는 JetBrains IDE에서
> 편집을 Manual 모드로 확인하라고 권합니다.
> `acceptEdits` 모드에서는 IDE가 자동 실행하는 설정 파일까지
> 고칠 수 있어 위험이 커질 수 있기 때문입니다.

---

## 4. 마무리

오늘은 클로드 코드 인텔리제이 사용법을
설치, 연결, 활용의 3단계로 알아보았습니다.
CLI와 플러그인을 모두 설치하고, 프로젝트 루트의 내장 터미널에서
`claude`를 실행하는 것이 가장 확실한 시작입니다.

익숙한 IDE에서 바로 쓸 수 있으니
작업 흐름이 한결 가벼워지는 법이죠!
다음 글에서는 헷갈리기 쉬운
클로드와 클로드 코드의 차이를 정리해 보겠습니다.

여러분은 내장 터미널과 외부 터미널 중 어느 쪽이 더 편하신가요?
궁금한 점이 있다면 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 사용법 3단계 요약과 다음 글 클로드와 클로드 코드 차이 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드인텔리제이 #인텔리제이 #IntelliJ #JetBrains #클로드코드사용법 #AI코딩도구`

<!-- 공식 출처 (2026-10-30 확인)
- 지원 IDE, 설치 순서(CLI → 플러그인 → 재시작), Cannot launch Claude Code, 계정 조건, Claude command·WSL 명령, 내장 터미널 실행, /ide, Connected to IntelliJ IDEA., 프로젝트 루트, Cmd+Esc/Ctrl+Esc, 기능 4가지, Cmd+Option+K/Alt+Ctrl+K, @src/auth.ts#L1-99, 진단 자동 요청 안 함, Diff tool(auto/terminal, 연결 시에만 표시), 문제 해결(No available IDEs detected, 완전 재시작 여러 번), ESC 설정, acceptEdits 보안 주의: https://code.claude.com/docs/en/jetbrains
- 설치 명령, 진행 상황 미표시, claude --version, PATH: https://code.claude.com/docs/en/quickstart
- 플러그인 마켓플레이스: https://plugins.jetbrains.com/plugin/27310-claude-code-beta-
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 2 "프로젝트가 아닌 다른 폴더에서 claude를 켜 놓고 IDE를 못 찾아 헤맸다": https://github.com/anthropics/claude-code/issues/22232 (작업 폴더와 IDE 프로젝트 폴더 불일치 메시지), https://github.com/anthropics/claude-code/issues/10569 , https://code.claude.com/docs/en/jetbrains (프로젝트 루트에서 실행 안내)
- Step 2 "ESC가 안 먹혀 Ctrl+C로 끊었다는 분이 많다": https://github.com/anthropics/claude-code/issues/14526 (Ctrl+C 우회), https://github.com/anthropics/claude-code/issues/10618 (IntelliJ에서 ESC 안 됨), https://github.com/anthropics/claude-code/issues/13707 (Rider 터미널), https://code.claude.com/docs/en/jetbrains (ESC 설정)
-->
