# State

เราจะสร้าง State ด้วย `React.useState` ที่มี parameter เป็น state ตั้งต้น และ return ค่าออกมาเป็น array ของ state

เรามาลองดู Application เล็ก ๆ กันที่เรียกว่า Counter App

```js
import React, { useState } from "react";

function App() {
  const [number, setNumber] = useState(1);

  function handleAddNumber() {
    setNumber(number + 1);
  }

  return (
    <div className="counter-app">
      Counter: {number}
      <button onClick={handleAddNumber}>Add number</button>
    </div>
  );
}
```

🌟 **ข้อควรรู้**

เมื่อเราทำการอัพเดท number เสร็จเรียบร้อยแล้ว React จะทำการ Render Component Counter ใหม่ทั้งหมด
State เหมือนกับ Props ต่างกันตรงที่ว่า State นั้นมันถูก Scope ไว้ที่ Component นั้น ๆ และถูกควบคุมด้วย Component นั้น ๆ

<br><hr><br>

## Array Rendering

เราสามารถนำ State ที่เป็น Array มาแสดงผลบนหน้าเว็บได้ด้วย `Array.map()`

⚠️ และที่สำคัญอย่าลืมใส่ key prop ให้กับ element ที่ map ออกมาแต่ละชิ้นด้วย ในที่นี้เราจะใส่ที่ `<div key={product.id} className="product-item">`

```js
function Cart() {
  const [products, setProducts] = React.useState(MOCK_PRODUCTS);
  return (
    <div className="cart">
      {products.map((product) => {
        return (
          <div key={product.id} className="product-item">
            <h3 class="product-title">Product Title: {product.title}</h3>
            <p class="product-description">
              <b>Product Description:</b> {product.description}
            </p>
            <div class="product-price"><b>Product Price:</b> {product.price} Baht</div>
            <hr>
          </div>
        );
      })}
    </div>
  );
}

```

**ข้อมูล MOCK_PRODUCTS**

```js
const MOCK_PRODUCTS = [
  {
    title: "XiaoMi Air Purifier",
    description: "Lorem ipsum dolor sit amet.",
    price: 500,
  },
  {
    title: "XiaoMi Air Purifier",
    description: "Lorem ipsum dolor sit amet.",
    price: 600,
  },
  {
    title: "Macbook Pro M1",
    description: "Lorem ipsum dolor sit amet.",
    price: 20,
  },
];
```

<br><hr><br>

## Key Takeaway 🌟

- `React.useState` hook เป็น ฟังก์ชั่นที่รับ parameter เป็น state ตั้งต้น และ return ค่าออกเป็น array ของ state และ ฟังก์ชั่นที่ใช้อัพเดท State

- State เหมือนกับ Props ต่างกันตรงที่ว่า State นั้นมันถูก Scope ไว้ที่ Component นั้น ๆ และถูกควบคุมด้วย Component นั้น ๆ

<br><hr><br>

## Exercises 🏅

A) ให้ทำการเพิ่ม Function การทำงานของ Counter App

- Counter App สามารถที่จะ Reset Counter เป็น 0 ได้
- Counter App สามารถที่จะ Subtract Counter ออกทีละ 1 ได้

B) ให้นำข้อมูล Bills ออกมาแสดงผลผ่านหน้าเว็บ [(ดูข้อมูลได้ที่นี่)](https://gist.github.com/napatwongchr/8ac5740d326984ccd6700584301ecc72)

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
