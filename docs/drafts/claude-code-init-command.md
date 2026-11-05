# 클로드 코드 init 명령어 초안 만드는 법

> 💡 **한 줄 요약:** `/init` 한 줄로 CLAUDE.md 초안을 만들고,
> 틀린 곳만 고치면 됩니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 init 명령어로 CLAUDE.md 초안 만드는 법 대표 이미지]

"CLAUDE.md를 직접 쓰려니 뭘 적어야 할지 막막해요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 init 명령어**는
`/init` 한 줄로 CLAUDE.md 초안을 만들어 줍니다.

CLAUDE.md는 클로드 코드가 시작할 때 읽는
프로젝트 안내 메모 파일입니다.
오늘 이 글 하나만 끝까지 읽으시면 초안 만들기부터
틀린 곳 고치는 요령까지 혼자 하실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/memory)를
2026년 11월 5일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 코드가 있는 프로젝트 폴더
* **소요 시간:** 초안 생성은 금방 끝납니다
* **난이도:** 초급, 명령어를 입력해 보셨다면 충분합니다

초안은 폴더 안의 코드를 읽고 만들어집니다.
그래서 코드가 이미 들어 있는 프로젝트에서 시작해야
쓸 만한 내용이 담기죠.

---

## Step 1. 클로드 코드 init 명령어는 어떻게 실행할까?

처음 실행할 때 헷갈리기 쉬운 부분은 입력하는 위치입니다.
`/init`은 클로드 코드를 켠 뒤 대화창에 입력하는
슬래시 명령(`/`로 시작하는 명령)이에요.
하위 폴더에서 시작하면 파일이 그 폴더에 생길 수 있다는
후기도 있어서, 프로젝트 최상위 폴더에서 시작하길 권합니다.

아래 순서대로 차근차근 따라와 주세요.

1. 프로젝트 최상위 폴더로 이동해 클로드 코드를 실행합니다.
2. 대화창에 `/init`을 입력합니다.
3. 클로드가 코드를 살펴보고 초안을 만들 때까지 기다립니다.

```bash
cd 내-프로젝트-폴더
claude
```

클로드 코드가 켜지면 대화창에 아래 한 줄을 입력합니다.

```
/init
```

이미 CLAUDE.md가 있는 프로젝트라면
다시 실행해도 되는지 묻는 분이 있더라고요.
공식 문서는 이 경우 파일을 덮어쓰지 않고
개선할 점을 제안한다고 설명합니다.

[IMAGE: 다이어그램 | 설명: init 명령어 실행 흐름, 폴더 이동 후 /init 입력하면 CLAUDE.md 초안 생성]

> 📌 **전문가 Tip:** Cursor나 Copilot 규칙 파일이 있는 프로젝트라면
> `/init`이 그 내용을 읽어 초안에 반영합니다.
> 다른 도구에서 옮겨 오는 분께 유용한 기능이에요.

---

## Step 2. /init 초안에는 무엇이 담길까?

공식 문서가 설명하는 초안의 재료는 네 가지입니다.
빌드 명령, 테스트 명령, 프로젝트 구조 개요,
그리고 코드에서 찾아낸 작성 관례입니다.

* **빌드 명령:** 코드를 실행 가능한 상태로 만드는 명령
* **테스트 명령:** 코드가 잘 돌아가는지 검사하는 명령
* **구조 개요:** 폴더마다 맡은 역할
* **관례:** 코드에서 감지한 작성 규칙

[IMAGE: 포인트카드 | 설명: init 명령어가 CLAUDE.md 초안에 담는 빌드 명령, 테스트 명령, 구조 개요, 관례]

그럼 초안을 그대로 써도 될까요?
초안은 코드를 분석해 만든 결과라서 틀린 정보가 섞일 수 있습니다.
공식 도움말도 초안을 읽어 보고 부정확한 내용을 지운 뒤
저장하라고 안내합니다.

| 항목 | 초안이 해 주는 일 👍 | 직접 확인할 점 👎 |
| :--- | :--- | :--- |
| **명령어** | 빌드·테스트 명령을 찾아 적음 | 틀린 명령은 삭제 |
| **구조** | 폴더 역할을 정리해 줌 | 길면 핵심만 남김 |
| **규칙** | 감지한 관례를 반영 | 코드에 없는 약속은 직접 추가 |

[IMAGE: 비교표 | 설명: init 명령어 초안이 해 주는 일과 직접 확인할 점 비교]

---

## Step 3. CLAUDE.md 초안은 어떻게 다듬을까?

기본이 끝났다면 이제 다듬을 차례입니다.
초안을 그대로 두면 내용이 길어져
중요한 규칙이 묻힌다는 후기가 여러 곳에 보이더라고요.
공식 문서는 파일 하나를 200줄 아래로 맞추라고 권합니다.
길수록 컨텍스트(AI가 한 번에 읽는 분량)를 더 쓰고
지시를 덜 따르게 된다는 이유입니다.

1. 틀린 내용을 삭제합니다.
2. 파일 전체를 200줄 이하로 줄입니다.
3. 긴 설명은 `@` 표기로 다른 파일을 불러옵니다.
4. `/memory`로 파일을 열어 직접 고칩니다.

`@` 표기는 CLAUDE.md 안에 아래처럼 적습니다.
공식 문서 예시를 한국어로 옮긴 것입니다.

```
프로젝트 개요는 @README를 참고하고,
사용할 npm 명령은 @package.json을 참고하세요.
```

제대로 불러왔는지 보려면 `/context all`을 실행해
**Memory files** 목록에 CLAUDE.md가 있는지 확인하세요.

[IMAGE: 포인트카드 | 설명: CLAUDE.md 초안 다듬기 4가지, 틀린 내용 삭제와 200줄 이하와 @ 불러오기와 /memory 편집]

### 더 꼼꼼하게 만들고 싶다면?

환경 변수 `CLAUDE_CODE_NEW_INIT`을 `1`로 설정하면
`/init`이 대화형으로 진행됩니다.
먼저 CLAUDE.md, 스킬(반복 작업 지침서),
훅(특정 시점에 자동 실행되는 동작) 중
무엇을 만들지 묻습니다.

그다음 서브에이전트(보조 AI)로 코드를 살펴보고,
파일을 쓰기 전에 검토할 제안을 먼저 보여 줍니다.
공식 문서에 따르면 이 변수는 실행 방식만 바꾸니
켜 둬도 괜찮습니다.

```bash
CLAUDE_CODE_NEW_INIT=1 claude
```

---

## 4. 마무리

오늘은 클로드 코드 init 명령어로
CLAUDE.md 초안을 만들고 다듬는 법을 알아보았습니다.
실행은 `/init`, 점검은 틀린 내용 삭제,
정리는 200줄 이하만 기억하셔도 시작은 충분합니다.

한 번 만들고 끝내기보다 프로젝트가 바뀔 때
다시 손보는 분이 많더라고요.
처음부터 완벽한 파일을 만들 필요는 없어요.
작은 수정 하나가 클로드의 이해를 바꾸는 법이죠!

여러분의 프로젝트에서는 초안에 어떤 내용이 빠져 있었나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: init 명령어 3단계 요약, 실행하기와 점검하기와 다듬기]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드init #init명령어 #CLAUDEmd #클로드코드사용법 #AI코딩도구`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "다시 실행해도 되는지 묻는 분이 있다": https://www.inflearn.com/questions/1762120 , 공식 동작 설명 https://code.claude.com/docs/en/memory
- Step 1 "하위 폴더에서 시작하면 그 폴더에 생길 수 있다는 후기": 검색 결과 요약 기준. 공식 문서에는 생성 경로가 명시되어 있지 않음. 근거 출처 https://dev.to/subprime2010/claude-code-init-what-init-actually-generates-and-what-to-delete-19k2 , https://madplay.github.io/en/post/why-init-first-in-claude-code (발행 전 직접 실행해 확인 권장)
- Step 3 "초안을 그대로 두면 길어져 규칙이 묻힌다는 후기": https://dev.to/aicoding-guide/how-long-should-claudemd-be-the-200-line-target-and-what-it-costs-you-5a2e , https://dev.to/davekurian/your-claudemd-is-too-long-the-200-line-ceiling-that-actually-works-1fb0 , https://dev.to/subprime2010/claude-code-init-what-init-actually-generates-and-what-to-delete-19k2
- 마무리 "프로젝트가 바뀔 때 다시 손보는 분이 많다": https://dev.to/rajeshroyal/init-let-claude-write-its-own-onboarding-docs-1hp3 , https://gentic.news/article/master-claude-md-and-init-to-cut

공식 문서 근거 (2026-11-05 확인)
- /init 설명, 기존 파일 개선 제안, Cursor·Copilot 규칙 반영, CLAUDE_CODE_NEW_INIT, 200줄 권장, @ import, /context all: https://code.claude.com/docs/en/memory
- /init 초안 구성(빌드·테스트 명령, 구조 개요, 관례)과 "부정확한 내용 삭제" 안내: https://support.claude.com/en/articles/14553240-give-claude-context-claude-md-and-better-prompts
- /memory 설명, /init 명령 표: https://code.claude.com/docs/en/commands
-->
