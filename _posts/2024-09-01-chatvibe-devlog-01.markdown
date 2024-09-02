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

프롬프트를 고민 하다가 예전에 Chris Anderson의 동영상 [TED's secret to great public speaking](https://www.ted.com/talks/chris_anderson_ted_s_secret_to_great_public_speaking?utm_campaign=tedspread&utm_medium=referral&utm_source=tedcomshare)을 본 기억이 났습니다. 그분이 제시한 가이드라인을 참고로 해서 아래와 같이 프롬프트를 만들어서 "Gradient Descent(경사하강법)"을 주제로 테스트를 시도 했습니다. 경사하강법은 손실 함수(Loss function)의 최소값을 찾는 방법으로서, 딥러닝 학습을 위한 중요한 알고리즘입니다. 과연 일반인이 이해할 수 있도록 TED스럽게 말할 수 있을까요?

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

![chatgpt](/assets/chatgpt-response.png)


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
GPT-4o와 Claude Sonnet 3.5에서 테스트 해 보았고, 말하는 능력과 감정 표현은 Claude가 더 우수했습니다. 그래서 메인 LLM을 Claude로 변경하였습니다.

![claude](/assets/claude-response.png)

기쁨과 흥분도 잠시... 다양한 질문을 던져서 대답을 확인하는 중에 심각한 문제점을 발견했습니다. 그것은 바로 캐릭터가 "거짓말"을 한다는 것입니다!

### 믿을 수 있는 정보 제공

제가 기획한 챗봇은 판타지한 대화가 아니라 정확한 정보를 쉽고 친근하게 알려주는 것입니다. 그래서 캐릭터가 거짓말을 하는 문제는 반드시 해결이 되어야 했습니다.

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




