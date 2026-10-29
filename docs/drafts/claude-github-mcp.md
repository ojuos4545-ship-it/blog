# 클로드 깃허브 MCP 연결 방법 3단계

> 💡 **한 줄 요약:** 클로드 깃허브 MCP 연결은 토큰 만들기,
> 클로드 코드에 서버 추가, `/mcp`로 확인하고 부탁하기의
> 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 깃허브 MCP 연결 방법 3단계 대표 이미지]

"클로드가 깃허브 이슈와 PR을 직접 읽어 주면 좋겠는데,
토큰이니 헤더니 용어부터 막막해요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 깃허브 MCP 연결**은
깃허브에서 토큰을 만들고, 클로드 코드에 명령 한 줄로 서버를 추가한 뒤,
`/mcp`에서 연결 표시만 확인하면 끝납니다.

MCP(Model Context Protocol)는 AI가 바깥 서비스의 도구를
불러 쓰도록 약속해 둔 공개 규격입니다.
깃허브는 이 규격으로 만든 공식 원격 서버를 운영하고 있어서,
내 컴퓨터에 서버 프로그램을 따로 설치할 필요가 없죠.

오늘 이 글을 끝까지 따라오시면 클로드에게 이슈 정리 하나를
맡겨 보는 데까지 혼자 해 보실 수 있습니다.
명령어와 메뉴 이름은 [Claude Code 공식 문서](https://code.claude.com/docs/en/mcp)와
[깃허브 공식 설치 안내](https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-claude.md)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 깃허브 계정, 설치된 클로드 코드
* **사용하는 곳:** 터미널의 클로드 코드
* **난이도:** 초급, 명령어를 복사해 붙일 수 있으면 충분합니다

이 글은 깃허브가 직접 운영하는 공식 원격 서버를 기준으로 합니다.
예전에 많이 쓰던 npm 서버 패키지는 2025년 4월부터
지원 중단(deprecated) 상태라서,
오래된 글의 설정을 그대로 따라 하지 않는 편이 좋습니다.

Claude 웹이나 데스크톱 앱을 주로 쓰신다면
Step 2 끝의 비교표를 먼저 보셔도 괜찮습니다.
앱의 깃허브 연동은 MCP와 가져오는 정보가 달라서
목적에 따라 고르는 것이 맞기 때문이죠.

[IMAGE: 다이어그램 | 설명: 클로드 코드, 깃허브 MCP 서버, 내 저장소로 이어지는 연결 흐름]

---

## Step 1. 깃허브 토큰은 어떻게 만들까?

클로드 코드에서 깃허브 원격 서버를 쓸 때는
로그인 창 대신 개인 액세스 토큰(PAT)으로 사용자를 확인합니다.
토큰은 클로드에게 맡기는 열쇠인 셈인데요,
어떤 저장소까지 열어 줄지 미리 정해 두셨나요?

공식 문서는 저장소를 골라 권한을 줄 수 있는
세분화 토큰(fine-grained token)을 만들라고 안내합니다.
아래 순서대로 차근차근 따라와 주세요.

1. 깃허브 오른쪽 위 프로필 사진을 누르고 **Settings**로 갑니다.
2. **Developer settings > Personal access tokens**로 들어갑니다.
3. **Fine-grained tokens**에서 **Generate new token**을 누릅니다.
4. 토큰 이름과 만료 기간을 정합니다.
5. **Repository access**에서 쓸 저장소만 고릅니다.
6. 권한 항목에서 맡길 작업에 필요한 권한만 추가합니다.
7. 토큰을 만들고 화면에 나온 값을 바로 복사합니다.

토큰 값은 만든 직후 한 번만 보여 주니 꼭 바로 복사해 두세요.
권한은 처음엔 코드와 이슈를 읽는 정도로 작게 시작하고,
필요할 때 하나씩 늘리는 편이 안전합니다.

저도 처음엔 저장소 고르는 칸을 제대로 보지 않고 넘겼다가,
비공개 저장소를 찾을 수 없다는 답을 받았어요.
깃허브는 토큰이 닿지 않는 저장소를 '없음(404)'으로 돌려주기 때문에
이 부분에서 원인을 못 찾고 헤매는 분이 많더라고요.

[IMAGE: 포인트카드 | 설명: 깃허브 설정에서 MCP 연결용 세분화 토큰을 만드는 순서]

> 📌 **전문가 Tip:** 클래식 토큰을 쓴다면 `repo` 범위가 필요합니다.
> 다만 클래식 토큰은 내 모든 저장소에 닿을 수 있으니,
> 가능하면 저장소를 고를 수 있는 세분화 토큰을 쓰세요.

---

## Step 2. 클로드 코드에 깃허브 MCP 서버는 어떻게 추가할까?

토큰이 준비됐다면 이제 서버를 추가할 차례입니다.
클로드 코드 대화창이 아니라 **터미널**에 아래 명령을 입력하세요.
`YOUR_GITHUB_PAT` 자리에는 방금 복사한 토큰을 넣습니다.

```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/ \
  --header "Authorization: Bearer YOUR_GITHUB_PAT"
```

명령을 풀어 보면 `--transport http`는 원격 서버라는 뜻이고,
`github`는 내가 붙이는 서버 이름입니다.
`--header`에는 `Bearer` 뒤에 토큰을 붙여서
요청마다 이 열쇠를 함께 보내도록 적어 두는 것이죠.

깃허브 공식 안내의 윈도우 PowerShell 예시는
서버 이름 `github`를 `claude mcp add` 바로 뒤에 둡니다.
PowerShell에서 명령이 오류를 내면 이 순서로 입력해 보세요.

[IMAGE: 포인트카드 | 설명: claude mcp add 명령으로 클로드 코드에 깃허브 MCP 서버를 추가하는 구성]

### /mcp 로그인으로는 안 될까?

저도 처음엔 지난번 노션처럼 `/mcp`에서 로그인만 하면 되는 줄 알았어요.
그런데 깃허브 서버를 로그인 방식(OAuth)으로 붙이려다
동적 클라이언트 등록을 지원하지 않는다는 오류에 막혔다는 보고가
여러 곳에 꾸준히 올라와 있더라고요.

그래서 클로드 코드 공식 문서도 깃허브만큼은
토큰을 헤더에 담아 연결하는 방법으로 안내합니다.
로그인 버튼을 찾느라 시간을 쓰기보다
처음부터 토큰 방식으로 가는 편이 빠릅니다.

> 📌 **전문가 Tip:** 토큰은 비밀번호와 같습니다.
> `--scope project`로 추가하면 설정이 `.mcp.json`에 저장되어
> 팀 저장소에 토큰이 함께 올라갈 수 있으니 조심하세요.
> 여러 프로젝트에서 혼자 쓰려면 `--scope user`가 편합니다.

### Claude 앱에서는 어떻게 할까?

Claude 앱 대화창의 `+` 버튼에 있는 **Add from GitHub**는
저장소 파일을 대화에 불러오는 연동입니다.
고른 브랜치의 파일 이름과 내용만 가져오고,
커밋 기록이나 PR 정보는 가져오지 않는다는 점이 MCP와 가장 큰 차이죠.

데스크톱 앱은 깃허브 공식 안내 기준으로
원격 서버를 바로 붙이는 방식을 지원하지 않습니다.
도커(Docker)로 서버를 내 컴퓨터에 띄워야 해서,
처음이라면 클로드 코드에서 시작하는 편이 훨씬 간단합니다.

| 구분 | Claude 앱 GitHub 연동 | 클로드 코드 깃허브 MCP |
| :--- | :--- | :--- |
| **연결 방법** | 대화창 `+` > Add from GitHub | `claude mcp add` + 토큰 |
| **가져오는 것** | 고른 브랜치의 파일 내용 | 저장소, 이슈, PR 등 |
| **커밋·PR 정보** | 가져오지 않음 | 토큰 권한 안에서 조회 |
| **어울리는 일** | 코드 읽고 질문하기 | 이슈 정리, PR 확인 |

[IMAGE: 비교표 | 설명: Claude 앱 GitHub 연동과 클로드 코드 깃허브 MCP의 차이 비교]

---

## Step 3. 연결 확인하고 무엇을 부탁할까?

기본이 끝났다면 이제 실제로 연결됐는지 확인해 볼 차례입니다.
클로드 코드를 실행하고 대화창에 `/mcp`를 입력하면
`github` 줄에 체크 표시가 보여야 정상입니다.
터미널에서는 `claude mcp list`로 같은 상태를 볼 수 있어요.

명령은 문제없이 들어갔는데 실패 표시가 뜬다는 분도 꽤 많은데요.
`claude mcp add`는 토큰이 맞는지 검사하지 않고 설정만 저장해서,
예시의 `YOUR_GITHUB_PAT`를 그대로 두거나
토큰을 잘못 붙여도 일단 등록되거든요.

이럴 땐 실패 상세에 401 같은 응답 코드가 함께 나옵니다.
`claude mcp remove github`로 지운 뒤
토큰을 다시 확인해서 새로 추가하면 됩니다.

연결이 확인됐다면 이제 어떤 일부터 맡겨 볼까요?
저장소를 `계정/저장소` 형태로 정확히 밝혀 주면
클로드가 헤매지 않고 바로 찾아갑니다.

```
깃허브 내계정/내저장소에서 열린 이슈 중 bug 라벨이 붙은 것만 정리해줘
```

[IMAGE: 포인트카드 | 설명: /mcp로 깃허브 MCP 연결 상태를 확인하고 이슈 정리를 부탁하는 예시]

### 읽기만 맡기고 싶다면?

처음부터 쓰기 권한까지 맡기기는 부담스러우실 수 있죠.
깃허브 서버는 주소 끝에 `readonly`를 붙이면 읽기 도구만 켜 줍니다.
쓸 도구 묶음만 고르고 싶다면 `X-MCP-Toolsets` 헤더를 더하면 됩니다.

```bash
claude mcp add --transport http github https://api.githubcopilot.com/mcp/readonly \
  --header "Authorization: Bearer YOUR_GITHUB_PAT"
```

| 설정 | 넣는 곳 | 동작 |
| :--- | :--- | :--- |
| **기본** | 주소 `.../mcp/` | 저장소, 이슈, PR 등 기본 도구 |
| **읽기 전용** | 주소 `.../mcp/readonly` | 읽기 도구만 사용 |
| **묶음 선택** | 헤더 `X-MCP-Toolsets` | 예: `repos,issues`만 사용 |

[IMAGE: 비교표 | 설명: 깃허브 MCP 서버의 기본, 읽기 전용, 도구 묶음 선택 설정 비교]

하지만 중요한 건 서버 설정보다
**토큰 권한이 마지막 안전장치**라는 점이겠죠.
읽기 전용 주소를 쓰더라도 토큰 권한은 작게 유지해 두세요.

---

## 4. 마무리

오늘은 클로드 깃허브 MCP 연결을 토큰 만들기, 서버 추가,
연결 확인과 부탁하기의 3단계로 알아보았습니다.
토큰은 쓸 저장소만, 추가는 `claude mcp add` 한 줄,
확인은 `/mcp`, 이 세 가지만 챙기시면 첫 연결은 어렵지 않습니다.

처음에는 이슈 목록 정리처럼 읽기만 하는 일부터 맡겨 보세요.
열쇠를 작게 쥐여 줄수록 마음 편히 일을 맡길 수 있는 법이죠!
다음 글에서는 클로드 코드를 윈도우에 설치하는 방법을
3단계로 정리해 보겠습니다.

여러분은 깃허브의 어떤 일부터 클로드에게 맡겨 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 깃허브 MCP 연결 3단계 요약과 다음 글 클로드 코드 윈도우 설치 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드 #Claude #클로드코드 #깃허브MCP #클로드깃허브연결 #GitHubMCP #MCP사용법 #깃허브토큰`

<!-- 메인 키워드: 클로드 깃허브 MCP 연결
검색 의도: 깃허브 저장소·이슈·PR을 클로드가 직접 다루게 하고 싶은 사람이, 클로드 코드에 깃허브 공식 MCP 서버를 연결하는 순서(토큰 발급, 서버 추가, 연결 확인)와 인증·권한에서 막히기 쉬운 부분을 알고 싶다. -->

<!-- 공식 출처 (2026-10-29 확인)
- 클로드 코드 깃허브 예시: 세분화 토큰 발급(github.com/settings/personal-access-tokens), `claude mcp add --transport http github https://api.githubcopilot.com/mcp/ --header "Authorization: Bearer YOUR_GITHUB_PAT"`, add는 자격 증명을 검사하지 않아 자리표시자도 저장되지만 나중에 연결 실패, /mcp에서 체크 표시 확인, 잘못된 자격 증명은 ✘와 401 같은 HTTP 상태 표시, --scope local/project(.mcp.json)/user: https://code.claude.com/docs/en/mcp
- 깃허브 공식 설치 안내(Claude Code·Claude Desktop): 터미널에서 실행, Windows PowerShell 예시(서버 이름을 add 바로 뒤에), Claude Desktop은 원격 서버 미지원·도커 로컬 설정, npm 패키지 @modelcontextprotocol/server-github 2025년 4월 지원 중단, 확인 명령 claude mcp list·get: https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-claude.md
- 원격 서버 주소, 기본 도구 묶음(context, repos, issues, pull_requests, users), 클래식 토큰 최소 범위(repo 등): https://github.com/github/github-mcp-server
- 읽기 전용(주소 끝 /readonly, X-MCP-Readonly 헤더), 도구 묶음 선택(X-MCP-Toolsets 헤더, /x/{toolset} 경로): https://github.com/github/github-mcp-server/blob/main/docs/remote-server.md
- Claude 앱 GitHub 연동(대화창 + > Add from GitHub, 선택 브랜치의 파일 이름·내용만 동기화, 커밋 기록·PR 미포함): https://support.claude.com/en/articles/10167454-using-the-github-integration
- 세분화 토큰 메뉴 경로(Settings > Developer settings > Personal access tokens > Fine-grained tokens > Generate new token), 세분화 토큰 권장: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens (세션 네트워크 제한으로 직접 열람하지 못하고 검색 결과 요약으로 확인)
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "저장소 고르는 칸을 넘겼다가 비공개 저장소를 못 찾음 / 404로 돌려줘 헤매는 분이 많다": https://docs.mixpanel.com/docs/mcp-connections/github , https://fast.io/resources/github-copilot-personal-access-token-mcp/ , https://horadecodar.com.br/?p=43494 , https://github.com/github/github-mcp-server/issues/309
- Step 2 "/mcp 로그인만 하면 되는 줄 알았다 / OAuth로 붙이다 동적 클라이언트 등록 미지원 오류에 막혔다는 보고": https://github.com/anthropics/claude-code/issues/3273 , https://claudeissues.com/issue/3433-claude-code-cannot-connect-to-githubs-remote-mcp-server-using-oauth-authenticati , https://claudeissues.com/issue/50092-github-mcp-plugin-auth-fails-does-not-support-dynamic-client-registration
- Step 3 "명령은 들어갔는데 실패 표시가 뜬다 / 자리표시자·잘못된 토큰": https://code.claude.com/docs/en/mcp , https://startdebugging.net/2026/05/fix-github-mcp-server-tool-calls-fail-silently-without-pat/ , https://lzw.me/docs/opencodedocs/ko/affaan-m/everything-claude-code/faq/troubleshooting-mcp/
(claudeissues.com, startdebugging.net 등은 세션 네트워크 제한으로 직접 열람하지 못하고 검색 결과 요약으로 확인)
-->
