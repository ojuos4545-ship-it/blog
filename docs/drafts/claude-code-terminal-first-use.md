# 클로드 코드 터미널 처음 쓰는 법 4단계

> 💡 **한 줄 요약:** 클로드 코드 터미널 처음 쓰는 법은
> 열기, 설치, 로그인, 첫 질문의 4단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 터미널 처음 쓰는 법 4단계 대표 이미지]

"터미널이라는 검은 창부터 겁이 나요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 터미널 처음 쓰는 법**은
창을 열고 설치 명령 한 줄을 붙여 넣은 뒤,
`claude`를 입력해 로그인하는 것이 전부입니다.

오늘 이 글 하나만 끝까지 읽으시면 설치부터 첫 질문까지
혼자 하실 수 있습니다.
명령어와 조작법은 [Claude Code 공식 터미널 가이드](https://code.claude.com/docs/en/terminal-guide)를
2026년 11월 5일에 확인해 정리했습니다.

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 컴퓨터, 클로드 구독 또는 Console 계정
* **소요 시간:** 설치까지 금방 끝납니다
* **난이도:** 입문, 터미널을 처음 열어 봐도 충분합니다

클로드 코드는 명령어를 외우는 도구가 아니라
말로 부탁하는 도구입니다.
전체 흐름은 아래 그림으로 먼저 훑어보세요.

[IMAGE: 다이어그램 | 설명: 클로드 코드 터미널 시작 순서 열기, 설치, 로그인, 질문]

---

## Step 1. 터미널은 어떻게 열까?

터미널은 글자로 컴퓨터에 일을 시키는 창입니다.
마우스로 누르는 대신 키보드로 입력한다는 점만 다르죠.
아래 순서대로 차근차근 따라와 주세요.

* **맥:** `Cmd + Space`, `Terminal` 입력 후 Enter
* **리눅스:** `Ctrl + Alt + T`
* **윈도우:** `Win + X`, Windows PowerShell 선택

윈도우에서는 한 가지만 조심하세요.
PowerShell과 CMD는 비슷해 보여도 쓰는 명령이 다릅니다.
줄 맨 앞에 `PS`가 보이면 PowerShell이니 제대로 열린 겁니다.

[IMAGE: 비교표 | 설명: 클로드 코드 터미널 열기와 붙여넣기 방법을 맥과 윈도우로 비교]

> 📌 **전문가 Tip:** 윈도우에서 `irm`이 인식되지 않는다는 메시지가 나오면
> CMD에 들어와 있다는 뜻입니다.
> 창을 닫고 PowerShell로 다시 여세요.

---

## Step 2. 클로드 코드는 어떻게 설치할까?

설치는 명령 한 줄을 붙여 넣으면 끝납니다.
맥과 리눅스는 아래 첫 줄을, 윈도우 PowerShell은
둘째 줄을 복사해 붙여 넣고 Enter를 누르세요.
(붙여넣기는 맥 `Cmd + V`, 리눅스 `Ctrl + Shift + V`,
윈도우 `Ctrl + V`입니다.)

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

```powershell
irm https://claude.ai/install.ps1 | iex
```

설치 중에는 화면에 진행 표시가 나오지 않으니
창을 닫지 말고 기다려 주세요.
끝나면 `Claude Code successfully installed!`라는 문구가 보입니다.
이제 새 터미널 창을 열고 아래 명령으로 확인합니다.

```bash
claude --version
```

버전 번호가 나오면 설치 성공입니다.
저도 설치 직후 같은 창에서 바로 `claude`를 입력했다가
`command not found`가 떠서 당황했어요.
이 부분에서 막히는 분이 꽤 많더라고요.

원인은 설치된 폴더가 PATH(컴퓨터가 명령어를 찾아보는 폴더 목록)에
들어 있지 않아서입니다.
새 터미널 창을 열어도 같다면 맥(zsh) 기준으로 아래 두 줄을 실행하세요.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 설치 후 command not found가 뜰 때 확인할 순서]

> 📌 **전문가 Tip:** `syntax error near unexpected token '<'`가 나오면
> 같은 명령을 한 번 더 실행해 보세요.
> 계속된다면 Homebrew를 쓰는 분은 `brew install --cask claude-code`로
> 설치할 수도 있습니다.

---

## Step 3. 클로드 코드 첫 실행과 로그인은 어떻게 할까?

기본이 끝났다면 이제 실행할 차례입니다.
클로드 코드는 지금 열어 둔 폴더를 기준으로 일하기 때문에
작업할 폴더로 먼저 이동하는 것이 좋습니다.

1. `cd` 명령으로 작업할 폴더로 이동합니다.
2. `claude`를 입력하고 Enter를 누릅니다.
3. 브라우저가 열리면 클로드 계정으로 로그인합니다.
   (이때 주의할 점은 아래에서 설명합니다.)

```bash
cd <작업할 폴더 경로>
claude
```

로그인 단계에서는 계정 종류에서 막히는 경우가 많더라고요.
공식 문서가 안내하는 계정은 Claude 구독(Pro, Max 등)이나
Console 계정이라, 무료 계정만으로는 시작이 어려울 수 있습니다.
브라우저가 자동으로 열리지 않을 때는 `c` 키를 눌러
로그인 주소를 복사한 뒤 브라우저에 붙여 넣으면 됩니다.

한 번 로그인하면 다음부터는 다시 하지 않아도 됩니다.
계정을 바꾸고 싶을 때만 클로드 코드 안에서 `/login`을 입력하세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 첫 실행 순서 폴더 이동, claude 입력, 로그인]

---

## Step 4. 첫 질문과 기본 조작은 어떻게 할까?

로그인이 끝나면 입력창이 나타납니다.
여기에 말하듯 적고 Enter를 누르면 됩니다.
처음에는 파일을 건드리지 않는 질문으로 시작해 보세요.

```
이 폴더에 어떤 파일이 있는지 알려주고 무슨 프로젝트인지 설명해줘
```

폴더가 비어 있어도 괜찮습니다.
"웹페이지 하나 만들어줘"처럼 부탁하면 파일을 만들어 줍니다.
파일을 만들거나 바꾸기 전에 허락을 묻는 화면이 뜨는데요.
이때 Enter를 누르면 **Yes**가 선택됩니다.

저도 처음엔 화면을 마우스로 눌러 보다가 반응이 없어서 한참 헤맸어요.
터미널에서는 클릭이 되지 않고 방향키로 움직입니다.
이 점을 몰라서 멈칫하는 분이 많더라고요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 터미널에서 쓰는 Esc, /help, exit 기본 조작]

터미널에서 시작하는 명령은 아래 세 가지만 알아도 충분합니다.

| 명령 | 하는 일 |
| :--- | :--- |
| `claude` | 새 대화 시작 |
| `claude -c` | 가장 최근 대화 이어가기 |
| `claude -r` | 이전 대화 골라서 다시 열기 |

허락을 묻는 방식은 `Shift + Tab`으로 바꿀 수 있습니다.
하지만 중요한 건 방식을 바꾸는 것이 아니라
**처음에는 화면에 뜨는 내용을 읽고 허락하는 습관**이겠죠.

---

## 5. 마무리

오늘은 클로드 코드 터미널 처음 쓰는 법을
열기, 설치, 로그인, 첫 질문의 4단계로 알아보았습니다.
막히면 새 터미널, `claude --version`, PATH 순서로
확인하시면 대부분 풀립니다.

처음 한 번만 넘기면 그다음은 말로 부탁하면 됩니다.
작은 첫 질문 하나가 익숙함을 만들어 주는 법이죠!

여러분은 클로드 코드로 가장 먼저 무엇을 시켜 보고 싶으신가요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 터미널 처음 쓰는 법 요약: 확인, 실행, 도움말]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드설치 #클로드코드터미널 #터미널처음쓰기 #AI코딩도구 #AI에이전트`

<!-- 경험 문장 근거 (style-guide 10장)
- Step 2 "설치 직후 command not found에 당황 / 막히는 분이 많다": https://code.claude.com/docs/en/terminal-guide.md , https://www.gpters.org/news/post/claude-code-command-not-found-fix-KcgtD1R3tKw4wim , https://inventivehq.com/knowledge-base/claude/zsh-command-not-found-claude
- Step 3 "로그인 단계에서 계정 종류로 막히는 경우가 많다": https://code.claude.com/docs/en/quickstart.md , https://www.gpters.org/news/post/claude-code-command-not-found-fix-KcgtD1R3tKw4wim
- Step 4 "마우스로 눌러 보다 헤맨다 / 멈칫하는 분이 많다": https://code.claude.com/docs/en/terminal-guide.md (터미널에서는 클릭이 되지 않고 방향키로 이동)
- 사실 확인(설치 명령, PATH 수정, 로그인 `c` 키, /login, Esc, /help, exit, Shift+Tab, claude -c/-r, PowerShell 구분): https://code.claude.com/docs/en/terminal-guide.md , https://code.claude.com/docs/en/quickstart.md , https://code.claude.com/docs/en/authentication.md (2026-11-05 확인)
-->
