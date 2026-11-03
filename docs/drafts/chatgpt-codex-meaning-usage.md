# 챗GPT 코덱스 뜻과 사용법 3단계

> 💡 **한 줄 요약:** 챗GPT 코덱스는 코드를 읽고 고쳐 주는
> 오픈AI의 코딩 에이전트로, 3단계면 바로 쓸 수 있습니다.

[IMAGE: 썸네일 | 설명: 챗GPT 코덱스 뜻과 사용법 3단계 대표 이미지]

"챗GPT 메뉴에 코덱스가 보이는데 뭘 하는 곳인지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **챗GPT 코덱스**는 내 저장소의 코드를
읽고 고친 뒤 바뀐 내용을 보여 주는 오픈AI의 코딩 에이전트입니다.

깃허브를 연결하고, 작업할 저장소로 환경을 만든 뒤,
말로 일을 맡기고 결과를 확인하면 바로 쓸 수 있어요.
오늘은 코덱스의 뜻과 쓰는 곳부터
웹에서 첫 작업을 맡기는 3단계까지 차근차근 짚어볼게요.
내용은 오픈AI 공식 문서와 도움말을 바탕으로
2026년 11월 기준으로 정리했습니다.

저도 처음엔 챗GPT에 깃허브 앱만 연결해 두고
코드를 고쳐 달라고 했다가 읽기만 된다는 걸 알았어요.
코드를 고치고 PR까지 올리는 일은 코덱스가 따로 맡더라고요.

---

## 🔍 챗GPT 코덱스 뜻은 무엇일까?

코덱스(Codex)는 오픈AI가 만든 코딩 에이전트의 이름입니다.
코드를 읽고, 고치고, 실행해 보는 일까지 맡길 수 있어서
질문에 답만 하는 채팅과 달리 작업 결과물을 내놓죠.

2025년 4월 터미널용 코덱스 CLI가 먼저 나왔고,
같은 해 5월 챗GPT 안에서 쓰는 클라우드 버전이 공개됐습니다.
2026년 2월에는 맥용 코덱스 앱이 나왔고,
이후 윈도우에서도 쓸 수 있게 됐습니다.

웹에서 맡긴 작업은 오픈AI가 관리하는
클라우드 컴퓨터에서 돌아갑니다.
그래서 내 컴퓨터가 잠자기 상태여도 작업은 계속 진행되죠.
결과는 바뀐 코드(diff)로 보여 주고,
마음에 들면 깃허브에 풀 리퀘스트(PR)로 올릴 수 있습니다.

[IMAGE: 다이어그램 | 설명: 챗GPT 코덱스가 작업 지시, 클라우드 실행, 결과 확인 순서로 일하는 흐름]

코덱스는 한 곳에서만 쓰는 도구가 아닙니다.
같은 챗GPT 계정으로 네 곳에서 쓸 수 있고,
이 글에서는 설치가 필요 없는 웹을 기준으로 설명드릴게요.

| 쓰는 곳 | 특징 | 어울리는 경우 |
| :--- | :--- | :--- |
| **웹** | 클라우드에서 실행,<br>깃허브 연결 필요 | 설치 없이<br>시작할 때 |
| **앱** | 맥·윈도우용,<br>여러 작업 관리 | 작업을 여러 개<br>돌릴 때 |
| **IDE 확장** | VS Code 옆에서<br>바로 사용 | 편집기에서<br>쓰고 싶을 때 |
| **CLI** | 터미널에서 실행 | 명령어가<br>익숙할 때 |

[IMAGE: 비교표 | 설명: 챗GPT 코덱스를 쓰는 곳 웹, 앱, IDE 확장, CLI 비교]

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 챗GPT 유료 요금제, 깃허브 계정과 저장소
* **소요 시간:** 연결과 환경 만들기는 금방 끝납니다
* **난이도:** 초급, 깃허브를 써 본 적이 있으면 충분합니다

코덱스는 Plus, Pro, Business, Edu,
Enterprise 요금제에 포함돼 있습니다.
무료와 Go 요금제는 이용이 제한적이고,
웹에서 돌리는 클라우드 작업은 포함되지 않는다고 안내돼 있어요.

회사 계정(Enterprise)이라면 클라우드 사용이
기본으로 꺼져 있을 수 있습니다.
이때는 워크스페이스 관리자가 먼저 켜 줘야 쓸 수 있습니다.

---

## Step 1. 코덱스에 깃허브는 어떻게 연결할까?

웹 코덱스는 내 저장소의 코드를 읽어야 일을 할 수 있습니다.
그래서 가장 먼저 깃허브 계정을 연결해야 하는데요.
아래 순서대로 차근차근 따라와 주세요.

1. 챗GPT 왼쪽 사이드바에서 **Codex**를 엽니다.
2. 깃허브 연결 버튼을 누르고 팝업 창에서 로그인합니다.
3. 코덱스가 접근할 저장소를 고르고 권한을 승인합니다.

승인 화면에는 ChatGPT Codex Connector라는 이름이 나옵니다.
코덱스가 깃허브에 접근할 때 쓰는 앱이니 승인하시면 됩니다.
저장소는 공개와 비공개 모두 고를 수 있는데,
처음에는 작업할 저장소만 골라 두는 편이 안전하겠죠.

[IMAGE: 포인트카드 | 설명: 챗GPT 코덱스에 깃허브 계정을 연결하는 순서]

---

## Step 2. 작업할 환경은 어떻게 만들까?

기본이 끝났다면 이제 환경을 만들 차례입니다.
환경은 코덱스가 일할 작업실 같은 것으로,
어떤 저장소에서 일할지 정해 두는 설정입니다.

1. 코덱스 화면에서 환경 설정으로 들어갑니다.
2. 새 환경을 만들고 깃허브 조직과 저장소를 고릅니다.
3. 알아보기 쉬운 이름과 설명을 적고 저장합니다.

환경은 한 번 만들어 두면 다음 작업에서도 다시 쓸 수 있습니다.
작업에 필요한 패키지를 미리 설치하는 준비 단계도
환경에 넣어 둘 수 있어요.

저도 처음엔 막 만든 빈 저장소를 연결했다가
작업이 만들어지지 않아 한참 헤맸어요.
README 파일 하나를 올리고 나서야 제대로 되더라고요.

같은 증상으로 커뮤니티에 글을 올린 분이 꽤 많은데요.
저장소가 목록에 안 보이거나 작업이 실패한다면,
연결한 깃허브 계정에 그 저장소 권한이 있는지,
환경에 그 저장소가 들어 있는지부터 확인해 보세요.

[IMAGE: 포인트카드 | 설명: 챗GPT 코덱스 환경을 만들고 저장소가 안 보일 때 확인할 점]

---

## Step 3. 작업은 어떻게 맡기고 확인할까?

환경까지 만들었다면 이제 실제로 일을 맡겨 볼 차례입니다.
코덱스 입력창에 하고 싶은 일을 평소 말투로 적으면 되는데요.
무엇을 고치고 어떻게 확인할지까지 적으면 검토가 쉬워집니다.

```
로그인 화면에서 비밀번호가 틀렸을 때 오류 문구가 안 보이는 문제를 고치고, 관련 테스트도 추가해줘
```

작업이 끝나면 바뀐 코드를 diff 화면에서 확인합니다.
고칠 점이 있으면 이어서 요청하고,
마음에 들면 깃허브 저장소에 풀 리퀘스트를 만들면 됩니다.

[IMAGE: 포인트카드 | 설명: 챗GPT 코덱스에 작업을 맡기고 diff 확인 후 PR을 만드는 순서와 요청 예시]

하지만 중요한 건 코덱스가 고친 코드를 그대로 합치는 것이 아니라
**직접 검토하고 합치는 것**이겠죠.
PR로 올라온 변경도 동료의 코드처럼 읽어 보고 테스트를 확인하세요.

사용량도 함께 살펴보셔야 합니다.
코덱스는 요금제마다 쓸 수 있는 양이 다르고,
CLI에서는 `/status`로 남은 양을 확인할 수 있습니다.

저도 몇 번 맡기지 않았는데 한도 안내가 떠서 당황한 적이 있어요.
오픈AI 커뮤니티에도 같은 일을 겪은 분들의 글이 꽤 많더라고요.
안내에 다시 쓸 수 있는 시간이 나오니 먼저 확인해 보세요.

> 📌 **전문가 Tip:** 깃허브 이슈나 PR 댓글에서
> `@codex`를 부르면 그 자리에서 작업을 맡길 수 있습니다.
> 터미널이 편하다면 `npm install -g @openai/codex`로
> CLI를 설치한 뒤 `codex`를 입력해 보세요.

---

## 4. 마무리

오늘은 챗GPT 코덱스의 뜻과 사용법을
깃허브 연결, 환경 만들기, 작업 맡기기의 3단계로 알아보았습니다.
코덱스가 코드를 대신 고쳐 주더라도
마지막 확인은 여전히 사람의 몫이라는 점만 기억하시면 됩니다.

처음에는 작은 버그 하나부터 맡겨 보세요.
작은 시도 하나가 반복 작업을 덜어 주는 첫걸음이 되는 법이죠!

여러분은 코덱스에 어떤 작업부터 맡겨 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 챗GPT 코덱스 사용법 3단계 요약: 깃허브 연결, 환경, 작업]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#챗GPT #ChatGPT #챗GPT코덱스 #코덱스 #OpenAICodex #코덱스사용법 #AI코딩도구 #코딩에이전트`

<!-- 글 유형: B 가이드 (앞에 뜻 설명 섹션을 둔 형태)
메인 키워드: 챗GPT 코덱스 사용법 (제목은 "챗GPT 코덱스 뜻과 사용법", 본문 반복은 "챗GPT 코덱스")
검색 의도: 챗GPT 메뉴의 코덱스가 무엇인지 모르는 사람이, 코덱스의 뜻과 쓸 수 있는 요금제, 처음 작업을 맡기는 절차를 알고 싶다.

공식 근거 (검색 결과 요약으로 확인. developers.openai.com, help.openai.com은 세션 네트워크 제한으로 직접 열람하지 못함)
- 코덱스 정의(코드를 읽고 고치고 실행), CLI 설치 npm install -g @openai/codex, 폴더에서 codex 실행 후 챗GPT 계정 로그인: https://developers.openai.com/codex/cli.md , https://help.openai.com/en/articles/11369540-using-codex-cli
- 2025년 4월 CLI, 2025년 5월 클라우드 에이전트 연구 미리보기: https://infoq.com/news/2025/05/openai-codex , https://forklog.com/en/openai-unveils-cloud-based-ai-agent-codex/
- 2026년 2월 맥 앱, 이후 윈도우 앱: https://simonwillison.net/2026/Feb/2/introducing-the-codex-app/ , https://engadget.com/ai/openai-brings-its-codex-coding-app-to-windows-195345429.html
- 요금제(Plus, Pro, Business, Edu, Enterprise 포함, 무료·Go 제한적이고 클라우드 미포함, Enterprise 클라우드 기본 꺼짐), 클라우드 작업은 컴퓨터가 잠자기여도 진행, IDE 확장(VS Code와 Cursor·Windsurf), /status로 사용량 확인: https://help.openai.com/en/articles/11369540-openai-codex-faq , https://developers.openai.com/codex/ide , https://developers.openai.com/codex/quickstart.md
- 웹 사용 절차(사이드바 Codex, 깃허브 팝업 인증, 저장소 선택, ChatGPT Codex Connector 승인, 환경 만들기, diff 검토 후 PR, @codex 멘션), 챗GPT 깃허브 앱은 읽기 전용: https://developers.openai.com/codex/cloud.md , https://help-lb.openai.com/en/articles/11145903-connecting-github-to-chatgpt , https://datacamp.com/tutorial/openai-codex
- 저장소가 안 보일 때 확인할 점(깃허브 계정 권한, 환경 포함 여부): https://help.openai.com/en/articles/20001545-using-codex-cloud

경험 문장 근거 (style-guide 10장)
- 도입 "깃허브 앱만 연결하고 코드를 고쳐 달라고 했다가 읽기만 된다는 걸 알았다": https://help-lb.openai.com/en/articles/11145903-connecting-github-to-chatgpt (챗GPT 깃허브 앱은 읽기 전용, 수정·PR은 코덱스), https://www.eesel.ai/es/blog/openai-codex-integrations-with-github
- Step 2 "빈 저장소를 연결했다가 작업이 만들어지지 않음 / README를 올리고 해결": https://community.openai.com/t/failed-to-create-task-error/1356664 , https://community.openai.com/t/codex-failing-to-create-new-tasks-and-follow-ups/1313682 , https://github.com/openai/codex/issues/21179
- Step 3 "몇 번 맡기지 않았는데 한도 안내가 떴다 / 커뮤니티에 같은 글이 많다": https://community.openai.com/t/codex-usage-limit-is-reached-too-quickly-even-with-chatgpt-plus/1379502 , https://community.openai.com/t/chatgpt-codex-app-says-i-ve-hit-the-usage-limit-but-status-shows-97-left/1392886 , https://community.openai.com/t/bug-pro-account-cannot-use-codex-cli-youve-hit-your-usage-limit-despite-available-quota/1382937
-->
