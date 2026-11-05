# 클로드 코드 .env 파일 보호하는 3가지

> 💡 **한 줄 요약:** .env는 읽기 차단 규칙, 샌드박스,
> 비밀값 줄이기의 3겹으로 지키는 것이 안전합니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 .env 파일 보호하는 3가지 대표 이미지]

"클로드 코드가 내 .env 파일을 읽는 건 아닐까 불안해요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 .env 파일 보호**는
`permissions.deny` 규칙, 샌드박스, 비밀값 줄이기의
3겹으로 하시면 됩니다.

한 가지 방법만 쓰면 빈틈이 생기기 쉬워서
각각 무엇을 막고 무엇을 못 막는지까지 나눠 정리했습니다.
오늘 이 글 하나만 끝까지 읽으시면
내 프로젝트에 맞는 설정을 직접 넣어 보실 수 있습니다.
설정과 동작은 [Claude Code 공식 문서](https://code.claude.com/docs/en/permissions)를
2026년 11월 5일에 확인해 정리했습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 .env 파일 보호 3겹, 읽기 차단 규칙에서 샌드박스와 비밀값 줄이기로 이어지는 순서]

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드, 프로젝트 폴더의 .env 파일
* **소요 시간:** 설정 파일 하나 기준으로 금방 끝납니다
* **난이도:** 초급, JSON 파일을 열어 본 적이 있으면 충분합니다

처음이라면 프로젝트 폴더의 `.claude/settings.json`에
설정을 넣어 보세요.
이 파일은 그 폴더에서 작업하는 모두에게 적용되는
공유 설정이라, 팀이 같은 규칙을 쓰기 좋습니다.

---

## Step 1. .env 읽기는 deny 규칙으로 어떻게 막을까?

가장 먼저 할 일은 `permissions.deny`에 읽기 금지 규칙을 넣는 것입니다.
저도 처음엔 규칙 한 줄이면 전부 막힌다고 생각했어요.
그런데 규칙을 넣었는데도 .env가 읽혔다는 사례가
이슈로 올라와 있어서, 확인 단계까지 함께 알려 드릴게요.

아래 순서대로 차근차근 따라와 주세요.

1. 프로젝트 폴더의 `.claude/settings.json`을 엽니다.
2. 파일이 없다면 새로 만들어도 됩니다.
3. 아래 내용을 넣고 저장합니다.

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)"
    ]
  }
}
```

`Read(./.env)`는 현재 폴더의 .env를 막고,
`Read(./.env.*)`는 `.env.local`처럼 뒤에 이름이 붙은
파일까지 막습니다.
공식 문서에 따르면 Read 규칙은 같은 경로에 대한
Edit와 Write 도구도 함께 막아 줍니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 .env 파일 보호를 위한 permissions.deny 읽기 차단 규칙 3줄]

> 📌 **전문가 Tip:** `.claudeignore` 파일로 막아 두셨다면 주의하세요.
> 공식 문서는 이 파일이 효과가 없다고 안내합니다.
> 항목을 `Read` deny 규칙으로 옮겨 주세요.

### 제대로 막혔는지는 어떻게 확인할까?

클로드 코드에서 `/permissions`를 입력하면
규칙 목록과 각 규칙이 들어 있는 파일이 나옵니다.
규칙이 보이면 아래처럼 부탁해서 거절되는지도 확인해 보세요.

```
.env 파일 내용을 읽어서 보여줘
```

규칙이 보이지 않는다면 `/status`에서 `Setting sources` 줄을 확인하고,
파일의 JSON 오류는 `claude doctor`로 찾을 수 있습니다.

---

## Step 2. deny 규칙의 빈틈은 샌드박스로 어떻게 막을까?

기본이 끝났다면 이제 빈틈을 메울 차례입니다.
공식 문서에 따르면 Read deny 규칙은 내장 파일 도구와
`cat`, `head`, `tail`, `sed`처럼 클로드 코드가 알아보는
명령에 적용됩니다.

하지만 파일 이름을 쓰지 않고 읽는 `grep -r pattern .` 같은 명령이나,
파이썬·노드 스크립트가 직접 파일을 여는 경우는
적용되지 않는다고 합니다.
규칙만 넣고 안심했다가 grep 결과에 .env 줄이 딸려 나오는 걸
뒤늦게 알았다는 분도 있더라고요.

| 접근 경로 | deny 규칙 | 샌드박스 |
| :--- | :--- | :--- |
| **Read 도구** | 막음 | 막지 못함 |
| **`cat .env`** | 막음 | 막음 |
| **`grep -r`** | 막지 못함 | 막음 |
| **파이썬·노드 스크립트** | 막지 못함 | 막음 |

[IMAGE: 비교표 | 설명: 클로드 코드 .env 파일 보호에서 deny 규칙과 샌드박스가 각각 막는 접근 경로 비교]

그래서 두 가지를 함께 씁니다.
샌드박스는 기본으로 꺼져 있어서 클로드 코드에서 `/sandbox`를 입력해 켜거나,
설정 파일에 `sandbox.enabled`를 `true`로 넣으면 됩니다.
지원 환경은 macOS, Linux, WSL2이고,
리눅스와 WSL2는 `bubblewrap`과 `socat`을 먼저 설치해야 합니다.
네이티브 윈도우에서는 샌드박스 없이 실행된다고 하니 꼭 확인하세요.

이제 .env를 막는 항목을 넣을 차례입니다.
아래는 홈 폴더 아래의 모든 .env를 막는 공식 문서의 예시 방식입니다.
프로젝트가 홈 폴더 안에 있다는 전제입니다.

```json
{
  "sandbox": {
    "enabled": true,
    "filesystem": {
      "denyRead": ["~/**/.env"]
    }
  }
}
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 샌드박스를 켜고 .env 읽기를 막는 순서]

> 📌 **전문가 Tip:** 샌드박스 경로는 Read 규칙과 표기법이 다릅니다.
> 샌드박스는 `~/`가 홈 기준, `/tmp/build`가 절대 경로입니다.
> Read 규칙은 `//path`가 절대 경로, `/path`가 프로젝트 기준입니다.

`denyRead`는 내장 Read 도구를 막지 못한다고 하니
Step 1의 deny 규칙은 그대로 두세요.
두 설정이 서로의 빈틈을 채우는 구조입니다.

---

## Step 3. .env 속 비밀값 자체는 어떻게 줄일까?

클로드 코드 .env 파일 보호의 마지막은 값 자체를 줄이는 일입니다.
규칙과 샌드박스를 모두 걸어도 파일 안에 값이 많을수록
사고가 났을 때의 피해는 커집니다.
보안 연구팀 Knostic은 클로드 코드가 .env 같은 파일을
따로 묻지 않고 불러온다고 보고했는데요.
프로젝트를 열었을 뿐인데 .env 값이 이미 쓰이고 있었다는 사례도
함께 소개되어, 파일을 어디에 두는지부터 다시 보게 됩니다.

세 가지만 바꿔도 노출될 수 있는 값이 줄어듭니다.

1. .env를 프로젝트 폴더 밖으로 옮기고, 경로도 고칩니다.
2. 키는 필요한 권한만 가진 개발용 키로 바꿉니다.
3. 운영 서버의 키는 .env 대신 비밀 관리 서비스에 둡니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 .env 파일 보호를 위해 비밀값을 줄이는 세 가지 방법]

> 📌 **전문가 Tip:** 키가 대화에 노출됐을지도 모른다는 생각이 들면
> 해당 키를 새로 발급받아 바로 교체하세요.
> 교체한 뒤에는 이전 키가 더 이상 쓰이지 않는지 확인하세요.

---

## 4. 마무리

오늘은 클로드 코드 .env 파일 보호를
deny 규칙, 샌드박스, 비밀값 줄이기의 3겹으로 알아보았습니다.
규칙 하나로 끝내지 않고 겹겹이 두면
한 곳이 뚫려도 다른 곳이 받쳐 줍니다.

처음에는 `Read(./.env)` 한 줄과 `/permissions` 확인부터 시작해 보세요.
작은 설정 하나가 큰 사고를 막아 주는 법이죠!

여러분은 .env 말고 또 어떤 파일을 막아 두고 계신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 .env 파일 보호 3겹 요약, deny 규칙과 샌드박스와 비밀값 줄이기]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드env #env파일보호 #클로드코드보안 #클로드코드샌드박스 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "규칙 한 줄이면 전부 막힌다고 생각했다 / 규칙을 넣었는데도 읽혔다는 사례": https://github.com/anthropics/claude-code/issues/24846 , https://github.com/anthropics/claude-code/issues/56997 , https://medium.com/@jason.croucher/i-tried-to-stop-claude-from-reading-my-env-it-took-five-rounds-078d8e291cb4
- Step 2 "grep 결과에 .env 줄이 딸려 나오는 걸 뒤늦게 아는 분": https://dev.to/aicoding-guide/stop-claude-code-reading-your-env-with-a-read-deny-rule-5f16 , https://dev.to/vildandenai/stop-claude-code-from-reading-your-env-with-three-deny-rules-24bl
- Step 3 "프로젝트를 열었을 뿐인데 .env 값이 쓰이고 있었다는 사례 / 파일 위치부터 다시 봄": https://www.knostic.ai/blog/claude-loads-secrets-without-permission , https://nhimg.org/articles/claude-code-auto-reads-env-files-exposing-secrets-by-default/ (보안 업체의 보고이며 Anthropic 공식 확인은 아님)
공식 문서 확인(2026-11-05): https://code.claude.com/docs/en/permissions , https://code.claude.com/docs/en/sandboxing , https://code.claude.com/docs/en/settings
-->
