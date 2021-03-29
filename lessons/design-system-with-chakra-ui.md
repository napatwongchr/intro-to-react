# Design System

A design system คือ Collection ของ Components ที่สามารถนำมา Reuse ใช้ใหม่ได้เรื่อย ๆ สิ่งที่สำคัญคือ **Components เหล่านี้ต้องมี standard ที่ชัด** ที่สามารถนำไป**ใช้สร้าง Products ได้ หลาย ๆ Products**

**ตัวอย่างของ Design System**

- [Google Material](https://material.io/)
- [Apple Human Interface](https://developer.apple.com/design/)
- [Microsoft Fluent Design System](https://www.microsoft.com/design/fluent/#/)
- [Vercel Design](https://vercel.com/design)
- Etc.

<br><hr><br>

## Why Design System

1. สามารถ**ตรวจสอบความถูกต้อง**ของหน้าตา Products ได้

2. สร้าง **Visual Design Language** ขึ้นมา - ตรงนี้เป็นประโยชน์มาก ๆ ทำให้ทีม Design / Developer ที่พัฒนา Products เห็นหน้าตาแบบเดียวกันได้ ในเรื่องของ สี, ตัวอักษร, ขนาด, หน้าตา Component ต่าง ๆ ที่อยู่บนเว็บ

เช่น ตรงนี้สีฟ้า ซึ่งฟ้ามีหลายสีมาก ๆ ทีม Design และ Developer เห็นเป็นสีฟ้าที่เฉดเท่าไหร่ ?​

3. เป็นการ**สร้าง UI/pattern library**

4. มี **Design Document** ที่บอกว่า Component หน้าตาแบบนี้ใช้ยังไง ใช้ตอนไหนบ้าง

<br><hr><br>

## Start Building Design System With Chakra UI

เราสามาร

```js
// 1. Import the extendTheme function
import { extendTheme } from "@chakra-ui/react";

// 2. Extend the theme to include custom colors, fonts, etc
const colors = {
  brand: {
    900: "#1a365d",
    800: "#153e75",
    700: "#2a69ac",
  },
};

const theme = extendTheme({ colors });

// 3. Pass the `theme` prop to the `ChakraProvider`
function App() {
  return (
    <ChakraProvider theme={theme}>
      <App />
    </ChakraProvider>
  );
}
```

<br><hr><br>
