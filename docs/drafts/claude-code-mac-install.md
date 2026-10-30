# 클로드 코드 맥 설치 방법 3단계

> 💡 **한 줄 요약:** 클로드 코드 맥 설치는 터미널 명령 실행,
> 새 창에서 확인, 첫 실행과 로그인의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 맥 설치 방법 3단계 대표 이미지]

"맥북에 깔아 보려는데 터미널부터 낯설어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 맥 설치**는
터미널에 명령 한 줄을 붙여 넣고,
새 창에서 `claude --version`으로 확인한 뒤,
`claude`를 실행해 로그인하면 끝납니다.

Node.js나 Homebrew를 먼저 깔지 않아도 되고,
관리자 비밀번호를 넣을 일도 없습니다.
오늘 이 글 하나만 끝까지 읽으시면 설치부터 첫 대화까지
혼자 해 보실 수 있습니다.
설치 명령과 요구 사항은 [Claude Code 공식 문서](https://code.claude.com/docs/en/setup)를
2026년 10월 30일에 확인해 정리했습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 맥 설치 흐름: 터미널 명령 실행, 새 창에서 확인, 실행과 로그인]

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** macOS 13.0 이상 맥, 유료 Claude 요금제
* **사양:** 메모리 4GB 이상, 인터넷 연결
* **난이도:** 초급, 복사와 붙여넣기만 할 줄 알면 됩니다

macOS 버전은 화면 왼쪽 위 Apple 메뉴의
"이 Mac에 관하여"에서 확인할 수 있습니다.
13.0보다 낮다면 소프트웨어 업데이트부터 해 주세요.
버전이 낮으면 설치 중에 `dyld` 오류가 나는데,
Homebrew로 바꿔 깔아도 같은 파일을 받아서 해결되지 않습니다.

요금제는 Pro, Max, Team, Enterprise나 Console 계정이 필요합니다.
공식 문서에 따르면 무료 요금제에는 클로드 코드가 포함되지 않죠.
인텔 맥과 애플 실리콘(M 시리즈) 맥 모두 같은 명령으로 설치됩니다.

---

## Step 1. 클로드 코드 맥 설치 명령은 어디에 입력할까?

맥에서는 기본으로 들어 있는 **터미널** 앱에 명령을 입력합니다.
처음이라 터미널이 어디 있는지 모르셔도 괜찮아요.
아래 순서대로 차근차근 따라와 주세요.

1. `Cmd + Space`를 눌러 Spotlight 검색을 엽니다.
2. "터미널" 또는 "Terminal"을 입력하고 Enter를 누릅니다.
3. 커서가 깜빡이는 창에 아래 명령을 붙여 넣고 Enter를 누릅니다.

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

내려받는 동안에는 진행 표시가 나오지 않습니다.
(멈춘 것처럼 보여도 창을 닫지 말고 기다려 주세요.)
끝나면 `Claude Code successfully installed!`라는 문구가 나옵니다.

검색하다 보면 Node.js를 깔고 npm으로 설치하라는
예전 글도 많이 보이는데요.
그 방법으로 깔다가 권한 오류(`EACCES`)가 나자
앞에 `sudo`를 붙여 다시 시도하는 분이 많더라고요.
공식 문서는 `sudo npm install -g`를 쓰지 말라고
분명히 적어 두었으니 기본 설치 명령을 쓰는 편이 안전합니다.

Homebrew를 이미 쓰고 계신다면 아래 명령으로 깔아도 됩니다.
`claude-code`는 보통 일주일쯤 늦게 따라오는 안정(stable) 버전이고,
새 버전을 바로 받고 싶다면 `claude-code@latest`를 씁니다.

```bash
brew install --cask claude-code
```

[IMAGE: 비교표 | 설명: 클로드 코드 맥 설치 방식 기본 설치, Homebrew, npm의 장점과 주의점 비교]

| 설치 방식 | 장점 👍 | 주의점 👎 |
| :--- | :--- | :--- |
| **기본 설치(curl)** | 공식 권장, 자동 업데이트 | 진행 표시가 없음 |
| **Homebrew** | brew로 한꺼번에 관리 | 자동 업데이트가 안 됨 |
| **npm** | Node.js 환경에 익숙하면 편함 | Node.js 22 이상, sudo 금지 |

> 📌 **전문가 Tip:** Homebrew에서 `No Cask with this name exists`가 뜨면
> 내 컴퓨터의 목록이 오래된 것입니다.
> `brew update`로 목록을 새로 받은 뒤 설치 명령을 다시 입력하세요.

---

## Step 2. 설치가 잘 됐는지 어떻게 확인할까?

기본 설치가 끝났다면 이제 제대로 깔렸는지 확인해 볼 차례입니다.
여기서 꼭 기억할 점은 **새 터미널 창**을 열어야 한다는 것입니다.
설치에 쓴 창은 예전 경로 정보를 그대로 쥐고 있기 때문이죠.

`Cmd + N`으로 새 창을 열고 아래 명령을 입력해 보세요.
버전 번호가 나오면 설치가 끝난 것입니다.

```bash
claude --version
```

더 꼼꼼히 보고 싶다면 `claude doctor`를 실행하면 됩니다.
대화를 시작하지 않고 설치 상태와 설정 오류,
고칠 방법이 담긴 경고까지 한 번에 보여 줍니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 맥 설치 확인 명령 claude --version과 claude doctor 정리]

### command not found가 뜬다면?

맥에서 가장 많이 막히는 곳이 바로 여기입니다.
저도 설치 완료 문구를 보고 바로 `claude`를 입력했다가
`zsh: command not found: claude`를 보고
설치가 실패한 줄 알았어요.

이 메시지는 설치 실패가 아니라 경로 문제인 경우가 대부분입니다.
설치 프로그램은 `~/.local/bin/claude`에 파일을 두는데,
이 폴더가 PATH(명령을 찾는 폴더 목록)에 빠져 있으면 못 찾습니다.
설치 마지막에 나오는 `Setup notes:` 안내에도 같은 내용이 적혀 있죠.

맥의 기본 셸인 zsh라면 아래 두 줄을 차례로 입력합니다.
첫 줄은 설정을 저장하고, 둘째 줄은 지금 창에 바로 적용합니다.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

입력한 뒤에는 새 창을 열어 `claude --version`을 다시 확인합니다.
`echo $0`으로 셸을 확인했을 때 bash가 나온다면
`~/.zshrc` 대신 `~/.bash_profile`에 같은 줄을 넣어 주세요.

[IMAGE: 포인트카드 | 설명: 클로드 코드 맥 설치 후 command not found 해결: PATH에 ~/.local/bin 추가]

---

## Step 3. 첫 실행과 로그인은 어떻게 할까?

이제 실제로 클로드 코드를 켜 볼 차례입니다.
작업할 프로젝트 폴더로 이동한 다음 `claude`를 입력하면 됩니다.

```bash
cd ~/my-project
claude
```

폴더 경로를 직접 치기 번거롭다면
`cd `까지 입력한 뒤 Finder에서 폴더를 터미널 창으로 끌어다 놓아 보세요.
경로가 자동으로 채워집니다.

처음 실행하면 브라우저 창이 열리면서 로그인을 요청합니다.
평소 쓰는 Claude 계정으로 로그인하고 허용하면
터미널로 돌아와 대화를 시작할 수 있죠.
로그인이 끝나면 말로 부탁해 보세요.

```
이 폴더에 어떤 파일이 있는지 보고 프로젝트 구조를 설명해줘
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 맥 첫 실행 순서: 폴더 이동, claude 입력, 브라우저 로그인]

터미널에서는 마우스로 클릭하지 않고 키보드로 움직입니다.
작업을 멈추고 싶으면 `Esc`, 끝내려면 `exit`를 입력하면 되고,
쓸 수 있는 명령이 궁금하면 `/help`를 입력해 보세요.

하지만 중요한 건 여러 방법을 써 보는 것이 아니라
**설치 방식 하나만** 유지하는 것이겠죠.
Homebrew로 깐 분들이 업데이트 알림을 보고 `brew upgrade`를 했는데
이미 최신이라는 답만 받는 경우가 많더라고요.
Homebrew 안정 버전이 조금 늦게 올라오기 때문인데,
이를 피하려고 다른 방법으로 겹쳐 깔면 엉뚱한 버전이 실행될 수 있습니다.

설치가 겹쳤는지 궁금하다면 `which -a claude`를 입력해 보세요.
경로가 두 개 이상 나오면 하나만 남기고 지우면 됩니다.
공식 문서는 `~/.local/bin/claude`에 깔리는 기본 설치를 권합니다.

---

## 4. 마무리

오늘은 클로드 코드 맥 설치 방법을
명령 실행, 새 창에서 확인, 첫 실행과 로그인의 3단계로 알아보았습니다.
설치 뒤 새 창을 여는 것과 PATH 두 줄,
이 두 가지만 기억하셔도 대부분의 막힘은 피할 수 있습니다.

설치가 끝났다면 작은 폴더 하나에서 먼저 말을 걸어 보세요.
낯선 터미널도 몇 번 열다 보면 금방 손에 익는 법이죠!
다음 글에서는 인텔리제이에서 클로드 코드를 쓰는 방법을
3단계로 정리해 보겠습니다.

설치하다 막힌 메시지가 있다면 그대로 댓글로 남겨 주세요.
함께 원인을 찾아보겠습니다. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 맥 설치 3단계 요약과 다음 글 인텔리제이 사용법 3단계 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드설치 #클로드코드맥 #맥설치 #클로드코드사용법 #AI코딩도구 #바이브코딩`

<!-- 공식 출처 (2026-10-30 확인)
- 시스템 요구 사항(macOS 13.0+, 4GB+ RAM, x64·ARM64, 인터넷 연결), curl 설치 명령, 진행 표시 없음, Homebrew cask 두 종류(claude-code=stable 약 1주 늦음, claude-code@latest), Homebrew 자동 업데이트 안 됨·brew upgrade, npm 방식 Node.js 22 이상·sudo npm install -g 금지, claude --version, claude doctor, 유료 요금제(무료 미포함), 브라우저 로그인, 기본 설치 자동 업데이트: https://code.claude.com/docs/en/setup
- 터미널 여는 법(Cmd + Space, Spotlight, Terminal), "Claude Code successfully installed!", command not found 시 zsh PATH 두 줄, Esc·exit·/help: https://code.claude.com/docs/en/terminal-guide
- ~/.local/bin/claude 위치, Setup notes 안내, zsh: command not found: claude 문구, macOS bash는 ~/.bash_profile, echo $0, which -a claude로 중복 설치 확인·하나만 남기기, Cask 'claude-code' is unavailable → brew update, dyld 오류는 macOS 13 미만·Homebrew로도 해결 안 됨: https://code.claude.com/docs/en/troubleshoot-install
-->

<!-- 경험 문장 근거 (style-guide 10장)
- Step 1 "npm으로 깔다가 권한 오류(EACCES)가 나자 sudo를 붙여 다시 시도하는 분이 많다": https://support.claude.com/en/articles/14552646 , https://www.morphllm.com/claude-code-install , https://inventivehq.com/knowledge-base/claude/how-to-fix-permission-errors , https://horadecodar.com.br/?p=39672
- Step 2 "설치 완료 문구를 보고 바로 claude를 입력했다가 zsh: command not found: claude를 보고 설치가 실패한 줄 알았다": https://code.claude.com/docs/en/troubleshoot-install , https://www.morphllm.com/common-errors/zsh-command-not-found-claude , https://inventivehq.com/knowledge-base/claude/zsh-command-not-found-claude , https://www.digitalmarketer.co.kr/insights/claude-code-install-errors , https://github.com/anthropics/claude-code/issues/471
- Step 3 "Homebrew로 깐 분들이 업데이트 알림을 보고 brew upgrade를 했는데 이미 최신이라는 답만 받는 경우가 많다": https://claudeissues.com/issue/41194-homebrew-claude-update-advertises-version-not-available-in-stable-cask , https://claudeissues.com/issue/49590-misleading-update-available-message-for-homebrew-users , https://claudeissues.com/issue/40464-cli-shows-update-available-when-already-on-latest-homebrew-cask-version
- 참고: gpters.org, inflearn.com은 이 세션 네트워크 제한으로 본문을 직접 열지 못했고 검색 결과 요약으로만 확인했다.
-->
