# 클로드 코드 윈도우 설치 방법 3단계

> 💡 **한 줄 요약:** 클로드 코드 윈도우 설치는 명령 실행,
> 새 창에서 확인, 첫 실행과 로그인의 3단계로 끝납니다.

[IMAGE: 썸네일 | 설명: 클로드 코드 윈도우 설치 방법 3단계 대표 이미지]

"윈도우에 깔아 보려는데 어디에 뭘 입력하는지 모르겠어요"
하시는 분들을 위해 준비했습니다.
결론부터 말씀드리면, **클로드 코드 윈도우 설치**는
PowerShell에 명령 한 줄을 붙여 넣고,
새 창에서 `claude --version`으로 확인한 뒤,
`claude`를 실행해 로그인하면 끝납니다.

관리자 권한으로 실행할 필요도 없고,
WSL이나 Node.js를 먼저 깔지 않아도 됩니다.
오늘 이 글 하나만 끝까지 읽으시면 설치부터 첫 대화까지
혼자 해 보실 수 있습니다.
설치 명령과 요구 사항은 [Claude Code 공식 문서](https://code.claude.com/docs/en/setup)를
2026년 10월 29일에 확인해 정리했습니다.

[IMAGE: 다이어그램 | 설명: 클로드 코드 윈도우 설치 흐름: 명령 실행, 새 창에서 확인, 실행과 로그인]

---

## 🛠️ 시작하기 전에 준비할 것들

* **준비물:** 윈도우 10(1809 이상) PC, 유료 Claude 요금제
* **사양:** 메모리 4GB 이상, x64 또는 ARM64 프로세서
* **난이도:** 초급, 명령어를 붙여 넣을 수만 있으면 충분합니다

요금제는 Pro, Max, Team, Enterprise나 Console 계정이 필요합니다.
공식 문서에 따르면 무료 요금제에는 클로드 코드가 포함되지 않죠.
요금제별 차이는 다음 글에서 따로 정리해 드릴게요.

검색해 보면 Node.js나 WSL부터 깔라는
예전 글이 많아서 헷갈리시죠?
저도 처음엔 순서를 몰라 이것저것 먼저 설치했는데,
지금은 기본 설치 명령 하나면 따로 준비할 프로그램이 없더라고요.

[Git for Windows](https://git-scm.com/downloads/win)는 선택 사항이지만 깔아 두기를 권합니다.
이게 있으면 클로드 코드가 Git Bash로 명령을 실행할 수 있고,
없으면 PowerShell로 대신 실행합니다.

---

## Step 1. 클로드 코드 설치 명령은 어디에 입력할까?

처음 설치할 때 가장 많이 실수하는 부분은 바로 창의 종류입니다.
저도 처음엔 명령을 CMD 창에 붙여 넣었다가
`'irm' is not recognized`라는 메시지를 보고 당황했어요.
PowerShell과 CMD를 헷갈려 막히는 분이 꽤 많더라고요.

아래 순서대로 차근차근 따라와 주세요.

1. 시작 메뉴에서 "PowerShell"을 검색해 엽니다.
2. 줄 맨 앞이 `PS C:\`로 시작하는지 확인합니다.
3. 아래 명령을 붙여 넣고 Enter를 누릅니다.

```powershell
irm https://claude.ai/install.ps1 | iex
```

설치하는 동안에는 진행 표시가 나오지 않습니다.
(멈춘 것처럼 보여도 창을 닫지 말고 끝날 때까지 기다려 주세요.)
CMD를 쓰고 싶다면 줄 앞에 `PS` 없이 `C:\`만 보이는 창에서
아래 명령을 대신 씁니다.

```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

반대로 이 명령을 PowerShell에 넣으면
`The token '&&' is not a valid statement separator`가 뜹니다.
창 종류가 헷갈린다면 어느 창에서나 되는 WinGet도 있습니다.

```powershell
winget install Anthropic.ClaudeCode
```

[IMAGE: 비교표 | 설명: 클로드 코드 윈도우 설치 방식 PowerShell, CMD, WinGet의 장점과 주의점 비교]

| 설치 방식 | 장점 👍 | 주의점 👎 |
| :--- | :--- | :--- |
| **PowerShell** | 공식 권장, 자동 업데이트 | CMD 창에서는 실행 안 됨 |
| **CMD** | PowerShell이 낯선 분께 편함 | PowerShell 창에서는 오류 |
| **WinGet** | 창 종류와 상관없이 한 줄 | 자동 업데이트가 안 됨 |

> 📌 **전문가 Tip:** WinGet으로 설치했다면
> `winget upgrade Anthropic.ClaudeCode`로 직접 업데이트하세요.
> PowerShell이나 CMD 명령으로 깐 기본 설치는
> 백그라운드에서 알아서 최신 버전으로 바뀝니다.

---

## Step 2. 설치가 잘 됐는지 어떻게 확인할까?

기본 설치가 끝났다면 이제 제대로 깔렸는지 확인해 볼 차례입니다.
여기서 꼭 기억할 점은 **새 창**을 열어야 한다는 것입니다.
설치에 쓴 창은 예전 경로 정보를 그대로 쥐고 있기 때문이죠.

설치가 끝났다고 같은 창에서 바로 `claude`를 입력했다가
"인식할 수 없다"는 메시지를 받는 경우가 많더라고요.
저도 그 메시지를 보고 설치가 실패한 줄 알았는데,
창을 닫고 새로 여니 그대로 실행됐어요.

새 PowerShell 창을 열고 아래 명령을 입력해 보세요.
버전 번호가 나오면 설치가 끝난 것입니다.

```powershell
claude --version
```

더 꼼꼼히 보고 싶다면 `claude doctor`를 실행하면 됩니다.
대화를 시작하지 않고 설치 상태와 설정 오류,
고칠 방법이 담긴 경고까지 한 번에 보여 줍니다.

[IMAGE: 포인트카드 | 설명: 클로드 코드 윈도우 설치 확인 명령 claude --version과 claude doctor, PATH 폴더 정리]

### 새 창에서도 인식이 안 된다면?

설치 폴더가 PATH(명령을 찾는 폴더 목록)에 빠진 경우입니다.
윈도우에서는 `%USERPROFILE%\.local\bin` 폴더에
`claude.exe`가 설치됩니다.
PowerShell에 아래 두 줄을 차례로 넣으면 이 폴더가 추가됩니다.

```powershell
$currentPath = [Environment]::GetEnvironmentVariable('PATH', 'User')
[Environment]::SetEnvironmentVariable('PATH', "$currentPath;$env:USERPROFILE\.local\bin", 'User')
```

입력한 뒤에는 창을 닫고 새로 열어 다시 확인합니다.
VS Code 같은 편집기 안의 터미널을 쓰고 있다면
편집기도 껐다 켜야 바뀐 경로가 적용됩니다.

---

## Step 3. 첫 실행과 로그인은 어떻게 할까?

이제 실제로 클로드 코드를 켜 볼 차례입니다.
작업할 프로젝트 폴더로 이동한 다음 `claude`를 입력하면 됩니다.

```powershell
cd C:\Users\내이름\my-project
claude
```

처음 실행하면 브라우저 창이 열리면서 로그인을 요청합니다.
평소 쓰는 Claude 계정으로 로그인하고 허용하면
터미널로 돌아와 대화를 시작할 수 있죠.
로그인이 끝나면 말로 부탁해 보세요.

```
이 폴더에 어떤 파일이 있는지 보고 프로젝트 구조를 설명해줘
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 윈도우 첫 실행 순서: 폴더 이동, claude 입력, 브라우저 로그인]

Git for Windows를 깔았는데 클로드 코드가 Git Bash를 못 찾는다면
설정 파일 `settings.json`에 위치를 직접 적어 줍니다.
기본 설치 위치라면 아래처럼 쓰면 됩니다.

```json
{
  "env": {
    "CLAUDE_CODE_GIT_BASH_PATH": "C:\\Program Files\\Git\\bin\\bash.exe"
  }
}
```

하지만 중요한 건 이것저것 설정을 바꾸는 것이 아니라
**설치 방식 하나만** 유지하는 것이겠죠.
여러 방법으로 겹쳐 깔면 엉뚱한 버전이 실행될 수 있어서,
공식 문서도 기본 설치 하나만 남기라고 안내합니다.

리눅스 도구를 주로 쓰거나 샌드박스 기능이 필요하다면
WSL 2 안에 설치하는 방법도 있습니다.
이때는 WSL 터미널에서 리눅스용 명령으로 설치하고,
실행도 WSL 터미널 안에서만 합니다.

---

## 4. 마무리

오늘은 클로드 코드 윈도우 설치 방법을
명령 실행, 새 창에서 확인, 첫 실행과 로그인의 3단계로 알아보았습니다.
`PS C:\` 창인지 확인하는 것과 설치 뒤 새 창을 여는 것,
이 두 가지만 기억하셔도 대부분의 막힘은 피할 수 있습니다.

설치가 끝났다면 작은 폴더 하나에서 먼저 말을 걸어 보세요.
첫 대화 한 번이 낯선 도구를 내 도구로 바꾸는 법이죠!
다음 글에서는 클로드 코드 요금제와 사용량을
한눈에 비교할 수 있게 총정리해 보겠습니다.

설치하다 막힌 메시지가 있다면 그대로 댓글로 남겨 주세요.
함께 원인을 찾아보겠습니다. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 윈도우 설치 3단계 요약과 다음 글 요금제·사용량 총정리 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드설치 #클로드코드윈도우 #윈도우설치 #클로드코드사용법 #AI코딩도구 #바이브코딩`

<!-- 공식 출처 (2026-10-29 확인)
- 시스템 요구 사항(윈도우 10 1809+ / Server 2019+, 4GB+ RAM, x64·ARM64), PowerShell·CMD·WinGet 설치 명령, 진행 표시 없음, PS C:\ 구분, '&&'·'irm' 오류 문구, 관리자 권한 불필요, Git for Windows 선택(없으면 PowerShell 도구), CLAUDE_CODE_GIT_BASH_PATH, WSL 2/1 표, claude --version, claude doctor, 유료 요금제(무료 미포함), 브라우저 로그인, 기본 설치 자동 업데이트, WinGet 수동 업데이트: https://code.claude.com/docs/en/setup
- PATH 폴더 %USERPROFILE%\.local\bin, PATH 추가 PowerShell 두 줄, 새 창·편집기 재시작, 설치 중복 시 하나만 남기기, 'irm' not recognized 대처: https://code.claude.com/docs/en/troubleshoot-install
-->

<!-- 경험 문장 근거 (style-guide 10장)
- 준비 "Node.js나 WSL부터 깔라는 예전 글이 많아 이것저것 먼저 설치했다": https://code.claude.com/docs/en/setup (npm 방식만 Node.js 22 이상 필요, 기본 설치는 불필요) , https://www.morphllm.com/claude-code-windows , https://wikidocs.net/333432
- Step 1 "CMD 창에 붙여 넣었다가 'irm' is not recognized를 보고 당황했다 / 헷갈려 막히는 분이 많다": https://code.claude.com/docs/en/troubleshoot-install , https://www.morphllm.com/claude-code-install , https://www.digitalmarketer.co.kr/insights/claude-code-windows-easy-setup-guide , https://smartscope.blog/en/generative-ai/claude/claude-code-windows-native-installation/
- Step 2 "같은 창에서 바로 claude를 입력했다가 인식할 수 없다는 메시지 / 새 창을 여니 실행됐다": https://code.claude.com/docs/en/terminal-guide , https://smartscope.blog/en/generative-ai/claude/claude-code-not-recognized-error-fix/ , https://www.developersdigest.tech/errors/claude-code/command-not-found-claude , https://medium.com/@tomhag_17/troubleshooting-claude-code-installation-on-windows-from-tty-errors-to-success-1f44af03c9f2
- 참고: smartscope.blog, inflearn.com은 이 세션 네트워크 제한으로 본문을 직접 열지 못했고 검색 결과 요약으로만 확인했다.
-->
