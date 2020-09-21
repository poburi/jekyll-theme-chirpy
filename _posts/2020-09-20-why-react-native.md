---
title: React Native를 선택한 이유
author: Poburi
date: 2020-09-20 13:56:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
---

# 왜 React Native를...

1. 플래너 앱은 단순한 기능을 수행하는 애플리케이션
  - 소켓을 사용할까?
  - API 요청을 통해 기능 수행
  - 아무튼 간단해...

2. React 유 경험자
  - 어드민 & 플래너 웹 만들때 리액트를 사용해본 경험 있을 유

Object-C, Swift... 대체재가 될 수 있을까?
없다면 저 두가지를 배워야겠지? 제발 되어줘 대체재가

# 브릿지가 되어줘

React Native는 로컬의 노드 서버에서 published JavaScript 코드를 수행하기 때문에 에뮬레이터를 비롯한 실제 디바이스에서 변경사항 확인을 애플리케이션의 컴파일 없이 새로 고침으로 충분히 가능!

### 더 자세히 알아보자

- React Native는 `react-native run <platform>`명령어로 프로젝트를 구동하면 먼저 로컬에 index.platform.bundle을 게시하는 노드 웹서버를 실행
- platform에 해당하는 IOS/Android 프로젝트를 빌드하고 에뮬레이터 혹은 디바이스에 설치된다. 이 프로젝트에서 로컬에 구동된 index.platform.bundle을 다운받는다.
- 다운로드 후에 React Native 빌드 프로세스를 통해 JavaScript 런타임 환경으로 전달되어 프로젝트가 구동된다. 이후부터는 JavaScript의 수정이 생기면 새로 고침만으로 변경사항을 확인 할 수 있다.
- 그렇기 때문에 여러 대의 기기에 한 번 설치 후에는 다시 컴파일이 필요 없이 변경사항을 확인 할 수 있다.
<span style="font-size:12px;font-style:italic">특히 여러 디바이스에서 확인 필요한 디자인 QA를 진행할 때 가장 큰 장점이 될 듯</span>
- 토한 이 기능을 통해 Code Push를 사용하여 이미 배포된 애플리케이션의 재배포 없이 JavaScript 수정이 가능합니다.

# 개발기

state의 잦은 변경은 자칫 불필요하게 빈번한 화면 render를 수행하게 될 수 있음.
이를 효율적으로 처리하기 위해서는 적절한 shouldComponentUpdate[^shouldComponentUpdate]를 활용해야한다.

효율적인 render를 위해서 무엇보다 각 컴포넌트를 목적에 따라 __작게__ 나누고, 컴포넌트는 필요한 props와 state만 다루는 것이 결국 render가 수행되어야 하는 시점을 쉽게 판단할수 있도록 해준다.

# 그럼 필요한 라이브러리들은?

1. 네트워크
2. 위치수집
3. 기타 라이브러리
  - react-navigation
    -  애플리케이션에서 필요한 화면전환 제공
    - 화면전환 뿐 아니라 여러 편리한 기능을 제공하는 [react-native-navigation](https://github.com/wix/react-native-navigation) 라이브러리도 있다.

---

[^shouldComponentUpdate]: render가 수행되기 전에 render 필요 여부를 return하는 React 생명주기의 일부