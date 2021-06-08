---
title: "리액트 네이티브 컴포넌트"
categories:
  - React Native
tags:
  - Javascript
  - React
  - React Native
toc: true
toc_label: "리액트 네이티브 컴포넌트"
---

## ActivityIndicator

데이터를 불러와서 화면에 보여주기 전까지의 로딩을 표시하는 컴포넌트 입니다.

### 크기 (size)

기본값은 **small** 이며, 조금 더 큰 사이즈를 원하는 경우에 **large** 로 변경할 수 있습니다. 안드로이드의 경우에는 숫자로 사이즈를 조절할 수 있지만 ios는 두가지만 제공하고 있기 때문에 선택해서 사용해야 합니다.

### 색상 (color)

색상을 표현하는 값을 넣을 수 있습니다. 일반적으로 **#000000** 과 같은 헥사코드를 사용합니다.

### 샘플코드

```jsx
import React from "react";
import { ActivityIndicator, View } from "react-native";

const App = () => (
  <View>
    <ActivityIndicator />
    <ActivityIndicator size="large" />
    <ActivityIndicator size="small" color="#0000ff" />
    <ActivityIndicator size="large" color="#00ff00" />
  </View>
);

export default App;
```

## Button

말 그대로 버튼을 의미하는 컴포넌트입니다. 하지만, 리액트 네이티브에서 제공하는 버튼은 스타일을 자유롭게 수정할 수 없습니다. 그러므로 저는 **Button** 보다는 **TouchableOpacity**를 사용하여 프로젝트에 맞는 버튼을 만드는 것을 추천합니다.

### 버튼 내용 (title)

이 값은 필수적으로 입력해야 하며, 버튼에 들어가는 내용을 의미합니다.

### 클릭 이벤트 함수 (onPress)

이 값은 필수적으로 입력해야 하며, 버튼을 클릭한 이후의 행동을 정의하는 함수입니다.

### 샘플코드

```jsx
import React from "react";
import { Button, View, Alert } from "react-native";

const App = () => (
  <View>
    <Button
      title="Press me"
      onPress={() => Alert.alert("Simple Button pressed")}
    />
  </View>
);

export default App;
```
