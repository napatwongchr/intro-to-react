# React Hooks

React Hooks คือ **function ที่ทำให้เราใช้ Feature ของ React ได้ใน Function component**

<br><hr><br>

## Why React Hooks ?

React Team ออก Feature ตัวนี้มาด้วยเหตุผล 3 ข้อหลัก ๆ

**1. การ Reuse ใช้ Logic ระหว่าง Component**

ปกติแล้วเราจะใช้ Higher-order component (HOC) หรือ Render Props ในการ Reuse Logic ระหว่าง Components ซึ่งทำให้เกิด wrapper hell

**2. Component ที่ซับซ้อนมากๆ จะทำให้ยากต่อการทำความเข้าใจ**

การที่ใช้ Lifecycles methods ทำให้ Logic ต่างๆ กระจัดกระจายกันออกไปทำให้ดูยาก

**3. Class เป็นสิ่งที่ทำความเข้าใจยากต่อคน และคอมพิวเตอร์**

this เป็นสิ่งที่ทำความเข้าใจยาก และมีผลต่อกับ optimisation เวลา compile

<br><hr><br>

## State Hook

State Hook คือ function ที่ทำให้เราใส่ state เข้าไปใน Function component ได้

```js
import React, { useState } from "react";

function Counter() {
  const [counter, setCounter] = useState(0);
  return (
    <div>
      <h1>{counter}</h1>
      <button onClick={() => setCounter(counter + 1)}>Add</button>
      <button onClick={() => setCounter(counter - 1)}>Subtract</button>
    </div>
  );
}

export default Counter;
```

<br><hr><br>

## Effect Hook

Effect Hook คือ function ที่ทำให้เราทำ **Side effects** ได้ใน Function Component

**Side Effects** คือ การที่เราเปลี่ยน State ของโปรแกรมจากทางอ้อม เช่น เราเรียก Function นั้น ๆ แล้วได้ผลลัพธ์ แล้วเราได้ Effect นั้นกลับมาเมื่อไหร่ไม่รู้ แล้วมาเปลี่ยน State ของโปรแกรมของเรา

![Side Effect Illustration](./images/side-effects-illustration.png)

**ตัวอย่าง Side Effects**

- แก้ไข Variable ที่อยู่นอก Scope ตัวเอง (Ex. Global variable)
- Logging จาก console
- Network requests
- รัน process อื่น ๆ จากข้างนอก Application ของตัวเอง
- เขียนไฟล์
- Render Elements เข้าไปในหน้าเว็บ

ลองมาใช้ Effect Hook กัน

```js
import React, { useEffect } from "react";

function EffectCounter() {
  useEffect(() => {
    console.log("Run the side effect operations"); // Run ทุกครั้งที่ Component render
  });

  return (
    <div>
      <h1>0</h1>
    </div>
  );
}

export default EffectCounter;
```

### Array Dependency List

```js
useEffect(() => {
  console.log(‘Sync effect with ALL STATE’)
})
```

รันทุก ๆ ครั้งที่ Component render การที่ไม่ใส่ [] หมายความว่า Component จะ Sync กับทุก State ที่เปลี่่ยนแปลง

```js
useEffect(() => {
  console.log(‘Sync effect with NO STATE’)
}, [])
```

รันครั้งแรกที่ Component render เนื่องจากเราใส่ [] หมายความว่า มันไม่ต้อง Sync กับ State อะไรเลย

```js
useEffect(() => {
  console.log(‘Sync effect with THESE STATES')
}, [state1, state2, state3, stateEtc])
```

รันทุก ๆ ครั้งที่ state1 หรือ state2 หรือ state3 หรือ stateEtc เปลี่ยนแปลงใน Component

🌟 **จุดประสงค์ที่แท้จริงของ useEffect คือ การ Sync Side Effects เข้ากับ State ของ Application ของเรา**

### useEffect and Component Lifecycles

จริง ๆ แล้วถ้าเราถามว่า Class component มี Lifecycle methods ต่าง ๆ แล้วถ้าเราใช้แต่ Function component หล่ะ​ ?​ เราจะจัดการ Cases ที่ Class component จัดการ ได้ยังไง

ตัวอย่าง

```js
import { useState, useEffect } from "react";

function EffectCounter() {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    // Could compare to componentDidMount
    console.log("Run this effect only at the first time");
  }, []);

  useEffect(
    function () {
      console.log(
        "Run this effect at the first time and run again when counter has changed"
      );
      return () => {
        // Could compare to componentWillUnmount
        console.log("Run when component will be disappear from web page");
      };
    },
    [counter] // Could compare to componentDidUpdate
  );

  function handleAddCounter() {
    setCounter(counter + 1);
  }

  return (
    <div>
      <h1>Counter: {counter}</h1>
      <button onClick={handleAddCounter}>Add</button>
    </div>
  );
}

export default EffectCounter;
```

🌟 **จริงๆแล้วเราสามารถเทียบการทำงานกันได้แบบข้างบน แต่จริงๆแล้วมันทำงานคนละแบบกัน ถ้าคิดแยกจะดีกว่า**

<br><hr><br>

## Context Hook

โดยปกติแล้ว React จะมีปัญหาเรื่องของ **“Prop drilling”** คือ การที่เรามี Parent แล้วมี Child ที่ต้องการข้อมูลจาก Parent ห่างลงไปอีกหลาย ๆ ชั้นทำให้เราต้อง Pass props ลงไปผ่านทุก ๆ ชั้น

![Props Drilling Problem](./images/props-drilling-1.png)

**React Context เกิดมาแก้ไขปัญหานี้** ทำให้เราเหมือนสร้างวาร์ปให้กับข้อมูลส่งไปให้ Child ที่อยู่ชั้นลึก ๆ ได้เลย​โดยไม่ต้องส่งผ่านมาเรื่อย ๆ

![Context API](./images/props-drilling-2.png)

<br><hr><br>

## Reducer Hook

Reducer Hook คือ Redux แต่อยู่ในรูปแบบของ Hook **เราสามารถ Update state ผ่าน Action type ได้ มีประโยชน์เวลาต้องจัดการ State เยอะ ๆ ใน Component**

![Use Reducer Hook](./images/use-reduce-hook.png)

<br><hr><br>

## Callback Hook

TBD

<br><hr><br>

## Memo Hook

TBD

<br><hr><br>

## Bonus Exercises 🏅

- [Click here !](https://github.com/napatwongchr/codecamp-hook-exercises)

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
