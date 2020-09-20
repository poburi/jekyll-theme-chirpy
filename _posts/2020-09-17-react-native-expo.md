---
title: React Native Expo
author: Poburi
date: 2020-09-17 13:56:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
---

# 1

내용 수정하고 저장을 하면 자동으로 리프레쉬되면서 변경 내용을 바로 확인 시켜주는 것.

⌘ ctrl + R

핸드폰에서 개발자 메뉴에 접근하고 싶다면 폰을 흔들어?

시뮬레이터에서 `⌘ + D`를 누르면 개발자 메뉴에 접근할 수 있어

# 2 - mobile app을 만드는 3가지 방법

1) 완전 네이티브

스위프트, 오브젝트-씨, 자바, 코틀린으로 만드는 안드로이드 앱

2) 앱 기반 웹뷰

하이브리드 웹뷰.

앱 안에서 작동하는 웹 사이트 같은 것

3) 리액트 네이티브

안드로이드, IOS 둘다 자바스크립트 엔진이 내장 되어 있기 때문에, 자바스크립트를 실행할 수 있어.

자바스크립트를 이용해서 안드로이드, IOS의 네이티브 엔진에게 자바스크립트를 이용한 메시지를 보내는 것.

연결을 이어주는 브릿지 처럼. 

교통체증 처럼 너무 많은 데이터를 보내거나 최적화할 때 리액트 네이티브는 절절치 않다.

예를 들면 3D 비디오 게임같은...

# 3 - View, Text whatever component

```javascript
return (
    <View style={styles.container}>
        <Text>안녕</Text>
    </View>
)
```

view = div

test = span

이런 룰이 생긴 이유는 브릿지 역할을 하기 때문

styleSheet도 구현해 놨기 때문에 css를 쓸 수 있긴 한데 

자바스크립트 오브젝트 처럼 써야 함.

```javascript
const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: "red",
        alignItems: "center",
        justifyContent: "center"
    }
})
```

일반 웹에서는 부모에 color를 주면 자식이 상속받지?

근데 리액트 네이티브는 그렇지 않아. View에게 color 값을 줘도 소용이 없다구.

각 각 줘야되 각.각.

`<Text>`컴포넌트에도 스타일을 줘보자.

```javascript
return (
    <View style={styles.container}>
        <Text style={styles.text}>안녕</Text>
    </View>
)
```

그리고 스타일을 만들어줘.

```javascript
const styles = StyleSheet.create({
    ...,
    text : {
        color: "white",
        fontSize: 15,
    }
})
```

## Text 컴포넌트 스타일링 할 때 주의할 점

픽셀은 안되는데 %는 되

