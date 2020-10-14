---
title: 깃허브 템플릿을 이용해 React Navite 초기 템플릿 만들기
author: Poburi
date: 2020-10-14 11:15:00 +0000
categories: [Dev, Git]
tags: [git, github]
---

`React`, `React Native` 프로젝트 할 때마다 매번 세팅 작업을 해주는 것은 매우 귀찮은 일이다.

그래서 깃허브에서 제공해주는 템플릿을 만들어 사용해봤다.

---

# 템플릿으로 변경

템플릿으로 사용할 레파지토리를 만들어서 Setting 항목으로 들어가면 template 관련 체크박스가 보이는데 체크만 해주면 끝.

![image](https://user-images.githubusercontent.com/45615584/95934295-80025e00-0e0b-11eb-9743-3d444850b3b7.png)

# 나만의 초기 RN 세팅

### 1. prettier, eslint

기본적으로 `prettier`, `eslint`를 잡아주는데

cli로 RN 프로젝트를 생성하면 보통 `.js` 확장자로 세팅이 되어있는데 이것을 `json`으로 잡는다.

바꿔주는 이유는 CTO님께 여쭤봤더니 `.json` 포맷이 자동완성 기능이 더 편하기 때문이라고 한다.

- `.eslintrc.json`:

```json
{
  "root": true,
  "extends": "@react-native-community",
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "rules": {
    "@typescript-eslint/no-unused-vars": "warn"
  }
}
```

- `.prettierrc`:

```json
{
  "bracketSpacing": true,
  "jsxBracketSameLine": true,
  "singleQuote": true,
  "trailingComma": "all",
  "semi": true,
  "printWidth": 180
}
```

### 2. dependencies

자주 사용하는 디펜던시를 설치해준다.

작업할 때 자주 설치하는 목록을 정리해봤다.:

- async-storage

- netinfo

- [react-navigation](https://reactnavigation.org/docs/getting-started)

- moment

- numeral

- bottom-sheet

- styled-component

- touch-id

- simple-toast

- onesignal

# Github에 올리기

- 로컬 프로젝트에 git 초기화:

```bash
git init
```

- git repository url remote 연결:

```bash
git remote add origin "repository url"
```

- push

---

# 마무리

사용할 때는 `Use This Template`를 눌러서 프로젝트를 만들어주면 된다.

![image](https://user-images.githubusercontent.com/45615584/95935491-5ac31f00-0e0e-11eb-96ba-72f648a35400.png)
