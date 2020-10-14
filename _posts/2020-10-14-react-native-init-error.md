---
title: React Native API 정리
author: Poburi
date: 2020-10-13 11:15:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
pin: true
---
 
# Animated

- 애니메이션 값을 변경 사항에 첨부 할 수 있다는 것
- 상태값을 조정하여 transition을 해보자

```javascript
const alpha = Math.PI / 6; // 180도를 6으로 나눈 수를 알파값으로 설정
const [toggled, setToggle] = useState(false);
return (
  <View style={styles.container}>
    {cards.slice(0,3).map((card, index)=>{ // card를 0-3만큼 참조 (=얕은 복사) 
      const rotate = toggled ? (inde - 1) * alpha : 0; // 활성화 되면 변환을 주고 아니면 0(=그대로)
      return (
        <Animated.View
          key={card}
          style={[
            styles.overlay,
            {
              transform: [{rotate: `${rotate}rad`}],
            }
          ]}
        >
          <Card {...{card}} />
        </Animated.View>
      );
    })}
    <Button
      label={toggled ? "Reset" : "Start"}
      primary
      onPress={()=>setToggle((prev)=>!prev)} // true/false toggle
    />
  </View>
);
```
