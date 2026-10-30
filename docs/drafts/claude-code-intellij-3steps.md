# 클로드 코드 인텔리제이 사용법 3단계

> 💡 **한 줄 요약:** 클로드 코드 인텔리제이 사용법은 CLI 설치,
> 플러그인 설치, IDE 터미널에서 실행의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 인텔리제이 사용법 3단계 대표 이미지]

"인텔리제이에서 쓰고 싶은데 플러그인만 깔면 되는 건가요?"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 인텔리제이 사용법**은
클로드 코드 CLI를 먼저 설치하고, JetBrains 플러그인을 깐 뒤,
IDE 내장 터미널에서 `claude`를 실행하면 끝입니다.

클로드 코드는 코드를 읽고, 파일을 고치고, 명령을 실행해 주는
에이전트형 코딩 도구입니다.
인텔리제이와 연결하면 수정 내용을 IDE의 diff 화면에서 보고,
지금 선택한 코드를 따로 붙여 넣지 않고도 물어볼 수 있죠.

오늘 이 글 하나만 끝까지 읽으시면 설치부터 IDE 연결 확인까지
혼자 해 보실 수 있습니다.
설치 순서와 설정 이름은 [Claude Code 공식 문서](https://code.claude.com/docs/ko/jetbrains)를
2026년 10월 30일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 인텔리제이 같은 JetBrains IDE, 유료 Claude 구독
* **소요 시간:** 설치와 로그인까지 금방 끝납니다
* **난이도:** 초급, IDE 터미널을 열어 봤다면 충분합니다

공식 문서에 따르면 플러그인은 IntelliJ IDEA, PyCharm,
WebStorm, Android Studio, PhpStorm, GoLand처럼
대부분의 JetBrains IDE에서 동작합니다.
여러분이 쓰는 IDE도 이 목록에 있으신가요?
다만 IntelliJ IDEA의 판(edition)별 지원 여부는
공식 문서에 따로 나와 있지 않습니다.

계정은 Pro, Max, Team, Enterprise 구독이나
Claude Console 계정이면 되고, API 키는 따로 필요 없습니다.
Free 플랜에는 클로드 코드가 포함되지 않으니
이 점은 미리 확인해 두세요.

마켓플레이스에서 찾을 플러그인 이름은 **Claude Code [Beta]**입니다.
2026년 10월 30일 기준 공식 문서에도 [Beta] 표기가 붙어 있는데요.
이름이 비슷한 다른 플러그인도 검색되니,
Anthropic이 만든 공식 플러그인인지 꼭 확인하세요.

[IMAGE: 다이어그램 | 설명: 클로드 코드 인텔리제이 연결 3단계 흐름: CLI 설치, 플러그인 설치, IDE 터미널에서 실행]

---

## Step 1. 클로드 코드 CLI는 왜 먼저 설치할까?

처음에 놓치기 쉬운 부분이 바로 이 순서입니다.
플러그인 안에는 클로드 코드 CLI가 들어 있지 않아서,
CLI를 찾지 못하면 "Cannot launch Claude Code" 알림이 뜹니다.
플러그인이 IDE 터미널에서 `claude` 명령을 실행해 연결하는 구조이기 때문이죠.

아래 순서대로 차근차근 따라와 주세요.

1. 운영체제에 맞는 설치 명령을 터미널에 입력합니다.
2. 새 터미널 창을 열고 `claude --version`을 실행합니다.
3. `claude`를 실행해 브라우저 창에서 로그인합니다.

```bash
# macOS, Linux, WSL
curl -fsSL https://claude.ai/install.sh | bash

# Windows PowerShell
irm https://claude.ai/install.ps1 | iex
```

설치 명령은 내려받는 동안 진행 상황을 보여 주지 않으니
멈춘 것 같아도 잠시 기다려 주세요.
`claude --version`에서 버전 번호가 나오면 설치가 끝난 것이고,
`claude`를 찾을 수 없다고 나오면
설치 경로가 아직 PATH에 없는 상태입니다.

처음 `claude`를 실행하면 브라우저에 로그인 창이 열립니다.
창이 자동으로 안 열리면 `c`를 눌러 로그인 주소를 복사하고,
브라우저에 코드가 보이면 터미널의
`Paste code here if prompted` 자리에 붙여 넣으면 되죠.
터미널에 `Login successful`이 뜨면 `Enter`를 눌러 계속합니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 CLI 설치 명령, 설치 확인, 첫 로그인 순서 정리]

> 📌 **전문가 Tip:** Homebrew나 WinGet으로도 설치할 수 있지만,
> 이 두 방법은 자동 업데이트가 되지 않아 직접 올려 줘야 합니다.
> 공식 권장 방식인 Native 설치는 백그라운드에서
> 알아서 업데이트됩니다.

---

## Step 2. 인텔리제이 플러그인은 어떻게 설치할까?

기본이 끝났다면 이제 IDE 쪽을 준비할 차례입니다.
공식 안내는 [JetBrains 마켓플레이스](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-)에서
플러그인을 설치하고 IDE를 다시 시작하는 것이 전부입니다.

1. 마켓플레이스에서 **Claude Code [Beta]**를 찾습니다.
2. 플러그인을 설치합니다.
3. IDE를 다시 시작합니다.

여기서 IDE를 한 번 재시작했는데도 반영이 안 돼서,
완전히 껐다 켜고 나서야 됐다는 분이 많더라고요.
공식 문서에도 완전한 재시작을 여러 번 해야 할 수 있다고 적혀 있으니,
기능이 안 보이면 IDE를 확실히 종료했다가 다시 켜 보세요.

### 플러그인이 claude를 못 찾을 때는?

`claude`가 IDE가 찾지 못하는 위치에 설치돼 있으면
Claude 아이콘을 눌렀을 때 "command not found"가 뜹니다.
이때는 **Settings → Tools → Claude Code [Beta]**의
**Claude command** 칸에 실행할 명령이나 전체 경로를 넣으면 됩니다.

* **기본:** `claude`
* **전체 경로:** `/usr/local/bin/claude`처럼 설치 위치 그대로
* **WSL:** `wsl -d Ubuntu -- bash -lic "claude"`

WSL 명령의 `Ubuntu`는 자기 배포판 이름으로 바꿔 주세요.
JetBrains 원격 개발(Remote Development)을 쓴다면
로컬 클라이언트가 아니라 **Settings → Plugin (Host)**에서
원격 호스트에 플러그인을 설치해야 한다는 점도 기억해 두세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 플러그인 Claude command 경로 설정 예시 3가지]

---

## Step 3. IDE와 연결은 어떻게 확인할까?

공식 문서가 권하는 가장 기본적인 방법은
IDE 내장 터미널에서 `claude`를 실행하는 것입니다.
이렇게 하면 모든 연동 기능이 켜집니다.
이때 IDE에서 연 프로젝트 루트와 같은 폴더에서 시작해야
클로드가 IDE와 같은 파일을 봅니다.

에디터에서 바로 열고 싶다면 Mac은 `Cmd+Esc`,
Windows와 Linux는 `Ctrl+Esc`를 누르거나
화면의 Claude Code 버튼을 눌러도 됩니다.
그렇다면 늘 쓰던 외부 터미널에서는 어떻게 연결할까요?

iTerm2나 Windows Terminal 같은 외부 터미널이라면
`claude`를 실행한 뒤 `/ide`를 입력하면 됩니다.
연결되면 `Connected to IntelliJ IDEA.` 같은 메시지가 나오죠.

| 실행 위치 | 연결 방법 | 참고 |
| :--- | :--- | :--- |
| **IDE 내장 터미널** | `claude` 실행만 하면 연결 | 공식 문서의 기본 방법 |
| **외부 터미널** | `claude` 실행 후 `/ide` 입력 | 연결 메시지로 확인 |
| **외부 터미널 자동 연결** | `autoConnectIde`를 `true`로 설정 | 기본값은 `false` |

외부 터미널에서도 매번 자동으로 연결하고 싶다면
`/config`의 **Auto-connect to IDE (external terminal)**를 켜면 됩니다.
이 항목이 바로 `autoConnectIde` 설정입니다.

[IMAGE: 비교표 | 설명: 클로드 코드 인텔리제이 연결 방법 비교: IDE 내장 터미널과 외부 터미널]

### 연결되면 무엇이 달라질까?

연결이 끝나면 IDE 안의 정보가 클로드 코드로 넘어가고,
클로드의 수정안은 IDE 화면에 표시됩니다.
공식 문서에 적힌 기능은 아래와 같습니다.

* **diff 보기:** 수정 내용이 IDE diff 뷰어에 열립니다
* **선택 영역 공유:** 선택한 코드와 열린 파일이 함께 전달됩니다
* **파일 참조:** `Cmd+Option+K`(Windows·Linux는 `Alt+Ctrl+K`)
* **진단 공유:** IDE의 lint·구문 오류를 클로드가 읽습니다

파일 참조 단축키를 누르면 `@src/auth.ts#L1-99` 같은
참조가 입력창에 들어갑니다.
진단은 한 번에 파일 하나씩 읽고, 편집 뒤에 자동으로 요청하지는 않으니
필요할 때 확인해 달라고 직접 말해 보세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 연결 후 쓸 수 있는 기능 4가지]

### "No available IDEs detected"가 뜰 때는?

저도 처음엔 외부 터미널에서 `/ide`를 입력했다가
"No available IDEs detected"라는 메시지만 보고 한참 헤맸어요.
플러그인을 다시 깔거나 터미널을 바꿔 가며 시도하는 분이 많은데요,
공식 문서가 안내하는 확인 순서는 이렇습니다.

1. 플러그인이 설치돼 있고 켜져 있는지 확인합니다.
2. IDE를 완전히 종료했다가 다시 켭니다.
3. IDE 내장 터미널에서 `claude`를 실행해 봅니다.

2026년 9월 23일 배포된 클로드 코드 2.1.281에서는
`/ide`가 실행 중인 IDE를 나열하면서도
이 메시지를 보여 주던 문제가 고쳐졌습니다.
CLI가 오래된 버전이라면 업데이트부터 해 보세요.

Windows에서 WSL2로 클로드 코드를 돌린다면
대개 WSL2의 네트워크 방식이나 Windows 방화벽이 연결을 막습니다.
공식 문서는 방화벽 규칙 추가를 권장 해결법으로 들고,
Windows 11 22H2 이상이라면 미러링 네트워크 모드를 대안으로 안내합니다.

### 수정 내용이 터미널에만 뜰 때는?

플러그인을 깔았는데도 diff가 IDE 창이 아니라
터미널에만 보인다면 `/config`의 **Diff tool**을 확인하세요.
`auto`는 IDE에서, `terminal`은 터미널에서 diff를 보여 주고,
기본값은 `auto`입니다.

이 항목은 IDE에 연결됐을 때만 `/config`에 나타납니다.
항목이 안 보인다면 아직 연결되지 않은 상태이니,
IDE 내장 터미널에서 실행하거나 `/ide`를 먼저 입력해 주세요.

### ESC로 작업이 멈추지 않을 때는?

작업을 멈추려고 ESC를 눌렀는데 반응이 없어서
결국 `Ctrl+C`로 세션을 통째로 끝냈다는 이야기가 자주 보여요.
IDE가 ESC 키를 에디터로 포커스를 옮기는 데 먼저 쓰는 것이
흔한 원인으로 꼽힙니다.

1. **Settings → Tools → Terminal**로 갑니다.
2. "Move focus to the editor with Escape"를 끕니다.
3. 적용한 뒤 ESC를 다시 눌러 봅니다.

옵션을 끄는 대신 "Configure terminal keybindings"에서
"Switch focus to Editor" 단축키를 지워도 됩니다.
다만 플러그인 버튼으로 실행했을 때는 이 설정만으로
해결되지 않았다는 사용자 보고도 있습니다.

[IMAGE: 비교표 | 설명: 클로드 코드 인텔리제이 연결 문제 증상별 해결법 정리]

> 📌 **전문가 Tip:** JetBrains IDE에서 `acceptEdits` 모드로 쓰면
> 클로드 코드가 IDE가 자동 실행할 수 있는 설정 파일을 고칠 수 있어
> Bash 실행 권한 확인을 우회할 위험이 커질 수 있습니다.
> 공식 문서는 편집에 Manual 모드를 쓰고,
> 신뢰할 수 있는 프롬프트로만 쓰라고 권합니다.

---

## 4. 마무리

오늘은 클로드 코드 인텔리제이 사용법을
CLI 설치, 플러그인 설치, IDE 터미널 실행의 3단계로 알아보았습니다.
플러그인만으로는 동작하지 않으니 CLI부터 설치하고,
연결이 안 되면 IDE를 완전히 다시 켠 뒤 `/ide`로 확인해 보세요.

설정 몇 가지만 맞춰 두면 매일 여는 IDE가
든든한 작업 공간으로 바뀌는 법이죠!
다음 글에서는 헷갈리기 쉬운 클로드와 클로드 코드의 차이를 정리해 보겠습니다.

여러분은 인텔리제이와 외부 터미널 중 어디에서 쓰실 생각인가요?
궁금한 점이나 막힌 부분은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 인텔리제이 3단계 요약과 다음 글 클로드와 클로드 코드 차이 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드인텔리제이 #인텔리제이 #IntelliJ #JetBrains플러그인 #클로드코드사용법 #AI코딩도구`

<!-- 공식 출처 (2026-10-30 확인)
- 설치 순서(CLI → 플러그인 → IDE 터미널 실행), 지원 IDE 목록, 플러그인 이름 Claude Code [Beta], 계정 조건(API 키 불필요), Cannot launch Claude Code, Claude command 예시·WSL 명령, Plugin (Host), Cmd+Esc/Ctrl+Esc, 프로젝트 루트, /ide와 Connected to IntelliJ IDEA., 연결 후 기능(diff, 선택 영역, Cmd+Option+K/Alt+Ctrl+K, getDiagnostics), 문제 해결(재시작, No available IDEs detected, command not found, WSL2 방화벽·미러링, ESC 설정), acceptEdits 보안 주의: https://code.claude.com/docs/ko/jetbrains , https://code.claude.com/docs/en/jetbrains
- 마켓플레이스 주소: https://plugins.jetbrains.com/plugin/27310-claude-code-beta-
- 설치 명령, Homebrew·WinGet 자동 업데이트 없음, Native 자동 업데이트, claude --version, 진행 상황 미표시: https://code.claude.com/docs/en/overview
- 로그인 순서(c 키, Paste code here if prompted, Login successful): https://code.claude.com/docs/en/authentication
- autoConnectIde(기본 false, Auto-connect to IDE (external terminal)), Diff tool(기본 auto): https://code.claude.com/docs/en/settings-reference
- Free 플랜 미포함: https://claude.com/pricing
- 2.1.281(2026-09-23) /ide 메시지 수정: https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md , https://registry.npmjs.org/@anthropic-ai/claude-code
- ESC 설정으로도 안 됐다는 사용자 보고: https://github.com/anthropics/claude-code/issues/10618
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 2 "한 번 재시작으로는 반영이 안 돼서 완전히 껐다 켜고 나서야 됐다는 분이 많다": https://code.claude.com/docs/en/jetbrains , https://github.com/anthropics/claude-code/issues/23192 , https://github.com/anthropics/claude-code/issues/1232
- Step 3 "외부 터미널에서 /ide를 입력했다가 No available IDEs detected만 보고 한참 헤맸다 / 다시 깔거나 터미널을 바꿔 시도하는 분이 많다": https://code.claude.com/docs/en/jetbrains , https://github.com/anthropics/claude-code/issues/22232 , https://github.com/anthropics/claude-code/issues/23119 , https://github.com/anthropics/claude-code/issues/1232
- Step 3 "ESC에 반응이 없어 Ctrl+C로 세션을 끝내는 분이 많다": https://code.claude.com/docs/en/jetbrains , https://github.com/anthropics/claude-code/issues/1002 , https://github.com/anthropics/claude-code/issues/10618
-->
