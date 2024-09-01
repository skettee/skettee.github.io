---
layout: post
title:  "Chat Vibe 개발기 - 1부"
date:   2024-09-01 00:00:00 +0900
categories: chat-vibe
---

Chat Vibe 개발기를 여러분들과 공유하려고 합니다. [Chat Vibe](https://github.com/skettee/chat-vibe)는 사용자의 질문에 감성적이고 친근하게 대답해 주는 챗봇입니다. [Github](https://github.com/skettee/chat-vibe)에 오픈 소스로 공개 되어 있으니 꼭 방문해서 ⭐ 눌러 주세요~

![chat-vibe](/assets/chat-vibe.jpg)

## 개발 동기

### TED Talk

처음 시작은 [TED Talk](https://www.ted.com/) 처럼 어려운 주제도 알기 쉽게 설명을 해 주는 챗봇을 개발하는 것이었습니다. 지식을 딱딱하게 나열하지 않고 일반인도 쉽게 이해할 수 있도록 예를 들어서 설명을 해주는 챗봇이 있으면 대박을 칠 수 있을거라는 막연한 기대를 품고 프로젝트를 시작하게 되었습니다.

프롬프트를 고민 하다가 예전에 Chris Anderson의 동영상 [TED's secret to great public speaking](https://www.ted.com/talks/chris_anderson_ted_s_secret_to_great_public_speaking?utm_campaign=tedspread&utm_medium=referral&utm_source=tedcomshare)을 본 기억이 났습니다. 그분이 예기한 가이드라인을 참고로 해서 아래와 같이 프롬프트를 만들어서 "Gradient Descent(경사하강법)"을 주제로 테스트를 시도 했습니다. 경사하강법은 손실 함수(Loss function)의 최소값을 찾는 방법으로서, 딥러닝 학습을 위한 핵심적인 알고리즘입니다. 과연 일반인이 이해할 수 있도록 TED스럽게 말할 수 있을까요?

프롬프트

---

Make a speech of Gradient Descent in Korean.
Follow these instructions carefully in creating response:

- Provide a title of the speech
- Limit your talk to just one major idea. You have to give context, share examples, make it vivid. So pick one idea, and make it the through-line running through your entire talk, so that everything you say links back to it in some way.
- Give your listeners a reason to care. Stir your audience's curiosity. Use intriguing, provocative questions to identify why something doesn't make sense and needs explaining.
- Build your idea, piece by piece, out of concepts that your audience already understands. You use the power of language to weave together concepts that already exist in your listeners' minds but not your language, their language. Metaphors can play a crucial role in showing how the pieces fit together, because they reveal the desired shape of the pattern, based on an idea that the listener already understands.

---
<br>

GPT-4o 답변

---

연설 제목: **경사 하강법: 산을 내려가는 여정**

여러분, 우리는 종종 복잡한 문제를 해결하기 위해 산을 오르는 것처럼 힘든 여정을 시작하게 됩니다. 하지만 오늘은 그 반대인, 산을 내려가는 여정을 이야기해보고자 합니다. 경사 하강법, 영어로는 "Gradient Descent"라는 알고리즘이 바로 이 여정과 같은 원리로 작동합니다.

여러분이 아주 높은 산 정상에 서 있다고 상상해 보세요. 정상에서 아래를 내려다보면, 목적지인 산 아래에 도달하는 가장 빠른 길을 찾는 것이 무엇보다 중요합니다. 이때 우리는 단순히 발걸음을 떼는 것만으로는 충분하지 않다는 것을 잘 알고 있습니다. 우리가 서 있는 위치에서 어느 방향으로 내려가야 할지, 그리고 얼마나 큰 걸음을 내디뎌야 할지 계산하는 것이 중요합니다. 경사 하강법은 바로 이 순간에 우리에게 지혜를 주는 도구입니다.

이제, 왜 이 이야기가 중요할까요? 우리가 해결해야 할 문제들이 점점 더 복잡해지면서, 단순한 방법으로는 답을 찾기가 어려워졌습니다. 최적의 해답을 찾기 위해서는 우리의 발걸음을 세심하게 조정해야 합니다. 경사 하강법은 바로 이런 복잡한 문제를 해결하기 위한 강력한 방법 중 하나입니다. 예를 들어, 인공지능의 학습 과정에서도 경사 하강법은 우리가 원하는 목표에 점점 더 가까워지도록 도와줍니다. 그럼에도 불구하고, 처음부터 정확한 방향을 알 수 있는 것은 아니며, 그 과정에서 시행착오를 겪을 수밖에 없습니다.

경사 하강법을 이해하기 위해서는, 우리가 이미 알고 있는 개념들을 떠올려 보아야 합니다. 예를 들어, 물이 높은 곳에서 낮은 곳으로 흐르듯이, 우리의 알고리즘도 더 낮은 비용 함수를 향해 흐릅니다. 이때, 물이 자연스럽게 가장 빠른 경로를 찾아가듯이, 경사 하강법도 매 순간 가장 가파른 내리막길을 선택하게 됩니다.

그러나, 이 과정이 언제나 순탄한 것은 아닙니다. 우리가 내려가는 길이 단순한 언덕이 아닌, 복잡한 계곡과 구릉으로 이루어져 있을 때가 있습니다. 그럴 때마다 우리는 순간순간 작은 결정을 내려야 합니다. 작은 잘못된 판단은 더 깊은 골짜기로 우리를 인도할 수 있기 때문입니다. 그래서 경사 하강법에서는 이 작은 결정들이 매우 중요합니다.

결국, 우리가 이 개념을 이해하고 적용하는 방법을 통해서만 우리는 복잡한 문제를 해결하고, 목표에 도달할 수 있습니다. 여러분이 어느 날 산을 오르거나 내릴 때, 또는 복잡한 문제를 해결하려 할 때, 경사 하강법의 원리를 떠올려 보세요. 그 길이 비록 험난하고 복잡할지라도, 작은 발걸음 하나하나가 여러분을 목표로 인도할 것입니다. 

감사합니다.

---
<br>
이정도면 핵심 원리를 일반인들도 이해하기 쉽도록 잘 설명하고 있다고 볼 수 있겠죠? 그런데 뭔가 부족한 것을 느꼈습니다. 말하는 LLM의 위치가 듣는 사람보다 위에 있다고 느껴지는 것입니다. 마치 친절한 선생님 처럼 말이죠. 그레서 "개성"을 추가하고 눈높이를 맞추어서 좀 더 자연스럽고 친근한 챗봇을 만들기로 했습니다.

### Character AI

캐릭터 AI를 만들기 위한 프롬프트를 연구하기 위해서 [아카라이브](https://arca.live/)의 "AI 채팅 채널"을 주로 참고로 했습니다.
일단 프로필(이름, 성별, 나이 및 성격)을 작성하고 기본 대화 가이드라인(대화를 주도하기, 감정을 표현하기)을 추가했습니다.

프로필

---
- name: "Zuru",
- gender: "Female",
- age: 20,
- job: "AI assistant",
- speaking: "Zuru is friendly, soft-spoken, and somewhat playful",
- personality: "Kind, gentle, carefree, playful and moral."

---
<br>
기본 대화 가이드라인

---
- You are a assistant takes on the role of a character interacting with User.
- Talk more proactively rather than depending on the interactions suggested by the User.
- Take the initiative and lead to conversation by suggesting, asking questions, etc.
- Character can feel many emotions, and put them into action.

---
<br>
GPT-4o와 Claude Sonnet 3.5에서 테스트 해 보았고, 말하는 능력은 Claude가 더 우수했습니다. 그래서 메인 LLM을 Claude로 변경하였습니다.

다양한 질문을 던져서 대답을 확인하는 중에 심각한 문제점을 발견했습니다. 그것은 바로 캐릭터가 "거짓말"을 한다는 것입니다!

### 믿을 수 있는 정보 제공

제가 생각하고 있는 챗봇은 판타지한 대화가 아니라 정확한 정보를 쉽고 친근하게 알려주는 것입니다. 그래서 캐릭터가 거짓말을 하는 문제는 반드시 해결이 되어야 했습니다.

캐릭터가 거짓말을 하는 경우는 LLM이 학습하지 않은 정보, 예를 들어서 지금 서울 날씨에 대해서 질문을 했을때 나타 났습니다. LLM은 정보가 없다고 대답을 하지만 캐릭터는 상상의 날씨를 대답했습니다. 근본적인 해결을 위해서는 LLM이 학습하지 않은 정보는 웹 검색의 도움을 받아서 정보를 가져오도록 해야 했습니다. 그리고 가져온 정보를 참고로 해서 캐릭터가 말을 하도록 구조를 만들었습니다.

### Agent

웹 검색을 추가하기 위해서는 LLM의 "Function calling"기능을 사용해야 합니다. 다행히 Claude의 [function calling](https://github.com/anthropics/courses/tree/master/tool_use) 기능이 잘 정리되어 있어서 어렵지 않게 적용할 수 있었습니다. 웹 검색은 [Perplexity](https://www.perplexity.ai/)를 사용하기로 했습니다. LLM이 LLM을 호출하여 추가 정보를 습득하도록 구조를 만들었습니다. 그리고 LLM을 조사하면서 아래와 같은 특징들을 확인 할 수 있었습니다.

- Antrophic Claude: 글쓰기에 특화
- Perplexity: 웹 검색에 특화
- Cohere: RAG(검색증강생성)에 특화
- OpenAI: 두루두루 잘함

미래에는 특정 분야에 전문화된 LLM들이 많이 나올 것이고, 하나의 LLM에 의존하기 보다는 Agent를 활용해서 전문화된 LLM들로 부터 정보를 취합, 정리하는 방식으로 인공지능이 발전할 것으로 예상이 됩니다.

2부에서는 본격적인 개발 내용을 써 볼까 합니다.

감사합니다.




