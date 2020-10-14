---
title: React Native folder structure & Init
author: Poburi
date: 2020-10-01 09:15:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
pin: true
---

# 폴더 구조

- Rn Template:

```
.
├── src
|   ├── @types
│   ├── assets
│   │  ├── fonts
│   │  ├── images
│   ├── components
│   │  ├── Common
│   │  |   ├── BottomSheet
│   │  |   ├── SPassword
│   │  |   ├── ...
│   ├── hooks
│   ├── layouts
│   │  ├── TabsLayout
│   │  |   ├── index.tsx
│   │  |   ├── Header.tsx
│   ├── screens
│   │  ├── Private
│   │  ├── Public
│   │  ├── ...
│   ├── utils
│   │  ├── ALibrary
│   │  ├── ...
│   ├── Root.tsx
```

# 변경

`/index.js`:

```javascript
import "react-native-gesture-handler"; // react navigation 사용
import { AppRegistry } from "react-native";
import Root from "./src/Root";
import { name as appName } from "./app.json";

AppRegistry.registerComponent(appName, () => Root);
```

`/src/Root.tsx`:

```javascript
import React from "react";
import { View, Text } from "react-native";

const Root = () => {
  return (
    <View>
      <Text>Init!</Text>
    </View>
  );
};

export default Root;
```
