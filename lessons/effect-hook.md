# Effect Hook

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

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
