# 클로드 코드 플러그인 사용법 3단계 정리

> 💡 **한 줄 요약:** 클로드 코드 플러그인 사용법은 설치,
> 실행 확인, 관리의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 플러그인 사용법 3단계 정리 대표 이미지]

"플러그인이 좋다는데 어디서 받고 어떻게 켜는지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 플러그인 사용법**은
`/plugin`에서 골라 설치하고, `/`로 실행되는지 확인한 뒤,
안 쓰는 것은 끄거나 지우면 됩니다.

플러그인은 스킬, 에이전트, 훅, MCP 서버를
한 번에 묶어 설치하는 꾸러미입니다.
오늘 이 글 하나만 끝까지 읽으시면 플러그인 하나를 설치해서
실행하고 정리하는 데까지 혼자 하실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/discover-plugins)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 터미널에서 `claude` 실행
* **소요 시간:** 플러그인 하나 기준으로 금방 끝납니다
* **난이도:** 초급, 슬래시 명령을 써 본 적이 있으면 충분합니다

먼저 꼭 알아야 할 개념 하나만 짚고 갈게요.
**마켓플레이스**는 플러그인을 모아 둔 목록이고,
Anthropic 공식 목록의 이름은 `claude-plugins-official`입니다.
터미널에서 클로드 코드를 처음 실행하면
이 공식 목록이 자동으로 등록됩니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 플러그인을 마켓플레이스에서 찾아 설치하고 실행하는 흐름]

---

## Step 1. 클로드 코드 플러그인은 어떻게 설치할까?

처음 설치할 때 가장 많이 막히는 부분은 마켓플레이스 등록입니다.
저도 설치 명령을 넣었다가 공식 마켓플레이스를
찾을 수 없다는 메시지가 떠서 한참 헤맸어요.
VS Code 확장으로만 쓰던 분들이 여기서 많이들 막히시더라고요.

아래 순서대로 차근차근 따라와 주세요.

1. 프로젝트 폴더에서 `claude`를 실행합니다.
2. `/plugin`을 입력하고 **Discover** 탭에서 플러그인을 고릅니다.
3. 상세 화면의 **Will install** 항목을 읽어 봅니다.
4. 설치 범위를 고르면 설치가 끝납니다.

이름을 알고 있다면 바로 설치 명령을 써도 됩니다.
커밋과 PR 작업을 돕는 공식 플러그인을 예로 들면 아래와 같습니다.

```
/plugin install commit-commands@claude-plugins-official
```

마켓플레이스를 찾을 수 없다는 메시지가 나오면
공식 마켓플레이스를 직접 추가하고 다시 설치하면 됩니다.
다른 사람이 만든 마켓플레이스도 같은 명령에
GitHub 저장소 이름(`owner/repo`)을 넣어 추가합니다.

```
/plugin marketplace add anthropics/claude-plugins-official
```

설치 범위는 세 가지 중에서 고릅니다.
누가 이 플러그인을 쓰게 할지 정하는 단계라 표로 정리했습니다.

| 범위 | 적용되는 곳 | 기록되는 파일 |
| :--- | :--- | :--- |
| **user** | 이 컴퓨터의 모든 프로젝트 | `~/.claude/settings.json` |
| **project** | 이 저장소의 모든 협업자 | `.claude/settings.json` |
| **local** | 이 저장소에서 나만 | `.claude/settings.local.json` |

[IMAGE: 비교표 | 설명: 클로드 코드 플러그인 설치 범위 user, project, local 비교]

같은 플러그인이 여러 범위에 있으면
local, project, user 순서로 우선합니다.
project 범위는 설정 파일만 공유되기 때문에,
협업자도 각자 한 번씩 설치 명령을 실행해야 하죠.

> 📌 **전문가 Tip:** 플러그인은 내 컴퓨터에서
> 내 권한으로 코드를 실행할 수 있습니다.
> 공식 문서도 설치 전에 믿을 수 있는지 확인하라고 안내하니,
> **Will install** 목록과 플러그인 홈페이지를 꼭 읽어 보세요.

---

## Step 2. 설치한 플러그인은 어떻게 실행할까?

기본이 끝났다면 이제 플러그인이 켜졌는지 확인할 차례입니다.
설치 요약 마지막 줄이 `Plugin is now active.`이면
바로 쓸 수 있고, `Run /reload-plugins to apply.`이면
다시 불러오기가 필요합니다.
이때는 패널이 닫히면서 클로드 코드가 알아서 실행해 줍니다.

플러그인 기능은 대화창에 `/`를 입력하면 목록에 나옵니다.
이름은 `/플러그인이름:스킬이름` 형태라서,
앞의 예시라면 `/commit-commands:commit`으로 실행합니다.
`/plugin`의 **Installed** 탭에서도 설치 범위와 함께 볼 수 있어요.

### 설치했는데 명령이 안 보이면 어떻게 할까?

설치는 끝났는데 `/` 목록에 명령이 안 보여서
고장 난 줄 아는 분이 꽤 많더라고요.
저도 같은 세션에서 바로 찾다가 안 보여서
다시 설치할 뻔했어요.

아래 순서로 하나씩 확인해 보세요.

1. `/plugin`의 **Installed** 탭에서 켜져 있는지 봅니다.
2. 같은 화면의 **Errors** 탭에서 오류를 확인합니다.
3. 이번 세션에 설치했다면 `/reload-plugins`를 실행합니다.
4. 그래도 안 보이면 클로드 코드를 새로 시작합니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 플러그인 명령이 안 보일 때 확인하는 순서]

상세 화면에 스킬이 하나도 없는 플러그인이라면
처음부터 `/` 목록에 나올 명령이 없는 것입니다.
이 경우는 오류가 아니니 플러그인 설명을 다시 읽어 보세요.

---

## Step 3. 클로드 코드 플러그인은 어떻게 관리할까?

플러그인은 설치보다 정리가 더 중요합니다.
궁금한 것을 이것저것 설치해 두다 보면,
쓰지도 않는 플러그인이 대화 공간을 차지하는 경우가 많더라고요.
켜 둔 플러그인은 쓰지 않을 때도 매번 일정한 분량을 대화에 더합니다.

관리는 `/plugin`의 **Installed** 탭에서 대부분 해결됩니다.

* **끄기·켜기:** 목록에서 플러그인을 고르고 Space 키
* **업데이트·삭제:** Enter로 상세 화면을 열고 메뉴 선택
* **안 쓰는 것 찾기:** `Not used recently` 묶음 확인

세션 밖 터미널에서는 아래 명령으로 같은 일을 할 수 있습니다.

```bash
claude plugin list
claude plugin disable <이름>@<마켓플레이스>
claude plugin uninstall <이름>@<마켓플레이스>
claude plugin details <이름>
```

`claude plugin details`를 실행하면 그 플러그인이
켜져 있는 동안 항상 더해지는 토큰 수를 보여 줍니다.
많이 차지하는 플러그인부터 끄면 정리가 훨씬 쉬워지죠.

업데이트는 마켓플레이스마다 기본값이 다릅니다.
공식 마켓플레이스는 자동 업데이트가 기본으로 켜져 있고,
다른 마켓플레이스는 기본으로 꺼져 있습니다.
업데이트돼도 지금 세션은 원래 버전을 쓰니,
안내가 뜨면 `/reload-plugins`로 반영하면 됩니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 플러그인 끄기, 업데이트, 삭제 관리 명령 정리]

하지만 중요한 건 플러그인을 많이 설치하는 것이 아니라
**지금 쓰는 것만** 켜 두는 것이겠죠.
마켓플레이스를 통째로 지우면 그곳에서 설치한
플러그인이 모두 함께 삭제된다는 점도 알아 두세요.

---

## 4. 마무리

오늘은 클로드 코드 플러그인 사용법을
설치, 실행 확인, 관리의 3단계로 알아보았습니다.
설치는 `/plugin` 하나, 다시 불러오기는 `/reload-plugins` 하나만
기억하셔도 시작은 충분합니다.

처음에는 공식 마켓플레이스에서 플러그인 하나만 설치해 보세요.
필요한 도구를 하나씩 더하다 보면
나에게 맞는 작업 환경이 만들어지는 법이죠!

여러분은 어떤 플러그인부터 설치해 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 플러그인 사용법 3단계 요약: 설치, 실행 확인, 관리]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드플러그인 #플러그인사용법 #플러그인마켓플레이스 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "공식 마켓플레이스를 찾을 수 없다는 메시지로 헤맸다 / VS Code 확장으로만 쓰던 분들이 막힌다":
  https://code.claude.com/docs/en/plugins/troubleshooting (Marketplace "claude-plugins-official" not found 항목) ,
  https://claudeissues.com/issue/22310-official-plugin-marketplace-claude-plugins-official-is-inaccessible ,
  https://github.com/anthropics/claude-code/issues/66750
- Step 2 "설치했는데 / 목록에 명령이 안 보여 고장 난 줄 안다 / 다시 설치할 뻔했다":
  https://github.com/anthropics/claude-code/issues/37862 ,
  https://claudeissues.com/issue/64956-bug-plugins-not-loading-from-marketplace-after-adding-claude-plugins-official ,
  https://scratchandwin.tcl.com/blog/claude-code-plugins-installed-but
- Step 3 "이것저것 설치하다 보면 안 쓰는 플러그인이 대화 공간을 차지한다":
  https://wmedia.es/en/tips/claude-code-unused-plugins-cost ,
  https://dev.to/ohugonnot/claude-code-i-had-10-plugins-active-at-once-heres-what-it-actually-costs-2ckn ,
  https://madewithlove.com/blog/your-claude-code-is-burning-through-tokens-heres-how-to-fix-it/
- 사실 확인(공식 문서): https://code.claude.com/docs/en/discover-plugins , https://code.claude.com/docs/en/plugins/security
-->
