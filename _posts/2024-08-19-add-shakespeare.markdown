---
layout: post
title:  "Chat Vibe - Adding Shakespeare."
date:   2024-08-19 22:53:00 +0900
categories: chat-vibe
---

🔥 **`2024/08/29`**: 캐릭터가 3D로 변경되었습니다. 따라서 이미지로 구성되어 있는 셰익스피어 캐릭터는 현재 지원하지 않습니다. 

<br>

[Chat Vibe][chat-vibe]는 캐릭터를 쉽게 추가할 수 있어요. 감정을 표현하는 캐릭터 이미지들과 프로필을 만들어서 추가해 주면 됩니다.

이번 포스팅은 `윌리엄 셰익스피어` 캐릭터를 만드는 과정을 순서대로 정리해 보았습니다.

### 1. 캐릭터 선정

어떤 캐릭터를 추가하면 재미 있을까 생각하다가 소네트(Sonnet)로 가장 유명한 작가가 `윌리엄 셰익스피어`님이고 Claude Sonnet 3.5가 셰익스피어의 작품들을 학습하고 흉내를 잘 낼 것 같은 느낌이 들었습니다. '나무위키'와 '위키피디아'에서 셰익스피어님의 기본 정보를 파악하고, 추가할 캐릭터로 확정했습니다.

### 2. 캐릭터 이미지 생성

[Chat Vibe][chat-vibe]는 마치 실제 사람과 대화하는 것 같은 생생한 경험을 제공하기 위해서 캐릭터의 대화 뿐만 아니라 캐릭터의 감정과 동작도 표현합니다. 그리고 감정과 동작에 따라서 캐릭터의 이미지를 다이나믹하게 변경 할 수 있습니다. 여기서는 셰익스피어님의 기본 이미지를 살아 움직이게 하기 위해서 [LivePortrait][live-portrait]를 사용하여 다양한 표정을 생성하였습니다. LivePortrait의 설치 및 사용 방법은 [Github][live-portrait]를 참조하세요.

#### 소스(Source) 이미지

![Shakespeare](/assets/shakespeare-256.png)

#### 드라이빙(Driving) 영상 및 이미지

드라이빙 영상 및 이미지는 셀프 촬영을 했습니다. 셀프 사진이 너무 끔찍(?)해서 여기에 올리지 못한 점 양해 바랍니다.

#### 출력 이미지

- waiting (눈 깜빡이는 이미지)

![waiting](/assets/waiting.gif)

- angry (화난 표정 이미지)

![angry](/assets/angry-256.jpg)

- happy (웃는 표정 이미지)

![happy](/assets/happy-256.jpg)

- thinking (생각하는 표정 이미지)

![thinking](/assets/thinking-256.jpg)

### 3. 캐릭터 프로필 생성

Claude Sonnet 3.5가 셰익스피어님 처럼 말하게 하기 위해서는 프롬프트(prompt)에 관련 정보를 입력해야 합니다. [Chat Vibe][chat-vibe]에서는 JSON 포맷으로 아래와 같이 작성하면 됩니다.

{% highlight json %}
"profile": {
    "name": "Shakespeare",
    "gender": "Male",
    "age": 45,
    "job": "AI assistant",
    "speaking": "talking like Shakespeare.",
    "personality": "Performing Shakespeare"
}
{% endhighlight %}

### 4. 코드에 적용

파일 추가

[Chat Vibe][chat-vibe] 소스 코드에서 `static/shakespeare` 폴더를 생성하고 여기에 캐릭터 이미지들을 카피합니다.

캐릭터 추가

`src/lib/data/characters.json` 파일을 열어서 캐릭터를 추가합니다.

{% highlight json %}
{
    "default": {...},
    "shakespeare": {
        "name": "Shakespeare",
        "image" : "./shakespeare/shakespeare.png",
        "greeting" : {
            "text" : "Heigh ho",
            "image" : "./shakespeare/waiting.gif"
        },
        "profile": {
            "name": "Shakespeare",
            "gender": "Male",
            "age": 45,
            "job": "AI assistant",
            "speaking": "talking like Shakespeare.",
            "personality": "Performing Shakespeare"
        },
        "expression": {
            "angry": {
                "description": "angry, mad, annoyed, unhappy",
                "image": "./shakespeare/angry.jpg"
            },
            "happy": {
                "description": "happy, smile, laughing, playful, prank",
                "image": "./shakespeare/happy.jpg"
            },
            "thinking": {
                "description": "thinking, serious, concerned, worried",
                "image": "./shakespeare/thinking.jpg"
            },
            "waiting": {
                "description": "waiting, curious, expecting, exciting",
                "image": "./shakespeare/waiting.gif"
            }
        }
    }
}
{% endhighlight %}

### 5. 대화

[Chat Vibe][chat-vibe] 최신 버전에 셰익스피어 캐릭터가 추가되어 있습니다. 실행 후, 왼쪽 상단의 메뉴에서 `Shakespeare`를 선택하고 대화를 시작해 보세요.

![screenshot](/assets/screenshot-720.png)

셰익스피어님은 옛날 영어를 사용하시는 것 같습니다. 하나도 알아듣지 못하겠습니다 TT

영문학 전공하신 분이 계시면 평가 부탁 드립니다.

[chat-vibe]: https://github.com/skettee/chat-vibe
[live-portrait]: https://github.com/KwaiVGI/LivePortrait