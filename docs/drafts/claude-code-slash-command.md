# 클로드 코드 슬래시 명령어 만들기 3단계

> 💡 **한 줄 요약:** 클로드 코드 슬래시 명령어 만들기는
> 파일 만들기, 내용 쓰기, 실행하기의 3단계입니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 슬래시 명령어 만들기 3단계 대표 이미지]

"매번 똑같은 지시를 다시 적는 게 너무 번거로워요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 슬래시 명령어 만들기**는
`.claude/commands/` 폴더에 마크다운 파일 하나를 만들고,
그 파일 이름으로 `/이름`을 입력하면 끝납니다.

슬래시 명령어는 자주 쓰는 지시문을 파일로 저장해 두고
`/이름`으로 불러 쓰는 기능입니다.
오늘 이 글 하나만 끝까지 읽으시면
나만의 명령어를 만들어서 바로 써 보실 수 있습니다.
설정과 문법은 [Claude Code 공식 문서](https://code.claude.com/docs/en/skills)를
기준으로 정리했습니다.

---

## 🛠️ 시작하기 전에 알아둘 것들

* **준비물:** 클로드 코드 설치, 텍스트 편집기
* **소요 시간:** 파일 하나 기준으로 금방 끝납니다
* **난이도:** 초급, 마크다운이 처음이어도 충분합니다

공식 문서에 따르면 커스텀 명령어는 스킬로 통합되었습니다.
`.claude/commands/deploy.md` 파일과
`.claude/skills/deploy/SKILL.md` 스킬은 둘 다 `/deploy`를 만들고
같은 방식으로 동작합니다.
기존 `commands` 파일도 계속 쓸 수 있지만, 같은 이름이면 스킬이 우선합니다.

저도 처음엔 파일을 만들어 놓고 `/`를 눌렀는데 목록에 안 보여서 당황했어요.
이런 일을 겪는 분이 꽤 많더라고요.

[IMAGE: 다이어그램 | 설명: 슬래시 명령어 파일이 /이름 입력으로 호출되어 클로드가 본문 지시를 수행하는 흐름]

---

## Step 1. 슬래시 명령어 파일은 어디에 만들까?

처음 만들 때 가장 먼저 정할 것은 파일 위치와 이름입니다.
프로젝트 폴더 안에 `.claude/commands/` 폴더를 만들고
그 안에 마크다운 파일을 하나 만듭니다.
파일 이름(확장자 제외)이 곧 명령어 이름이 됩니다.

아래 순서대로 차근차근 따라와 주세요.

1. 프로젝트 폴더로 이동합니다.
2. `.claude/commands/` 폴더를 만듭니다.
3. 그 안에 `explain-file.md` 파일을 만듭니다.

터미널에서는 아래 두 줄이면 됩니다.

```bash
mkdir -p .claude/commands
touch .claude/commands/explain-file.md
```

하위 폴더를 만들면 폴더 이름이 명령어 앞에 붙습니다.
예를 들어 `.claude/commands/frontend/component.md`는
`/frontend:component`로 실행합니다.

[IMAGE: 포인트카드 | 설명: 슬래시 명령어 파일 위치 .claude/commands와 파일 이름이 명령어 이름이 되는 규칙]

> 📌 **전문가 Tip:** 모든 프로젝트에서 쓰고 싶다면
> `~/.claude/skills/<이름>/SKILL.md`에 만드세요.
> 이 경로의 스킬도 같은 `/이름`으로 동작합니다.

---

## Step 2. 슬래시 명령어 안에는 무엇을 적을까?

기본이 끝났다면 이제 파일 안을 채워 볼 차례입니다.
맨 위에는 `---`로 감싼 설정을 쓰고,
그 아래에 클로드에게 시킬 내용을 적습니다.

```markdown
---
description: 파일 하나를 초보자도 이해하게 설명합니다
argument-hint: [파일 경로]
---

$ARGUMENTS 파일을 읽고 무슨 일을 하는지
초보자도 이해할 수 있게 세 줄로 설명해 주세요.
```

핵심 항목은 세 가지입니다.

* `description`: 이 명령어가 무엇을 하는지 한 줄 설명
* `argument-hint`: 자동완성에 보이는 인자 힌트
* `$ARGUMENTS`: 명령어 뒤에 적은 내용이 들어갈 자리

`/explain-file src/app.js`처럼 실행하면
`$ARGUMENTS` 자리에 `src/app.js`가 들어갑니다.
인자가 여러 개라면 `$0`, `$1`처럼 순서대로 꺼내 쓸 수 있습니다.
값에 공백이 있다면 따옴표로 묶어 주세요.

[IMAGE: 포인트카드 | 설명: 슬래시 명령어 파일에 적는 description, argument-hint, $ARGUMENTS 세 가지]

> 📌 **전문가 Tip:** 터미널 명령의 결과를 미리 넣고 싶다면
> 느낌표 뒤에 명령을 백틱으로 감싸 쓰세요.
> 예를 들어 !`git status --short`처럼 적습니다.
> 단, 명령이 실패하면 호출 전체가 중단되니
> 실패해도 괜찮은 명령에는 `|| true`를 붙이세요.

---

## Step 3. 만든 슬래시 명령어는 어떻게 실행하고 공유할까?

대화창에 `/`를 입력하면 명령어 목록이 나옵니다.
`/explain-file src/app.js`처럼 이름 뒤에 인자를 붙여 실행해 보세요.
팀과 함께 쓰려면 `.claude/commands/` 폴더를 git에 커밋하면 됩니다.

저장 위치별 장단점은 아래 표로 정리했습니다.

[IMAGE: 비교표 | 설명: 슬래시 명령어를 저장하는 commands, 프로젝트 skills, 개인 skills 위치별 장단점 비교]

| 위치 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **.claude/commands/** | 파일 하나로 간단히 시작 | 구형식이라 같은 이름이면 스킬이 우선 |
| **.claude/skills/이름/** | 지원 파일을 함께 둠 | 폴더와 SKILL.md가 필요 |
| **~/.claude/skills/이름/** | 모든 프로젝트에서 사용 | 팀과는 공유되지 않음 |

하지만 중요한 건 공유한 명령어를 꼼꼼히 확인하는 것이겠죠.
저장소에 들어 있는 명령어의 `allowed-tools` 설정은
신뢰하지 않은 폴더에서도 적용됩니다.
받은 파일은 실행하기 전에 내용을 읽어 보세요.

### 목록에 안 보일 때는 어떻게 할까?

터미널에서는 잘 되는데 에디터 확장에서만
명령어가 안 보인다는 이야기도 많더라고요.
버전을 올린 뒤에 자동완성에서 사라졌다는 후기도 있었어요.

먼저 파일이 `.claude/commands/`에 있고 확장자가 `.md`인지 보세요.
설정 부분이 파일의 첫 줄에서 `---`로 시작하는지도 확인해야 합니다.
처음 만든 스킬 폴더가 인식되지 않을 때는 `/reload-skills`를 실행하고,
그래도 안 보이면 클로드 코드를 다시 시작해 보세요.

필드 이름이 틀려도 오류 없이 무시됩니다.
`argument-hint`처럼 하이픈까지 정확히 적으세요.
이름에 `<`나 `>` 같은 문자를 쓰면 로드되지 않습니다.

---

## 4. 마무리

오늘은 클로드 코드 슬래시 명령어 만들기를
파일 만들기, 내용 쓰기, 실행하기의 3단계로 알아보았습니다.
`.claude/commands/`에 파일 하나만 만들어도
나만의 명령어가 생기니 부담 없이 시작해 보세요.

자주 쓰는 지시 하나만 골라 명령어로 만들어 보세요.
작은 파일 하나가 반복 작업을 크게 줄여 주는 법이죠!

여러분은 어떤 지시를 가장 먼저 명령어로 만들고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 슬래시 명령어 만들기 3단계 요약, 파일 만들기와 내용 쓰기와 실행하기]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드슬래시명령어 #슬래시명령어 #커스텀명령어 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- 시작하기 전 "파일을 만들었는데 / 목록에 안 보여 당황했다 / 겪는 분이 많다": https://claudeissues.com/issue/10357-bug-custom-slash-commands-not-appearing-in-claude-code , https://claudeissues.com/issue/5995-custom-slash-commands-not-appearing-in-autocomplete-claude-code-1-0-83 , https://claudeissues.com/issue/7283-bug-custom-slash-commands-no-longer-working
- Step 3 "터미널에서는 되는데 에디터 확장에서만 안 보임": https://claudeissues.com/issue/62979-claude-code-vscode-extension-does-not-detect-custom-slash-commands-from-claude-c , https://claudeissues.com/issue/42158-bug-custom-slash-commands-from-claude-commands-not-showing-in-autocomplete-v2-1
- Step 3 "버전을 올린 뒤 자동완성에서 사라짐": https://claudeissues.com/issue/41398-custom-slash-commands-from-claude-commands-no-longer-appear-in-autocomplete-v2-1 , https://claudeissues.com/issue/48923-custom-slash-commands-from-claude-commands-not-populating-autocomplete-menu-v2-1
- 사실 확인(파일 위치와 이름 규칙, 하위 폴더 네임스페이스, commands와 skills의 관계와 우선순위, frontmatter 필드, $ARGUMENTS와 $0 $1, 느낌표 백틱 실행과 실패 시 중단, /reload-skills, 필드 이름 오타 무시, 이름 제한 문자, allowed-tools 신뢰 폴더 적용, git 커밋 공유): 공식 문서 https://code.claude.com/docs/en/skills
- "마지막 이미지의 NEXT(다음 글 예고)"는 다음 글 주제를 알 수 없어 넣지 않았다. 주제가 정해지면 마무리 문단과 06번 이미지에 추가한다.
-->
