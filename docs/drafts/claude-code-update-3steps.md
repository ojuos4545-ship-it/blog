# 클로드 코드 업데이트 방법 3단계

> 💡 **한 줄 요약:** 클로드 코드 업데이트 방법은 버전 확인,
> 설치 방식별 명령 실행, 재시작 후 재확인의 3단계입니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 업데이트 방법 3단계 대표 이미지]

"분명히 업데이트했는데 버전이 그대로예요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 업데이트 방법**은
`claude --version`으로 현재 버전을 확인하고,
설치 방식에 맞는 명령을 실행한 뒤, 다시 켜서 확인하면 끝입니다.

클로드 코드는 공식 설치 스크립트로 설치한 기본 방식(네이티브)이면
백그라운드에서 알아서 업데이트됩니다.
하지만 Homebrew나 WinGet으로 설치했다면 직접 올려야 하고,
이 차이를 몰라 헤매는 분이 많아요.
오늘 이 글 하나만 끝까지 읽으시면
내 설치 방식에 맞는 명령을 바로 고르실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/setup)를
2026년 11월 5일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 터미널, 이미 설치된 클로드 코드
* **소요 시간:** 명령 한두 개면 금방 끝납니다
* **난이도:** 초급, 명령어를 입력해 본 적이 있으면 충분합니다

내가 어떤 방식으로 설치했는지 모르셔도 괜찮습니다.
Step 1에서 한 번에 확인하는 방법을 알려 드릴게요.

[IMAGE: 다이어그램 | 설명: 클로드 코드 업데이트 3단계, 버전 확인과 명령 실행과 재확인 흐름]

---

## Step 1. 지금 쓰는 버전은 어떻게 확인할까?

가장 먼저 할 일은 내 클로드 코드가 지금 몇 버전인지 보는 것입니다.
터미널을 열고 아래 두 줄을 차례로 입력해 보세요.

```bash
claude --version
claude doctor
```

`claude --version`은 버전 번호를 한 줄로 알려 줍니다.
`claude doctor`는 대화를 시작하지 않고 설치 상태와 설정,
마지막 업데이트 시도 결과를 점검해 주는 진단 명령이에요.
`Auto-updates` 줄이 `enabled`인지도 여기서 볼 수 있습니다.

클로드 코드를 쓰다 보면 화면 아래쪽에 빨간색으로
`Auto-update failed · Run claude doctor` 문구가 뜰 때가 있어요.
저도 처음 봤을 때는 어디부터 손대야 할지 몰라 한참 들여다봤습니다.
다행히 이 문구가 떠도 작업은 계속할 수 있고,
업데이트만 설치되지 않은 상태라고 공식 문서가 설명합니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 업데이트 1단계, 버전과 설치 상태를 확인하는 명령 정리]

> 📌 **전문가 Tip:** `claude doctor`는 읽기만 하는 진단이라
> 몇 번을 실행해도 설정이 바뀌지 않습니다.
> 빨간 문구가 보인다면 먼저 `claude update`를 실행하세요.

---

## Step 2. 설치 방식별 업데이트 명령은 무엇일까?

기본이 끝났다면 이제 실제로 올려 볼 차례입니다.
설치 방식에 따라 명령이 달라지는데요.
아래 표에서 내 방식을 찾아 한 줄만 입력하세요.

| 설치 방식 | 자동 업데이트 | 직접 입력할 명령 |
| :--- | :--- | :--- |
| **네이티브** (기본) | 됨 | `claude update` |
| **Homebrew** | 안 됨 | `brew upgrade claude-code` |
| **WinGet** | 안 됨 | `winget upgrade Anthropic.ClaudeCode` |
| **npm** | 폴더 권한에 따라 다름 | `npm install -g @anthropic-ai/claude-code@latest` |

[IMAGE: 비교표 | 설명: 클로드 코드 업데이트 명령을 네이티브, Homebrew, WinGet, npm 설치 방식별로 비교]

네이티브 방식은 `claude update` 하나로 바로 올라갑니다.
이미 최신이면 `Claude Code is up to date`라고 알려 주고,
새로 설치되면 `Successfully updated from`으로 시작하는 문장이 나옵니다.
Homebrew에서 `claude-code@latest` 버전을 설치했다면
`brew upgrade claude-code@latest`를 쓰세요.
apt, dnf, apk로 설치했다면 평소 쓰는 시스템 업그레이드 명령으로 올립니다.

Homebrew나 WinGet으로 깔고 자동으로 올라가는 줄 알고 지내다가
버전이 그대로인 걸 뒤늦게 알아채는 분이 꽤 많더라고요.
공식 문서도 이 두 방식은 자동 업데이트가 되지 않는다고 따로 안내합니다.
또 새 버전 알림이 떴는데 패키지 관리자에는 아직 올라오지 않아
업그레이드가 실패하는 경우도 있으니, 그때는 잠시 뒤 다시 해 보세요.

### npm 설치에서 권한 오류가 나면 어떻게 할까?

npm으로 설치했다면 `@latest`를 꼭 붙여야 합니다.
`npm update -g`는 처음 설치할 때의 범위를 따라가서
최신 버전으로 안 올라갈 수 있다고 공식 문서가 경고해요.

권한 오류가 나면 일단 `sudo`부터 붙이는 분이 많은데요.
이렇게 하면 이후 설치가 더 꼬이는 경우가 많더라고요.
공식 문서도 `sudo npm install -g`를 쓰지 말라고 안내하며,
npm 권한 오류가 반복되면 네이티브 설치로 옮기라고 권합니다.

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

위 명령은 macOS, Linux, WSL용입니다.
Windows PowerShell에서는 아래 명령을 쓰세요.

```powershell
irm https://claude.ai/install.ps1 | iex
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 업데이트가 막힐 때 확인할 4가지: 빨간 문구, 권한 오류, npm, 패키지 관리자]

---

## Step 3. 업데이트가 끝나면 무엇을 확인할까?

업데이트를 설치했다면
열려 있는 클로드 코드 세션을 모두 닫고 새로 시작하세요.
백그라운드로 받은 업데이트는 다음에 시작할 때 적용된다고
공식 문서에 나와 있습니다.
새로 켠 뒤에는 `claude --version`으로 번호가 바뀌었는지 보면 됩니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 업데이트 후 세션 종료, 재시작, 버전 확인 순서]

### 새 기능이나 새 모델이 안 보이면 어떻게 할까?

그럴 때는 업데이트 채널을 확인해 보세요.
채널은 `/config`의 **Auto-update channel** 메뉴나
`settings.json`의 `autoUpdatesChannel`로 바꿉니다.

| 채널 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **latest** (기본값) | 새 기능을 나오자마자 받음 | 갓 나온 버전이라 문제를 만날 수 있음 |
| **stable** | 약 1주 지난 버전, 큰 문제가 있던 릴리스는 건너뜀 | 새 모델에 필요한 버전이 아직 없을 수 있음 |

갓 나온 모델은 stable 채널이 주는 버전보다
더 새로운 클로드 코드를 요구할 수 있습니다.
공식 문서도 이럴 때는 latest 채널로 옮기라고 안내해요.
Homebrew는 이 설정 대신 `claude-code`(stable)와
`claude-code@latest` 중 어느 쪽을 설치했는지로 채널이 정해집니다.

자동 업데이트를 끄고 싶다면
`settings.json`의 `env`에 `DISABLE_AUTOUPDATER`를 `"1"`로 넣으세요.
이 설정은 백그라운드 확인만 막기 때문에
`claude update`는 그대로 쓸 수 있습니다.

하지만 중요한 건 늘 가장 새 버전을 쓰는 것이 아니라,
**내 작업에 맞는 채널**을 고르는 것이겠죠.

---

## 4. 마무리

오늘은 클로드 코드 업데이트 방법을
버전 확인, 설치 방식별 명령, 재시작 후 재확인의 3단계로 알아보았습니다.
`claude --version`으로 확인하고 `claude update`로 올린다는 두 가지만
기억하셔도 시작은 충분합니다.

설치 방식만 알면 업데이트는 한 줄이면 끝나는 일이죠!
작은 확인 습관 하나가 낯선 오류를 줄여 주기를 바랍니다.

여러분은 어떤 방식으로 설치하셨나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 업데이트 3단계 요약: 버전 확인, 명령 실행, 재시작 후 재확인]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드업데이트 #클로드코드업데이트방법 #claudeupdate #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "빨간 Auto-update failed 문구를 처음 봤을 때 어디부터 손댈지 몰랐다 / 작업은 계속할 수 있다": https://code.claude.com/docs/en/troubleshoot-install.md (Auto-update failed 항목) , https://aident.ai/blog/fix-claude-code-auto-update-failed
- Step 2 "Homebrew·WinGet은 자동 업데이트가 안 되는데 모르고 지내는 분이 많다": https://code.claude.com/docs/en/setup (Update Claude Code 항목) , https://wmedia.es/en/tips/claude-code-how-to-update , https://inventivehq.com/knowledge-base/claude/how-to-update-claude-code
- Step 2 "npm 권한 오류에 sudo부터 붙이면 더 꼬인다": https://code.claude.com/docs/en/setup (npm 항목: sudo 사용 금지) , https://www.morphllm.com/npm-install-claude-code , https://claudepro.directory/guides/troubleshooting/fix-installation-errors
- 참고(경험 아님): `claude update`가 stable 채널을 보고 "최신"이라 답하는 이슈 https://github.com/anthropics/claude-code/issues/69319 (글에는 쓰지 않음)
- 모든 명령·채널 설명은 https://code.claude.com/docs/en/setup 을 2026-11-05에 확인한 내용
-->
