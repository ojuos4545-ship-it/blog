# 클로드 코드 컨텍스트 관리 3단계 총정리

> 💡 **한 줄 요약:** 클로드 코드 컨텍스트 관리는
> 확인하고, 비우고, 덜 채우는 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 컨텍스트 관리 3단계 총정리 대표 이미지]

"대화가 길어지니까 클로드가 앞에서 한 말을 자꾸 놓쳐요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 컨텍스트 관리**는
`/context`로 확인하고, `/compact`나 `/clear`로 비운 뒤,
처음부터 덜 채우는 습관만 들이면 됩니다.

컨텍스트는 클로드가 대화를 이어 갈 때 한꺼번에 들고 있는 작업 공간입니다.
오늘 이 글 하나만 끝까지 읽으시면
언제 확인하고 무엇으로 비울지 혼자 정하실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/how-claude-code-works)를
기준으로 정리했습니다.

---

## 🛠️ 시작하기 전에 알아둘 것들

* **준비물:** 클로드 코드 설치, 진행 중인 대화 하나
* **소요 시간:** 명령어 몇 개면 충분합니다
* **난이도:** 초급, 명령어를 입력해 보셨다면 충분합니다

컨텍스트에는 대화 기록뿐 아니라 읽은 파일 내용,
명령 실행 결과, CLAUDE.md, 불러온 스킬도 함께 쌓입니다.
이 공간이 한계에 가까워지면 클로드 코드가 대화를 요약본으로 압축하는데요.
이때 초반에 말한 세부 지시는 사라질 수 있습니다.

저도 긴 작업 중간에 앞서 정해 둔 규칙을 놓치는 일을 겪었어요.
대화가 길어질수록 클로드가 지시에서 벗어나거나
같은 작업을 반복한다는 이야기가 많더라고요.

[IMAGE: 다이어그램 | 설명: 컨텍스트가 쌓이고, 가득 차고, 요약되는 과정과 초반 세부 지시가 사라질 수 있는 지점]

---

## Step 1. /context로 컨텍스트는 어떻게 확인할까?

기본은 지금 무엇이 자리를 차지하는지 아는 것입니다.
클로드 코드 대화창에 `/context`를 입력하면
무엇이 공간을 쓰고 있는지 확인할 수 있습니다.

컨텍스트에 쌓이는 주요 항목은 다음과 같습니다.

* 대화 기록: 지금까지 나눈 요청과 답변
* 파일과 명령 출력: 읽은 파일 내용, 실행 결과
* CLAUDE.md와 메모리: 세션마다 불러오는 규칙
* 스킬과 시스템 지침: 불러온 스킬, 기본 지침

`/context`로 보면 CLAUDE.md나 MCP 설정이 자리를 꽤 차지하는 경우가 있더라고요.
설정이 길어졌다면 Step 3에서 정리해 보세요.

[IMAGE: 포인트카드 | 설명: /context로 확인하는 컨텍스트 구성, 대화 기록과 파일·명령 출력과 CLAUDE.md·스킬]

---

## Step 2. 컨텍스트는 /compact와 /clear 중 무엇으로 비울까?

처음에 헷갈리기 쉬운 부분은 두 명령의 차이입니다.
같은 작업을 이어 갈 때는 `/compact`,
관련 없는 새 작업으로 넘어갈 때는 `/clear`를 씁니다.

`/compact`는 대화를 요약해서 공간을 되찾는 명령입니다.
남길 내용은 `/compact focus on the API changes`처럼
지시문을 붙여서 정할 수 있습니다.

`/clear`는 새 세션을 시작하는 것과 같아서
이전 대화가 컨텍스트에서 모두 사라집니다.
나중에 돌아올 대화라면 `/rename`으로 이름을 붙인 뒤
`/clear`를 하고, `/resume`으로 다시 불러오세요.

[IMAGE: 비교표 | 설명: 컨텍스트를 비우는 /compact, /clear, Compact instructions의 장단점 비교]

| 방법 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **/compact** | 같은 작업을 이어 갈 수 있음 | 초반 세부 지시가 사라질 수 있음 |
| **/clear** | 쌓인 낡은 컨텍스트를 모두 비움 | 이전 대화가 사라짐 |
| **Compact instructions** | 자동 압축에도 남길 내용을 정함 | CLAUDE.md가 길어짐 |

> 📌 **전문가 Tip:** 자동 압축에도 남길 내용을 정하고 싶다면
> CLAUDE.md에 `Compact instructions` 항목을 만드세요.
> 아래처럼 한 줄만 적어도 압축할 때 참고합니다.

```markdown
# Compact instructions

When you are using compact, please focus on test output and code changes
```

---

## Step 3. 컨텍스트를 덜 채우려면 어떻게 할까?

비우는 것만큼 중요한 건 처음부터 덜 채우는 것이겠죠.
네 가지만 기억해 두세요.

* CLAUDE.md는 200줄 이하로, 꼭 필요한 내용만
* 작업별 긴 지침은 스킬로 옮기기
* 큰 출력이 나오는 일은 서브에이전트에게
* 안 쓰는 MCP 서버는 꺼 두기

CLAUDE.md는 세션이 시작될 때마다 컨텍스트에 들어옵니다.
특정 작업에만 쓰는 긴 지침은 스킬로 옮기면
필요할 때만 불러오니 기본 공간을 아낄 수 있습니다.

테스트 결과나 로그처럼 출력이 큰 일을 직접 시키면
컨텍스트가 금세 차 버리는 경우가 많더라고요.
이런 일은 서브에이전트에게 맡기면 요약만 돌아옵니다.
서브에이전트는 자기만의 컨텍스트 창에서 일하기 때문이죠.

MCP 도구 정의는 필요할 때만 불러오지만,
서버를 많이 켜 둘수록 도구 이름과 서버 지침이 자리를 차지합니다.
쓰지 않는 서버는 `/mcp`에서 꺼 두세요.

[IMAGE: 포인트카드 | 설명: 컨텍스트를 덜 채우는 방법, CLAUDE.md 200줄 이하와 스킬과 서브에이전트와 MCP 정리]

---

## 4. 마무리

오늘은 클로드 코드 컨텍스트 관리를
확인, 비우기, 덜 채우기의 3단계로 알아보았습니다.
`/context` 하나와 `/compact`, `/clear` 둘만 기억하셔도
시작은 충분합니다.

대화가 길어졌다 싶을 때 `/context`부터 열어 보세요.
작은 확인 습관 하나가 흐려진 답변을 되살리는 법이죠!

여러분은 컨텍스트가 가득 차서 곤란했던 적이 있으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 컨텍스트 관리 3단계 요약, 확인과 비우기와 덜 채우기]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드컨텍스트 #컨텍스트관리 #컨텍스트윈도우 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- "긴 작업 중 앞서 정한 규칙을 놓친다 / 지시에서 벗어나거나 같은 작업을 반복": 공식 문서 "instructions from early in the conversation can get lost" https://code.claude.com/docs/en/how-claude-code-works , 사례 정리 https://www.morphllm.com/claude-code-auto-compact , https://mcpcat.io/guides/managing-claude-code-context , https://blog.vincentqiao.com/en/posts/claude-code-compact/
- "/context로 보면 CLAUDE.md나 MCP 설정이 자리를 차지한다": https://code.claude.com/docs/en/how-claude-code-works , https://code.claude.com/docs/en/costs , https://www.jdhodges.com/blog/claude-code-context-slash-command-token-usage/
- "출력이 큰 일(테스트 결과, 로그)을 직접 시키면 금세 찬다": https://code.claude.com/docs/en/costs (Delegate verbose operations to subagents), https://code.claude.com/docs/en/how-claude-code-works (auto-compaction이 반복되는 큰 출력 문제)
- 사실 확인: /compact focus 예시, Compact instructions 예시, /rename 후 /clear 후 /resume, CLAUDE.md 200줄 이하, 스킬 on-demand, 서브에이전트 별도 컨텍스트와 요약 반환, MCP 도구 정의 지연 로드는 모두 위 두 공식 문서 기준
-->
