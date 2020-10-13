---
title: [React-Native] Async storage API 사용하여 토큰 로그인 처리
author: Poburi
date: 2020-10-10 11:15:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
pin: true
---

LocalStorage와 비슷한 대체제로 앱에 전역적으로 적용되는 암호화되지 않은 비동기식 키-값 스토리지 시스템이다.

- 설치:

```bash
yarn add @react-native-community/async-storage
```

- 사용:

`import { useAsyncStorage } from '@react-native-community/async-storage';` 추가

# getItem

키에 대한 문자열 값을 가져오고 없으면 `null`을 가져온다.

- 문법:

| getItem(key);

```javascript
const { getItem: TokenGetItem } = useAsyncStorage('@token');
...
const isHasToken = (await TokenGetItem()) !== null ? true : false;
```


