---
title: React Native 컴포넌트 정리
author: Poburi
date: 2020-10-10 16:32:00 +0000
categories: [Dev, React Native]
tags: [react navtive]
pin: true
---

# Button

기본 버튼 컴포넌트로 최소 수준의 사용자 지정을 지원한다.
`TouchableOpacity`나 `TouchableWithoutFeedback` 컴포넌트를 이용해서 원하는 버튼을 만들 수 있다.

```html
<Button
  onPress={onPressLearnMore}
  title="Learn More"
  color="#ddd"
  accessibilityLabel="Leartn more about this purple button"
/>
```

## onPress

사용자가 버튼을 탭할 때 호출되는 핸들러.
첫 번째 함수 인수는 [PressEvent](https://reactnative.dev/docs/pressevent)형식의 이벤트다.


## accessibilityLabel

시각 장애인 접근성 기능에 대해 표시 하는 텍스트 

# FlatList

섹션 지원이 필요한 경우 `<SectionsList>`를 사용하자.

```javascript

<Item 
  item={item} 
  onPress={()=>setSelectedId(item.id)}
 />

<FlatList
  data={DATA}
  renderItem={renderItem}
  keyExtractor={(item)=>item.id}
  extraData={selectedId}
/>
```
## renderItem

```javascript
renderItem({item, index, separators});
```

데이터에서 항목을 가져와 목록에 렌더링합니다.

# ScrollView

## ScrollView vs FlatList

ScrollView를 적재적소에 사용하지 못하면  렌더링 속도가 느려지고 메모리 사용량이 증가한다.

데이터가 많은 경우 FlatList.

조-끔 스크롤 있는 경우 ScrollView.

# TextInput

키보드를 통해 앱에 텍스트를 입력하게 도와주는 컴포넌트.

자동수정, 자동 대문자, 자리표시, 숫자 키패드와 같은 다양한 키보드 유형의 기능을 제공한다.

- basic:
```javascript
const [value, onChangeText] = useState('Placeholder!');

...

<TextInput
  onChangeText={text=>onChangeText(text)}
  value={value}
/>
```

![image](https://user-images.githubusercontent.com/45615584/95722186-8fb86000-0cae-11eb-9f17-88a492c3e57c.png)

- multi & custom:
```javascript
const CustomLikeThis = (props) => {
  return (
    <TextInput
      {...props} // 모든 props 상속
      editable
      maxLength={40}
    />
  );
}

const LearnTextInput = () => {
  const [value, onChageText] = useState('Placeholder MultiLine!');

  return (
    <View 
      style={{
        backgroundColor: value,
        borderBottomColor: '#000',
        borderBottomWidth: 1,
      }}
    >
      <CustomLikeThis
        multiline
        numberOfLines={4}
        onChnageText={text=>onChageText(text)}
        value={value}
      />
    </View>
  )
}

export default LearnTextInput;
```

![image](https://user-images.githubusercontent.com/45615584/95723061-ae6b2680-0caf-11eb-9a3d-998206f59b0e.png)


## keyboardType

키보드 타입 지정

- default
- number-pad
- numeric
- email-address
- phone-pad

## returnKeyType

리턴 키의 문구를 결정

### 모든 플랫폼:
- done (=완료)
- go (=이동)
- next (=다음)
- search (=검색)
- send (=보내기)
