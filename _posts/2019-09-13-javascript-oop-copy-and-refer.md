---
title: 자바스크립트 Oop 얕은 복사, 깊은 복사 그리고 프로토타입
author: Poburi
date: 2020-09-13 19:34:00 +0800
categories: [Dev, Error]
tags: [js]
toc: true
---

## 참조 (얕은 복사)

자바스크립트에서 객체는 참조다. 참조는 참조한 객체의 데이터를 바꾸면, 원본의 데이터가 영향을 받는다
즉, 참조한 데이터의 값을 바꾸게 되면 원본의 데이터에 영향을 받는다.

`__proto__`가 참조의 영향을 받아서 우리는 중복없이 객체를 관리 할 수 있는 것.

객체의 종류로는 객체, 배열, 함수가 있다.
따라서 객체, 배열, 함수의 데이터를 **복사**하려면 특별한 방법이 필요하다.

## 복사 (깊은 복사)

원시값은 특별한 방법으로 복사해도 원본 데이터에 영향을 받지 않는다.
복사는 원본데이터에 영향을 받지 않는다.

원시값의 종류로는 불린, 문자열, 숫자가 있다.
원시값은 자동으로 복사가 된다.

```javascript
let a = 1;
let b = a;

b = 2;

console.log(a); // 1
console.log(b); // 2
```

하지만, 객체는 원시값이 아니므로 위의 방법대로 하면 원본데이터도 바뀐다고했다. 
그렇다면 객체를 참조가 아닌 복사를 하고 싶다면 어떻게 해야 할까?

크게 4가지 방법이 있다.

1. `JSON` 메서드를 이용한 깊은 복사:

```js
JSON.parse(JSON.stringify(obj));
```

가장 쉬운 방법이긴 한데, 성능적으로 좋지 않아서 지양하는 것이 좋다.

2️. arr.slice(): 배열을 복사하는 법

3️. 1단계만 복사, 나머지는 참조:

```javascript
Object.keys(obj).forEach(function(key){
   obj2[key] = obj[key];
})
```

3-1. 3.의 다른 방법 및 축약:

```javascript
Object.assign(복사할곳, 복사할대상);
```

4️. 2단계까지 복사

```javascript
function copyObj(obj){
	var copy = {};
    if(typeof obj === 'object' && obj !== null){
       for (var attr in obj) {
       		if(obj.hasOwnProperty(attr)) {
            	copy[attr] = copyObj(obj[attr]);
            }
       }
    } else {
    	copy = obj;
    }
    return copy;
}
```

# 프로토타입

프로토타입은 팩토리 패턴에서 유용한 개념입니다. 
객체들끼리 서로 공유되게 해주는 개념이라고 생각하면 될 것 같아요.

이렇게 서로 공유하면 뭐가 좋을까요?
객체들끼리 서로 공유가 되니까 프로토타입만 바꿔도 한번에 추가, 수정, 삭제를 해줄 수 있다는 점이 좋겠죠.
중복요소들을 하나에 모아놓고, 나중에 바뀔 경우 프로토타입으로 정의한 객체만 바꿔주는 식으로 활용할 수도 있을 것 같죠?

이해가 쉽도록 공장을 예로 들어보려고 합니다.
프로토타입으로 정의할 공통적인 틀을 만들어봅시다.

```javascript
// 중복요소 모음
var commonFactory = {
    type: 'card',
    attack: function () {},
    defend: function () {}
}
```

`type`, `attack`, `defend`는 모든 카드에 들어갈 공통요소가 됩니다.

프로토타입을 이용할 카드 공장을 만들어봅시다.

```javascript
// 카드 공장
function cardFactory(name, hp, sp) {
    var card = {
        name: name,
        hp: hp,
        sp: sp
    }
    card.__proto__ = commonFactory;
    return card;
}
```

`card.__proto__ = commonFactory;` 이 부분이 객체가 참조인 점을 이용한 부분입니다.

`cardFactory()`로 생성된 카드는 commonFacotry의 값을 변경함에 따라 영향을 받을 수 있습니다.

카드 공장을 돌려서 card들을 찍어내봅시다.

```javascript 
var card1 = cardFactory('po', 100, 100);
var card2 = cardFactory('ju', 150, 150);
...
var card30000 = cardFactory('mimi', 180, 180);
```

카드를 30000장이나 찍어냈다고 가정하고, 이 카드들의 타입이 'card'인지도 잘 확인을 했습니다.

![image](https://user-images.githubusercontent.com/45615584/93020787-1d565080-f61a-11ea-9b85-b1ca7e1a8d48.png)

그런데 갑자기 카드 납품을 하려고 했더니 카드가 아니라 장난감으로 바꿔달라고 요청이 들어왔습니다.

모든 카드들의 타입을 바꿀 필요 없이 프로토타입으로 정의한 공통적인 틀만 변경하면 쉽게 바꿀 수 있습니다.

```javascript
commonFactory.type = '장남감';
```

![image](https://user-images.githubusercontent.com/45615584/93020824-6908fa00-f61a-11ea-920c-433df0e08984.png)

모든 카드들의 타입이 장난감으로 바꼈습니다.

이제 또 납품을 하려고 했더니 카드에 가로와 세로의 크기를 넣어달라고 한다면 마찬가지로 프로토타입을 이용해 추가해 줄 수 있습니다.

```javascript
commonFactory.width = 100;
commonFactory.height = 300;
```

![image](https://user-images.githubusercontent.com/45615584/93020975-462b1580-f61b-11ea-9fa8-1c745e3f5111.png)

# 그런데 말입니다...

사실 표준이 아니기 때문에 `__proto__`를 쓰지 않습니다. 

쓰지 말라고 했으니 위에 만들어놓은 공장을 바꿔보겠습니다.

핵심은 `Object.Create(프로토타입)`입니다. 알아서 프로토타입을 생성해줍니다.

![image](https://user-images.githubusercontent.com/45615584/93021230-95be1100-f61c-11ea-93f4-3b95ebecfa81.png)

카드 공장도 `__proto__`를 빼고 바꿔줍니다.

```javascript
function cardFactory(name, hp, sp) {
    var card = Object.create(commonFactory);
    card.name = name,
    card.hp = hp,
    card.sp = sp
    return card;
}
```

위의 `card = Object.crate(commonFacotry)`를 `__proto__`를 사용해서 표현하면 

```
var card = {};
card.__proto__ = commonFactory;
```

이렇게 되는 거죠.

아무튼, 실무에서는 꼭 Object.create()로 사용하는 걸로...!