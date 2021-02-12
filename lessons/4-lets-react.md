# Let's React

จากบทที่แล้วเราได้ทำการสร้าง h1 element ภายใต้ div id root ด้วย Vanilla JS ในบทเรียนนี้เราจะเริ่มใช้ React ในการสร้าง Elements

```html
<body>
    <div id="root"></div>
    <script>
        const rootElement = document.getElementById("root")
        const element = document.createElement("h1")
        element.className="hello-react-text"
        element.textContent = "Hello, React !"
        rootElement.append(element)
    </script>
</body>
```

ก่อนอื่นเราจะไปเอา package ของ React มาจาก CDN ที่ UNPKG แล้ว link ไฟล์เข้ามาในโปรเจคของเราด้วย `<script src="...">`

```html
<body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@17.0.0/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@17.0.0/umd/react-dom.development.js"></script>
    ...
</body>
```

เมื่อเรา link มาแล้วเราจะสามารถเรียกใช้ API ของ React ได้ เริ่ม refactor มาเป็น React กันดีกว่า

```html
<script>
    const rootElement = document.getElementById("root")
    const element = React.createElement(
        "h1",
        { className: "hello-react-text" },
        "Hello, React !"
    )
    ReactDOM.render(element, rootElement)
</script>
```

จากโค้ดด้านบน

1. เราสร้าง element ขึ้นมาใหม่ด้วย `React.createElement`  ซึ่งรับ parameters ดังนี้
     - ตัวแรกคือ string element tag
     - ตัวที่สองคือ attributes object ของ element
     - ตัวที่สามคือ children ของ element

2. จากนั้น เรา assign เข้าไปในตัวแปร element เหมือนเดิม

3. ต่อไป เราจะแสดงผล element ที่สร้างไปบนหน้าเว็บด้วย `ReactDOM.render` ซึ่งรับ parameters ดังนี้
     - ตัวแรกคือ element ท่ี่ต้องการจะ render
     - ตัวที่สองคือ element ที่จะถูกใช้ในการ render element ที่ส่งเข้ามาผ่าน parameter ตัวแรก

4. ลองรันโค้ดบน browser ดูเราจะเห็น "Hello, React !" และถ้าลองเปิด devtool เราจะสังเกตเห็น className ที่เราใส่ลงไปเป็น attribute ด้วย

แล้วถ้าเราอยากสร้าง element ที่เป็น child ของอีกตัวหล่ะ เราสามารถเขียนเป็นแบบนี้ได้

```html
<body>
    <div id="root"></div>
    
    <script>
        const rootElement = document.getElementById("root")
        const element = React.createElement(
            "div",
            { className: "container" },
            React.createElement(
                "h1",
                { className: "hello-react-text" },
                "Hello, React !"
            )
        )
        ReactDOM.render(element, rootElement)
    </script>
</body>
```

<br><hr><br>

## Key Takeaway 🌟

- เราสามารถสร้าง element บนหน้าเว็บด้วย `React.createElement`

- เราเอา element ไปแสดงผลบนหน้าเว็บด้วย `ReactDOM.render`

- เราจะสังเกตเห็นว่า เวลาเราใช้ `React.createElement` ในการสร้าง HTML Elements มากขึ้นเรื่อย code มันชักจะเริ่มอ่านยาก ต่อไปเราจะมาดูวิธีจัดการปัญหานี้ของ React ซึ่งก็คือ **JSX**