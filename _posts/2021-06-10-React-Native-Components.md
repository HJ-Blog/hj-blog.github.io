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
    <TouchableOpacity
      onPress={() => setSelectedId(item.id)}
    >
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
      <TouchableOpacity
        onPress={() => setSelectedId(item.id)}
      >
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

## Image / ImageBackground

둘 다 이미지를 표현하기 위한 컴포넌트이며, 이미지의 크기를 수동으로 지정해야 합니다. 로컬에 있는 이미지, 외부 이미지 링크, data:... 형식의 이미지 파일을 보여줄 수 있습니다.
<br>
<br>
**ImageBackground** 는 컴포넌트 내부에 또다른 컴포넌트를 렌더링해서 이미지 위에 또다른 무언가를 보여줄 수 있습니다.

### 이미지 경로 (source)

프로젝트 폴더 내에 있는 로컬 이미지 경로, 외부에 있는 이미지 링크 그리고 data:... 형식의 이미지 파일을 나타냅니다.

#### 로컬 이미지 경로

```js
require("../react-native-logo.png");
```

#### 외부 이미지 링크

```js
{
  uri: "https://reactnative.dev/img/tiny_logo.png";
}
```

#### data: 형식의 파일

```js
{
  uri: "data:image/png;base64, ... ";
}
```

### 샘플코드

```jsx
import React from "react";
import { View, Image, StyleSheet } from "react-native";

const styles = StyleSheet.create({
  tinyLogo: {
    width: 50,
    height: 50,
  },
  logo: {
    width: 66,
    height: 58,
  },
});

const App = () => {
  return (
    <View>
      <Image
        style={styles.tinyLogo}
        // source={require("../react-native-logo.png")}
      />
      <Image
        style={styles.tinyLogo}
        source={
          {
            // uri: "https://reactnative.dev/img/tiny_logo.png",
          }
        }
      />
      <Image
        style={styles.logo}
        source={
          {
            // uri: "data:image/png;base64, ... ",
          }
        }
      />
      <ImageBackground
      // source={require("../react-native-logo.png")}
      >
        <Text>이미지 위에 보여집니다</Text>
      </ImageBackground>
    </View>
  );
};

export default App;
```

## KeyboardAvoidingView

가상 키보드 때문에 보이지 않는 영역에 대한 문제를 해결하기위한 컴포넌트입니다. 키보드 높이에 따라 화면의 높이, 위치 또는 하단 패딩을 자동으로 조정할 수 있습니다.

### 자동 조정 옵션 (behavior)

가상 키보드에 의해 화면이 조정되는 옵션을 선택할 수 있습니다. **height(높이)**, **position(위치)**, **padding(하단 패딩)**

### 샘플코드

```jsx
import React from "react";
import {
  View,
  KeyboardAvoidingView,
  TextInput,
  Text,
  Platform,
  TouchableWithoutFeedback,
  Button,
  Keyboard,
} from "react-native";

const App = () => {
  return (
    <KeyboardAvoidingView
      behavior={
        Platform.OS === "ios" ? "padding" : "height"
      }
    >
      <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
        <View>
          <Text>Header</Text>
          <TextInput placeholder="Username" />
          <View>
            <Button title="Submit" onPress={() => null} />
          </View>
        </View>
      </TouchableWithoutFeedback>
    </KeyboardAvoidingView>
  );
};

export default App;
```

## Modal

모달 팝업의 형태를 나타내는 컴포넌트 입니다. 2가지의 애니메이션 타입을 설정할 수 있습니다.

### 애니메이션 타입(animationType)

기본값은 **none**이며, 모달 팝업이 나타나는 애니메이션을 지정할 수 있습니다. **slide**는 아래에서 위로 스윽~ 하고 올라오는 애니메이션이고, **fade**는 투명한 상태에서 점점 뚜렷하게 나타내는 애니메이션입니다.

```jsx
<Modal animationType="slide">
  <Text>Hello World!</Text>
</Modal>
<Modal animationType="fade">
  <Text>Hello World!</Text>
</Modal>
<Modal animationType="none">
  <Text>Hello World!</Text>
</Modal>
```

### 팝업의 영역 (transparent)

true 값으로 설정하면 전체 영역을 차지하는 모달팝업을 사용하고, false 라면 내부의 내용에 맞는 영역에만 팝업이 나타납니다.

```jsx
<Modal transparent={true}>
  <Text>Hello World!</Text>
</Modal>
```

### 나타내기/숨기기 (visible)

팝업에서 가장 핵심적인 기능인 나타내기/숨기기 입니다. 상태를 관리하는 useState 훅에서 boolean 형태의 값으로 관리하여 사용할 수 있습니다.

```jsx
const [modalVisible, setModalVisible] = useState(false);

<Modal visible={modalVisible}>
  <Text>Hello World!</Text>
</Modal>;
```

### 팝업이 닫힐 때 (onRequestClose)

팝업이 닫힐 때 실행되는 함수입니다. 안드로이드에서 뒤로가기, 애플티비의 메뉴 버튼 클릭을 눌렀을 경우와같이 팝업이 닫힐 때 호출될 수 있습니다.

```jsx
<Modal
  onRequestClose={() => {
    Alert.alert("팝업이 닫힙니다.");
    setModalVisible(!modalVisible);
  }}
>
  <Text>Hello World!</Text>
</Modal>
```

### 샘플코드

```jsx
import React, { useState } from "react";
import { Modal, Text, View, Alert } from "react-native";

const App = () => {
  const [modalVisible, setModalVisible] = useState(false);
  return (
    <View style={styles.centeredView}>
      <Modal
        animationType="slide"
        transparent={true}
        visible={modalVisible}
        onRequestClose={() => {
          Alert.alert("팝업이 닫힙니다.");
          setModalVisible(!modalVisible);
        }}
      >
        <Text>Hello World!</Text>
      </Modal>
    </View>
  );
};

export default App;
```

## Pressable

손가락으로 눌렀을 때의 각각의 타이밍에 대해서 이벤트를 제공하고 있는 컴포넌트입니다. 다양한 태그를 감싸서 사용할 수 있습니다.
<br>
<br>
이 컴포넌트는 딱 2가지의 경우로 동작이 진행됩니다.
<br>
<br>
**누른다(onPressIn) - 뗀다(onPressOut) - 눌렀다 떼는 행위를 했다(onPress)**
<br>
<br>
**누른다(onPressIn) - 오래 누른다(onLongPress) - 뗀다(onPressOut)**

### 누른다 (onPressIn)

Pressable 컴포넌트를 누르기 시작했을때 실행되는 함수입니다.

### 오래 누른다 (onLongPress)

Pressable 컴포넌트를 누르기 시작해서 떼지 않고 0.5초 이상 있으면 실행되는 함수입니다.

### 오래 누른다의 기준시간 (delayLongPress)

Pressable 컴포넌트를 누르기 시작해서 떼지 않고 **delayLongPress** 밀리초 이상 있으면 onLongPress 함수가 실행됩니다.

### 뗀다 (onPressOut)

Pressable 컴포넌트를 누르다가 손을 떼는 순간 실행되는 함수입니다.

### 눌렀다 떼는 행위를 했다 (onPress)

Pressable 컴포넌트를 누르다가 손을 떼서 onPressOut 함수가 실행된 다음에 실행되는 함수입니다.
(단, 0.5초 이상 눌렀을 경우에는 onPressOut 함수 이후에 onPress 함수가 호출되지 않습니다.)

### 못누르게 비활성화 (disabled)

특정 경우에 useState 훅과 함께 사용하여 누르지 못하게 비활성화를 할 수도 있습니다.
(아이디를 입력해야 로그인을 누를 수 있다)

### 샘플코드

```jsx
<Pressable
  onPress={() => {
    setTimesPressed((current) => current + 1);
  }}
  style={({ pressed }) => [
    {
      backgroundColor: pressed
        ? "rgb(210, 230, 255)"
        : "white",
    },
  ]}
>
  {({ pressed }) => (
    <Text style={styles.text}>
      {pressed ? "잘 눌렸습니다!" : "눌러봐~~~~~~~~~~~~~"}
    </Text>
  )}
</Pressable>
```

## RefreshControl

이 컴포넌트는 ScrollView 라는 컴포넌트와 함께 사용됩니다. 우리가 스마트폰에 있는 앱을 이용하다 보면 새로고침을 하고 싶을 때가 있습니다. 이미 알고 있는 분도 있겠지만, 대부분의 경우에 화면을 **위에서 아래로 당기면 새로고침**이 됩니다.
<br>
<br>
특히 **스크롤이 있는 화면**에서 이러한 기능이 필수적으로 들어가고 있는 추세입니다.
<br>
<br>
이렇게 스크롤이 맨 위에 있을 때, 보여지는 화면을 새로고침을 하기 위해 위에서 아래로 당기면 스마트폰에서 로딩 화면이 보여지게 됩니다. 이러한 화면을 위해 리액트 네이티브에서는 **RefreshControl** 컴포넌트를 지원하고 있습니다.

### 화면의 새로고침 완료 여부 (refreshing)

- 화면이 새로고짐 하기 전에는 false 입니다.
- 위에서 아래로 드래그 하여 새로고침이 시작하면 true 로 변합니다.
- 다시 새로고침이 완료되면 false 로 변합니다.

### 샘플코드

```jsx
import React from "react";
import {
  RefreshControl,
  SafeAreaView,
  ScrollView,
  Text,
} from "react-native";

const wait = (timeout) => {
  return new Promise((resolve) =>
    setTimeout(resolve, timeout)
  );
};

const App = () => {
  const [refreshing, setRefreshing] = React.useState(false);

  const onRefresh = React.useCallback(() => {
    setRefreshing(true);
    wait(2000).then(() => setRefreshing(false));
  }, []);

  return (
    <SafeAreaView>
      <ScrollView
        refreshControl={
          <RefreshControl
            refreshing={refreshing}
            onRefresh={onRefresh}
          />
        }
      >
        <Text>
          아래로 당기면 새로고침 로딩화면이 보입니다~
        </Text>
      </ScrollView>
    </SafeAreaView>
  );
};

export default App;
```
