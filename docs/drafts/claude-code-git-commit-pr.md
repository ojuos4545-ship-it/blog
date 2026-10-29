# 클로드 코드 깃 커밋·PR 맡기기 3단계

> 💡 **한 줄 요약:** 브랜치를 먼저 만들고, 말로 커밋과 PR을 부탁한 뒤,
> 권한과 서명 줄만 설정하면 깃 작업을 맡길 수 있습니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 깃 커밋·PR 맡기기 3단계 대표 이미지]

"커밋 메시지 쓰는 것도, PR 설명 채우는 것도 귀찮아요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 깃 커밋**과 PR은
새 브랜치에서 "커밋해줘", "PR 만들어줘"라고 말로 부탁하면 됩니다.

클로드 코드는 대화를 시작할 때 현재 브랜치,
아직 커밋하지 않은 변경, 최근 커밋 기록을 함께 봅니다.
그래서 따로 설명하지 않아도 무엇이 바뀌었는지 알고 메시지를 써 주죠.
오늘 이 글 하나만 끝까지 읽으시면 커밋부터 PR, 권한 설정까지
혼자 맡겨 보실 수 있습니다.
명령어와 설정은 [Claude Code 공식 문서](https://code.claude.com/docs/en/common-workflows)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 깃 저장소 폴더, 클로드 코드, GitHub CLI(`gh`)
* **소요 시간:** `gh` 로그인까지 마쳤다면 금방 끝납니다
* **난이도:** 초급, 커밋을 한 번이라도 해 봤다면 충분합니다

PR까지 맡기려면 `gh`가 설치되어 있고 로그인되어 있어야 합니다.
공식 문서도 `gh`가 설치되고 로그인된 상태라면
따로 설명하지 않아도 클로드가 PR을 열고 리뷰 댓글을 읽는다고 안내합니다.
로그인은 `gh auth login`, 확인은 `gh auth status`로 합니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 깃 커밋부터 PR까지 브랜치, 커밋, 푸시, PR 4단계 흐름]

---

## Step 1. 클로드 코드 깃 커밋은 어떻게 맡길까?

처음 맡길 때 가장 많이 실수하는 부분은 바로 브랜치입니다.
클로드 코드는 지금 체크아웃된 브랜치에 그대로 커밋하기 때문에,
main에서 시작하면 커밋도 main에 쌓입니다.
저도 처음엔 main에서 바로 시작했다가
커밋을 새 브랜치로 다시 옮기느라 애먹었어요.

아래 순서대로 차근차근 따라와 주세요.

1. 작업할 프로젝트 폴더에서 클로드 코드를 실행합니다.
2. 새 브랜치를 만들어 달라고 먼저 부탁합니다.
3. 작업이 끝나면 바뀐 내용을 보여 달라고 합니다.
4. 내용을 확인한 뒤 커밋을 부탁합니다.

말은 아래처럼 하면 됩니다.
커밋할 파일을 직접 정해 주면 상관없는 파일이
함께 들어가는 일을 줄일 수 있습니다.

```
새 브랜치를 만들고, 바뀐 파일을 보여준 다음 로그인 수정 내용만 커밋해줘
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 깃 커밋을 맡기는 순서: 브랜치, 변경 확인, 커밋]

> 📌 **전문가 Tip:** 브랜치 규칙은 `CLAUDE.md`에 적어 두세요.
> "main에 직접 커밋하지 말고 새 브랜치에서 작업한다"처럼
> 한 줄만 적어 둬도 매번 말하지 않아도 됩니다.
> 원격 저장소의 main 브랜치 보호까지 켜 두면 더 안전합니다.

---

## Step 2. PR은 어떻게 만들까?

기본이 끝났다면 이제 PR을 열어 볼 차례입니다.
공식 문서도 "PR 만들어줘"처럼 바로 부탁하거나,
변경 요약부터 차근차근 시키는 두 가지 방법을 안내합니다.
이때 클로드는 `gh pr create` 명령으로 PR을 만듭니다.
PR은 원격에 올라간 브랜치로 만들기 때문에 푸시도 함께 진행됩니다.

1. 지금까지 바뀐 내용을 요약해 달라고 합니다.
2. PR을 만들어 달라고 부탁합니다.
3. PR 설명에 더 넣을 내용이 있으면 다듬어 달라고 합니다.

```
지금까지 바꾼 내용을 요약해서 PR 만들어줘. 테스트 방법도 설명에 넣어줘
```

[IMAGE: 포인트카드 | 설명: 클로드 코드로 PR을 만드는 3단계와 요청 문장 예시]

이 단계에서 `gh`가 없거나 로그인이 안 되어 있어서
PR이 안 만들어지는 분이 꽤 많더라고요.
이럴 땐 터미널에서 `gh auth status`부터 확인해 보세요.
로그인이 풀려 있다면 `gh auth login`으로 다시 로그인하면 됩니다.

PR을 올리기 전에는 한 번 더 살펴보는 습관이 좋습니다.
공식 문서도 만들어진 PR을 제출 전에 검토하고,
놓친 위험은 없는지 클로드에게 짚어 달라고 하라고 권합니다.
나중에 그 PR 작업으로 돌아가고 싶다면
`claude --from-pr <PR 번호>`로 연결된 세션을 찾을 수 있습니다.

---

## Step 3. 권한과 서명 줄은 어떻게 정할까?

깃 작업을 맡기다 보면 두 가지가 신경 쓰이실 텐데요.
하나는 클로드가 어디까지 묻지 않고 실행해도 되는지,
다른 하나는 커밋에 자동으로 붙는 서명 줄입니다.

먼저 권한입니다. `.claude/settings.json`에 아래처럼 적으면
커밋은 묻지 않고 실행하고, 푸시는 막을 수 있습니다.

```json
{
  "permissions": {
    "allow": ["Bash(git commit *)"],
    "deny": ["Bash(git push *)"]
  }
}
```

다만 `git -C . push`처럼 다르게 쓴 명령은 이 규칙에 걸리지 않으니,
푸시는 원격 저장소의 브랜치 보호와 함께 막는 편이 확실합니다.
푸시를 막아 두면 PR을 열기 전에 푸시는 직접 하셔야 합니다.

다음은 서명 줄입니다.
클로드 코드가 만든 커밋 끝에는 기본으로
`Co-Authored-By: <모델 이름> <noreply@anthropic.com>` 줄이 붙고,
PR 설명에는 `Generated with Claude Code` 문구가 들어갑니다.
커밋 기록에서 이 줄을 처음 보고 어디서 붙었는지
한참 찾았다는 이야기가 꽤 자주 보이더라고요.

| 설정 | 하는 일 | 비고 |
| :--- | :--- | :--- |
| **attribution.commit** | 커밋 서명 줄 변경 | 빈 문자열이면 숨김 |
| **attribution.pr** | PR 설명 문구 변경 | 빈 문자열이면 숨김 |
| **attribution: false** | 모든 서명 숨김 | v2.1.281 이상 |
| **includeCoAuthoredBy** | 예전 설정 | v2.0.62부터 사용 중단 |

[IMAGE: 비교표 | 설명: 클로드 코드 커밋 서명 줄 설정 attribution 항목별 비교]

서명 줄을 그대로 둘지 숨길지는 장단점이 있습니다.

| 선택 | 장점 👍 | 단점 👎 |
| :--- | :--- | :--- |
| **그대로 두기** | AI가 함께 쓴 기록이 남음 | 팀 규칙과 다를 수 있음 |
| **숨기기** | 기존 커밋 형식을 유지함 | AI 사용 여부가 안 보임 |

하지만 중요한 건 서명 줄보다 **내가 내용을 확인했는지**이겠죠.
누가 썼든 커밋과 PR의 책임은 결국 올린 사람에게 있으니,
맡기더라도 변경 내용은 꼭 직접 훑어보세요.

---

## 4. 마무리

오늘은 클로드 코드 깃 커밋과 PR을 맡기는 방법을
브랜치와 커밋, PR 만들기, 권한과 서명 설정의 3단계로 알아보았습니다.
"새 브랜치에서 커밋해줘", "PR 만들어줘" 두 문장만
기억하셔도 시작은 충분합니다.

처음에는 작은 수정 하나로 연습해 보세요.
손이 덜 가는 만큼 확인하는 눈은 더 밝아지는 법이죠!

여러분은 커밋 메시지를 어떤 형식으로 쓰고 계신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 깃 커밋·PR 3단계 요약과 다음 글 VS Code 사용법 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드깃커밋 #클로드코드PR #깃커밋 #풀리퀘스트 #GitHubCLI #AI코딩도구`

<!-- 공식 출처 (2026-10-29 확인)
- PR 만들기 흐름, claude --from-pr, PR 검토 팁: https://code.claude.com/docs/en/common-workflows
- 클로드가 보는 깃 상태(현재 브랜치, 미커밋 변경, 최근 커밋), 서명 줄 출처: https://code.claude.com/docs/en/how-claude-code-works
- gh 설치·로그인 시 PR 열기와 리뷰 댓글 읽기: https://code.claude.com/docs/en/best-practices
- attribution, attribution.commit/pr 기본값, false는 v2.1.281 이상, includeCoAuthoredBy는 v2.0.62부터 사용 중단: https://code.claude.com/docs/en/settings-reference
- Bash(git commit *) 허용, Bash(git push *) 차단, git -C . push 미매칭: https://code.claude.com/docs/en/permissions
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "main에서 바로 시작했다가 커밋을 새 브랜치로 옮기느라 애먹었다": https://angelo-lima.fr/en/claude-code-git-workflows/ , https://developertoolkit.ai/en/claude-code/quick-start/version-control/ , https://claudeissues.com/issue/48474-claude-repeatedly-commits-and-pushes-directly-to-main-despite-explicit-instructi
- Step 2 "gh가 없거나 로그인이 안 돼 PR이 안 만들어지는 분이 많다": https://smartscope.blog/en/generative-ai/claude/claude-code-web-advanced-guide/ , https://claudecodeguides.com/claude-code-crash-course-github/ , https://blink.new/blog/claude-code-with-github
- Step 3 "Co-Authored-By 줄을 처음 보고 어디서 붙었는지 찾았다는 이야기가 자주 보인다": https://velvetshark.com/til/claude-code-github-co-author , https://deku.posstree.com/en/generative_ai/claude-code-attribution/ , https://claudeissues.com/issue/33830-bug-co-authored-by-attribution-should-not-be-default-behavior-for-git-commits
-->
