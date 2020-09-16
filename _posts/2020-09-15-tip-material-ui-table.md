---
title: React Native Setup JDK 설치 이슈 해결
author: Poburi
date: 2020-09-16 13:56:00 +0000
categories: [Dev, Error]
tags: [error]
toc: true
---

리액트 네이티브 설치 공식 문서에는 

```bash
$ brew cask install adoptopenjdk/openjdk/adoptopenjdk8
```

이렇게 나와있어서 그대로 했는데 안됨ㅠㅠㅠㅠ

찾아보니 [brew issue](https://discourse.brew.sh/t/how-to-install-openjdk-with-brew/712)의 문제로 아직 공식적으로 brew로 설치가 불가능하다고 한다.

# AdoptOpenJDK

[AdoptOpenJDK](https://adoptopenjdk.net/)는 사전에 prebuild 형태로 java binary를 제공하는 커뮤니티 그룹이다. Mac 뿐만 아니라 윈도우, 리눅스 환경도 제공하고 있다.

공식적으로 OpenJDK를 설치하는건 직접 빌드해서 사용하는 방법이 있지만, 빌드 이외에도 자잘한 JAVA_HOME (빌드해서 사용했더니 “/usr/libexec/java_home” 이 동작하지 않았다..) 설정 문제라던가 버전업을 편하게 하기 위해서 homebrew를 사용해서 AdoptOpenJDK를 설치하도록 했다.

설치 방법은 [여기](https://github.com/AdoptOpenJDK/homebrew-openjdk)를 참고했다.

1. 최신 AdoptOpenJDK 설치:

```bash
$ brew cask install adoptopenjdk 
```

2. 설치 할 버전을 골라서 설치:

```bash
$ brew tap AdoptOpenJDK/openjdk
$ brew cask install adoptopenjdk14
```


# Switch JDK version

- `~/.zshrc` 혹은 `~/.bash_profile`에 아래 코드 추가:

```bash
jdk() {
        version=$1
        export JAVA_HOME=$(/usr/libexec/java_home -v"$version");
        java -version
 }
```

- 사용법:

```bash
$ jdk 1.8
```

`jdk` 명령어 뒤에 원하는 버전을 뒤에 붙인다.


# 결과

![image](https://user-images.githubusercontent.com/45615584/93351239-6efa1780-f874-11ea-839b-2e4e88e858ff.png)


드디어 안드로이드 JDK에 체크 표시가 떴다. 이제 SDK 잡으러 가야지... 😓

`Android 10 (Q)` 설치 했는데 왜 안잡히는건지 모르겠다 정말 👿👿👿👿