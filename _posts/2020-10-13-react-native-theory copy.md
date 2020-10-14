---
title: 리액트 네이티브 template 설치 에러
author: Poburi
date: 2020-10-14 11:15:00 +0000
categories: [Dev, Error]
tags: [error]
---
 
# 문제

타입스크립트 템플릿을 사용하여 리액트 네이티브 프로젝트 생성:

```
npx react-native init AwesomeTSProject --template react-native-template-typescript
```

에러 발생:

| error An unexpected error occurred: "https://registry.yarnpkg.com/react-natvie-template-typescript: Not found".

<blockquote 
  style="
  background-color: rgba(255,229,100,.3);
  border-left: 8px solid #ffe564;
  padding: 15px 30px 15px 15px;
  color: #000;
  "
>
  <strong>NOTE</strong> 위의 명령이 실패하면 이전 버전의 react-native 또는 react-native-cli가 PC에 전역 적으로 설치되어있을 수 있습니다. cli를 제거하고 npx를 사용하여 cli를 실행하십시오.
</blockquote>


# 해결

기존에 `cli` 삭제 하고 새로운 `cli`를 전역으로 설치하였다. 

- 기존 레거시 cli 삭제:

```
npm uninstall -g react-native-cli
```

- 새로운 cli 전역 설치:

```
yarn global add @react-native-community/cli
```

- 프로젝트 재설치:

```
npx react-native init RnTemplate --template react-native-template-typescript
```

---

![image](https://user-images.githubusercontent.com/45615584/95932069-ca80dc00-0e05-11eb-8525-2fa8cde6b9fc.png)

