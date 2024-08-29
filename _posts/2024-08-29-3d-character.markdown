---
layout: post
title:  "Chat Vibe - 3D Character for the good vibes."
date:   2024-08-29 00:32:00 +0900
categories: chat-vibe
---

자연스러운 캐릭터의 움직임과 표정 변화를 구현하기 위해서 캐릭터를 3D로 변경하였습니다.

![expression](/assets/expression.gif)

3D 라이브러리는 [three.js](https://threejs.org/)와 [three-vrm](https://github.com/pixiv/three-vrm)를 사용하였고 표정은 VRM(VR용 인간형 3D 모델링 파일 포맷)에서 제공하는 기본 Expression을 사용하여 구현하였습니다.

## 1. 사용된 소프트웨어

- [VRoid Studio](https://vroid.com/en/studio): 인간형 3D 모델링 무료 소프트웨어. 모델링 지식이 없어도 쉽게 캐릭터를 제작할 수 있습니다.
- [Blender 4.1](https://www.blender.org/): 무료 3D 컴퓨터 그래픽 제작 소프트웨어. 최신 버젼은 기존 플러그인을 사용할 수 없어서 4.1을 사용하였습니다.
- [Mixamo](https://www.mixamo.com/): 3D 캐릭터의 다양한 동작을 다운 받을 수 있는 사이트입니다.
- [VRM Add-on for Blender][VRM Add-on for Blender]: 블렌더에서 VRM 파일을 사용하기 위한 플러그인.
- [Rokoko Blender Plugin][Rokoko Blender Plugin]: 애니메이션 리타겟팅을 위한 블렌더 플러그인.

## 2. 캐릭터 생성

VRoid Studio에서 캐릭터를 생성하고 VRM 파일로 저장합니다.

## 3. 동작 애니메이션 생성

- 사용할 애니메이션을 Mixamo에서 선택하여 다운로드 합니다.
- Blender를 열고 생성한 VRM 캐릭터를 불러옵니다.
- Mixamo에서 다운받은 애니메이션을 불러옵니다.
- Rokoko의 [Retargeting][Retargeting]을 사용하여 VRM 캐릭터에 애니메이션을 적용합니다.
- 애니메이션이 적용된 캐릭터를 VRMA(VRM 애니메이션 파일 포멧)으로 저장합니다.

## 4. 표정 애니메이션 생성

- Blender를 열고 생성한 VRM 캐릭터를 불러옵니다.
- Expressions(Object > VRM > Expressions)에서 표정 컨트롤을 사용해서 애니메이션을 제작합니다.
- 표정 애니메이션이 적용된 캐릭터를 VRMA(VRM 애니메이션 파일 포멧)으로 저장합니다.

## 5. 클립 생성
- three.js, three-vrm 라이브러리를 사용해서 생성한 애니메이션(VRMA)을 [AnimationClip][AnimationClip]으로 변환합니다.
- 애니메이션 클립들을 JSON파일로 저장합니다.

## 6. 적용
- 캐릭터 VRM 파일과 애니메이션 클립 JSON 파일을 `static/models/`에 카피합니다.
- `characters.json` 파일에 캐릭터 정보와 애니메이션 정보를 추가합니다.

이제 자연스러운 캐릭터 AI와 즐겁게 채팅을 시작해 보세요!

[VRM Add-on for Blender]: https://vrm-addon-for-blender.info/en/
[Rokoko Blender Plugin]: https://github.com/Rokoko/rokoko-studio-live-blender
[Retargeting]: https://github.com/Rokoko/rokoko-studio-live-blender#retargeting
[AnimationClip]: https://threejs.org/docs/#api/en/animation/AnimationClip