---
title: "디자인 시스템"
categories:
  - Frontend
tags:
  - Frontend
  - Design System
toc: true
toc_label: "디자인 시스템"
---

## 왜 사용할까요?

우선 **디자인 시스템**은 다시 사용할 수 있는 요소들을 모아놓은 묶음이며, 대표적으로는 **색상, 폰트, 간격** 등이 있습니다. 이렇게 만들어 둔 구성요소들을 조립하여 여러가지 새로운 요소들을 만들어낼 수 있기 때문에 디자인 시스템 사용을 권장합니다.
<br>

### 효율성

유사한 구성 요소를 처음부터 만들지 않고, 디자인 시스템을 사용하면 디자이너와 개발자가 구성 요소를 재사용하여 효율성을 높일 수 있습니다.

### 일관성

디자인 시스템은 구성 요소를 만들기 위한 원칙을 정의하여, 다양한 플랫폼에서 일관된 경험을 만들 수 있습니다.

### 규모

효율성과 일관성이 향상되어 회사는 대규모 제품을 더 빠르게 구축 할 수 있습니다.

## 색상

```js
const colors = {
  primary: {
    lighter: "#a8bbff",
    light: "#485aff",
    main: "#1227ec",
    dark: "#1b2bba",
    darker: "#000c78",
  },
  gray: {
    white: "#ffffff",
    gray10: "#fbfbfb",
    gray20: "#e6e6e6",
    gray30: "#c6c6c6",
    gray40: "#a7a7a7",
    gray50: "#646464",
    gray60: "#4d4d4d",
    gray70: "#2b2b2b",
    Black: "#111111",
    RealBlack: "#000000",
  },
  blueGray: {
    gray05: "#fdfeff",
    gray10: "#f4f8fb",
    gray20: "#e7edf2",
    gray30: "#bcc4cc",
  },
  tableRow: {
    normal: "#fdfeff",
    hover: "#f4f8fb",
    selected: "#e7edf2",
  },
  button: {
    normal: "#3249f1",
    hover: "#1b2bba",
    selected: "#000c78",
    disabled: "#e7edf2",
  },
  states: {
    disabled: "#e5e5e5",
    action: "#2b3ee8",
    success: "#7dcd71",
    warning: "#ffe278",
    error: "#fa704e",
  },
};
```

## 폰트

```js
const fonts = {
  heading1: {
    fontSize: "60px",
    letterSpacing: "-1.5px",
  },
  heading2: {
    fontSize: "48px",
    letterSpacing: "-1px",
  },
  heading3: {
    fontSize: "34px",
    letterSpacing: "-1.2px",
  },
  heading4: {
    fontSize: "26px",
    letterSpacing: "-1.2px",
  },
  heading5: {
    fontSize: "20px",
    letterSpacing: "-0.6px",
  },
  heading6: {
    fontSize: "17px",
    letterSpacing: "-0.8px",
  },
  subtitle1: {
    fontSize: "20px",
    letterSpacing: "-0.6px",
  },
  subtitle2: {
    fontSize: "17px",
    letterSpacing: "-0.8px",
  },
  subtitle3: {
    fontSize: "15px",
    letterSpacing: "-0.6px",
  },
  body1: {
    fontSize: "18px",
    letterSpacing: "-0.8px",
  },
  body2: {
    fontSize: "14px",
    letterSpacing: "-0.8px",
  },
  elementt1: {
    fontSize: "16px",
    letterSpacing: "0px",
  },
  elementt2: {
    fontSize: "16px",
    letterSpacing: "-0.4px",
  },
  caption1: {
    fontSize: "13px",
    letterSpacing: "-0.4px",
  },
  caption2: {
    fontSize: "12px",
    letterSpacing: "0px",
  },
};
```

## 간격

```js
const spacing = {
  xxs: "4px",
  xs: "8px",
  xs: "16px",
  sm: "20px",
  lg: "40px",
  xl: "60px",
};
```
