# 리서치: 클로드 코드 인텔리제이 사용법 3단계

* 조사일: 2026-10-30
* 기준 시점: 2026년 5월 이후 자료 우선
* 확인한 출처 수: 22개 (광고성 제외)
  * 공식 문서(code.claude.com)는 발행일 표기가 없는 상시 갱신 문서다. 2026-10-30에 본문을 직접 열어 확인했다.
  * 2026년 5월 이후 날짜가 확인되는 자료: 변경 기록 항목(2026-05-06 ~ 2026-10-30, npm 배포일 기준) [S9][S10]
  * GitHub 이슈는 대부분 2025~2026년 초 자료라 발행일을 함께 적었다.
* 접속이 막혀 본문을 열지 못한 곳: plugins.jetbrains.com(플러그인 마켓 페이지), www.jetbrains.com(JetBrains 도움말), yozm.wishket.com, inflearn.com, wikidocs.net, github.blog. 이곳 내용은 사실 근거로 쓰지 않았다.

## 한눈에 보기

* IntelliJ IDEA에서 Claude Code를 쓰는 공식 방법은 Anthropic의 "Claude Code [Beta]" 플러그인을 JetBrains 마켓플레이스에서 설치하는 것이다. 플러그인은 CLI를 포함하지 않으므로 Claude Code CLI를 따로 설치해야 한다. [S1][S2]
* 공식 문서 순서는 ① CLI 설치 ② 플러그인 설치 후 IDE 재시작 ③ IDE 내장 터미널에서 `claude` 실행(외부 터미널이면 `/ide`)이다. 처음 `claude`를 실행하면 로그인 안내가 나온다. [S1][S2]
* 연결되면 코드 변경이 IDE diff 뷰어로 열리고, 선택 영역·열린 파일이 자동 공유되며, IDE 검사 진단(lint·구문 오류)을 Claude가 읽을 수 있다. [S1][S2]
* 유료 Claude 구독(Pro, Max, Team, Enterprise) 또는 Claude Console 계정이 필요하고 API 키는 필요 없다. Free 플랜에는 Claude Code가 포함되지 않는다. [S2][S11]
* 흔한 문제는 ESC 키가 작업을 멈추지 않음, `/ide`에서 "No available IDEs detected", diff가 IDE 대신 터미널에만 뜸, WSL2 연결 실패다. 공식 문서에 각각 해결법이 있다. [S2][S13][S15][S17]

## 1. 기본 정의 (도입용, 짧게)

Claude는 Anthropic이 만든 AI로, 웹·모바일(iOS, Android)과 macOS·Windows 데스크톱 앱에서 쓸 수 있다. Anthropic 소개 페이지는 Claude를 "단순한 AI 어시스턴트를 넘어선 협업자"로 설명한다. [S12]

Claude Code는 코드베이스를 읽고, 파일을 고치고, 명령을 실행하고, 개발 도구와 연동되는 에이전트형 코딩 도구다. 터미널, IDE, 데스크톱 앱, 브라우저에서 쓸 수 있다. [S3]

* Claude Code는 터미널(CLI), VS Code, JetBrains, 데스크톱 앱, 웹 등 여러 곳에서 같은 엔진으로 돌아가며, 저장소의 CLAUDE.md·설정·MCP 서버가 모든 곳에서 공통으로 쓰인다. [S3]
* 공식 비교표에서 JetBrains는 "IntelliJ, PyCharm, WebStorm 등 JetBrains IDE 안에서 작업"하는 용도이고, 제공 기능은 "diff 뷰어, 선택 영역 공유, 터미널 세션"으로 적혀 있다. [S8]
* JetBrains 연동은 IDE 터미널 안에서 CLI를 실행하는 방식이다. [S8]

## 2. 준비물: 지원 IDE, 계정, 시스템 요건

공식 문서에 따르면 플러그인은 대부분의 JetBrains IDE에서 동작하며, 예로 IntelliJ IDEA, PyCharm, Android Studio, WebStorm, PhpStorm, GoLand를 든다. [S1][S2]

* 플러그인 이름: 마켓플레이스 표기는 "Claude Code [Beta]"이고, 설치 후 설정 메뉴도 **Settings → Tools → Claude Code [Beta]**다. (2026-10-30 조회 기준 문서에 여전히 Beta 표기) [S1][S2]
* 마켓플레이스 주소: https://plugins.jetbrains.com/plugin/27310-claude-code-beta- [S2]
* 계정: 유료 Claude 구독(Pro, Max, Team, Enterprise) 또는 Claude Console 계정이면 되고, API 키는 필요 없다. [S2]
* 그 밖의 로그인 방법: Amazon Bedrock, Google Cloud Agent Platform, Microsoft Foundry 같은 클라우드 제공자도 환경 변수 설정으로 쓸 수 있고, `ANTHROPIC_API_KEY` 환경 변수를 승인하면 로그인 화면을 건너뛴다. [S3][S6]
* 공식 문서는 터미널 CLI, VS Code, JetBrains가 서드파티 제공자도 지원한다고 적는다. [S3]
* 요금(claude.com/pricing, 2026-10-30 조회, 달러 표기): Free $0(Claude Code 미포함), Pro 월 결제 $20 또는 연 결제 시 월 $17($200 선결제), Max 월 $100부터. Pro와 Max에는 Claude Code가 포함된다. [S11]
* CLI 시스템 요건: macOS 13.0 이상, Windows 10 1809 이상 또는 Windows Server 2019 이상, Ubuntu 20.04 이상, Debian 10 이상, Alpine Linux 3.19 이상, RAM 4GB 이상, x64 또는 ARM64, 인터넷 연결 필요. 셸은 Bash, Zsh, PowerShell, CMD. [S7]

## 3. 1단계: Claude Code CLI 설치와 로그인

플러그인은 IDE 내장 터미널에서 `claude` 명령을 실행해 연결하는 구조라서, CLI가 PATH에 없으면 "Cannot launch Claude Code"(한국어 문서: "Claude Code를 시작할 수 없음") 알림이 뜬다. 그래서 CLI를 먼저 설치한다. [S1][S2]

* 설치 명령(공식, 권장인 Native Install) [S3]
  * macOS, Linux, WSL: `curl -fsSL https://claude.ai/install.sh | bash`
  * Windows PowerShell: `irm https://claude.ai/install.ps1 | iex`
  * Windows CMD: `curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd`
* 다른 설치 방법: Homebrew(`brew install --cask claude-code`), WinGet(`winget install Anthropic.ClaudeCode`). 이 두 방법은 자동 업데이트가 되지 않아 직접 업그레이드해야 한다. Native 설치는 백그라운드에서 자동 업데이트된다. [S3]
* 설치 확인: 새 터미널 창을 열고 `claude --version`을 실행하면 버전 번호가 나온다. `claude`를 찾지 못한다고 나오면 설치 경로가 PATH에 아직 없는 것이다. [S3]
* 설치 명령은 내려받는 동안 진행 상황을 표시하지 않는다. [S3]
* Windows 네이티브 환경에서는 Git for Windows 설치가 권장된다. 없으면 Bash 대신 PowerShell을 셸 도구로 쓴다. WSL은 필요 없다. [S3]
* 로그인 순서 [S6]
  1. 터미널에서 `claude`를 실행하면 첫 실행 때 브라우저 로그인 창이 열린다.
  2. 브라우저가 자동으로 안 열리면 `c`를 눌러 로그인 주소를 복사해 브라우저에 붙여 넣는다.
  3. 브라우저에 로그인 코드가 보이면 터미널의 `Paste code here if prompted` 자리에 붙여 넣는다.
  4. 완료되면 터미널에 `Login successful`이 뜨고 `Enter`를 눌러 계속한다.
* 다시 로그인하려면 `/logout`을 입력한다. [S6]

## 4. 2단계: JetBrains 플러그인 설치

JetBrains 마켓플레이스에서 Claude Code 플러그인을 설치하고 IDE를 다시 시작하는 것이 공식 안내다. [S1][S2]

* `claude`가 IDE가 찾지 못하는 위치에 설치돼 있으면 플러그인 설정의 **Claude command**(한국어 문서: "Claude 명령")에 전체 경로를 넣는다. 예: `claude`, `/usr/local/bin/claude`, `npx @anthropic-ai/claude-code` [S1][S2]
* WSL 사용자는 Claude command에 `wsl -d Ubuntu -- bash -lic "claude"`를 넣는다(`Ubuntu`는 자기 배포판 이름으로 바꾼다). [S1][S2]
* JetBrains 원격 개발(Remote Development)을 쓸 때는 로컬 클라이언트가 아니라 **Settings → Plugin (Host)**에서 원격 호스트에 플러그인을 설치해야 한다. [S1][S2]
* 플러그인 버전: 2026년 2월 GitHub 이슈에 "0.1.14-beta"가 보고돼 있다. 2026년 10월 현재 최신 버전 번호는 마켓플레이스 접속이 막혀 확인하지 못했다. [S16]

## 5. 3단계: IDE에서 실행하고 연결 확인

IDE 내장 터미널에서 `claude`를 실행하면 모든 연동 기능이 켜진다. 공식 문서가 권하는 가장 기본적인 방법이다. [S1][S2]

* 빠른 실행: Mac은 `Cmd+Esc`, Windows/Linux는 `Ctrl+Esc`로 에디터에서 바로 Claude Code를 열 수 있고, UI의 Claude Code 버튼을 눌러도 된다. [S1][S2]
* Claude가 IDE와 같은 파일을 보게 하려면 IDE 프로젝트 루트와 같은 디렉터리에서 Claude Code를 시작한다. [S1][S2]
* 외부 터미널(iTerm2, Windows Terminal 등)에서 쓸 때 [S1][S2]
  1. 외부 터미널에서 `claude` 실행
  2. `/ide` 입력
  3. 연결되면 `Connected to IntelliJ IDEA.` 같은 메시지가 나온다.
* `/ide` 명령의 공식 설명은 "IDE 연동을 관리하고 상태를 보여 준다"이다. [S22]
* 외부 터미널에서도 자동 연결하려면 전역 설정 `autoConnectIde`를 `true`로 둔다(기본값 `false`). `/config`에서는 **Auto-connect to IDE (external terminal)**로 보인다. 기본값이어도 JetBrains 터미널 안에서 실행하거나 `--ide`를 붙이면 연결된다. [S4]
* 환경 변수 `CLAUDE_CODE_AUTO_CONNECT_IDE`를 `true`로 두면 tmux 등으로 자동 감지가 실패할 때 연결을 강제로 시도하고, `false`면 자동 연결을 막는다. 이 변수가 `autoConnectIde` 설정보다 우선한다. [S5]

## 6. 연결 후 쓸 수 있는 기능 (공식 문서 기준)

연결 상태에서는 IDE 안의 정보가 Claude Code로 넘어가고, Claude의 수정안이 IDE 화면에 표시된다. 아래는 공식 문서에 적힌 것만 모았다. [S1][S2]

* **Diff 보기**: 코드 변경을 터미널 대신 IDE diff 뷰어에 연다. [S1][S2]
* **선택 영역·열린 파일 공유**: 현재 선택 영역이나 탭이 자동으로 공유된다. 연결 중에는 프롬프트를 보낼 때마다 선택 영역과 활성 파일 경로가 함께 들어가고, 대화 기록에 `⧉ Selected N lines from <file>` 줄이 표시된다. [S2]
  * 2026-09-14 배포된 2.1.271부터 입력창의 선택 표시가 `[⧉ …]` 모양으로 바뀌었고, Backspace로 지우면 그 선택을 빼고 보낼 수 있다. [S9][S10]
  * Claude가 작업 중일 때 메시지를 대기열에 넣으면 `Enter`를 누른 시점의 선택 영역이 유지된다. [S2]
* **파일 참조 단축키**: Mac `Cmd+Option+K`, Linux/Windows `Alt+Ctrl+K`로 `@src/auth.ts#L1-99` 같은 파일 참조를 넣는다. [S1][S2]
* **진단 공유**: Claude가 `getDiagnostics` 도구로 IDE 검사 결과(lint, 구문 오류 등 에디터의 오류·경고)를 읽는다. 한 번 호출에 파일 하나씩이며, 편집 후 자동으로 진단을 요청하지는 않는다. [S1][S2]
* **diff에서 직접 고치기**: 2026-04-15 배포된 2.1.110부터 IDE diff에서 제안 내용을 고친 뒤 수락하면 Write 도구가 그 사실을 모델에 알린다. [S9][S10]
* **권한 창에서 diff 열기**: 2026-05-13 배포된 2.1.141에서 IDE 연결 시 파일 수정 권한 창의 "view diff in your IDE" 선택지가 복구됐다. [S9][S10]
* 이 기능들은 플러그인이 띄우는 로컬 MCP 서버(이름 `ide`)를 통해 동작한다. 설정할 것이 없어 `/mcp` 목록에는 숨겨져 있다. 플러그인은 모델에 코드 실행 도구를 노출하지 않는다. [S2]

## 7. 설정 항목

설정은 Claude Code 쪽(`/config`)과 플러그인 쪽(IDE 설정 메뉴) 두 곳에 있다. [S1][S2]

* **Claude Code 쪽: Diff tool** [S1][S2][S4]
  1. `claude` 실행
  2. `/config` 입력
  3. **Diff tool**을 `auto`(IDE에서 diff 표시)나 `terminal`(터미널에 유지)로 고른다.
  * 기본값은 `"auto"`다. [S4]
  * Diff tool 항목은 IDE에 연결됐을 때만 `/config`에 보인다. 그래서 JetBrains 터미널에서 `claude`를 실행하거나, 외부 터미널이면 `/ide`를 먼저 실행해야 한다. [S1][S2][S4]
* **플러그인 쪽: Settings → Tools → Claude Code [Beta]** [S1][S2]
  * Claude command: 실행할 명령이나 전체 경로
  * Suppress notification for when Claude Command is not found: 명령을 못 찾았다는 알림 끄기
  * Enable using Option+Enter for multi-line prompts: macOS 전용. 켜면 Option+Enter로 줄바꿈. Option 키가 엉뚱하게 잡히면 끈다. 터미널을 다시 시작해야 적용된다.
  * Enable automatic updates: 플러그인 업데이트를 자동 확인·설치하고, 재시작할 때 적용
  * Networking (Advanced) → Accept connections from all network interfaces: 끄면 `127.0.0.1`에서만 연결을 받는다. 켜면 로컬 네트워크에서 포트에 접근할 수 있고 통신이 암호화되지 않은 `ws://`라 토큰과 내용이 평문으로 오간다. 루프백이 안 될 때만 켜라고 경고한다. [S2]
* **민감한 파일 제외**: `.env` 같은 파일은 `Read` 거부 규칙을 걸면 선택 텍스트와 열린 파일 알림이 Claude에 전달되지 않는다. [S2]
* **자동 설치 관련**: `autoInstallIdeExtension`(기본 `true`)은 VS Code 터미널에서 실행할 때 IDE 확장을 자동 설치하는 설정이다. [S4]

## 8. 흔한 문제와 해결법 (공식 문서 기준)

공식 문서 문제 해결 항목을 증상별로 정리했다. [S1][S2]

* **ESC 키로 작업이 멈추지 않을 때** [S1][S2]
  1. **Settings → Tools → Terminal**로 간다.
  2. "Move focus to the editor with Escape"(한국어 문서: "Escape로 편집기에 포커스 이동")를 끄거나, "Configure terminal keybindings"에서 "Switch focus to Editor" 단축키를 지운다.
  3. 적용한다.
* **플러그인을 깔았는데 기능이 안 보일 때** [S1][S2]
  * 프로젝트 루트에서 Claude Code를 실행했는지 확인
  * IDE 설정에서 플러그인이 켜져 있는지 확인
  * IDE를 완전히 다시 시작(여러 번 해야 할 수도 있다고 문서에 적혀 있음)
  * 원격 개발이면 원격 호스트에 플러그인이 설치됐는지 확인
* **`/ide`가 "No available IDEs detected"를 보여 줄 때** [S1][S2]
  * 플러그인 설치·활성화 확인, IDE 완전 재시작
  * `/ide` 없이 자동 연결을 기대했다면 IDE 내장 터미널에서 `claude`를 실행했는지 확인
  * WSL 사용자는 아래 WSL 항목 참고
* **Claude 아이콘을 눌렀더니 "command not found"일 때** [S1][S2]
  1. 터미널에서 `claude --version`으로 설치 확인
  2. 플러그인 설정에서 Claude command 경로 지정
  3. WSL이면 WSL 명령 형식 사용
* **WSL2에서 IDE가 감지되지 않을 때**: 원인은 보통 WSL2의 NAT 네트워킹이나 Windows 방화벽이 WSL2와 Windows의 IDE 사이 연결을 막는 것이다. WSL1은 영향이 없다. [S1][S2]
  * 권장 해결(기존 네트워크 모드 유지): WSL 안에서 `hostname -I`로 주소를 확인하고 앞 두 자리에 `.0.0/16`을 붙여 서브넷을 만든다(예: `172.21.123.45` → `172.21.0.0/16`). 관리자 PowerShell에서 `New-NetFirewallRule -DisplayName "Allow WSL2 Internal Traffic" -Direction Inbound -Protocol TCP -Action Allow -RemoteAddress 172.21.0.0/16 -LocalAddress 172.21.0.0/16`을 실행하고 IDE와 Claude Code를 다시 시작한다.
  * 다른 방법: Windows 사용자 폴더의 `.wslconfig`에 `[wsl2]` / `networkingMode=mirrored`를 넣고 PowerShell에서 `wsl --shutdown`. Windows 11 22H2 이상이 필요하고, Windows 10은 방화벽 규칙을 써야 한다.
* **보안 주의**: JetBrains IDE에서 `acceptEdits` 모드로 쓰면 Claude Code가 IDE가 자동 실행할 수 있는 IDE 설정 파일을 고칠 수 있어, Bash 실행 권한 확인을 우회할 위험이 커질 수 있다. 문서는 편집에 Manual 모드를 쓰고, 신뢰할 수 있는 프롬프트로만 쓰라고 권한다. [S2]
  * 2026-07-03 배포된 2.1.200부터 기존 "default" 권한 모드 이름이 "Manual"로 바뀌었다. [S9][S10]

## 9. 2026년 기준 최신 상태

플러그인은 2026-10-30 조회 기준 공식 문서에서 여전히 "Claude Code [Beta]"로 표기돼 있다. 정식 출시 발표는 찾지 못했다. [S1][S2]

* Claude Code CLI 최신 버전: 2026-10-30 기준 npm `latest` 2.1.314(2026-10-30 배포), `stable` 2.1.308(2026-10-22 배포). [S10]
* 2026년 5월 이후 JetBrains 관련 변경 기록(버전, npm 배포일) [S9][S10]
  * 2.1.132 (2026-05-06): JetBrains IDE 2025.2 터미널의 마우스 휠 스크롤 문제(엉뚱한 화살표 키 입력, 반대 방향, 과한 가속) 수정
  * 2.1.157 (2026-05-29): 시작할 때 뜨던 "/ide for …" 안내 제거
  * 2.1.160 (2026-06-01): 시작할 때 뜨던 JetBrains 플러그인 설치 제안 제거
  * 2.1.166 (2026-06-05): 2026.1 이상 JetBrains IDE 터미널(IntelliJ, PyCharm, WebStorm 등)의 화면 깜빡임 수정
  * 2.1.181 (2026-06-17): IDE 선택 영역 줄 번호가 하나씩 어긋나던 문제 수정(IntelliJ, VS Code)
  * 2.1.239 (2026-08-21): 플러그인 연결 상태의 JetBrains 터미널에서 Edit·Write가 약 5초씩 멈추던 문제 수정
  * 2.1.281 (2026-09-23): `/ide`가 실행 중인 IDE를 나열하면서도 "No available IDEs detected"를 보여 주던 문제 수정
  * 2.1.311 (2026-10-26): `/ide`가 아무것도 설치하지 않았는데 JetBrains 플러그인을 설치했다고 말하던 문제 수정
* 스크롤 속도 설정(`CLAUDE_CODE_SCROLL_SPEED`, `/scroll-speed`)은 JetBrains IDE 터미널에서는 적용되지 않는다. Claude Code가 자체 스크롤 처리를 쓰기 때문이다. [S5]

## 독자가 자주 묻는 것

* Q. 플러그인만 설치하면 바로 되나요?
  * A. 아니다. 플러그인은 CLI를 포함하지 않아 Claude Code CLI를 따로 설치해야 한다. 둘 다 설치해야 한다고 공식 문서에 적혀 있다. [S1][S2]
* Q. 무료 계정으로 쓸 수 있나요?
  * A. Free 플랜에는 Claude Code가 포함되지 않는다. Pro, Max, Team, Enterprise 유료 구독이나 Claude Console 계정이 필요하다. [S2][S11]
* Q. API 키를 따로 발급해야 하나요?
  * A. 유료 구독이나 Console 계정이면 API 키는 필요 없고, 처음 `claude`를 실행할 때 로그인하면 된다. [S2][S6]
* Q. IntelliJ 말고 PyCharm, WebStorm, Android Studio에서도 되나요?
  * A. 공식 문서는 IntelliJ IDEA, PyCharm, Android Studio, WebStorm, PhpStorm, GoLand를 포함한 대부분의 JetBrains IDE에서 동작한다고 적는다. [S1][S2]
* Q. iTerm2나 Windows Terminal 같은 외부 터미널에서도 연결되나요?
  * A. 외부 터미널에서 `claude`를 실행한 뒤 `/ide`를 입력하면 연결된다. 항상 자동 연결하려면 `autoConnectIde`를 켠다. [S2][S4]
* Q. 변경 내용을 IDE 창이 아니라 터미널에서 보고 싶어요.
  * A. `/config`에서 Diff tool을 `terminal`로 바꾼다. 이 항목은 IDE에 연결됐을 때만 보인다. [S2][S4]
* Q. `/config`에 Diff tool 항목이 안 보여요.
  * A. IDE에 연결되지 않은 상태다. JetBrains 터미널에서 `claude`를 실행하거나 외부 터미널에서 `/ide`를 먼저 실행한다. [S2][S4]
* Q. ESC를 눌러도 Claude가 멈추지 않아요.
  * A. IDE 터미널 설정에서 "Move focus to the editor with Escape"를 끄거나 "Switch focus to Editor" 단축키를 지운다. [S2] 이 설정으로도 안 됐다는 사용자 보고와 다른 우회법은 "엇갈리는 정보"에 적었다. [S14]
* Q. `.env` 같은 파일 내용이 넘어가는 게 걱정돼요.
  * A. 해당 경로에 `Read` 거부 규칙을 걸면 선택 텍스트와 열린 파일 알림이 Claude에 전달되지 않는다. [S2]

## 흔히 겪는 사례

style-guide 10장 기준으로, 여러 출처에서 반복되는 것만 골랐다. 수치(버전 등)는 경험 문장에 넣지 않는다.

* 사례: ESC로 작업을 멈추려 했는데 반응이 없어 결국 Ctrl+C로 세션을 통째로 끝내게 된다. IDE가 ESC를 "에디터로 포커스 이동"에 써 버리는 것이 흔한 원인으로 꼽히고, 터미널 설정에서 해당 옵션을 끄는 것이 대표 해결법이다. [S2][S13][S14]
* 사례: `/ide`를 입력했는데 "No available IDEs detected"가 뜨면서 IDE를 못 찾는다. 플러그인 설치·재시작을 반복하거나, 외부 터미널과 IDE 터미널을 바꿔 가며 시도하는 경우가 많다. [S2][S15][S16][S19]
* 사례: 플러그인을 깔았는데 수정 내용이 IDE diff 창이 아니라 터미널에만 표시된다. 큰 수정을 터미널로만 검토해야 해서 불편했다는 보고가 있고, 공식 문서는 `/config`의 Diff tool 확인과 IDE 내장 터미널 실행을 안내한다. [S1][S17][S18]
* 사례: 설정을 바꾼 뒤에도 IDE를 한 번 재시작해서는 안 되고 완전히 껐다 켜야 반영된다. 공식 문서에도 "여러 번 해야 할 수 있다"고 적혀 있다. [S2][S17][S19]
* 사례: Windows에서 WSL로 Claude Code를 돌리면 Windows 쪽 IntelliJ와 연결이 안 된다. 미러링 네트워크로 바꾸거나 방화벽 규칙을 추가해 해결한 보고가 있다. [S1][S2][S19]
* 참고(단일 출처 계열, 경험 문장에는 신중히): VS Code 확장처럼 사이드바 채팅 화면을 원하지만 JetBrains는 터미널 방식이라 아쉽다는 기능 요청이 있다. 이 요청은 비슷한 요청(#9738, #9469, #2044)과 중복 처리됐다. [S20][S8]

## 엇갈리는 정보

| 항목 | 주장 A (출처, 발행일) | 주장 B (출처, 발행일) | 비고 |
|---|---|---|---|
| ESC 키 해결법 | IDE 터미널 설정에서 "Move focus to the editor with Escape"를 끄거나 "Switch focus to Editor" 단축키를 지우면 해결된다 (S2 공식 문서, 상시 갱신 / S13 이슈 댓글, 2025-10-08) | 플러그인으로 실행했을 때는 이 옵션을 꺼도 안 됐다는 사용자 보고가 있다. 터미널에서 직접 `claude`를 실행하면 된다는 보고와 `Ctrl-[` 또는 `Ctrl-Esc`를 대신 쓰라는 우회법이 나왔다 (S14 GitHub 이슈 #10618, 2025-10-30 작성, 2026-02 기준 열린 상태) | 실행 방법(플러그인 버튼 vs 터미널 직접 실행)에 따라 달랐다는 보고. 공식 확인은 없음 |
| ESC 키와 터미널 엔진 | IntelliJ 2025.1.1과 새 터미널(Reworked 2025)을 쓰라는 제안 (S13 이슈 댓글, 2025-05-08) | Reworked 2025로 바꿔도 확실한 해결이 아니라는 보고 (S14 이슈 댓글, 작성일은 2025-10 ~ 2026-02 사이) | 공식 문서는 터미널 엔진을 해결법으로 언급하지 않음 [S2] |
| WSL2 연결 해결법 | 방화벽 규칙 추가가 권장 해결, 미러링 네트워크는 대안 (S1·S2 공식 문서, 상시 갱신) | 미러링 네트워크로 바꿔서 해결했다는 사용자 보고. Anthropic 담당자는 WSL보다 Windows PowerShell(Git Bash)판 Claude Code가 더 안정적이라고 권함 (S19 GitHub 이슈 #1232, 2025-08-06 / 2025-08-23 댓글) | 시점 차이. 최신 공식 문서를 앞에 둔다 |
| JetBrains 화면 형태 | 플러그인은 IDE 터미널에서 CLI를 실행하는 방식이고, 제공 기능은 "diff 뷰어, 선택 영역 공유, 터미널 세션" (S2, S8 공식 문서, 상시 갱신) | 2026년 변경 기록에 "VS Code and JetBrains panels"라는 표현이 나온다. 예: 사용량 한도 배너에 "Get more usage" 링크 추가 (S9 2.1.301, 2026-10-15 배포) | 해당 항목들은 `[VSCode]` 꼬리표가 붙어 있다. JetBrains용 채팅 패널이 있는지는 공식 문서로 확인 안 됨 |
| 문제 발생 원인(IDE 감지·diff) | 공식 문서는 플러그인 활성화, 프로젝트 루트, 재시작, WSL 네트워크를 원인으로 안내 (S2, 상시 갱신) | 특정 CLI 버전에서 생긴 회귀 버그로, Windows에서 IDE 연결이 아예 시도되지 않았고 이후 버전에서 고쳐졌다는 보고 (S16 GitHub 이슈 #23119, 2026-02-04 작성, 2026-02-11 해결 확인) | 2026-02 시점의 특정 버전 문제. 지금도 같은 증상이면 CLI 업데이트부터 확인하는 근거로만 쓴다 |

## 확인하지 못한 것

* 플러그인 최신 버전 번호, 최소 지원 IDE 버전, 다운로드 수: JetBrains 마켓플레이스(plugins.jetbrains.com) 접속이 막혀 확인하지 못했다. 2026-02 이슈에 0.1.14-beta가 보고된 것만 확인했다. [S16]
* 플러그인 정식(Beta 해제) 출시 여부: 공식 문서에 여전히 [Beta]로 표기돼 있고, 정식 출시 발표는 찾지 못했다.
* IntelliJ IDEA Community 판에서 동작하는지: 공식 문서는 "IntelliJ IDEA"라고만 적고 판(edition)을 구분하지 않는다.
* "통합 터미널에서 `claude`를 실행하면 JetBrains 플러그인이 자동 설치된다"는 설명: 검색 결과 요약과 일부 2025년 블로그 요약에 보였지만 본문을 열지 못했다. 현재 공식 문서는 마켓플레이스 설치만 안내하고, 자동 설치 설정 `autoInstallIdeExtension`은 "VS Code 터미널"에서의 동작으로 적혀 있으며, 2.1.160(2026-06-01)에서 시작 시 JetBrains 플러그인 설치 제안이 제거됐다. 글에서는 자동 설치를 단정하지 않는다. [S4][S9][S10]
* JetBrains 자체 AI Chat 안의 "Claude Agent", GitHub Copilot의 JetBrains용 Claude 에이전트 미리보기 같은 다른 경로: 검색 결과에는 보였지만 JetBrains 도움말과 github.blog 접속이 막혀 본문을 확인하지 못했다. Anthropic 공식 플러그인과 같은 것인지도 확인 안 됨.
* IntelliJ 터미널에서 한글 입력이 밀리거나 조합 중 글자가 안 보이는 문제: Claude Code 전반의 IME 이슈 보고는 있으나(2025-06 WebStorm 터미널 보고 1건 포함, 중복 처리로 종료) IntelliJ 전용 문제인지, 지금도 남아 있는지는 확인 안 됨. [S21]
* 빠른 실행 단축키(`Cmd+Esc`/`Ctrl+Esc`)가 다른 IDE 단축키와 충돌하는지: 공식 자료에서 확인 안 됨.
* 3rd-party 플러그인(Claude Code Pro, Claude Code Chat 등 마켓플레이스의 비공식 플러그인): 검색에 여러 개 보였지만 Anthropic 공식이 아니고 본문 확인을 못 해 다루지 않았다. 글에서 "Claude Code [Beta]"(Anthropic)와 혼동하지 않게 구분할 필요가 있다는 점만 참고한다.

## 참고 출처

| 번호 | 제목 | 발행처 | 발행일 | URL |
|---|---|---|---|---|
| S1 | JetBrains IDEs (한국어 공식 문서) | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/ko/jetbrains |
| S2 | JetBrains IDEs (영어 공식 문서) | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/jetbrains |
| S3 | Overview | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/overview |
| S4 | Settings reference (`autoConnectIde`, `autoInstallIdeExtension`, `diffTool`) | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/settings-reference |
| S5 | Environment variables | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/env-vars |
| S6 | Authentication | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/authentication |
| S7 | Advanced setup (System requirements) | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/setup |
| S8 | Platforms and integrations | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/platforms |
| S9 | Claude Code CHANGELOG.md | Anthropic (GitHub anthropics/claude-code) | 상시 갱신, 최신 항목 2.1.314 (2026-10-30 조회). 항목별 날짜는 S10 기준 | https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md |
| S10 | @anthropic-ai/claude-code 패키지 배포 기록 | npm registry | 버전별 배포일(본문에 표기), 2026-10-30 조회 | https://registry.npmjs.org/@anthropic-ai/claude-code |
| S11 | Pricing | Anthropic (claude.com) | 작성일 확인 불가 (2026-10-30 조회) | https://claude.com/pricing |
| S12 | Claude product overview | Anthropic (claude.com) | 작성일 확인 불가 (© 2026 표기, 2026-10-30 조회) | https://claude.com/product/overview |
| S13 | [BUG] Pressing ESC to interrupt does not work on IntelJIdea (#1002) | GitHub anthropics/claude-code 이슈 | 2025-05-08 (2026-01-07 종료) | https://github.com/anthropics/claude-code/issues/1002 |
| S14 | [Bug] ESC key doesn't work when claude terminal is started by intellij (#10618) | GitHub anthropics/claude-code 이슈 | 2025-10-30 (열린 상태, 2026-02-14 stale 표시) | https://github.com/anthropics/claude-code/issues/10618 |
| S15 | [BUG] /ide integration not working for JetBrains IDE (Intellij IDEA) (#22232) | GitHub anthropics/claude-code 이슈 | 2026-01-31 (2026-03-25 종료) | https://github.com/anthropics/claude-code/issues/22232 |
| S16 | [BUG] IDE integration broken in v2.1.23+ - Affects Jetbrains IDEs on Windows (#23119) | GitHub anthropics/claude-code 이슈 | 2026-02-04 (2026-02-11 해결 종료) | https://github.com/anthropics/claude-code/issues/23119 |
| S17 | Intellij diff editor not being used... TUI diffs only. Windows 11 (#23192) | GitHub anthropics/claude-code 이슈 | 2026-02-04 (2026-03-31 종료) | https://github.com/anthropics/claude-code/issues/23192 |
| S18 | [BUG] Claude code intellij plugin not able to open the diff view (#29464) | GitHub anthropics/claude-code 이슈 | 2026-02-28 (2026-03-28 종료) | https://github.com/anthropics/claude-code/issues/29464 |
| S19 | [BUG] Claude Code does not detect Jetbrains IDE on Windows WSL (#1232) | GitHub anthropics/claude-code 이슈 | 2025-05-22 (2025-08-23 종료) | https://github.com/anthropics/claude-code/issues/1232 |
| S20 | [FEATURE] IntelliJ IDEA plugin for Claude Code (like VS Code extension) (#13120) | GitHub anthropics/claude-code 이슈 | 2025-12-05 (2025-12-08 중복 종료) | https://github.com/anthropics/claude-code/issues/13120 |
| S21 | IME Composition Input Rendering Lag for Non-Latin Scripts (#1553) | GitHub anthropics/claude-code 이슈 | 2025-06-04 (같은 날 중복 종료) | https://github.com/anthropics/claude-code/issues/1553 |
| S22 | Commands (`/ide`) | Anthropic (Claude Code Docs) | 작성일 확인 불가 (상시 갱신, 2026-10-30 조회) | https://code.claude.com/docs/en/commands |
