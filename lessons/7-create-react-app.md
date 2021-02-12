# Create React App

Create React App คือ เครื่องมือที่ Set up environment สำหรับพัฒนา React Application ให้เรียบร้อยแล้วโดยที่เราไม่ต้องไปนั่ง Set up เอาเองตั้งแต่แรก

<br><hr><br>

## Let's Use It !

เราสามารถที่จะเรียกใช้ Create React App ได้ด้วย npx ตามข้างล่างเลย

```
npx create-react-app my-app
cd my-app
npm start
```

<br><hr><br>

## Import and Export

**1. Named Import**

```js
// อยู่ในไฟล์ Counter.js

function Counter() {
  return <h1>Counter</h1>
}

export Counter
```

เวลา Import เข้ามาใช้ในไฟล์ App

```js
// อยู่ในไฟล์ App.js
import { Counter } from "./Counter";

function App() {
  return (
    <div className="app-container">
      <Counter />
    </div>
  );
}
```

**2. Module Import**

```js
// อยู่ในไฟล์ Counter.js

function Counter() {
  return <h1>Counter</h1>;
}

export default Counter;
```

```js
// อยู่ในไฟล์ App.js
import Counter from "./Counter";

function App() {
  return (
    <div className="app-container">
      <Counter />
    </div>
  );
}
```

<br><hr><br>

## Exercises 🏅

A) ให้สร้าง Component `GreetingMessage` ที่แสดงข้อความทักทาย ซึ่งข้อความสามารถทักทายแต่ละคนได้

**เงื่อนไข:** สร้างไว้อีก File แล้ว Import เข้ามาใช้ใน App Component

B) ให้สร้าง Component `ProductItem` ที่แสดงข้อมูล Product แตกต่างกันออกไป

ข้อมูล Product มีดังนี้

- title: "XiaoMi Air Purifier"
- description: "Lorem ipsum dolor sit amet."
- price: 500

**เงื่อนไข:** สร้างไว้อีก File แล้ว Import เข้ามาใช้ใน App Component
