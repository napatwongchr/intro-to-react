# UI Component

UI Component ทำให้เราสามารถที่จะพัฒนา React App ได้รวดเร็วมากยิ่งขึ้น ปกติแล้วเราเขียน Component Button ขึ้นมาเองจากที่ผ่านมา เราจะมาลองใช้ UI Component กัน

<br><hr><br>

## React UI Component Landscape

React UI Component มีหลายเจ้ามาก ๆ

- [Antd](https://ant.design/)
- [Chakra UI](https://chakra-ui.com/)
- [Meterial UI](https://material-ui.com/)
- [Theme UI](https://theme-ui.com/)
- [Evergreen](https://evergreen.segment.com/)
- Etc.

<br><hr><br>

## Chakra UI

![Chakra UI Logo](./images/chakra-ui-logo.png)

Chakra UI เป็น Component Library ตัวนึงที่มีจุดเด่นในด้านของความรวดเร็ว ความง่าย และยัง support เรื่องของ web accessibility ในการพัฒนา React Application

<br><hr><br>

## Setting Up Chakra

1. เริ่ม Setup Chakra ด้วยการ install packages ให้เราเปิด terminal ขึ้นมา

`npm i @chakra-ui/react @emotion/react@^11 @emotion/styled@^11 framer-motion@^4`

2. Setup ChakraProvider ในไฟล์ `index.js`

```js
import * as React from "react";

// 1. import `ChakraProvider` component
import { ChakraProvider } from "@chakra-ui/react";

function App() {
  // 2. Use at the root of your app
  return (
    <ChakraProvider>
      <App />
    </ChakraProvider>
  );
}
```

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
