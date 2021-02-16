# State

เราจะสร้าง State ด้วย `React.useState` ที่มี parameter เป็น state ตั้งต้น และ return ค่าออกมาเป็น array ของ state

เรามาลองดู Application เล็ก ๆ กันที่เรียกว่า Counter App

```js
function App() {
  const [number, setNumber] = React.useState(1);

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

เราสามารถนำ State ที่เป็น Array มาแสดงผลได้แบบนี้

```js
function Cart() {
  const [products, setProducts] = React.useState(MOCK_PRODUCTS);
  return (
    <div className="cart">
      {products.map((product) => {
        return (
          <div className="product-item">
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

B) ให้นำข้อมูล Bills ออกมาแสดงผลผ่านหน้าเว็บ

```js
const BILLS_MOCK = [
  {
    id: "1",
    transactionDate: "2020-08-01",
    total: 12345,
    location: "Chonburi",
    paymentType: "Cash",
    member: {
      name: "Tle",
      age: "26",
    },
    pointRate: 0.01,
  },
  {
    id: "2",
    transactionDate: "2020-08-01",
    total: 12298,
    location: "Chonburi",
    paymentType: "Cash",
    member: {
      name: "Tle",
      age: "26",
    },
    pointRate: 0.01,
  },
  {
    id: "3",
    transactionDate: "2020-08-01",
    total: 41012,
    location: "Suphanburi",
    paymentType: "Mastercard",
    member: {
      name: "Peter",
      age: 33,
    },
    pointRate: 0.01,
  },
  {
    id: "4",
    transactionDate: "2020-08-02",
    total: 24826,
    location: "Trang",
    paymentType: "MasterCard",
    member: {
      name: "Ball",
      age: 31,
    },
    pointRate: 0.01,
  },
  {
    id: "5",
    transactionDate: "2020-08-21",
    total: 47202,
    location: "Trat",
    paymentType: "VISA",
    member: null,
  },
  {
    id: "6",
    transactionDate: "2020-08-15",
    total: 29815,
    location: "Lopburi",
    paymentType: "VISA",
    member: {
      name: "Tle",
      age: 26,
    },
    pointRate: 0.01,
  },
  {
    id: "7",
    transactionDate: "2020-08-14",
    total: 28375,
    location: "Chonburi",
    paymentType: "VISA",
    member: {
      name: "Jak",
      age: 36,
    },
    pointRate: 0.01,
  },
  {
    id: "8",
    transactionDate: "2020-08-19",
    total: 26923,
    location: "Chiang Mai",
    paymentType: "QR",
    member: null,
  },
];
```
