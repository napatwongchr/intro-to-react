# Chakra Basics

## Style Props

Chakra ใช้ concept ของ **style props** ในการเปลี่ยนแปลง style ของ component

```js
import { Box } from "@chakra-ui/react";

<Box m="10px" width="100px" height="100px" bg="tomato" color="white">
  Tomato
</Box>;
```

- `m` คือ margin
- bg คือ background
- width, height, color ตรงตัวกับใน css ปกติ

[ดูข้อมูลเพิ่มเติมได้ที่นี่](https://chakra-ui.com/docs/features/style-props)

<br><hr><br>

## Chakra Components

Chakra จะมี **Component built-in สำเร็จรูป** ทำให้เราสามารถที่จะสร้าง UI ได้ไวขึ้นกว่าเดิมมาก

<br><hr><br>

## Layout

การสร้างกล่องบนหน้าเว็บปกติเราจะใช้ div tag ใน chakra จะมี component `Box`

```js
import { Box } from "@chakra-ui/react";

<Box bg="tomato" w="100%" p={4} color="white">
  This is the Box
</Box>;
```

ถ้าเราจะสร้าง div ที่เป็น flex box เราจะใช้ component `Flex`

```js
import { Flex } from "@chakra-ui/react";

<Flex>
  <Box p="4" bg="red.400">
    Box 1
  </Box>
  <Spacer />
  <Box p="4" bg="green.400">
    Box 2
  </Box>
</Flex>;
```

## Typography

ถ้าเราจะใส่ข้อความบนหน้าเว็บเราจะใช้ component `Text`

```js
import { Text, Stack } from "@chakra-ui/react";

<Stack spacing={3}>
  <Text fontSize="6xl">(6xl) In love with React & Next</Text>
  <Text fontSize="5xl">(5xl) In love with React & Next</Text>
  <Text fontSize="4xl">(4xl) In love with React & Next</Text>
  <Text fontSize="3xl">(3xl) In love with React & Next</Text>
  <Text fontSize="2xl">(2xl) In love with React & Next</Text>
  <Text fontSize="xl">(xl) In love with React & Next</Text>
  <Text fontSize="lg">(lg) In love with React & Next</Text>
  <Text fontSize="md">(md) In love with React & Next</Text>
  <Text fontSize="sm">(sm) In love with React & Next</Text>
  <Text fontSize="xs">(xs) In love with React & Next</Text>
</Stack>;
```

สิ่งที่น่าสนใจสำหรับ Text component คือ props `isTruncated`

```js
<Text color="gray.500" isTruncated>
  Lorem ipsum is placeholder text commonly used in the graphic, print, and
  publishing industries for previewing layouts and visual mockups.
</Text>
```

ถ้าเราจะใส่หัวข้อของข้อความเราจะใช้ `Heading` component

```js
<Heading as="h1" size="4xl" isTruncated>
  (4xl) In love with React & Next
</Heading>
```

## Buttons

เราจะใช้ `Button` component ในการสร้างปุ่ม

```js
import { Button, Stack } from "@chakra-ui/react";

<Stack spacing={4} direction="row" align="center">
  <Button colorScheme="teal" size="xs">
    Button
  </Button>
  <Button colorScheme="teal" size="sm">
    Button
  </Button>
  <Button colorScheme="teal" size="md">
    Button
  </Button>
  <Button colorScheme="teal" size="lg">
    Button
  </Button>
</Stack>;
```

## Inputs

ตัวอย่าง Input components

```js
import { Input } from "@chakra-ui/react";

<Stack spacing={3}>
  <Input placeholder="extra small size" size="xs" />
  <Input placeholder="small size" size="sm" />
  <Input placeholder="medium size" size="md" />
  <Input placeholder="large size" size="lg" />
</Stack>;
```

🌟 **ที่ยกตัวอย่างมาทั้งหมดนั้นเป็นแค่ส่วนหนึ่งของ Chakra Component ให้เราไปลองไล่ดูใน [Document](https://chakra-ui.com/docs/getting-started) ต่อมันจะมี Component ให้เราเลือกใช้เยอะมาก ๆ**

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
