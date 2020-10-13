---
title: React Native IOS/Android 생체 인증 적용기
author: Poburi
date: 2020-10-13 11:15:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
pin: false
---

# 개발 스팩

- React Native

- TypeScript

- JDK 1.8.1

# 설계

### 라이브러리

```bash
npm i --save react-native-touch-id
cd ios
pod install
```

### 구현할 기능

- isSupported
  - 지문
  - Face ID

- authenticate
  - 패스워드

 
- useBiometrics:
```javascript
const Biometrics = () => {

  ...

  // isSupported
  const optionalConfigObject: AuthenticateConfig = {
    fallbackLabel: 'Show Passcode',
    passcodeFallback: false,
  };
 
  const isSupported = async (): Promise<boolean> => {
    return new Promise((resolve) => {
      TouchID.isSupported()
        .then((biometryType) => {
          // Success code
          resolve(true);
          if (biometryType === 'FaceID') {
            // console.log('FaceID is supported.');
          } else {
            // console.log('TouchID is supported.');
          }
        })
        .catch((error: any) => {
          resolve(false);
          switch (error.name) {
            case 'LAErrorPasscodeNotSet':
              // console.log('폰 암호 비활성화');
              break;
            default:
              break;
          }
        });
    });
  };

  const authenticate = async (cb: (result: boolean) => void) => {
    TouchID.authenticate('패스워드의??', optionalConfigObject)
      .then((success: boolean) => {
        cb(success);
      })
      .catch((error: AuthenticationError) => {
        console.log(error.code);
        cb(false);
      });
  };

  return { authenticate, isSupported };
}
```

- 가져다 쓰기:
```javascript
const { authenticate, isSupported } = useBoimetrics();
const handleResult = (result: boolean) => {
    console.log('Bio Check', result);
    if (result) {
      navigation.reset({ index: 0, routes: [{ name: 'Tabs' }] });
    } else {
      sheetRef.current?.snapTo(1);
    }
  };

...

const initialize = async () => {
  const isBiomtrics = await isSupported(); //=> true/false

  ...

  // 패스워드 체크 후
  authenticate(handleResult);
}
```

- 1초 후 반응하도록:

```javascript
useEffect(() => {
    setTimeout(() => initialze(), 1000);
    // eslint-disable-next-line react-hooks/exhaustive-deps
  }, []);
```

