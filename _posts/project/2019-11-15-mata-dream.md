---
layout: post
title:  "[Vanillacoding]project-2-mata-dream"
date:   2019-11-15
excerpt: "바닐라코딩 부트캠프 2차 프로젝트"
project: true
tag:
- react-native
- socket
- express
- aws
- mongodb
comments: false
---

# MATA-DEREAM!

## Intorduction

- **MATA-DEREAM** 은 한강 공원에 자리 잡은 사람에게 그 자리를 구매하는 가상 앱입니다.
- react-native, expo를 사용하여 앱을 구현하였습니다.

<br>[![Video Label](http://img.youtube.com/vi/e6tEy4qXAHI/0.jpg)](https://www.youtube.com/watch?v=e6tEy4qXAHI) 

## Content

- [Requirements](#Requirements)
- [Installation](#Installation)
- [Features](#Features)
- [Skills](#Skills)
- [Test](#Test)
- [Deployment & Continuous Integration](#Deployment-&-Continuous-Integration)
- [Project Control](#Project-Control)
- [Challenges](#Challenges)
- [Things To Do](#Things-To-Do)
- [Sincere Thanks](#Sincere-Thanks)

## Requirements

- 모바일 앱 어플입니다.
- 웹으로 구동하시려면 Xcode, simulator가 설치 되있어야합니다
- 모바일 위치 서비스를 켜시고 시작하여야 앱에서 위치 정보를 읽을 수 있습니다.

## Installation

```javascript
git clone https://github.com/Kyounghwan01/mata-dream-server.git
cd mataDream-server
yarn install
yarn ios or yarn start

git clone https://github.com/Kyounghwan01/mata-dream-app.git
cd mataDream-app
yarn install
yarn start

```

## Features

- Facebook login
- JSON Web Token Authentication
- 로그아웃
- 공원 리스트 페이지
- 공원 별 자리 판매 위치 확인
- 사진 저장, 카메라, 앨범 접근
- 공원 별 자리 등록, 삭제 기능
- 실시간 채팅, 교환 기능

## Skills

### Client-Side

- ES2015+
- react-native
- react-navigation
- Expo

### Server-Side

- Node.js
- Express
- ES2015+
- JSON Web Token Authentication
- MongoDB
- Mongoose
- Atlas

## Test

- Reducer Unit Test (Jest)
- Component Unit Test (Jest, Enzyme)
- e2e (detox) : 여러 시도했으나 `expo` 지원 중지로 인하여 실패
  - 실행까지는 성공했으나, detox가 element를 인식하지 못하여 클릭 및 타이핑 불가
  - https://github.com/wix/Detox/blob/master/docs/Guide.Expo.md

## Deployment & Continuous Integration

### Client

- Google Play Store 배포 (예정)

### Server

- AWS Elastic beanstalk를 통해 서비스 배포
- CircleCI를 통한 배포 자동화

## Project Control

- Git Branch 활용
- Trello 활용한 Task Management

## Challenges

### react-native 특징 파악

- `react-navigation`의 `createSwitchNavigator`, `createBottomNavigator`, `createAppContainer` 사용법을 자세히 보았습니다.
  - 결론으로 위 네비게이션을 통해 이미 짜여진 구조에서는 새로 추가하는 것이 매우 어렵다는 것을 알았습니다.
  - 그에 따라 화면 구조를 먼저 배치하고 내부를 채워 넣는 방법으로 개발을 진행하였습니다.

### 실시간 채팅, 정보 교환

- `socket.io`를 이용하여 상대방과 채팅하였습니다.
- 상대방의 행동에 따라 실시간으로 다른 반응 도출
  - 교환 수락시, 본인에게 대기 이벤트, 상대방에게는 상대방이 교환 수락 알림 이벤트
  - 교환 거부시, 상대방에게 거부 이벤트
  - 판매자 채팅방에 구매자 1 접근시, 실시간으로 구매자 2 접근 못하도록 이벤트
- `socket`은 해당 컴포넌트를 벗어나면 `disconnect, room leave`를 해줘야 다음 컴포넌트에 영향을 주지 않는데, `react-native`의 경우 componentWillUnMount를 해도 `socket`이 끊기지 않았습니다. 결론은 `navigation` prop에 `addListener('didBlur', callback)`에 화면을 벗어나면 나오는 이벤트를 callback에 넣어서 해결하였습니다.
- AWS에 서버를 배포한 이후에는 실시간 기능이 매우 느려졌습니다 (local 서버가 1초라면 배포 서버는 5초 정도)

### 코드 재사용, 모듈화

- 최대한 재사용 가능한 코드를 만들도록 하였습니다 (마감기한에 다가옴에 따라 뒤로 갈수록 지키지 못함..)

### AWS S3 자료 저장 및 삭제


## Things To Do

- react-native e2e test
  - react-native의 경우 expo가 지원을 안하기에 자체적으로는 불가능 하고, `expo build:ios`를 통해 `.ipa`파일을 만들어야 `detox`를 통해 e2e 테스트를 실행가능한데, 빌드를 하려면 apple 라이센스를 구입해야만 빌드가 가능하여 작성을 중지하였습니다. 라이센스 구매 할 일이 생기면 꼭 e2e테스트를 해보고 싶습니다.
- 좀 더 디테일 한 `socket.io` 활용
  - 마감에 쫒겨서 socket 코드가 너무 모듈화되지 않았습니다.
- 채팅 전송시 알람 기능

## Sincere Thanks

[Ken Huh](https://github.com/Ken123777) / Vanilla Coding
