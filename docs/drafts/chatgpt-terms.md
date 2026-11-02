# 챗GPT 용어 뜻 15가지 총정리

> 💡 **한 줄 요약:** 챗GPT 용어는 기본 개념 5개, 답의 품질 4개,
> 기능 6개로 나누면 한 번에 정리됩니다.

[IMAGE: 썸네일 | 설명: 챗GPT 용어 뜻 15가지 총정리 대표 이미지]

안녕하세요, 여러분!
결론부터 말씀드리면, **챗GPT 용어**는
기본 개념 5개, 답의 품질을 좌우하는 4개,
기능 이름 6개로 묶어 보면 훨씬 쉽게 들어옵니다.

설명 글을 읽다 보면 토큰, 할루시네이션, GPTs 같은 말이
한꺼번에 나와서 막막하셨죠?
GPT와 GPTs가 같은 말인지 묻는 분도 꽤 많더라고요.
저도 처음엔 이름이 비슷한 기능끼리 자꾸 섞어 불렀어요.

오늘은 꼭 알아야 할 15개 용어를 묶음별로 쉽게 풀고,
헷갈리는 짝은 표로 구분해 드리겠습니다.
기능 이름과 일정은 2026년 11월 2일 기준으로
OpenAI 발표와 관련 보도를 확인해 정리했습니다.

---

## 1. 챗GPT 기본 용어 5가지는 무엇일까?

챗GPT를 처음 쓸 때 가장 먼저 만나는 말들입니다.
이 다섯 가지만 알아도 설명 글이
훨씬 덜 낯설게 느껴지실 거예요.

| 용어 | 뜻 한 줄 |
| :--- | :--- |
| **LLM** | 많은 글을 배워 다음 말을<br>예측하는 언어 모델 |
| **GPT** | 오픈AI가 만든 LLM 시리즈 이름 |
| **프롬프트** | 내가 챗GPT에게 보내는 요청 문장 |
| **토큰** | AI가 글을 잘게 나눠 처리하는 단위 |
| **컨텍스트 창** | 한 대화에서 AI가 한 번에<br>참고하는 기억 공간 |

**LLM**은 대규모 언어 모델(Large Language Model)의 줄임말입니다.
엄청난 양의 글을 학습해서
앞뒤 문맥에 어울리는 다음 말을 이어 붙이는 방식으로 답을 만들죠.
**GPT**는 그중 오픈AI가 만든 모델 시리즈를 부르는 이름이고,
챗GPT는 이 모델을 대화창으로 쓰게 만든 서비스입니다.

[IMAGE: 다이어그램 | 설명: LLM, GPT, 챗GPT의 관계: 언어 모델에서 대화 서비스까지]

**프롬프트**는 거창한 말 같지만 결국 내가 입력하는 요청입니다.
"보고서 써 줘"보다 "회의 내용을 세 줄로 요약해 줘"처럼
목적과 형식을 구체적으로 적을수록 원하는 답에 가까워집니다.

**토큰**은 단어나 글자 조각 단위라서
같은 글도 언어에 따라 개수가 달라집니다.
**컨텍스트 창**은 이 토큰으로 크기를 재는데요.
대화가 길어져 이 공간을 넘으면
앞쪽 내용부터 흐려지거나 요약되어 밀려납니다.

저도 긴 대화 중에 처음 정해 둔 조건을
챗GPT가 잊은 듯해서 당황한 적이 있어요.
같은 일을 겪었다는 글이 꽤 많더라고요.

[IMAGE: 포인트카드 | 설명: 챗GPT 기본 용어 프롬프트, 토큰, 컨텍스트 창 한눈에 보기]

> 📌 **전문가 Tip:** 대화가 너무 길어졌다면
> 지금까지 내용을 요약해 달라고 한 뒤,
> 그 요약을 새 대화에 붙여 넣고 이어 가 보세요.

---

## 2. 답의 품질을 좌우하는 용어 4가지는?

기본 용어가 익숙해졌다면 이제 답이 맞는지,
얼마나 깊은지를 가르는 말을 알아볼 차례입니다.
이 네 가지는 결과를 믿고 써도 될지 판단하는 데 직접 쓰입니다.

| 용어 | 뜻 한 줄 |
| :--- | :--- |
| **할루시네이션** | 그럴듯하지만 사실이 아닌 답 |
| **추론** | 답하기 전에 단계를 나눠<br>더 오래 생각하는 방식 |
| **검색** | 웹에서 최신 정보를 찾아<br>출처와 함께 답하는 기능 |
| **딥 리서치** | 여러 자료를 찾아 읽고<br>보고서로 정리하는 기능 |

**할루시네이션**(환각)은 챗GPT가 모르는 내용을
아는 것처럼 지어내는 현상입니다.
모델이 사실을 찾아보는 대신 그럴듯한 다음 말을 예측하기 때문에
생기는 일이라, 말투만 보고는 구분하기 어렵습니다.

특히 많이 겪는 건 출처입니다.
저도 참고 논문을 알려 달라고 했다가
제목과 저자까지 그럴듯한데 찾아보니 없는 자료를 받은 적이 있어요.
도서관 안내문과 연구에서도 자주 경고하는 사례더라고요.

그래서 출처와 중요한 수치는 원문에서 직접 확인하고,
최신 정보는 검색 기능으로 묻는 습관이 필요합니다.
챗GPT에게 맞는지 다시 물어보는 것만으로는
부족하다는 연구 결과도 있으니 참고해 주세요.

[IMAGE: 포인트카드 | 설명: 챗GPT 할루시네이션을 줄이는 확인 습관 3가지]

**추론**은 수학, 코딩, 복잡한 비교처럼
단계가 많은 질문에 강한 방식입니다.
모델 메뉴에서 빠른 답부터 깊이 생각하는 단계까지 고를 수 있는데요.
메뉴 이름과 모델은 요금제와 시기에 따라 자주 바뀌니
내 화면에서 확인하시는 편이 정확합니다.

**검색**은 최신 소식이나 가격처럼 바뀌는 정보를 물을 때 씁니다.
**딥 리서치**는 검색을 여러 번 반복해 자료를 모으고,
출처가 달린 긴 보고서로 정리해 주는 기능이라
간단한 질문보다 조사 과제에 어울립니다.

---

## 3. 챗GPT 기능 용어 6가지는 무엇일까?

여기부터는 챗GPT를 내 작업에 맞게 쓰는 기능 이름들입니다.
처음부터 다 설정할 필요는 없고,
뜻만 알아 두셨다가 필요할 때 하나씩 켜 보시면 됩니다.

| 용어 | 뜻 한 줄 |
| :--- | :--- |
| **메모리** | 대화에서 알게 된 내 정보를<br>기억해 다음 답에 반영 |
| **맞춤 설정** | 말투와 답 형식을<br>내가 직접 적어 두는 지시문 |
| **임시 채팅** | 기록에 남지 않고<br>새 메모리도 만들지 않는 대화 |
| **프로젝트** | 대화, 파일, 지침을<br>주제별로 묶는 폴더 |
| **GPTs** | 특정 작업용으로 만든<br>맞춤형 챗GPT |
| **에이전트** | 답 대신 여러 단계의 일을<br>직접 해 주는 AI |

**메모리**는 챗GPT가 스스로 쌓는 기억이고,
**맞춤 설정**은 내가 직접 적는 규칙입니다.
메모리에 무엇이 저장됐는지는 설정에서 보고 지울 수 있고,
기능 자체를 끌 수도 있습니다.

**임시 채팅**은 민감한 내용을 물어볼 때 좋습니다.
대화 기록에 남지 않고, 오픈AI는 모델 학습에도 쓰지 않는다고 안내합니다.
**프로젝트**는 폴더 안 대화에만 지침과 파일이 적용되어
주제가 섞이지 않게 해 주죠.

[IMAGE: 포인트카드 | 설명: 챗GPT 기능 용어 메모리, 맞춤 설정, 임시 채팅, 프로젝트 정리]

**GPTs**는 큰 변화가 있는 용어입니다.
오픈AI는 2026년 9월에 GPTs를 종료하고
플러그인으로 옮기겠다고 발표했고,
보도에 따르면 기본 종료일은 2026년 12월 11일입니다.
직접 만든 GPTs가 있다면 일정을 계정 안내에서 꼭 확인해 보세요.

**에이전트**는 사이트를 오가며 자료를 모아 표로 만드는 것처럼
여러 단계의 일을 대신 처리하는 AI를 말합니다.
지금 챗GPT에서는 Work가 이 역할을 맡고 있습니다.

---

## 4. 헷갈리는 챗GPT 용어는 어떻게 구분할까?

가장 많이 묻는 건 메모리, 맞춤 설정, 프로젝트의 차이입니다.
셋 다 무언가를 기억해 두는 기능처럼 보이는데요.
누가 정하고 어디까지 적용되는지로 나누면 쉽게 구분됩니다.

| 기능 | 누가 정하나 | 적용 범위 |
| :--- | :--- | :--- |
| **메모리** | 챗GPT가<br>대화에서 저장 | 여러 대화 전체 |
| **맞춤 설정** | 내가 직접 작성 | 모든 대화 |
| **프로젝트** | 내가 폴더별로 작성 | 그 폴더 안 대화만 |

[IMAGE: 비교표 | 설명: 챗GPT 메모리, 맞춤 설정, 프로젝트 차이 비교]

하나 더 헷갈리는 짝은 GPT와 GPTs입니다.
**GPT**는 모델 이름이고, **GPTs**는 그 모델 위에
지침과 파일을 얹어 만든 맞춤형 챗봇이에요.
이름은 한 글자 차이지만 가리키는 대상이 전혀 다릅니다.

하지만 중요한 건 용어를 다 외우는 것이 아니라
**내 상황에 맞는 기능을 고르는 것**이겠죠.
늘 같은 말투를 원하면 맞춤 설정,
주제별로 자료를 모아 쓰려면 프로젝트부터 시작해 보세요.

---

## 5. 마무리

오늘은 챗GPT 용어 15가지를
기본 개념, 답의 품질, 기능의 세 묶음으로 알아보았습니다.
토큰과 컨텍스트 창은 대화 길이를,
할루시네이션은 답을 확인하는 습관을 기억하시면 충분합니다.

모르는 말이 나올 때마다 이 표를 한 번씩 꺼내 보세요.
단어 하나를 이해하면 기능 하나가 훨씬 가깝게 느껴지는 법이죠!
챗GPT를 더 편하게 쓰는 데 도움이 되었기를 바랍니다.

여러분은 어떤 용어가 가장 헷갈리셨나요?
궁금한 점은 언제든 댓글로 남겨주세요. 감사합니다!

[IMAGE: 포인트카드 | 설명: 챗GPT 용어 15가지 세 묶음 요약]

---

<!-- 아래는 발행 메타 정보입니다. 본문에 붙여넣지 않습니다. -->

**태그:** `#챗GPT용어 #ChatGPT #챗GPT사용법 #할루시네이션 #프롬프트 #토큰 #챗GPT메모리 #GPTs`

<!-- 글 유형: A 정보·리뷰형 / 메인 키워드: 챗GPT 용어 (세부 의도: 용어 뜻)
검색 의도: 챗GPT를 쓰다 마주치는 토큰, 할루시네이션, GPTs, 메모리 같은 용어의 뜻을 한 번에 쉽게 알고 싶다.

경험 문장 근거 (style-guide 10장)
- 도입 "GPT와 GPTs가 같은 말인지 묻는 분이 많다 / 비슷한 기능끼리 섞어 불렀다":
  https://www.magicaiprompts.com/docs/chatgpt/what-is-gpt (GPT가 모델과 맞춤형 챗봇 두 뜻으로 쓰임) ,
  https://www.gpters.org/hello/post/g-wide-shallow-broad-MmkHCNM6tTah0Q6 ,
  https://memx.app/blog/chatgpt-memory-vs-instructions-vs-projects/ (메모리·맞춤 설정·프로젝트 혼동)
- 1장 "긴 대화에서 처음 정한 조건을 잊은 듯했다 / 같은 일을 겪은 글이 많다":
  https://www.pcworld.com/article/3168543/chatgpt-forgets-things-in-long-threads-heres-the-fix.html ,
  https://memx.app/fix/chatgpt-forgets-previous-messages/ ,
  https://www.memorylake.ai/blogs/chatgpt-forgets-earlier-in-the-conversation ,
  https://evermind.ai/blogs/why-chatgpt-forgets-context
- 2장 "참고 논문을 물었더니 존재하지 않는 자료를 받았다 / 도서관·연구에서 자주 경고":
  https://pmc.ncbi.nlm.nih.gov/articles/PMC10484980 ,
  https://researchlibrary.lanl.gov/posts/beware-of-chat-gpt-generated-citations/ ,
  https://libanswers.royalroads.ca/faq/213154 ,
  https://chipstreet.com/2023/07/18/i-asked-chatgpt-to-provide-citations-it-hallucinated-its-sources/

사실 확인 (세션 네트워크에서 help.openai.com 접속이 막혀 검색 결과 요약으로 교차 확인)
- LLM·GPT·토큰·컨텍스트 창·할루시네이션 정의: https://wikidocs.net/436624 , https://ai-toolbox.co/chatgpt-glossary , https://coddy.tech/docs/ko/prompts/ai-hallucination
- 긴 대화 요약 후 새 대화로 옮기기: https://memx.app/fix/chatgpt-forgets-previous-messages/ , https://www.pcworld.com/article/3168543/chatgpt-forgets-things-in-long-threads-heres-the-fix.html
- 모델 메뉴에서 생각 깊이 선택, 요금제별 모델 차이: https://help.openai.com/en/articles/20001354-gpt-6-and-other-models-in-chatgpt , https://www.datastudios.org/post/chatgpt-all-models-currently-available-complete-guide-updated-mid-2025
- 딥 리서치(여러 단계 웹 조사, 출처 달린 보고서): https://openai.com/index/introducing-deep-research/ , https://en.wikipedia.org/wiki/ChatGPT_Deep_Research
- 메모리 보기·삭제·끄기, 맞춤 설정과의 구분, 임시 채팅(기록·메모리·학습 제외):
  https://openai.com/ko-KR/index/memory-and-new-controls-for-chatgpt/ ,
  https://www.digitalmarketer.co.kr/class/chatgpt-astra-basics/chatgpt-memory-and-custom-instructions
- 프로젝트(폴더별 파일·지침): https://academy.openai.com/public/clubs/work-users-ynjqu/resources/projects , https://findskill.ai/blog/chatgpt-projects-explained-2026/
- GPTs 종료(2026.9.11 발표, 기본 종료일 2026.12.11, 플러그인으로 이전):
  https://virtualizationreview.com/articles/2026/09/28/openai-to-retire-custom-gpts-replace-them-with-plugins.aspx ,
  https://www.edtechinnovationhub.com/news/openai-to-retire-custom-gpts-in-december-as-creators-move-to-plugins ,
  https://ai.utah.edu/blog/posts/2026/guidance-custom-gpt-migration.php
- 에이전트 → Work: 기존 글 chatgpt-agent-meaning-usage.md의 사실 확인 메모와 동일
-->
