# React

ก่อนที่เราจะใช้ React เรามาลองสร้าง Element บนหน้าเว็บด้วย Vanilla JavaScript กันก่อน
เขียน div ที่มี id เป็น root ขึ้นมา

## Creating HTML Elements With Vanilla JavaScript

```html
<body>
  <div id="root"></div>
</body>
```

ต่อไปเราจะทำการสร้างข้อความ "Hello, React !" ลงบนหน้าเว็บภายใต้ div element เราจะเขียน script tag ขึ้นมา แล้วทำการหา div ที่มี id เป็น root ไปเก็บไว้ในตัวแปร rootElement ด้วย document.getElementById

```html
<body>
  <div id="root"></div>
  <script>
    const rootElement = document.getElementById("root");
  </script>
</body>
สร้าง element h1 ขึ้นมาโดยมีข้อความ "Hello, React !" ด้วย document.createElement
<body>
  <div id="root"></div>
  <script>
    const rootElement = document.getElementById("root");
    const element = document.createElement("h1");
  </script>
</body>
```

จากนั้น assign string "Hello, React !" ลงไปใน attribute ของ element ซึ่งก็คือ textContent และ className เป็น "hello-react-text"

````html
<body>
  <div id="root"></div>
  <script>
    const rootElement = document.getElementById("root");
    const element = document.createElement("h1");
    element.textContent = "Hello, React !";
    element.className = "hello-react-text";
  </script>
</body>

ต่อไปเราจะเอา element ไปแสดงผลในหน้าเว็บด้วยการ append element เข้าไปใน
rootElement ```html
<body>
  <div id="root"></div>
  <script>
    const rootElement = document.getElementById("root");
    const element = document.createElement("h1");
    element.textContent = "Hello, React !";
    element.className = "hello-react-text";
    rootElement.append(element);
  </script>
</body>
````

ถ้าเราเปิดหน้าเว็บขึ้นมา เราจะเห็น Hello, React !

<br><hr><br>

## Key Takeaway 🌟

- เราสร้าง element บนหน้าเว็บแบบดั้งเดิมด้วย Vanilla JavaScript ด้วย document API ของ browser ซึ่งก็คือ `document.createElement`

- เราสามารถจัดการ element ด้วยการหา element นั้น ๆ มาจาก `document.getElementById` ซึ่งเป็น selector API ของ browser

- เราสามารถสร้าง UI บนหน้าเว็บด้วย API ของ Browser แบบดั้งเดิมตามโค้ดตัวอย่างด้านบน
  ต่อไปเราจะ refactor โค้ดส่วนนี้โดยใช้ React กัน
