# 클로드 코드 반복 작업 자동화 3단계

> 💡 **한 줄 요약:** 클로드 코드 반복 작업 자동화는
> 자주 하는 부탁은 스킬로, 매번 해야 하는 일은 훅으로,
> 정해진 시간에 할 일은 `/loop`로 맡기면 됩니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 반복 작업 자동화 3단계 대표 이미지]

"매번 같은 부탁을 길게 다시 쓰는 게 너무 번거로워요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 반복 작업 자동화**는
자주 쓰는 부탁을 스킬로 저장하고,
빠지면 안 되는 일은 훅으로 걸고,
시간에 맞춰 할 일은 `/loop`로 돌리는 3단계면 충분합니다.

저도 처음엔 같은 요청 문장을 메모장에 모아 두고
쓸 때마다 복사해서 붙이곤 했어요.
이렇게 같은 부탁을 계속 다시 쓰다가
명령으로 저장하는 방법을 찾았다는 후기가 꽤 많더라고요.

오늘 이 글 하나만 끝까지 읽으시면 반복되는 일을
어디에 맡겨야 하는지 직접 고르실 수 있습니다.
설정 방법은 [Claude Code 공식 문서](https://code.claude.com/docs/en/skills)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 작업할 프로젝트 폴더
* **먼저 할 일:** 일주일 동안 반복한 부탁 적어 보기
* **난이도:** 초급, 파일을 만들고 저장할 줄 알면 충분합니다

반복 작업이라고 다 같은 방법으로 맡기지는 않습니다.
내가 부탁할 때 하는 일인지, 늘 빠짐없이 해야 하는 일인지,
정해진 시간에 할 일인지에 따라 도구가 달라지는데요.
세 단계의 흐름을 한 장으로 먼저 보고 넘어가겠습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 반복 작업 자동화의 스킬, 훅, /loop 3단계 흐름]

---

## Step 1. 자주 하는 부탁은 어떻게 명령으로 만들까?

처음 할 때 가장 많이 하는 실수는
긴 부탁 문장을 매번 새로 쓰는 것입니다.
이런 부탁은 스킬로 저장해 두면 `/이름` 한 번으로 꺼내 쓸 수 있습니다.

아래 순서대로 차근차근 따라와 주세요.

1. 프로젝트에 `.claude/skills/<이름>/` 폴더를 만듭니다.
2. 그 안에 `SKILL.md` 파일을 만들고 부탁 내용을 적습니다.
3. 클로드 코드에서 `/이름`을 입력해 실행합니다.

GitHub 이슈를 고치는 부탁을 예로 들면 아래와 같습니다.
명령 뒤에 적은 내용은 `$ARGUMENTS` 자리에 그대로 들어갑니다.

```markdown
---
name: fix-issue
description: GitHub 이슈 번호를 받아 우리 규칙대로 고친다
disable-model-invocation: true
---

GitHub 이슈 $ARGUMENTS 를 읽고, 우리 코딩 규칙대로 고쳐줘.
```

이렇게 저장하면 `/fix-issue 123`만 입력해도
"이슈 123을 읽고 고쳐줘"라는 부탁이 전달됩니다.
모든 프로젝트에서 쓰고 싶다면
`~/.claude/skills/`에 저장하면 되죠.

[IMAGE: 포인트카드 | 설명: 클로드 코드 Step 1 스킬 파일 위치와 /이름 실행, $ARGUMENTS 사용법]

> 📌 **전문가 Tip:** 배포처럼 결과가 남는 일은
> `disable-model-invocation: true`를 꼭 넣어 두세요.
> 이 줄이 있으면 내가 직접 입력할 때만 실행되고,
> 없으면 설명을 보고 클로드가 알아서 꺼내 쓸 수도 있습니다.

---

## Step 2. 매번 해야 하는 일은 어떻게 자동으로 돌릴까?

기본이 끝났다면 이제 빠지면 안 되는 일을 맡길 차례입니다.
저는 `CLAUDE.md`에 "파일을 고친 뒤엔 포맷터를 돌려"라고 적어 뒀는데,
대화가 길어지면 가끔 그냥 넘어가더라고요.
지침은 읽는데 매번 지키지는 않는다는 이야기가 여러 곳에서 나옵니다.

공식 문서도 `CLAUDE.md`와 스킬은 클로드가 읽고 판단하는 지침이라
지킨다는 보장이 없다고 설명합니다.
반면 **훅**은 정해진 순간마다 클로드 코드가 직접 실행하는 명령이라,
클로드가 기억하든 말든 매번 돌아갑니다.

| 구분 | CLAUDE.md·스킬 | 훅 |
| :--- | :--- | :--- |
| **누가 실행** | 클로드가 읽고 판단 | 클로드 코드가 매번 실행 |
| **맞는 일** | 지침, 선호, 팀 절차 | 예외 없는 규칙 |
| **예시** | 이름 짓는 방식 | 고친 파일마다 포맷 |

[IMAGE: 비교표 | 설명: 클로드 코드 반복 작업 자동화에서 CLAUDE.md·스킬과 훅의 차이 비교]

훅은 설정 파일의 `hooks` 칸에 적습니다.
아래는 클로드가 파일을 고치거나 만들 때마다
Prettier로 모양을 정리하는 공식 문서의 예시입니다.
프로젝트의 `.claude/settings.json`에 넣으면 됩니다.

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [{ "type": "command", "command": "jq -r '.tool_input.file_path' | xargs npx prettier --write" }]
      }
    ]
  }
}
```

`PostToolUse`는 도구를 쓴 직후라는 뜻이고,
`Edit|Write`는 파일을 고치거나 만들 때만 돌리라는 조건입니다.
JSON이 어렵다면 "고친 파일마다 prettier를 돌리는 훅을 만들어줘"처럼
말로 부탁해도 되고, 만든 뒤에는 `/hooks`로 목록을 확인합니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 Step 2 훅 설정 위치, 실행 시점, /hooks 확인 순서]

(이때 주의할 점은 훅을 꼭 필요한 규칙에만 쓰는 것입니다.
훅은 내 컴퓨터에서 명령을 그대로 실행하고,
늘어날수록 관리할 것도 많아지기 때문입니다.)

---

## Step 3. 정해진 시간에 할 일은 어떻게 맡길까?

배포가 끝났는지, CI가 통과했는지 몇 분마다 확인하는 일도 있죠.
이럴 때는 `/loop` 뒤에 간격과 부탁을 적으면
열려 있는 세션에서 그 부탁을 정해진 간격마다 다시 실행합니다.

```
/loop 5m 배포가 끝났는지 확인하고 결과를 알려줘
```

간격은 `s`, `m`, `h`, `d` 단위로 적고,
간격을 빼면 클로드가 상황을 보고 다음 확인 시점을 정합니다.
`/loop 20m /review-pr 1234`처럼 스킬을 넣을 수도 있는데요,
`disable-model-invocation: true`가 붙은 스킬은
실행되지 않고 글자로만 전달되니 함께 기억해 두세요.

저도 `/loop`를 걸어 두고 노트북을 덮었다가,
다시 열어 보니 확인이 멈춰 있던 적이 있어요.
`/loop`는 세션이 열려 있을 때만 돌아서,
터미널을 닫으면 멈춘다는 이야기가 여러 곳에서 반복해서 나오더라고요.

공식 문서 기준으로 반복 작업은 만든 지 7일이 지나면 스스로 끝납니다.
간격을 정해 둔 반복은 `Esc`로 멈추지 않으니
"배포 확인 반복을 취소해줘"처럼 말로 부탁해야 하죠.
세션 없이도 돌려야 한다면 예약 작업을 쓰면 됩니다.

| 방식 | 좋은 점 👍 | 주의할 점 👎 |
| :--- | :--- | :--- |
| **/loop** | 지금 세션에서 바로 시작 | 세션을 닫으면 멈춤 |
| **데스크톱 예약 작업** | 세션 없이 내 파일로 실행 | 컴퓨터는 켜 둬야 함 |
| **클라우드 예약 작업** | 컴퓨터를 꺼도 실행 | 최소 간격 1시간, 새로 받은 코드로 실행 |

[IMAGE: 비교표 | 설명: 클로드 코드 Step 3 /loop, 데스크톱 예약 작업, 클라우드 예약 작업 비교]

한 번만 알림을 받고 싶다면 `/loop` 없이
"오후 3시에 릴리스 브랜치 푸시하라고 알려줘"처럼 말로 부탁하면 됩니다.
그 시간에 한 번 실행된 뒤 스스로 지워집니다.

---

## 4. 마무리

오늘은 클로드 코드 반복 작업 자동화를
스킬로 저장하기, 훅으로 매번 돌리기, `/loop`로 시간 맡기기의
3단계로 알아보았습니다.
"내가 부탁할 일인가, 빠지면 안 되는 일인가, 시간에 맞춰 할 일인가"
이 질문 하나만 기억하셔도 어디에 맡길지 고르실 수 있습니다.

처음에는 가장 자주 쓰는 부탁 하나만 스킬로 저장해 보세요.
작은 자동화 하나가 하루의 반복을 덜어 주는 법이죠!
다음 글에서는 클로드에 노션 MCP를 연결하는
3단계를 정리해 보겠습니다.

여러분은 어떤 반복 작업부터 맡겨 보고 싶으신가요?
궁금한 점은 언제든 댓글로 편하게 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 반복 작업 자동화 3단계 요약과 다음 글 노션 MCP 연결 3단계 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드자동화 #반복작업자동화 #클로드코드스킬 #클로드코드훅 #AI코딩도구 #업무자동화`

<!-- 메인 키워드: 클로드 코드 반복 작업 자동화
검색 의도: 클로드 코드에 같은 부탁을 반복하는 사람이, 자주 쓰는 부탁·매번 해야 하는 일·정해진 시간에 할 일을 각각 어떻게 자동으로 맡기는지 알고 싶다. -->

<!-- 공식 출처 (2026-10-29 확인)
- 스킬(.claude/skills/<name>/SKILL.md, ~/.claude/skills, name·description·disable-model-invocation, $ARGUMENTS, /fix-issue 123 예시, 설명을 보고 클로드가 자동 실행 가능, .claude/commands는 예전 방식): https://code.claude.com/docs/en/skills
- 훅(정해진 순간 항상 실행되는 결정적 제어, PostToolUse + Edit|Write + prettier 예시를 .claude/settings.json에, /hooks로 확인, 말로 훅 작성 요청 가능, 설정 위치 ~/.claude/settings.json·.claude/settings.json·.claude/settings.local.json): https://code.claude.com/docs/en/hooks-guide
- CLAUDE.md·스킬은 비결정적·보장 없음, 매번 해야 하면 훅, 결과가 남는 스킬은 disable-model-invocation, 훅·deny 규칙은 적게 유지: https://code.claude.com/docs/en/best-practices
- /loop(간격 s·m·h·d, 간격 생략 시 클로드가 정함, 스킬 넣기와 disable-model-invocation 스킬은 글자로 전달, 세션이 열려 있고 쉬는 동안만 실행, 7일 만료, 고정 간격 반복은 Esc로 안 멈추고 말로 취소, 한 번 알림은 말로, 클라우드·데스크톱·/loop 비교표: 클라우드 최소 1시간·새 복제·컴퓨터 불필요, 데스크톱 컴퓨터 켜 둬야 함·세션 불필요): https://code.claude.com/docs/en/scheduled-tasks
-->

<!-- 경험 문장 근거 (style-guide 10장)
- 도입 "같은 요청 문장을 모아 두고 매번 복사해 붙임 / 명령으로 저장하는 방법을 찾았다는 후기": https://codesignal.com/learn/courses/customizing-claude-code-for-reusable-visualization-workflows/lessons/creating-custom-slash-commands , https://claudemaster.net/learn/how-to-save-reusable-prompts-as-claude-code-slash-commands , https://catalins.tech/ai-slash-commands/ , https://aiengineerguide.com/til/claude-code-custom-command/
- Step 2 "CLAUDE.md에 포맷터 규칙을 적었는데 대화가 길어지면 가끔 넘어감 / 지침은 읽는데 매번 지키지는 않는다": https://uptodata.substack.com/p/what-actually-anchors-an-ai-coding , https://www.aicodex.to/articles/claude-md-vs-hooks , https://dev.to/thryx/how-to-use-claude-code-hooks-turn-rules-into-guarantees-57oe , https://blakecrosley.com/blog/claude-code-hooks-explained , https://code.claude.com/docs/en/best-practices
- Step 3 "/loop를 걸어 두고 노트북을 덮었다가 멈춰 있었음 / 터미널을 닫으면 멈춘다": https://amitkoth.com/claude-code-loop/ , https://wmedia.es/en/tips/claude-code-close-laptop-keeps-working , https://jwatte.com/blog/claude-code-loop-vs-schedule/ , https://www.mindstudio.ai/blog/what-is-claude-code-loop-command-recurring-tasks , https://code.claude.com/docs/en/scheduled-tasks
-->
