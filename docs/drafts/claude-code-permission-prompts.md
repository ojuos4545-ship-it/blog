# 클로드 코드 권한 요청 안 뜨게 하는 3단계

> 💡 **한 줄 요약:** 클로드 코드 권한 요청은 자주 쓰는 명령을
> 허용 규칙에 넣고, 작업에 맞는 권한 모드로 바꾼 뒤,
> 그 모드를 기본값으로 저장하면 크게 줄어듭니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 권한 요청 안 뜨게 하는 3단계 대표 이미지]

"명령 하나 돌릴 때마다 Yes를 누르느라 손이 쉴 틈이 없어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 권한 요청**은
자주 쓰는 명령을 허용 규칙으로 등록하고,
작업에 맞게 권한 모드를 바꾼 뒤,
그 모드를 설정 파일에 기본값으로 저장하는 3단계로 줄일 수 있습니다.

저도 처음엔 확인 창이 뜰 때마다 별생각 없이 Yes만 눌렀어요.
같은 명령을 몇 번이고 승인하다 보면 작업 흐름이 끊기는데요,
이 승인 피로 때문에 설정을 찾아보는 분이 꽤 많더라고요.

이 글을 끝까지 따라오시면 안전은 지키면서
확인 창만 줄이는 설정을 혼자 하실 수 있습니다.
설정 이름과 동작은 [Claude Code 공식 문서](https://code.claude.com/docs/en/permissions)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 작업 중인 프로젝트 폴더
* **먼저 확인:** 입력창 아래에 보이는 지금 권한 모드
* **난이도:** 초급, 설정 파일을 열어 저장할 줄 알면 됩니다

권한 요청은 클로드가 내 컴퓨터에서 무언가를 바꾸기 전에
먼저 허락을 받는 장치입니다.
기본 모드(Manual)에서는 파일 읽기와 검색은 묻지 않지만,
명령 실행과 파일 수정은 실행 전에 확인 창을 띄우는데요.
그래서 목표는 확인 창을 모두 끄는 것이 아니라
**안심되는 일만 묻지 않게** 만드는 것입니다.

세 단계의 흐름을 먼저 한 장으로 보고 넘어가겠습니다.
자주 쓰는 명령부터 풀고, 모드를 고른 뒤, 그 선택을 저장하는 순서입니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 권한 요청을 줄이는 3단계 흐름: 허용 규칙, 권한 모드, 기본값 저장]

---

## Step 1. 자주 쓰는 명령은 어떻게 미리 허용할까?

처음에 가장 많이 하는 실수는
확인 창에서 매번 첫 번째 **Yes**만 누르는 것입니다.
Bash 명령 확인 창에는
"Yes, and don't ask again"이라는 선택지가 있는데요.

이걸 고르면 규칙이 저장소 맨 위의
`.claude/settings.local.json` 파일에 저장되고,
같은 저장소에서는 다음 세션부터 그 명령을 다시 묻지 않습니다.
다만 파일 수정 승인은 파일에 저장되지 않고
세션이 끝날 때까지만 유지됩니다.

저도 분명 허용했는데 또 묻길래 설정이 안 먹힌 줄 알았어요.
알고 보니 저장된 규칙은 확인 창이 보여 준 범위만 허용해서,
옵션이 조금 다르거나 `&&`로 이어 붙인 명령은
다시 묻는 경우가 많더라고요.

그래서 자주 쓰는 명령은 처음부터 규칙으로 적어 두는 편이 낫습니다.
아래 순서대로 차근차근 따라와 주세요.

1. 대화창에 `/permissions`를 입력합니다.
2. Allow 목록에 허용할 규칙을 추가합니다.
3. 규칙마다 어느 설정 파일에서 왔는지 확인합니다.

설정 파일에 직접 적어도 됩니다.
아래처럼 쓰면 npm 스크립트와 깃 커밋은 묻지 않고,
`git push`로 시작하는 명령은 아예 막습니다.

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(git commit *)"
    ],
    "deny": [
      "Bash(git push *)"
    ]
  }
}
```

`*`는 그 자리에 어떤 글자가 와도 된다는 뜻입니다.
`Bash(git log *)`는 `git log` 명령만 허용하지만,
`Bash(git *)`는 깃 명령 전체를 허용하니
`*`는 꼭 세부 명령 뒤에 붙이세요.

규칙은 거부(deny), 확인(ask), 허용(allow) 순서로 따집니다.
그래서 허용 규칙으로 거부 규칙에 예외를 만들 수는 없죠.

참고로 `CLAUDE.md`에 "묻지 말고 진행해"라고 적어도
확인 창은 그대로 뜹니다.
권한은 클로드 코드 프로그램이 직접 지키는 규칙이라서
`/permissions`, 설정 파일, 권한 모드로만 바꿀 수 있습니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 Step 1 허용 규칙 작성법: /permissions, 와일드카드 위치, deny 우선]

> 📌 **전문가 Tip:** 승인 기록이 쌓였다면
> `/fewer-permission-prompts`를 실행해 보세요.
> 지난 대화에서 자주 승인한 읽기 전용 명령을 찾아
> 허용 목록을 제안해 줍니다. 제안은 꼭 읽어 보고 적용하세요.

---

## Step 2. 권한 모드는 언제 무엇으로 바꿀까?

기본이 끝났다면 이제 작업 성격에 맞게 모드를 고를 차례입니다.
터미널에서는 `Shift+Tab`을 누를 때마다 모드가 바뀌고,
입력창 아래에 `accept edits on`처럼 지금 모드가 표시됩니다.
데스크톱 앱과 VS Code는 입력창 아래의 모드 메뉴에서 고르면 되죠.

| 모드 | 묻지 않고 하는 일 | 어울리는 상황 |
| :--- | :--- | :--- |
| **Manual** (`default`) | 파일 읽기와 검색 | 하나하나 확인하고 싶을 때 |
| **acceptEdits** | 파일 수정, `mkdir`·`mv` 같은 기본 명령 | 코드를 보면서 고칠 때 |
| **plan** | 읽기와 탐색, 수정은 계획 승인 뒤 | 고치기 전에 계획부터 볼 때 |
| **auto** | 대부분의 작업, 뒤에서 안전 검사 | 긴 작업을 맡길 때 |
| **bypassPermissions** | 거의 모든 작업 | 격리된 컨테이너·VM에서만 |

[IMAGE: 비교표 | 설명: 클로드 코드 권한 모드 Manual, acceptEdits, auto, bypassPermissions 비교]

확인 창을 가장 크게 줄여 주는 건 자동 모드(auto)입니다.
명령이 실행되기 전에 별도의 검사 모델이 내 요청과 맞는지 살펴보고,
강제 푸시나 `git reset --hard`, 운영 환경 배포 같은 일은 막아 줍니다.
검사에서 3번 연속, 또는 모두 20번 막히면
자동 모드가 멈추고 다시 확인 창을 띄웁니다.

자동 모드는 쓰는 모델과 조직 설정 같은 조건이 맞을 때만 메뉴에 나타납니다.
따로 정한 모드가 없다면 v2.1.283 이상의 터미널과 VS Code는
자동 모드로 시작합니다.
그런데도 확인 창이 자주 뜬다면 지금 모드부터 확인해 보세요.

Manual이나 acceptEdits 모드에서 Bash 확인 창에
"Yes, and switch to auto mode"가 보이기도 합니다.
이걸 고르면 그 명령을 승인하면서 바로 자동 모드로 넘어갑니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 자동 모드가 권한 요청을 줄이는 방식과 멈추는 조건]

저도 확인 창에 지쳤을 때 모든 확인을 건너뛰는 옵션부터 찾아봤는데요.
`--dangerously-skip-permissions`로 바로 넘어가는 분이 많더라고요.

하지만 공식 문서는 이 모드(bypassPermissions)를
인터넷이 막힌 컨테이너나 VM 같은 격리 환경에서만 쓰라고 합니다.
`.git`, `.claude` 같은 보호 폴더 수정까지 묻지 않고 진행하기 때문입니다.

---

## Step 3. 기본 권한 모드는 어떻게 저장할까?

마지막으로 고른 모드를 시작 모드로 저장할 차례입니다.
설정 파일의 `permissions.defaultMode`에 모드 이름을 적어 두면
새 세션이 그 모드로 시작합니다.

```json
{
  "permissions": {
    "defaultMode": "acceptEdits"
  }
}
```

설정 파일은 어디에 두느냐에 따라 적용 범위가 달라집니다.
많은 분들이 헷갈려하시는 부분이라 표로 정리했습니다.

| 파일 | 적용 범위 | 팀 공유 |
| :--- | :--- | :--- |
| `~/.claude/settings.json` | 내 모든 프로젝트 | 안 됨 |
| `.claude/settings.json` | 이 프로젝트 | 됨 (깃에 올림) |
| `.claude/settings.local.json` | 이 프로젝트, 나만 | 안 됨 |

주의할 점도 있습니다.
`"auto"`는 프로젝트 안의 두 파일에 적으면 적용되지 않아서,
자동 모드를 기본으로 쓰려면 `~/.claude/settings.json`에 적어야 합니다.
`bypassPermissions`도 프로젝트 파일에 적으면 무시되고
Manual 모드로 시작하죠.

한 번만 다른 모드로 시작하고 싶다면
실행할 때 아래처럼 옵션을 붙이면 됩니다.
시작 모드는 이 옵션, 설정 파일, 기본값 순서로 정해집니다.

```bash
claude --permission-mode plan
```

VS Code는 사용자 설정의 `claudeCode.initialPermissionMode`로 정하는데,
이 값에는 `auto`를 넣을 수 없습니다.
데스크톱 앱은 모드 메뉴에서 고른 값을 폴더마다 기억하고,
plan은 이번 세션에만 적용됩니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 기본 권한 모드 저장: defaultMode, 설정 파일 위치, 실행 옵션]

### 그래도 확인 창이 뜬다면?

설정을 다 했는데도 묻는다면 아래 세 가지를 확인해 보세요.

* `ask` 규칙에 걸린 명령인지
* `.git`, `.claude`, `.bashrc` 같은 보호 경로를 고치는지
* `&&`로 이은 명령에 허용 안 된 명령이 섞였는지

`ask` 규칙은 자동 모드에서도 확인 창을 띄웁니다.
보호 경로 수정은 허용 규칙으로도 미리 승인되지 않고,
Manual과 acceptEdits 모드에서는 매번 묻습니다.

하지만 중요한 건 확인 창을 하나도 남기지 않는 것이 아니라
**위험한 일만 묻게 남겨 두는 것**이겠죠.
남은 확인 창은 한 번 더 살펴보라는 신호로 보시면 됩니다.

---

## 4. 마무리

오늘은 클로드 코드 권한 요청을 줄이는 방법을
허용 규칙, 권한 모드, 기본값 저장의 3단계로 알아보았습니다.
자주 쓰는 명령은 `/permissions`로, 작업 방식은 `Shift+Tab`으로
정한다고 기억하시면 시작은 충분합니다.

처음부터 모든 확인을 끄기보다
자주 누르던 명령 몇 개만 먼저 허용해 보세요.
작은 설정 하나가 작업 흐름을 지켜 주는 법이죠!

다음 글에서는 클로드 에이전트의 뜻과
서브에이전트와의 차이를 쉽게 풀어 보겠습니다.
여러분은 어떤 명령에서 확인 창이 가장 자주 뜨시나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 권한 요청 줄이는 3단계 요약과 다음 글 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드권한 #권한모드 #자동모드 #클로드코드설정 #AI코딩도구 #AI에이전트`

<!-- 글 정보
- 유형: B 가이드
- 메인 키워드: 클로드 코드 권한 요청
- 검색 의도: 클로드 코드를 쓰다가 명령마다 뜨는 권한 확인 창이 번거로운 사람이, 안전을 해치지 않고 확인 창을 줄이거나 없애는 설정 방법을 알고 싶다.
- 사실 근거(공식 문서, 2026-10-29 확인): https://code.claude.com/docs/en/permissions , https://code.claude.com/docs/en/permission-modes
- 다음 글 예고: 클로드 에이전트 뜻, 서브에이전트와 차이
-->

<!-- 경험 문장 근거 (style-guide 10장)
- 도입 "Yes만 눌렀다 / 승인 피로로 설정을 찾아보는 분이 많다": https://www.mindstudio.ai/blog/claude-code-fewer-permission-prompt-allow-list , https://smartscope.blog/en/generative-ai/claude/claude-code-permission-automation-guide/ , https://rajiv.com/blog/2026/03/31/stop-asking-me-configuring-claude-code-permissions-for-uninterrupted-flow , https://toolnavs.com/ko/article/1787-claude-code-always-needs-permission-confirmation-release-in-a-hierarchical-manne
- Step 1 "허용했는데 또 묻는다 / 옵션이 다르거나 && 명령은 다시 묻는다": https://claudeissues.com/issue/2560-bug-claude-code-keeps-asking-for-permission-despite-already-having-it , https://claudeissues.com/issue/2023-bug-unnecessary-approval-prompts-for-chained-bash-commands-with-curl-interrupts , https://dev.to/vincentchabran/why-claude-code-keeps-asking-for-permission-and-how-to-fix-your-setup-so-it-stops-3ho8
- Step 2 "모든 확인을 건너뛰는 옵션부터 찾는 분이 많다": https://morphllm.com/claude-code-dangerously-skip-permissions , https://www.daveswift.com/claude-without-permission/ , https://wikidocs.net/blog/@openwiki/22392/
- 위 근거 페이지 중 dev.to, claudeissues.com은 세션 네트워크 제한으로 본문을 열지 못했고, 검색 결과 요약으로만 확인했다.
-->
