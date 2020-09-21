---
title: React Native Running App
author: Poburi
date: 2020-09-17 13:56:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
---

# IOS

## Step01 - Start Metro!

React Native와 함께 제공되는 JavaScript 번들러 [Metro](https://facebook.github.io/metro/docs/concepts/)를 시작합니다.

```bash
npx react-native start
```

## Step02 - Start App!

Metro가 돌게하고, 새로운 터미널을 열고 다음 명령어를 실행합니다.

```bash
npx react-native run-ios
```


# Android

```bash
npx react-native init AwsomeProject
# 특정 버전 또는 템플릿 사용할 경우
npx react-native init AwsomeProject --template react-natvie-template-typescript
```

## Step01 - 안드로이드 장치 준비

### 가상장치

안드로이드 스튜디오 사용할 경우 AVD Manager을 열어 장치를 선택해줍니다.


## Step02 - Start Metro!

React Native와 함께 제공되는 JavaScript 번들러 [Metro](https://facebook.github.io/metro/docs/concepts/)를 시작합니다.

```bash
npx react-native start
```

## Step03 - Start App!

Metro가 돌게하고, 새로운 터미널을 열고 다음 명령어를 실행합니다.

```bash
npx react-native run-android
```