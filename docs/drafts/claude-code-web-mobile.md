# 클로드 코드 웹·모바일 사용법 3단계

> 💡 **한 줄 요약:** 클로드 코드 웹·모바일 사용법은 깃허브 연결,
> 작업 맡기고 검토하기, 휴대폰으로 이어 보기의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 웹·모바일 사용법 3단계 대표 이미지]

"컴퓨터 앞에 없을 때도 클로드 코드에 일을 맡길 수 없을까요?"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 웹·모바일 사용법**은
claude.ai/code에서 깃허브를 연결하고, 저장소를 골라 일을 맡긴 뒤,
휴대폰의 Claude 앱으로 결과를 확인하는 것까지가 전부입니다.

클로드 코드 웹은 내 컴퓨터가 아니라 클라우드의 가상 컴퓨터에서
클로드 코드를 돌리는 방식입니다.
그래서 노트북을 닫아도 작업이 계속 이어지고,
휴대폰에서 진행 상황을 보며 방향을 바꿔 줄 수도 있죠.
요금제와 버튼 이름은 [Claude Code 공식 문서](https://code.claude.com/docs/en/web-quickstart)를
2026년 10월 29일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 유료 Claude 요금제, 깃허브 계정과 저장소
* **휴대폰:** iOS 또는 안드로이드용 Claude 앱
* **난이도:** 초급, 깃허브 저장소가 하나 있으면 충분합니다

요금제는 Pro, Max, Team이면 되고,
Enterprise는 클로드 코드가 포함된 좌석이어야 합니다.
클라우드 컴퓨터 비용은 따로 받지 않고,
평소 쓰는 사용량 한도에 함께 계산됩니다.

웹 세션이 움직이는 순서를 먼저 알아 두면 덜 헷갈립니다.
저장소를 클라우드에 복제하고, 클로드가 작업한 뒤,
새 브랜치로 깃허브에 올리면 내가 검토하는 흐름이죠.

[IMAGE: 다이어그램 | 설명: 클로드 코드 웹 세션이 저장소 복제부터 작업, 브랜치 푸시, 검토까지 진행되는 흐름]

---

## Step 1. 클로드 코드 웹은 어떻게 시작할까?

처음 한 번만 깃허브를 연결하면 그다음부터는 바로 쓸 수 있습니다.
아래 순서대로 차근차근 따라와 주세요.

1. 브라우저에서 claude.ai/code에 접속해 로그인합니다.
2. 깃허브 연결 안내가 뜨면 승인하고 돌아옵니다.
3. 비공개 저장소를 쓰려면 Claude GitHub 앱을 설치합니다.
4. 기본 환경(Default)이 만들어지면 준비가 끝납니다.

(이때 주의할 점은 3번입니다.
깃허브 로그인만으로는 공개 저장소만 다룰 수 있고,
비공개 저장소는 앱을 설치해야 목록에 나타납니다.)

저도 처음엔 앱 설치를 건너뛰었다가
제 비공개 저장소가 목록에 안 보여서 연결이 잘못된 줄 알았어요.
이 부분에서 막히는 분이 꽤 많더라고요.

앱을 설치할 때 저장소를 골라서 허용했다면
쓰려는 저장소가 허용 목록에 들어 있는지도 확인해 보세요.
깃허브 조직의 저장소라면 조직 소유자의 승인이 필요할 수 있습니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 웹 시작 3단계: 접속, 깃허브 연결, GitHub 앱 설치]

### 패키지 설치가 막힐 때는 어떻게 할까?

클라우드 세션이 어디까지 접속할 수 있는지는
환경의 네트워크 접근 수준이 정합니다.
기본값인 Trusted는 npm, PyPI 같은 주요 패키지 저장소와
깃허브처럼 허용 목록에 있는 곳만 열어 둡니다.

| 수준 | 접속할 수 있는 곳 |
| :--- | :--- |
| **None** | 외부 접속 없음 |
| **Trusted** (기본값) | 패키지 저장소, 깃허브 등 허용 목록 |
| **Full** | 모든 도메인 |
| **Custom** | 내가 정한 허용 목록 |

회사 내부 저장소나 별도 패키지 저장소에서 내려받으려다
접속이 막혔다는 분이 많더라고요.
이럴 때는 환경 설정에서 Custom을 고르고,
**Allowed domains** 칸에 필요한 도메인을 한 줄에 하나씩 적으면 됩니다.

> 📌 **전문가 Tip:** 환경은 입력창 아래 환경 선택 메뉴에서 고칩니다.
> 환경 이름 오른쪽의 설정 아이콘을 누르면
> 네트워크, 환경 변수, 설정 스크립트를 한곳에서 바꿀 수 있습니다.

---

## Step 2. 작업은 어떻게 맡기고 검토할까?

기본이 끝났다면 이제 실제로 일을 맡겨 볼 차례입니다.
입력창 아래에서 저장소와 브랜치를 고르고,
권한 모드를 정한 뒤 할 일을 적어 보내면 되죠.

클라우드 세션의 권한 모드는 세 가지입니다.
바로 고치고 브랜치까지 올리는 Accept edits,
계획을 먼저 보여 주는 Plan, 판별기가 대신 검토하는 Auto인데요.
처음이라면 Plan으로 계획부터 받아 보시길 권합니다.

```
README에 설치 방법 섹션을 추가하고, 명령어는 코드 블록으로 정리해줘
```

요청은 "테스트 고쳐줘"보다 파일 이름과 원하는 결과를 함께 적을수록 좋습니다.
오류 메시지가 있다면 그대로 붙여 넣는 것도 방법이죠.

### 내가 고친 코드가 세션에 없다면?

클라우드 세션은 내 컴퓨터가 아니라 깃허브에서 저장소를 가져옵니다.
그래서 내 컴퓨터에만 있는 커밋은 세션에 들어가지 않습니다.

저도 노트북에서 커밋만 해 두고 푸시를 잊은 채 세션을 열었다가,
방금 고친 내용이 없어서 당황했어요.
세션을 열기 전에 `git push`부터 해 두는 습관을 들이면 됩니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 웹에서 저장소를 고르고 권한 모드를 정해 작업을 맡기는 순서]

### 결과는 어디서 확인하고 PR로 올릴까?

클로드가 작업을 마치면 새 브랜치를 깃허브에 올립니다.
대화창 옆의 **Changes** 카드에 추가·삭제된 줄 수가 뜨고,
그 숫자를 누르면 바뀐 내용을 한눈에 볼 수 있습니다.

1. **Changes** 카드의 줄 수를 눌러 변경 화면을 엽니다.
2. 고칠 줄 옆의 `+`를 눌러 의견을 남깁니다.
3. 다음 메시지를 보내면 의견이 함께 전달됩니다.
4. 마음에 들면 **Create PR**을 눌러 PR을 만듭니다.

초안 PR로 올리고 싶다면 **Create PR**을 오른쪽 클릭해
**Create draft PR**로 바꾼 뒤 누르면 됩니다.
PR을 만든 뒤에도 세션은 그대로 살아 있어서,
리뷰 의견을 붙여 넣고 이어서 고쳐 달라고 할 수 있죠.

---

## Step 3. 휴대폰에서는 어떻게 이어 갈까?

휴대폰용 클로드 코드 앱이 따로 있는 것은 아닙니다.
같은 계정으로 Claude 앱에 로그인한 뒤 **Code** 탭을 누르면
웹에서 연 세션이 그대로 보입니다.

휴대폰에서도 세션을 새로 열거나, 진행 중인 세션에서
클로드의 질문에 답하고 방향을 바꿔 줄 수 있습니다.
"이 PR 지켜보다가 CI가 실패하면 고쳐줘"처럼 말하면
PR을 대신 지켜보게 할 수도 있는데요,
이 기능은 저장소에 Claude GitHub 앱이 설치되어 있어야 합니다.

내 컴퓨터에서 돌아가는 세션을 휴대폰으로 이어 보는 길도 있습니다.
터미널에서 `claude remote-control`로 시작하거나,
열려 있는 세션에서 `/remote-control`을 입력하면 되죠.

| 방식 | 장점 👍 | 주의할 점 👎 |
| :--- | :--- | :--- |
| **클라우드 세션** | 노트북을 꺼도 계속 진행 | 깃허브 저장소가 필요함 |
| **원격 제어** | 내 컴퓨터의 설정과 도구를 그대로 씀 | 컴퓨터를 켜 둬야 함 |

[IMAGE: 비교표 | 설명: 클로드 코드 모바일에서 쓰는 클라우드 세션과 원격 제어의 장점과 주의점 비교]

휴대폰에서는 `/plugin`, `/resume`처럼
터미널 화면에서만 동작하는 명령은 쓸 수 없습니다.
웹에서 하던 세션을 다시 내 컴퓨터로 가져오고 싶다면
저장소 폴더에서 `claude --teleport`를 실행하면 됩니다.

(이때 주의할 점은 작업 폴더에 커밋하지 않은 변경이 없어야 하고,
웹 세션과 같은 계정으로 로그인되어 있어야 한다는 것입니다.)

하지만 중요한 건 어디서 맡기느냐가 아니라
**올라온 변경 내용을 내 눈으로 확인하는 습관**이겠죠.
브라우저 탭을 닫아도 세션은 멈추지 않으니,
돌아와서 **Changes** 화면부터 꼼꼼히 살펴보세요.

---

## 4. 마무리

오늘은 클로드 코드 웹·모바일 사용법을
깃허브 연결, 작업 맡기고 검토하기, 휴대폰으로 이어 보기의
3단계로 알아보았습니다.
비공개 저장소가 안 보이면 GitHub 앱부터, 내 수정이 안 보이면
푸시부터 확인하시면 됩니다.

자리를 비운 사이에도 일이 진행되면 하루가 한결 가벼워지기 마련이죠!
다음 글에서는 클로드 코드로 낯선 코드를
빠르게 파악하는 방법을 정리해 보겠습니다.

여러분은 휴대폰으로 어떤 작업부터 맡겨 보고 싶으신가요?
막히는 부분이 있다면 편하게 댓글로 알려주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 웹·모바일 사용법 3단계 요약과 다음 글 낯선 코드 파악하기 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드웹 #클로드코드모바일 #클라우드세션 #클로드코드사용법 #AI코딩도구 #바이브코딩`

<!-- 메인 키워드: 클로드 코드 웹·모바일 사용법
검색 의도: 컴퓨터 앞이 아니어도 브라우저나 휴대폰으로 클로드 코드에 일을 맡기고 싶은 사람이, 깃허브 연결부터 작업 맡기기, 결과 확인과 휴대폰 사용법까지 알고 싶다. -->

<!-- 공식 출처 (2026-10-29 확인)
- 요금제(Pro, Max, Team, Enterprise 프리미엄·Chat + Claude Code 좌석), 별도 VM 요금 없음·사용량 한도 공유, 깃허브 연결 순서, 비공개 저장소는 GitHub 앱 설치 필요, 조직 소유자 승인, Default 환경(Trusted), 권한 모드 Auto/Accept edits/Plan(Manual·Bypass 없음), 구체적 요청 팁, Changes 카드, + 줄 의견, Create PR / Create draft PR(오른쪽 클릭), PR 후 세션 유지, 탭을 닫아도 세션 계속: https://code.claude.com/docs/en/web-quickstart
- 로컬 커밋은 푸시해야 세션에 반영(--cloud는 원격을 복제), teleport 조건(깨끗한 git 상태, 같은 저장소, 브랜치 푸시, 같은 계정), auto-fix(GitHub 앱 필요, 모바일에서 말로 요청): https://code.claude.com/docs/en/claude-code-on-the-web
- 네트워크 접근 수준 None/Trusted/Full/Custom, Allowed domains, 환경 선택 메뉴의 설정 아이콘: https://code.claude.com/docs/en/cloud-environments
- 모바일 Code 탭, 별도 앱 없음, 같은 계정 로그인, 원격 제어(claude remote-control, /remote-control), 컴퓨터를 켜 둬야 함, /plugin·/resume 불가: https://code.claude.com/docs/en/mobile
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "앱 설치를 건너뛰었다가 비공개 저장소가 목록에 안 보였다 / 막히는 분이 많다": https://code.claude.com/docs/en/web-quickstart (No repositories appear after connecting GitHub, Skip 버튼) , https://claudeissues.com/issue/27155-bug-github-repos-not-visible-in-claude-web-despite-app-installed , https://claudeissues.com/issue/58296-bug-github-repos-not-visible-in-claude-code-web-picker-despite-github-app-instal , https://claudeissues.com/issue/60637-bug-personal-repos-not-visible-in-claude-code-web-picker-despite-github-app-inst
- Step 1 "별도 패키지 저장소에서 내려받으려다 접속이 막혔다는 분이 많다": https://claudeissues.com/issue/54897-bug-claude-code-on-the-web-session-blocks-registry-tiptap-dev-private-npm-regist , https://claudeissues.com/issue/28385-feature-add-npm-cloudsmith-io-to-allowed-egress-hosts-for-claude-code-web , https://claudeissues.com/issue/19512-bug-claude-code-web-default-environment-prevents-fetching-of-github-release-arti
- Step 2 "커밋만 하고 푸시를 잊은 채 세션을 열었다가 고친 내용이 없었다": https://code.claude.com/docs/en/claude-code-on-the-web (push first if you have local commits) , https://clauderemotecontrol.com/claude-code-on-the-web/ , https://www.memorylake.ai/en/blogs/claude-code-cloud-sessions-local-setup
-->
