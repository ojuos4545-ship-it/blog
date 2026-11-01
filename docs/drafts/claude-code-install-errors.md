# 클로드 코드 설치 오류 해결 5가지

> 💡 **한 줄 요약:** 설치 오류는 메시지만 보면 원인이 보입니다.
> PATH, 중복 설치, 셸 명령, 네트워크, 인증서 순서로 확인하세요.

[IMAGE: 썸네일 | 설명: 클로드 코드 설치 오류 해결 5가지 대표 이미지]

결론부터 말씀드리면, **클로드 코드 설치 오류**는
대부분 다섯 가지 중 하나이고, 오류 메시지를 보면 어디서 막혔는지 바로 보입니다.
명령을 못 찾으면 PATH, 옛 버전이 뜨면 중복 설치,
설치 명령부터 실패하면 셸이나 네트워크를 보면 됩니다.

"설치 명령을 그대로 붙여 넣었는데 빨간 글씨만 잔뜩 나와요"
하시는 분들을 위해 준비했습니다.
오늘은 메시지별로 원인과 해결 명령을 하나씩 짚어볼게요.
명령과 오류 문구는 [Claude Code 공식 문서](https://code.claude.com/docs/en/troubleshoot-install)를
2026년 11월 1일에 확인해 정리했습니다.

---

## 1. 클로드 코드 설치 오류, 무엇부터 볼까?

오류가 나면 먼저 화면에 찍힌 메시지를 끝까지 읽어 보세요.
같은 "설치 실패"처럼 보여도 메시지에 따라 고칠 곳이 전혀 다릅니다.
자주 나오는 다섯 가지를 표로 정리했습니다.

| 증상 | 원인 | 먼저 할 일 |
| :--- | :--- | :--- |
| `command not found` | PATH 누락 | 설치 폴더를<br>PATH에 추가 |
| 옛 버전이 실행됨 | 중복 설치 | 설치를<br>하나만 남기기 |
| `irm`·`&&` 오류 | 셸에 안 맞는 명령 | 셸에 맞는<br>명령 다시 입력 |
| `<!DOCTYPE html>` | 스크립트 대신<br>웹 페이지 수신 | 연결 확인 뒤<br>다시 시도 |
| 인증서 오류 | 회사망 프록시 | 프록시·인증서<br>설정 |

[IMAGE: 비교표 | 설명: 클로드 코드 설치 오류 5가지 증상, 원인, 해결 방법 비교]

메시지만으로 헷갈린다면 `claude doctor`도 도움이 됩니다.
설치가 일단 끝나 `claude` 명령이 실행되는 상태라면,
대화를 시작하지 않고 설치 상태와 설정 문제를 점검해 줍니다.

---

## 2. 설치는 됐는데 claude가 안 될 때는?

설치 완료 문구까지 봤는데 `claude`를 치면 안 되는 경우입니다.
이때는 프로그램은 깔려 있고, 찾는 길이 막힌 경우가 대부분이죠.

### 오류 1. command not found: claude

맥에서는 `command not found: claude`,
윈도우에서는 `'claude' is not recognized`가 뜹니다.
설치 폴더가 PATH(명령을 찾는 폴더 목록)에 빠져 있다는 뜻입니다.
설치 프로그램은 맥·리눅스에서 `~/.local/bin`,
윈도우에서 `%USERPROFILE%\.local\bin`에 클로드 코드를 넣습니다.

맥 기본 셸(zsh)이라면 아래 두 줄을 입력합니다.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

윈도우는 PowerShell에서 아래 두 줄을 입력한 뒤
터미널을 새로 엽니다.

```powershell
$currentPath = [Environment]::GetEnvironmentVariable('PATH', 'User')
[Environment]::SetEnvironmentVariable('PATH', "$currentPath;$env:USERPROFILE\.local\bin", 'User')
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 설치 오류 command not found 해결: PATH에 설치 폴더 추가]

> 📌 **전문가 Tip:** 이미 열려 있던 터미널 창은 예전 PATH를 그대로 씁니다.
> VS Code 같은 편집기 안의 터미널이라면 편집기를 껐다 켜야
> 바뀐 PATH가 적용됩니다.

### 오류 2. 업데이트했는데 옛 버전이 실행될 때

예전에 npm으로 깔아 둔 클로드 코드가 남아 있으면
새로 설치한 버전 대신 옛 버전이 먼저 실행될 수 있습니다.
저도 기본 설치로 바꾼 뒤에 `claude --version`을 쳤는데
버전이 그대로라서 한참 헤맸어요.
같은 일을 겪었다는 글이 깃허브 이슈와 블로그에 꽤 많더라고요.

설치가 몇 개인지는 아래 명령으로 확인합니다.
맥·리눅스는 `which -a claude`, 윈도우는 `where.exe claude`입니다.
두 줄 이상 나오면 공식 문서가 권하는 기본 설치 하나만 남기고,
npm으로 깐 것은 아래 명령으로 지웁니다.

```bash
npm uninstall -g @anthropic-ai/claude-code
```

[IMAGE: 포인트카드 | 설명: 클로드 코드 중복 설치 확인과 정리: which -a claude, where.exe claude, npm uninstall]

---

## 3. 설치 명령부터 실패할 때는?

이번에는 설치 명령을 넣자마자 오류가 나는 경우입니다.
대부분 명령을 넣은 곳이 틀렸거나,
설치 파일을 받아 오는 길이 막힌 경우인데요.

### 오류 3. irm, &&, fsSL이 들어간 오류

설치 명령은 운영체제와 셸마다 다릅니다.
다른 셸용 명령을 붙여 넣으면 아래처럼 오류가 납니다.

* **`'irm' is not recognized`:** CMD 창에 PowerShell 명령을 넣은 경우
* **`'&&' is not a valid statement separator`:** PowerShell에 CMD 명령을 넣은 경우
* **`fsSL` 또는 `'bash' is not recognized`:** 윈도우에 맥용 명령을 넣은 경우

저도 처음엔 맥용 설치 명령을 윈도우 PowerShell에 그대로 붙여 넣었다가
`fsSL`이 들어간 낯선 오류를 보고 멈칫했어요.
이 실수로 질문을 올리는 분이 커뮤니티에 꽤 보이더라고요.
셸에 맞는 명령을 다시 정리해 드릴게요.

윈도우 PowerShell은 아래 명령입니다.

```powershell
irm https://claude.ai/install.ps1 | iex
```

윈도우 CMD는 아래 명령입니다.

```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

맥과 리눅스 터미널은 아래 명령입니다.

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

[IMAGE: 비교표 | 설명: 클로드 코드 설치 오류를 막는 셸별 설치 명령 PowerShell, CMD, 맥·리눅스 비교]

PowerShell 창은 주소 앞에 `PS`가 붙어 있어 CMD와 구분됩니다.
명령은 일부만 넣지 말고 한 줄 전체를 붙여 넣어야 합니다.
`irm` 부분만 실행하면 설치는 안 되고 스크립트 글자만 화면에 찍히거든요.

### 오류 4. syntax error near unexpected token '<'

`<!DOCTYPE html>`이 함께 보이면 설치 스크립트 대신
웹 페이지가 내려온 경우입니다.
일시적인 네트워크 문제나 서비스 장애가 원인일 때가 많아서,
몇 분 뒤 같은 명령을 다시 실행해 보는 것이 먼저입니다.

그래도 안 되면 내려받는 서버에 닿는지 확인합니다.
맥·리눅스 기준으로 아래 명령의 첫 줄에 `200`이 보이면 정상입니다.

```bash
curl -sI https://downloads.claude.ai/claude-code-releases/latest
```

`403`이 나오면 프록시나 네트워크 필터가 막고 있을 가능성이 큽니다.
메시지에 "App unavailable in region"이 보이면
클로드 코드를 지원하지 않는 국가에서 접속한 경우입니다.
급하다면 맥은 `brew install --cask claude-code`,
윈도우는 `winget install Anthropic.ClaudeCode`로 설치할 수도 있습니다.

### 오류 5. 인증서 오류와 회사망 프록시

`TLS connect error`나 `unable to get local issuer certificate`는
보안 연결 단계에서 막혔다는 뜻입니다.
회사 네트워크에서 설치할 때 이 오류로 막히는 분이 많더라고요.
회사 프록시가 오가는 연결을 검사하면서
회사 자체 인증서로 바꿔 끼우기 때문입니다.

이럴 때는 아래 순서로 확인해 보세요.

1. 회사 IT 담당자에게 프록시 주소를 받아 `HTTPS_PROXY`와 `HTTP_PROXY`에 넣기
2. 회사 인증서 파일을 받아 `curl --cacert`로 지정해 설치하기
3. 리눅스라면 `ca-certificates`로 시스템 인증서를 최신으로 바꾸기

[IMAGE: 다이어그램 | 설명: 클로드 코드 설치 오류 중 네트워크·인증서 문제 해결 순서]

하지만 중요한 건 오류를 빨리 없애는 것이 아니라
**안전하게** 설치하는 것이겠죠.
인증서 검사를 아예 끄는 방법이 검색에 보이기도 하는데요.
연결 내용이 노출될 수 있으니 회사 인증서를 지정하는 쪽을 권합니다.

---

## 4. 마무리

오늘은 클로드 코드 설치 오류를 해결하는 다섯 가지 방법을 알아보았습니다.
명령을 못 찾으면 PATH, 옛 버전이 뜨면 중복 설치,
명령부터 실패하면 셸과 네트워크, 인증서 순서로 보면 됩니다.

오류 메시지는 겁낼 대상이 아니라 원인을 알려 주는 안내문입니다.
메시지를 끝까지 읽는 습관 하나가 해결 시간을 크게 줄여 주는 법이죠!
다음 글에서는 클로드 코드를 쓸 때 알아 두면 좋은
터미널 기초 명령어 7가지를 정리해 보겠습니다.

여러분은 설치하다 어떤 오류에서 막히셨나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 클로드 코드 설치 오류 해결 5가지 요약과 다음 글 터미널 기초 명령어 예고]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#클로드코드 #ClaudeCode #클로드코드설치 #클로드코드설치오류 #클로드코드오류 #AI코딩도구 #바이브코딩`

<!-- 글 유형: A 정보·리뷰형 / 메인 키워드: 클로드 코드 설치 오류
검색 의도: 클로드 코드를 설치하다 오류 메시지를 만난 사람이 메시지별 원인과 바로 쓸 해결 명령을 알고 싶다.

경험 문장 근거 (style-guide 10장)
- 2장 오류 2 "기본 설치로 바꾼 뒤에도 버전이 그대로라 헤맸다 / 깃허브 이슈와 블로그에 많다":
  https://github.com/anthropics/claude-code/issues/9666 , https://github.com/anthropics/claude-code/issues/53432 , https://codenote.net/en/posts/claude-code-npm-to-native-install/ , https://university.tenten.co/t/uninstall-the-claude-code-node-js-version-and-install-the-latest-version/2193
- 3장 오류 3 "맥용 설치 명령을 윈도우 PowerShell에 붙여 넣었다가 fsSL 오류를 봤다 / 커뮤니티에 질문이 많다":
  https://www.inflearn.com/community/questions/1812097 , https://www.inflearn.com/community/questions/1829588 , https://www.morphllm.com/claude-code-install , https://code.claude.com/docs/en/troubleshoot-install (Wrong install command on Windows)
- 3장 오류 5 "회사 네트워크에서 설치할 때 인증서 오류로 막히는 분이 많다":
  https://github.com/anthropics/claude-code/issues/22756 , https://inventivehq.com/blog/ai-coding-cli-corporate-firewall-proxy-fixes , https://amitkoth.com/claude-code-corporate-proxy-tls-inspection/
- 사실 확인(오류 문구, 설치 위치, PATH 명령, which -a / where.exe, npm uninstall, 셸별 설치 명령, irm만 실행 시 스크립트 출력, HTML 응답·403·App unavailable in region, curl -sI 200 확인, brew·winget 대체 설치, TLS 오류·프록시 변수·curl --cacert·ca-certificates): https://code.claude.com/docs/en/troubleshoot-install (2026-11-01 확인)
-->
