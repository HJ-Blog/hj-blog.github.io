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

## FlatList

기본 목록 화면을 구성하기 위한 가장 편리한 인터페이스라고 합니다. 일반적으로 우리가 목록을 나타내는 화면을 구성하는 경우에 가장 필요로 하는 것이 **선택한 요소의 데이터**를 불러오는 방법입니다.
<br>
<br>
우선, FlatList 컴포넌트를 사용하기 위해서는 어떤 속성들이 필요하고, 어떻게 선택한 요소의 데이터를 불러올 수 있는지 알아보겠습니다.

### 데이터 (data)

이 속성에는 **배열 타입**의 데이터를 입력 받습니다. 아무래도 하나의 요소가 여러개의 정보를 가지고 있기 때문에 다음과 같이 오브젝트 배열일 가능성이 높습니다.

```js
const data = [
  { id: 1, name: "name_1", email: "email_1@gmail.com" },
  { id: 2, name: "name_2", email: "email_2@gmail.com" },
  { id: 3, name: "name_3", email: "email_3@gmail.com" },
];
```

### 렌더링 함수 (renderItem)

데이터(data) 배열 안에 있는 각각의 오브젝트를 렌더링하기 위한 함수입니다. **name, email**과 같이 오브젝트의 정보를 렌더링하는 컴포넌트를 반환합니다.
<br>
<br>
목록을 보여주는 화면에서는 각각의 요소가 클릭 시, 상세정보를 보여주는 액션이 필요하기 때문에, 클릭 이벤트를 연결해주기 위해서 전체를 **TouchableOpacity**로 감싸줬습니다.

```jsx
// 상태값
const [selectedId, setSelectedId] = useState(null);

// 렌더링 함수
function renderItem({ item }) {
  return (
    <TouchableOpacity onPress={() => setSelectedId(item.id)}>
      <Text>{item.name}</Text>
      <Text>{item.email}</Text>
    </TouchableOpacity>
  );
}
```

### 배열을 렌더링 할 때 사용할 키 값 (keyExtractor)

리액트에서는 반복적으로 특정 컴포넌트를 렌더링 하는 경우에 고유한 값을 가지는 key 속성값을 넣어 주어야 합니다. FlatList 에서는 keyExtractor 함수를 통해서 어떤 값으로 키 값을 넣어줄 것인지 지정해 줄 수 있습니다.

```jsx
<FlatList keyExtractor={(item, index) => item.id} />
```

### 렌더링에 영향을 주는 또다른 값 (extraData)

FlatList 안에 있는 요소들을 렌더링 하는 데에 영향을 주는 값은 데이터(data) 뿐입니다. 하지만, extraData 속성을 사용하면 추가적으로 영향을 주는 변수를 정의할 수 있습니다.
<br>
<br>
예를들어, 다음과 같이 선택된 요소의 아이디를 추가하면, 요소를 클릭하여 현재 선택된 아이디가 변할 때마다, 리스트가 새롭게 렌더링 됩니다.

```jsx
<FlatList extraData={selectedId} />
```

### 샘플코드

```jsx
import React, { useState } from "react";
import {
  FlatList,
  SafeAreaView,
  StatusBar,
  StyleSheet,
  Text,
  TouchableOpacity,
} from "react-native";

const data = [
  { id: 1, name: "name_1", email: "email_1@gmail.com" },
  { id: 2, name: "name_2", email: "email_2@gmail.com" },
  { id: 3, name: "name_3", email: "email_3@gmail.com" },
];

const App = () => {
  const [selectedId, setSelectedId] = useState(null);

  function renderItem({ item }) {
    return (
      <TouchableOpacity onPress={() => setSelectedId(item.id)}>
        <Text>{item.name}</Text>
        <Text>{item.email}</Text>
      </TouchableOpacity>
    );
  }

  return (
    <SafeAreaView>
      <FlatList
        data={data}
        renderItem={renderItem}
        keyExtractor={(item) => item.id}
        extraData={selectedId}
      />
    </SafeAreaView>
  );
};

export default App;
```
