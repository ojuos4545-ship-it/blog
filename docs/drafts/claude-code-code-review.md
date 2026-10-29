# 클로드 코드 코드 리뷰 받는 법 3단계

> 💡 **한 줄 요약:** 클로드 코드 코드 리뷰는 `/code-review`로
> 내 변경을 검토받고, 지적을 골라 고친 뒤,
> PR에서 한 번 더 확인받는 3단계면 충분합니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 코드 리뷰 받는 법 3단계 대표 이미지]

"코드는 다 짰는데 이대로 올려도 될지 불안해요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 코드 리뷰**는
`/code-review` 한 줄로 내 변경 사항을 검토받고,
나온 지적 중 진짜 문제만 골라 고친 뒤,
PR에서 한 번 더 확인받으면 끝납니다.

저도 처음엔 코드를 짠 그 대화에서 바로 "리뷰해줘"라고 했다가
칭찬에 가까운 답만 받고 넘어간 적이 있어요.
방금 짠 코드를 같은 대화에서 검토하면
자기가 내린 판단을 그대로 따라가기 쉽다는 이야기가
여러 곳에서 반복해서 나오더라고요.

오늘 이 글 하나만 끝까지 읽으시면 머지 전에
리뷰를 받고 결과를 다루는 순서를 혼자 익히실 수 있습니다.
명령과 기능은 [Claude Code 공식 문서](https://code.claude.com/docs/en/code-review-local)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 클로드 코드 설치, 변경 사항이 있는 git 저장소
* **PR 단계:** GitHub 저장소 (Step 3에서 사용)
* **난이도:** 초급, 브랜치와 커밋을 알면 충분합니다

`/code-review`는 요금제와 상관없이 쓸 수 있는 명령입니다.
리뷰도 내 세션에서 돌기 때문에
다른 작업과 똑같이 사용량에 포함되는데요.
세 단계의 흐름을 한 장으로 먼저 보고 넘어가겠습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 코드 리뷰를 받는 내 변경 검토, 골라서 고치기, PR 리뷰 3단계 흐름]

---

## Step 1. 내 변경 사항은 어떻게 리뷰받을까?

처음 할 때 가장 많이 하는 실수는
코드를 짠 대화에서 그대로 검토를 부탁하는 것입니다.
`/code-review`는 이 대화를 본 적 없는 새 서브에이전트가
변경 내용을 읽기 때문에, 코드를 만든 이유에 휩쓸리지 않습니다.

아래 순서대로 차근차근 따라와 주세요.

1. 작업한 저장소에서 클로드 코드를 실행합니다.
2. 대화창에 `/code-review`를 입력합니다.
3. 리뷰가 도는 동안 하던 일을 계속합니다. (결과는 끝나면 도착)
4. 도착한 지적을 읽고 고칠 것을 고릅니다. (Step 2)

아무것도 붙이지 않으면 현재 브랜치에서
아직 올리지 않은 커밋과 커밋 전 변경을 함께 봅니다.
다른 곳을 보고 싶다면 명령 뒤에 대상을 적으면 됩니다.

| 리뷰 대상 | 입력 |
| :--- | :--- |
| **현재 브랜치** (기본값) | `/code-review` |
| **브랜치끼리 비교** | `/code-review main...my-feature` |
| **PR 번호** | `/code-review 1234` |
| **폴더나 파일** | `/code-review src/auth` |

[IMAGE: 포인트카드 | 설명: 클로드 코드 Step 1 /code-review로 리뷰 대상을 정하는 방법]

`/review`를 입력해도 같은 리뷰가 실행됩니다.
명령을 외우기 어렵다면 "내 변경 사항 리뷰해줘"처럼
말로 부탁해도 클로드가 이 리뷰를 실행할 수 있죠.

---

## Step 2. 리뷰 지적은 어떻게 골라서 고칠까?

리뷰를 받았다면 이제 지적을 다룰 차례입니다.
저는 지적이 많을수록 좋은 줄 알고 전부 고치게 했다가,
쓸 일 없는 예외 처리와 테스트만 늘어난 적이 있어요.
스타일 지적 사이에 진짜 버그가 묻힌다는 후기도 꽤 많더라고요.

공식 문서도 문제를 찾으라고 하면 리뷰는 늘 뭔가를 찾아낸다며,
지적을 전부 고치면 필요 없는 구조와 테스트가 쌓인다고 경고합니다.
그래서 **동작이 틀리는 지적**부터 고르는 것이 핵심입니다.

```
리뷰 지적 중 실제로 동작이 틀리는 것만 고쳐줘.
스타일 지적은 건너뛰고, 고치지 않은 이유를 한 줄씩 알려줘.
```

지적이 너무 많거나 적다면 명령 뒤에 단계를 붙여 보세요.
`low`는 확신이 큰 지적만 보여 줘서 오탐이 줄고,
`medium`부터 `max`까지는 더 넓게 살핍니다.
상황에 맞는 방법을 표로 정리했습니다.

| 방법 | 하는 일 | 이럴 때 써요 |
| :--- | :--- | :--- |
| **/code-review low** | 확신이 큰 지적만 보여 줌 | 오탐이 많을 때 |
| **/code-review high** | 더 넓게 살펴봄 | 중요한 변경일 때 |
| **--fix** | 리뷰 뒤 지적을 바로 적용 | 고칠 게 분명할 때 |
| **/security-review** | 보안 취약점만 따로 검토 | 로그인·권한 코드일 때 |

[IMAGE: 비교표 | 설명: 클로드 코드 Step 2 리뷰 단계 low, high와 --fix, /security-review 비교]

(이때 주의할 점은 `--fix`를 쓰기 전에 커밋해 두는 것입니다.
백그라운드 리뷰가 고친 파일은 `/rewind`로 다 되돌아가지 않아서,
되돌릴 때는 git을 써야 하기 때문입니다.)

`/security-review`는 내 브랜치와 원격 기본 브랜치의 차이를 보고
인젝션, 인증 문제, 데이터 노출 같은 위험을 찾습니다.
`origin` 원격 저장소가 연결되어 있어야 동작하니 함께 확인해 주세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 Step 2 리뷰 지적을 골라서 고치는 기준]

> 📌 **전문가 Tip:** 팀 규칙은 `CLAUDE.md`에 적어 두세요.
> `/code-review`는 `CLAUDE.md`를 따라 검토하기 때문에
> 매번 같은 기준을 설명하지 않아도 됩니다.

---

## Step 3. PR에서는 코드 리뷰를 어떻게 받을까?

기본이 끝났다면 이제 PR에서 한 번 더 확인받을 차례입니다.
Team이나 Enterprise 요금제라면 관리자가 켜 두는
Code Review 서비스를 쓸 수 있는데요.
여러 에이전트가 함께 버그를 찾고, 검증 단계에서 오탐을 거른 뒤
문제가 있는 줄에 바로 댓글을 남깁니다.

리뷰가 PR을 승인하거나 막지는 않습니다.
머지 여부는 끝까지 팀이 정하는 것이죠.
저장소마다 PR을 열 때, 푸시할 때마다,
요청할 때만 중에서 리뷰가 도는 시점을 고를 수 있습니다.

1. 관리자가 Claude GitHub 앱을 설치하고 저장소를 고릅니다.
2. PR을 열면 정해 둔 시점에 리뷰가 시작됩니다.
3. 바로 받고 싶다면 PR에 `@claude review`를 댓글로 남깁니다.

(이때 댓글은 코드 줄이 아니라 PR 대화창에 새로 달아야 하고,
저장소에 쓰기 권한이 있는 사람이 남겨야 리뷰가 시작됩니다.)
지적에는 아래 세 가지 표시가 붙습니다.

| 표시 | 뜻 | 할 일 |
| :--- | :--- | :--- |
| 🔴 **Important** | 머지 전에 고쳐야 할 버그 | 고치고 다시 푸시 |
| 🟡 **Nit** | 사소한 문제, 머지를 막지 않음 | 골라서 반영 |
| 🟣 **Pre-existing** | 이 PR 전부터 있던 버그 | 따로 기록해 두기 |

[IMAGE: 비교표 | 설명: 클로드 코드 Step 3 PR 리뷰 지적 표시 Important, Nit, Pre-existing 비교]

고칠 필요가 없는 지적은 GitHub에서 스레드를 직접 해결 처리하면 됩니다.
답글만 다는 것으로는 지적이 사라지지 않고,
다음 리뷰가 그 답글을 읽고 판단하는 방식입니다.

리뷰에만 쓸 규칙은 저장소 맨 위의 `REVIEW.md`에 적습니다.
"Nit은 리뷰 한 번에 다섯 개까지만"처럼 쓰면 되는데요,
이 파일은 PR 안의 변경이 아니라 기본 브랜치에서 읽으니 먼저 머지해 두세요.
로컬 `/code-review`는 `REVIEW.md`를 읽지 않으니,
양쪽에 다 쓸 규칙은 `CLAUDE.md`에 두는 편이 좋습니다.

해당 요금제가 아니어도 PR 리뷰는 받을 수 있습니다.
`/code-review 1234 --comment`처럼 실행하면
리뷰 결과가 그 PR에 줄별 댓글로 달립니다.
API 키가 있다면 `/install-github-app`으로
GitHub Actions에 클로드를 붙이는 방법도 있습니다.

---

## 4. 마무리

오늘은 클로드 코드 코드 리뷰를 받는 법을
내 변경 검토, 골라서 고치기, PR에서 한 번 더 확인하기의
3단계로 알아보았습니다.
`/code-review` 한 줄과 "동작이 틀리는 것부터 고친다"는 기준만
기억하셔도 시작은 충분합니다.

리뷰는 코드를 깎아내리는 시간이 아니라
내가 놓친 것을 함께 찾는 시간이기 마련이죠!
다음 글에서는 클로드 코드로 반복 작업을 자동화하는
3단계를 정리해 보겠습니다.

여러분은 리뷰에서 어떤 지적을 가장 자주 받으시나요?
궁금한 점은 언제든 댓글로 편하게 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 코드 리뷰 3단계 요약과 다음 글 반복 작업 자동화 3단계 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드코드리뷰 #코드리뷰 #AI코드리뷰 #클로드코드사용법 #AI코딩도구 #바이브코딩`

<!-- 메인 키워드: 클로드 코드 코드 리뷰
검색 의도: 클로드 코드로 코드를 짠 사람이, 머지 전에 클로드에게 리뷰를 받는 명령과 지적을 다루는 기준, PR에서 리뷰를 받는 방법을 알고 싶다. -->

<!-- 공식 출처 (2026-10-29 확인)
- /code-review 사용법(모든 요금제, 내 세션 사용량에 포함, 백그라운드 서브에이전트로 실행 후 결과 도착, 기본 대상=업스트림보다 앞선 커밋+커밋 전 변경, main...my-feature / 1234 / src/auth 대상 지정, /review는 별칭, low는 확신 큰 지적만·medium~max는 범위 확대, --fix·--comment, --fix 수정은 체크포인트 밖이라 /rewind로 다 안 돌아가니 git 사용, CLAUDE.md는 읽고 REVIEW.md는 안 읽음, 말로 부탁해도 실행): https://code.claude.com/docs/en/code-review-local
- /code-review는 대화를 본 적 없는 새 서브에이전트가 diff를 검토, "리뷰는 늘 뭔가를 찾아내고 전부 고치면 불필요한 추상화·테스트가 쌓인다", skip style: https://code.claude.com/docs/en/best-practices
- /security-review(브랜치와 origin 기본 브랜치 차이, 인젝션·인증·데이터 노출, origin 원격 필요), /install-github-app: https://code.claude.com/docs/en/commands
- Code Review 서비스(Team·Enterprise, Owner가 설정, 여러 에이전트·검증·심각도 순위, 승인·차단하지 않음, 리뷰 시점 설정): https://code.claude.com/docs/en/code-review
- 심각도 Important·Nit·Pre-existing, @claude review(최상위 댓글, 쓰기 권한), 스레드 해결로 지적 해제, 답글은 리뷰를 시작하지 않음: https://code.claude.com/docs/en/code-review-pull-requests
- REVIEW.md(저장소 루트, 기본·베이스 브랜치에서 읽음, Nit 개수 제한 예시), CLAUDE.md와의 차이: https://code.claude.com/docs/en/code-review-customize
-->

<!-- 경험 문장 근거 (style-guide 10장)
- 도입 "코드를 짠 대화에서 바로 리뷰를 부탁했다가 칭찬에 가까운 답만 받음 / 같은 대화에서 검토하면 자기 판단을 따라가기 쉽다": https://levelup.gitconnected.com/claude-ai-said-excellent-work-and-then-my-team-found-3-critical-bugs-3b42ffb47d0e , https://www.besthub.dev/articles/is-changing-session-skill-or-model-the-same-why-claude-code-s-self-review-fails-fcc5917e7c66 , https://www.coddykit.com/courses/claude_architect/session-isolation-for-reviews-9200211 , https://claudeissues.com/issue/81178-model-feedback-fable-5-self-review-blind-spot-in-long-agentic-sessions-with-a-mi
- Step 2 "지적을 전부 고치게 했다가 쓸 일 없는 예외 처리와 테스트만 늘어남 / 스타일 지적 사이에 진짜 버그가 묻힌다": https://code.claude.com/docs/en/best-practices , https://photostructure.com/coding/claude-code-review/ , https://glama.ai/mcp/servers/@kesslerio/attio-mcp-server/blob/bfac8998f1ed13a89cec42088737ba764015f789/.github/docs/claude-review-known-issues.md , https://www.coddykit.com/courses/claude_architect/reducing-false-positives-9203766
-->
