# 클로드 코드 settings.json 설정법

> 💡 **한 줄 요약:** settings.json은 파일 위치 고르기,
> 권한 규칙 쓰기, 적용 확인의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 settings.json 설정법 3단계 대표 이미지]

"settings.json이 어디 있는지, 뭘 적어야 하는지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 settings.json 설정법**은
파일 위치를 고르고, 권한 규칙을 적고, 적용됐는지 확인하는
3단계면 충분합니다.

settings.json은 클로드 코드의 허용 범위와 환경 설정을
파일 하나에 적어 두는 설정 파일입니다.
JSON은 중괄호 안에 "이름": 값 쌍으로 적는 텍스트 형식을 말해요.

오늘 이 글 하나만 끝까지 읽으시면
복사해서 바로 쓸 수 있는 설정 예시까지 갖게 되실 거예요.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/settings)를
2026년 11월 5일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 텍스트 편집기
* **소요 시간:** 파일 하나 기준으로 금방 끝납니다
* **난이도:** 초급, 복사해서 붙여 넣을 수 있으면 충분합니다

처음이라면 프로젝트 폴더 하나를 정해서 시작해 보세요.
한 프로젝트에서 먼저 해 보면 나중에 다른 곳에 옮기기도 쉽습니다.

---

## Step 1. 클로드 코드 settings.json은 어디에 만들까?

처음 시작할 때 가장 많이 헷갈리는 부분은 바로 파일 위치입니다.
같은 규칙을 어느 파일에 적어야 하는지,
파일이 겹치면 어느 쪽이 이기는지 몰라 헤매는 분이 꽤 많더라고요.

아래 표로 정리했습니다.

| 범위 | 파일 위치 | 적용 대상 | 팀 공유 |
| :--- | :--- | :--- | :--- |
| **user** | `~/.claude/settings.json` | 내 컴퓨터의 모든 프로젝트 | 안 됨 |
| **project** | `.claude/settings.json` | 해당 프로젝트 | 됨 (커밋하면) |
| **local** | `.claude/settings.local.json` | 해당 프로젝트 | 안 됨 |

같은 항목이 여러 파일에 있으면 높은 쪽이 이깁니다.
공식 문서 기준 순서는 관리자 설정, 명령줄, local, project, user입니다.
다만 `permissions.allow` 같은 목록은 덮어쓰지 않고 합쳐집니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 settings.json 우선순위, user보다 project, project보다 local이 우선]

아래 순서대로 차근차근 따라와 주세요.

1. 터미널에서 프로젝트 폴더로 이동합니다.
2. 그 안에 `.claude` 폴더를 만듭니다.
3. 폴더 안에 `settings.json`을 만들고 `{}`를 적습니다.

```bash
mkdir -p .claude
```

빈 중괄호 한 쌍도 올바른 JSON이라 이대로 시작해도 됩니다.

팀이 함께 쓸 규칙은 project 파일에,
나만 쓸 설정은 local 파일에 두는 게 기본입니다.
팀 공유 파일의 `allow` 규칙은 팀원이 폴더를 신뢰한 뒤에 적용되고,
`deny`와 `ask` 규칙은 바로 적용됩니다.

[IMAGE: 비교표 | 설명: 클로드 코드 settings.json 범위 user, project, local의 장단점 비교]

| 범위 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **user** | 한 번 적으면 모든 프로젝트에 적용 | 팀과 공유되지 않음 |
| **project** | 커밋하면 팀이 같은 규칙을 씀 | 팀원 모두에게 적용되니 신중히 |
| **local** | 나만 쓰는 설정을 따로 둠 | 손으로 만들면 `.gitignore`에 직접 추가 |

> 📌 **전문가 Tip:** `.claude/settings.local.json`은
> 클로드 코드가 만들 때는 git 제외 목록에 알아서 넣어 주지만,
> 손으로 만든 파일은 `.gitignore`에 직접 추가해야 합니다.

---

## Step 2. 허용과 차단 규칙은 어떻게 쓸까?

기본이 끝났다면 이제 가장 자주 쓰는 `permissions`를 채워 볼 차례입니다.
`permissions`는 클로드가 도구를 쓸 때
그냥 할지, 물어볼지, 막을지를 정하는 항목이에요.

규칙은 `allow`(허용), `ask`(확인), `deny`(차단) 세 목록에 적습니다.
형식은 `도구(세부 조건)`이고, `*`는 뒤에 무엇이 와도 맞는다는
와일드카드(아무 글자나 대신하는 기호)입니다.
아래는 공식 문서 예시에 `ask` 한 줄을 더한 형태예요.

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "allow": [
      "Bash(npm run lint)",
      "Bash(npm run test *)"
    ],
    "ask": [
      "Bash(git push *)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)"
    ]
  }
}
```

이 설정은 린트와 테스트는 묻지 않고 실행하고,
`git push`는 매번 확인하고, `.env` 파일 읽기는 막습니다.
맨 윗줄의 `$schema`는 편집기에서 자동완성과 오류 표시를 켜 주는 주소예요.

규칙이 많아져도 확인 순서는 하나입니다.
클로드 코드는 `deny`, `ask`, `allow` 순서로 규칙을 보고,
먼저 맞는 규칙이 결과를 정합니다.
그래서 넓은 `deny` 규칙은 더 좁은 `allow` 규칙으로도 풀 수 없어요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 settings.json 규칙 확인 순서 deny, ask, allow]

허용 규칙을 넣었는데도 같은 확인창이 계속 뜬다는 분이 많더라고요.
`&&`로 이어 붙인 명령에서 다시 묻는 사례도 있다고 해요.
이럴 땐 확인창에 뜬 명령을 규칙과 한 글자씩 비교해 보세요.

> 📌 **전문가 Tip:** 차단 규칙은 보안 벽이 아니라 안전 장치입니다.
> 공식 문서에 따르면 `Read` 차단은 `cat` 같은 명령까지 막지만,
> 스크립트가 파일을 직접 여는 경우는 막지 못합니다.
> 완전히 막으려면 샌드박스(프로그램을 격리하는 기능)를 켜세요.

---

## Step 3. 설정이 제대로 적용됐는지 어떻게 확인할까?

클로드 코드 settings.json 설정법의 마지막은 확인입니다.
그 전에 `env`부터 한 줄 짚고 갈게요.

`env`는 클로드 코드 세션에서만 쓸 환경 변수를 적는 항목입니다.
환경 변수는 프로그램이 참고하는 설정값을 말해요.
예를 들어 Bash 명령의 기본 제한 시간은 2분(120000ms)인데,
아래처럼 5분으로 늘릴 수 있어요.

```json
{
  "env": {
    "BASH_DEFAULT_TIMEOUT_MS": "300000"
  }
}
```

위 `permissions`와 같은 중괄호 안에 쉼표로 이어서 적으면 됩니다.
팀이 공유하는 project 파일의 `env` 값은
대부분 팀원이 폴더를 신뢰한 뒤에 적용됩니다.

이제 클로드 코드를 실행하고 적용 여부를 확인할 차례입니다.

1. `/permissions`로 모든 규칙과 출처 파일을 봅니다.
2. `/status`로 읽어 들인 설정 파일을 확인합니다.
3. 문제가 있으면 터미널에서 `claude doctor`를 실행합니다. (거부된 항목을 알려 줍니다)

설정이 통째로 안 먹는 이유 중에는 JSON 문법 실수가 많더라고요.
끝에 남은 쉼표 하나, `//` 주석 하나로 파일이 무시됐다는 사례도 여럿 보였어요.
공식 문서에도 settings 파일은 엄격한 JSON이라 주석과 끝 쉼표가 오류이고,
다음 시작 때 Settings Error로 알려 준다고 적혀 있습니다.

의심된다면 문법부터 검사해 보세요.
올바르면 정리된 내용이 나오고, 틀리면 오류 위치가 나옵니다.

```bash
python3 -m json.tool .claude/settings.json
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 settings.json 적용 확인 명령 /permissions, /status, claude doctor]

---

## 4. 마무리

오늘은 클로드 코드 settings.json 설정법을
위치 고르기, 권한 적기, 확인하기의 3단계로 알아보았습니다.
위치는 project 파일 하나, 규칙은 막을 것부터,
확인은 `/permissions` 하나만 기억하셔도 시작은 충분합니다.

처음에는 `deny` 규칙 하나만 넣어 보세요.
작은 설정 하나가 매번 누르던 확인을 줄여 주는 법이죠!

여러분은 어떤 규칙부터 넣어 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 settings.json 설정법 3단계 요약: 위치, 권한, 확인]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드설정 #settingsjson #클로드코드권한설정 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "파일 위치·우선순위가 헷갈려 헤매는 분이 많다": https://dev.to/rulestack/claude-code-settings-precedence-which-of-your-five-settings-files-actually-wins-5133 , https://github.com/anthropics/claude-code/issues/12713
- Step 2 "허용 규칙을 넣어도 확인창이 계속 뜬다 / &&로 이은 명령에서 다시 묻는다": https://claudeissues.com/issue/18160-bug-claude-is-ignoring-allow-permissions-in-global-settings-json , https://claudeissues.com/issue/38261-bash-permission-allow-rules-not-honored-dont-ask-again-doesnt-persist , https://claudeissues.com/issue/18846-bug-bash-permissions-in-settings-json-not-enforced-requires-custom-hook-workarou
- Step 3 "끝 쉼표·주석 때문에 설정이 무시됐다는 사례": https://claudeissues.com/issue/2835-silent-failure-on-malformed-json-claude-settings-json-files , https://claudeissues.com/issue/24823-feature-settings-json-fails-silently-if-malformed , https://claudeissues.com/issue/9906-bug-claude-fails-to-read-settings-json-and-mcp-json-files-because-of-utf-8-bom-i

사실 근거 (공식 문서, 2026-11-05 확인)
- 설정 범위·파일 위치·우선순위·목록 병합·settings.local.json·/permissions·/status·$schema·JSON 오류 처리·claude doctor·프로젝트 allow/env 신뢰 조건: https://code.claude.com/docs/en/settings
- 규칙 문법·deny→ask→allow 평가 순서·Read 차단 범위와 샌드박스 권장: https://code.claude.com/docs/en/permissions
- BASH_DEFAULT_TIMEOUT_MS 기본값 120000ms: https://code.claude.com/docs/en/env-vars
-->
