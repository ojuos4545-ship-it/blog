# 클로드 노션 MCP 연결 방법 3단계

> 💡 **한 줄 요약:** 클로드 노션 MCP 연결은 커넥터 추가,
> 노션 로그인과 워크스페이스 선택,
> 대화에서 켜고 권한 정하기의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 노션 MCP 연결 방법 3단계 대표 이미지]

"노션에 정리해 둔 자료를 클로드가 직접 읽어 주면 좋겠는데,
어디서부터 연결해야 할지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 노션 MCP 연결**은
커넥터 목록에서 노션을 추가하고, 노션 계정으로 접근을 허용한 뒤,
대화에서 노션을 켜고 부탁하면 끝납니다.

MCP는 Model Context Protocol의 줄임말로,
AI가 외부 서비스와 연결되는 방식을 정해 둔 공개 표준입니다.
노션은 이 표준으로 만든 공식 서버를 제공하고,
클로드는 이것을 '커넥터'라는 이름으로 붙여 쓰는데요.
메뉴 이름은 [Claude 도움말](https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities)과
노션 공식 안내를 2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** Claude 계정, 노션 계정(워크스페이스 멤버)
* **사용하는 곳:** Claude 웹·데스크톱 앱, 또는 클로드 코드
* **난이도:** 초급, 버튼 몇 번과 로그인이면 충분합니다

노션 쪽에서는 워크스페이스 멤버만 연결할 수 있고,
게스트 계정은 연결이 거절됩니다.
팀(Team)·엔터프라이즈 요금제라면 조직 소유자가
먼저 노션 커넥터를 켜 둬야
각자 연결할 수 있다는 점도 기억해 두세요.

[IMAGE: 다이어그램 | 설명: 클로드 노션 MCP 연결 흐름: 클로드, 노션 커넥터, 노션 워크스페이스]

---

## Step 1. 노션 커넥터는 어디서 추가할까?

처음 헷갈리는 부분은 바로 메뉴 위치입니다.
노션 연결은 대화창이 아니라 설정의 커넥터 목록에서 시작하는데요.
아래 순서대로 차근차근 따라와 주세요.

1. Claude 웹이나 데스크톱 앱에서 **Customize > Connectors**로 갑니다.
2. **Connectors** 옆의 `+`를 눌러 목록을 엽니다.
3. 목록에서 **Notion**을 찾아 설명을 확인합니다.
4. **Connect**를 누릅니다. (노션 로그인 창이 이어서 열립니다)

대화창 왼쪽 아래 `+` 버튼이나 `/`를 누르고
**Connectors > Manage connectors**로 들어가도 같은 목록이 나옵니다.
한국어 화면에서는 메뉴 이름이 조금 다르게 보일 수 있어요.
웹이나 데스크톱에서 연결해 두면
휴대폰 Claude 앱에서도 다음 로그인부터 그대로 쓸 수 있죠.

[IMAGE: 포인트카드 | 설명: Claude 설정의 Connectors 메뉴에서 노션 커넥터를 추가하는 순서]

### 클로드 코드에서 연결한다면?

터미널에서 클로드 코드를 쓰신다면
명령 한 줄로 노션의 원격 서버를 추가합니다.
명령어 옵션과 공유 범위는 지난 MCP 사용법 글에서 자세히 다뤘어요.

```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

그다음 클로드 코드 대화창에 `/mcp`를 입력하고
노션을 골라 로그인을 진행하면 됩니다.
브라우저 창이 열리면 평소처럼 로그인하고 접근을 허용하면 되죠.

> 📌 **전문가 Tip:** 연결을 끊고 싶다면 **Customize > Connectors**에서
> 노션을 골라 연결을 해제하면 됩니다.
> 클로드 코드라면 `claude mcp remove notion`으로 지웁니다.

---

## Step 2. 노션 로그인과 워크스페이스는 어떻게 고를까?

**Connect**를 누르면 노션 로그인 창이 열립니다.
평소처럼 로그인하고 클로드의 접근을 허용하면 연결이 끝나는데요.
이때 꼭 확인해야 할 것이 바로 **워크스페이스 선택**입니다.

노션 승인 화면은 워크스페이스 하나를 기본으로 골라 두는데,
저도 처음엔 이걸 그대로 넘겼다가
원하던 곳이 아닌 다른 워크스페이스가 연결됐어요.
워크스페이스를 여러 개 쓰는 분들이
이 부분에서 많이들 헷갈리시더라고요.

잘못 연결했다면 Claude 설정에서 노션 연결을 해제하고,
다시 **Connect**를 눌러 승인 화면에서 원하는 곳을 고르면 됩니다.
보통 한 번에 워크스페이스 하나만 연결되니
대화마다 따로 바꿀 수는 없다는 점도 알아 두세요.

[IMAGE: 포인트카드 | 설명: 노션 로그인 화면에서 워크스페이스를 확인하고 클로드 접근을 허용하는 순서]

하나 더 알아 둘 점은 접근 범위입니다.
노션 공식 안내에 따르면 MCP는 연결한 사람의 노션 권한을
그대로 이어받습니다.
내가 노션에서 볼 수 있는 페이지라면 클로드도 볼 수 있다는 뜻이죠.

---

## Step 3. 대화에서 노션은 어떻게 켜고 부탁할까?

기본이 끝났다면 이제 실제로 일을 맡겨 볼 차례입니다.
대화창 왼쪽 아래 `+`나 `/`를 누르고 **Connectors**에 마우스를 올리면
연결된 서비스 목록이 나오고, 여기서 노션을 켜거나 끌 수 있습니다.
이 스위치는 대화마다 따로 적용됩니다.

연결은 해 뒀는데 클로드가 노션을 찾아보지 않는다는 분도 꽤 많더라고요.
저도 처음엔 연결만 해 두고 평소처럼 물어봤다가
노션을 들여다보지 않은 답을 받았어요.
부탁에 "노션에서"처럼 찾을 곳을 밝혀 주라는 조언이
여러 곳에서 반복되는 것도 그래서입니다.

```
노션에서 '주간 회의록' 페이지를 찾아 이번 주 결정 사항만 정리해줘
```

[IMAGE: 포인트카드 | 설명: 대화에서 노션 커넥터를 켜고 노션에서라고 밝혀 부탁하는 프롬프트 예시]

### 승인 창이 자꾸 뜬다면?

노션에 페이지를 만들거나 고치게 하면
클로드가 실행 전에 승인을 묻는 경우가 있습니다.
읽기는 한 번 허용했는데 쓰기 작업에서 또 물어서
번거롭다는 이야기가 많은데요.
작업 종류마다 따로 묻는 경우가 많기 때문이죠.

**Customize > Connectors**에서 노션을 고르면
**Tool permissions** 항목이 나옵니다.
도구 묶음이나 도구 하나마다 아래 세 가지 중 하나를 고를 수 있습니다.

| 설정 | 동작 | 어울리는 작업 |
| :--- | :--- | :--- |
| **Always allow** | 묻지 않고 바로 실행 | 자주 쓰는 읽기·검색 |
| **Needs approval** | 실행 전에 매번 확인 | 페이지 생성·수정 |
| **Blocked** | 아예 쓰지 않음 | 맡기고 싶지 않은 작업 |

[IMAGE: 비교표 | 설명: 노션 커넥터 Tool permissions의 Always allow, Needs approval, Blocked 비교]

팀·엔터프라이즈 요금제라면 소유자가 조직 전체에 정한 값이 적용되고,
사용자는 이를 바꿀 수 없습니다.
하지만 중요한 건 승인 창을 모두 없애는 것이 아니라
**되돌리기 어려운 작업만** 확인받는 것이겠죠.

---

## 4. 마무리

오늘은 클로드 노션 MCP 연결을
커넥터 추가, 로그인과 워크스페이스 선택, 대화에서 켜고 권한 정하기의
3단계로 알아보았습니다.
연결은 **Customize > Connectors**, 부탁할 때는 "노션에서" 한마디만
기억하셔도 시작은 충분합니다.

처음에는 회의록 요약처럼 읽기만 하는 일부터 맡겨 보세요.
작은 연결 하나가 노션을 오가는 수고를 덜어 주는 법이죠!
다음 글에서는 클로드의 권한 요청 창이 매번 뜨지 않게 하는 방법을
정리해 보겠습니다.

여러분은 노션의 어떤 페이지부터 클로드에게 맡겨 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 노션 MCP 연결 3단계 요약과 다음 글 권한 요청 줄이기 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드 #Claude #클로드노션연결 #노션MCP #클로드커넥터 #노션연동 #클로드코드 #MCP사용법`

<!-- 메인 키워드: 클로드 노션 MCP 연결
검색 의도: 노션 자료를 클로드가 직접 읽고 정리하게 하고 싶은 사람이, Claude 앱(또는 클로드 코드)에 노션을 연결하는 순서와 워크스페이스·권한 설정의 주의점을 알고 싶다. -->

<!-- 공식 출처 (2026-10-29 확인)
- 커넥터 추가 경로(Customize > Connectors, Connectors 옆 +, 대화창 + 또는 / > Connectors > Manage connectors, Connect/Install 후 인증), 대화마다 켜고 끄기, Tool permissions(Always allow·Needs approval·Blocked, 읽기/쓰기·삭제 묶음), 팀·엔터프라이즈는 소유자가 먼저 켜고 사용자는 덮어쓸 수 없음, 웹·데스크톱에서 연결하면 모바일에서도 사용, 연결 해제: https://support.claude.com/en/articles/11176164-use-connectors-to-extend-claude-s-capabilities , https://support.claude.com/en/articles/11724452-use-the-connectors-directory-to-extend-claude-s-capabilities
- 노션 호스티드 서버 주소(https://mcp.notion.com/mcp), OAuth, 클로드 코드는 http 방식으로 추가 후 /mcp로 인증, 연결한 사용자의 노션 권한을 그대로 이어받음, 게스트는 연결 불가: https://developers.notion.com/guides/mcp/get-started-with-mcp , https://www.notion.com/help/notion-mcp (세션 네트워크 제한으로 직접 열람하지 못하고 검색 결과 요약으로 확인)
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 2 "승인 화면의 기본 워크스페이스를 그대로 넘겨 다른 곳이 연결됨 / 워크스페이스가 여럿이면 헷갈림, 바꾸려면 해제 후 재연결": https://composio.dev/content/how-to-connect-multiple-notion-workspaces-to-claude , https://www.usecarly.com/blog/how-to-connect-multiple-notion-workspaces-to-claude/
- Step 3 "연결만 해 두고 물었더니 노션을 찾아보지 않음 / 부탁에 노션을 밝히라는 조언": https://pandaitech.my/blog/nak-sambung-ai-terus-ke-notion-guna-mcp , https://branched-cabbage-927.notion.site/Chapter-2-Connect-Claude-to-Your-Notion-31e6b6181b2080c3833fe5842ec5588a
- Step 3 "읽기는 허용했는데 쓰기에서 또 승인을 물음 / 작업 종류마다 따로 물음": https://ayyaztech.com/blog/how-to-connect-claude-to-notion-complete-setup-guide-2026 , https://claudeissues.com/issue/11380-bug-claude-continually-asks-for-permission-even-after-selecting-yes-always-allow
-->
