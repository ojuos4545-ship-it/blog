# 클로드 코드 MCP 사용법 3단계 총정리

> 💡 **한 줄 요약:** 클로드 코드 MCP 사용법은 서버 연결,
> 상태 확인, 범위 설정의 3단계입니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 MCP 사용법 3단계 총정리 대표 이미지]

"외부 도구를 연결하려는데 어디서부터 해야 할지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 MCP 사용법**은
`claude mcp add`로 서버를 추가하고,
`/mcp`로 연결 상태를 본 뒤, 공유 범위를 정하면 됩니다.

MCP는 Model Context Protocol의 줄임말로,
클로드 같은 AI 도구가 외부 서비스와 연결되는 방식을 정한 공개 표준입니다.
오늘 이 글 하나만 끝까지 읽으시면
서버 하나를 연결해서 직접 써 보는 데까지 혼자 하실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/mcp)를
기준으로 정리했습니다.

---

## 🛠️ 시작하기 전에 알아둘 것들

* **준비물:** 클로드 코드 설치, 연결할 서비스 계정
* **소요 시간:** 서버 하나 기준으로 금방 끝납니다
* **난이도:** 초급, 명령어를 입력해 보셨다면 충분합니다

MCP 서버는 연결 방식이 두 가지입니다.
원격(HTTP) 서버는 인터넷 주소로 연결하고,
로컬(stdio) 서버는 내 컴퓨터에서 직접 실행합니다.
공식 문서는 원격 서버를 권장하니 처음에는 원격부터 시작해 보세요.

[IMAGE: 다이어그램 | 설명: 클로드 코드가 MCP 서버를 거쳐 노션 같은 외부 서비스에 연결되는 흐름]

---

## Step 1. 클로드 코드 MCP 서버는 어떻게 연결할까?

처음 연결할 때 헷갈리기 쉬운 부분은 명령어 순서입니다.
저도 처음엔 로컬 서버를 추가하면서 `--`를 빼먹어 한참 헤맸어요.
이 부분에서 막히는 분이 많더라고요.

아래 순서대로 차근차근 따라와 주세요.

1. 작업할 프로젝트 폴더로 이동합니다.
2. 터미널에서 서버 연결 명령을 입력합니다.
3. `claude mcp list`로 목록에 들어갔는지 확인합니다.

원격 서버는 이름과 주소만 알면 됩니다.
노션을 예로 들면 아래와 같습니다.

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

로컬 서버는 `--`가 핵심입니다.
`--` 앞은 클로드 코드 옵션이고, 뒤는 서버를 실행하는 명령입니다.
`--`가 없으면 서버의 옵션을 클로드 코드가 자기 옵션으로 읽어 버립니다.

```bash
claude mcp add --transport stdio <이름> -- <실행 명령> [인자...]
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 MCP 서버를 연결하는 원격 HTTP와 로컬 stdio 명령 구조]

> 📌 **전문가 Tip:** 서버를 지울 때는 `claude mcp remove <이름>`을 씁니다.
> 원격 서버의 접근 권한까지 취소하려면
> 먼저 `claude mcp logout <이름>`을 실행하세요.
> 이 명령은 인증 서버가 취소를 지원할 때만
> 서비스 쪽 토큰까지 취소합니다.

---

## Step 2. /mcp로 연결 상태는 어떻게 확인할까?

기본이 끝났다면 이제 실제로 연결됐는지 볼 차례입니다.
클로드 코드를 실행하고 `/mcp`를 입력하면
서버별 상태가 `Connected`, `Needs authentication`,
`Failed to connect` 중 하나로 표시됩니다.

노션처럼 로그인이 필요한 원격 서버는 같은 메뉴에서 인증합니다.
브라우저가 열리면 로그인하고 접근을 허용하면 됩니다.
인증이 끝나면 평소처럼 말로 요청해 보세요.

```
노션의 '이번 주 할 일' 페이지에서 끝내지 못한 항목만 알려줘
```

[IMAGE: 포인트카드 | 설명: /mcp 메뉴에서 클로드 코드 MCP 연결 상태를 확인하고 브라우저로 로그인하는 순서]

### 연결이 안 될 때는 어떻게 할까?

`Failed to connect`라면 서버 이름과 주소에 오타가 없는지 먼저 보세요.
`Needs authentication`이면 `/mcp`에서 로그인을 진행하면 됩니다.

로컬 서버는 윈도우에서 `npx`로 실행하는 경우에
연결 실패로 뜨는 사례가 많더라고요.
서버를 실행하는 명령을 터미널에 그대로 입력해 보세요.
거기서도 오류가 나면 원인은 클로드 코드가 아니라 서버 쪽입니다.

로그인을 마쳤는데도 `Needs authentication`이 남는 경우도 있다고 합니다.
이럴 때는 `/mcp` 메뉴에서 **Clear authentication**을 고른 뒤
다시 인증해 보세요.

서버가 여러 개 끊겼다면 `/mcp reconnect all`로 한꺼번에 다시 연결할 수 있습니다.
이 명령은 클로드 코드 v2.1.284 이상에서 동작하니,
안 된다면 버전부터 확인해 보세요.

---

## Step 3. MCP 공유 범위는 어떻게 정할까?

서버를 어느 범위로 추가하느냐에 따라 쓰이는 곳이 달라집니다.
많은 분들이 궁금해하시는 부분이라 표로 정리했습니다.

| 범위 | 적용되는 곳 | 팀 공유 | 저장 위치 |
| :--- | :--- | :--- | :--- |
| **local** (기본값) | 현재 프로젝트만 | 안 됨 | `~/.claude.json` |
| **project** | 현재 프로젝트만 | 됨 (버전 관리) | 프로젝트 루트의 `.mcp.json` |
| **user** | 모든 프로젝트 | 안 됨 | `~/.claude.json` |

범위는 `--scope` 옵션으로 정합니다.
팀원과 같은 서버를 쓰고 싶다면 `project`로 추가하면 됩니다.

```bash
claude mcp add --transport http --scope project notion https://mcp.notion.com/mcp
```

[IMAGE: 비교표 | 설명: 클로드 코드 MCP 범위 local, project, user의 장단점 비교]

| 범위 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **local** | 내 작업에만 영향을 줌 | 팀원은 각자 설정해야 함 |
| **project** | 팀이 같은 설정을 씀 | 처음 쓸 때 승인 절차가 있음 |
| **user** | 모든 프로젝트에서 바로 씀 | 안 쓰는 프로젝트에도 연결됨 |

같은 이름의 서버가 여러 범위에 있으면
local, project, user 순서로 우선하고 정의가 합쳐지지는 않습니다.
프로젝트 범위 서버는 처음 쓰기 전에 승인을 묻는데요.
이 선택을 초기화하려면 `claude mcp reset-project-choices`를 실행하세요.

하지만 중요한 건 서버를 많이 연결하는 것이 아니라
**믿을 수 있는 서버만** 연결하는 것이겠죠.
공식 문서도 외부 내용을 가져오는 서버는
프롬프트 인젝션(숨겨진 지시문으로 AI를 속이는 공격)
위험에 노출될 수 있다고 경고합니다.

도구 결과가 1만 토큰을 넘으면 경고가 뜨고,
기본 한도는 2만 5천 토큰입니다.
한도를 바꾸려면 `MAX_MCP_OUTPUT_TOKENS` 환경 변수를 쓰세요.

---

## 4. 마무리

오늘은 클로드 코드 MCP 사용법을
연결, 확인, 범위 설정의 3단계로 알아보았습니다.
연결은 `claude mcp add` 하나, 확인은 `/mcp` 하나만
기억하셔도 시작은 충분합니다.

처음에는 서버 하나만 연결해 보세요.
작은 연결 하나가 작업 방식을 바꿔 주는 법이죠!

다음 글에서는 MCP를 쓰다 보면 마주치는
컨텍스트 관리를 다뤄 보겠습니다.
여러분은 어떤 도구부터 연결해 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 MCP 3단계 요약과 다음 글 컨텍스트 관리 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드MCP #MCP사용법 #MCP서버 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "`--`를 빼먹어 헤맸다 / 막히는 분이 많다": https://claudeissues.com/issue/18722-docs-cli-syntax-inconsistency-regarding-separator-for-claude-mcp-add , https://www.neura.market/errors/fix-mcp-server-npx-connection-failures-windows
- Step 2 "윈도우에서 npx 서버가 연결 실패로 뜨는 사례 / 서버 명령을 터미널에서 직접 실행": https://mcpcat.io/guides/fixing-mcp-error-32000-connection-closed/ , https://startdebugging.net/2026/06/fix-mcp-error-32000-connection-closed-in-claude-code/ , https://claudeissues.com/issue/4703-bug-mcp-server-connection-failures-on-windows , https://wmedia.es/en/tips/claude-code-mcp-failed-to-connect-en
- Step 2 "로그인 후에도 Needs authentication이 남는 경우 / Clear authentication 후 재인증": https://claudeissues.com/issue/60260-mcp-oauth-completes-but-token-is-not-honored-server-stays-in-needs-authenticatio , https://wmedia.es/en/tips/claude-code-authenticate-mcp-oauth-terminal
- 사실 확인(명령어, 상태 문구, 범위 표, 우선순위, 승인 초기화, 토큰 한도, 보안 경고, v2.1.284): 공식 문서 https://code.claude.com/docs/en/mcp
- "다음 글: 컨텍스트 관리"는 기존 시리즈 초안(MCP 글)의 예고를 따른 것이다. 다음 글이 바뀌면 마무리 문단과 06번 이미지를 고친다.
-->
