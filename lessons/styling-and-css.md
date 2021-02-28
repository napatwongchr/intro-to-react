# Styling and CSS

โดยปกติแล้ว React สามารถที่จะเขียน CSS ได้ด้วยการสร้างไฟล์ `.css` มาจากนั้นก็ให้ import เข้ามาในไฟล์ที่เราต้องการใช้ CSS Classes นั้น ๆ

ในไฟล์ App.js เราจะ import ไฟล์ CSS ที่เกี่ยวข้องเข้ามา

```js
import "./App.css";

function App() {
  return (
    <div className="postapp-header">
      <h1>Post App</h1>
      <button className="postapp-header-add-button">Add Post</button>
    </div>
  );
}
```

ภายใน App.css เราจะเขียน CSS ปกติ

```css
.postapp-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0px 15px;
  background-color: bisque;
}

.postapp-header-add-button {
  height: 40px;
}
```

<br><hr><br>

## Inline Styling

เราสามารถที่จะเขียน css แบบ inline ได้

⚠️ แต่ว่า inline style นั้นจะเขียนอยู่ในรูปแบบของ Object css properties จะต่างจากการเขียน css แบบปกติ ซึ่งจุดนี้ทำให้ Developer experience ของเราอาจจะไม่ดีมากนักในการเขียน css

```js
function App() {
  return (
    <div style={{
      display: "flex",
      justifyContent: "space-between",
      alignItems: "center",
      padding: "0px 15px",
      backgroundColor: "bisque",
    }}>
      <h1>Post App</h1>
      <button style={{
        height: "40px";
      }}>Add Post</button>
    </div>
  );
}
```

<br><hr><br>

## CSS IN JS

CSS In JS เป็น concept ที่เขียน **CSS ด้วย JS** ทำให้เราสามารถที่จะเขียน logic ที่มีความซับซ้อน CSS ของเราได้อย่างยืดหยุ่น เราจะแนะนำเครื่องมือที่ช่วยในการเขียน CSS ของเราด้วย concept ของ CSS in JS ก็คือ **"Emotion"**

<br><hr><br>

## Emotion

เราสามารถเขียน Styles ด้วย Emotion ได้หลายแบบ

- **CSS Prop**
- **Styled Component**
- Object Style

<br><hr><br>

## The CSS Prop

ให้เรา install emotion ลงมาใน project ก่อนด้วยคำสั่ง

`npm install --save @emotion/react`

`npm install --save-dev @emotion/babel-plugin`

แล้วลองเขียน component ขึ้นมา 1 ตัว จากนั้นให้เราใส่ `/** @jsxImportSource @emotion/react */` ไปที่ข้างบนสุดของไฟล์ component จากนั้น `import { css } from "@emotion/react";` แล้วเริ่มเขียน styles ด้วย css prop ได้ css ปกติเขียนยังไง css prop เขียนแบบนั้น

**ตัวอย่าง**

```js
/** @jsxImportSource @emotion/react */
import { css } from "@emotion/react";

function GreetingMessage() {
  return (
    <h1
      css={css`
        color: cornflowerblue;
        font-size: 50px;
      `}
    >
      Hello Codecamp 8 with Emotion{" "}
    </h1>
  );
}

export default GreetingMessage;
```

<br><hr><br>

## Styled Component

ถ้าเราจะเขียนในรูปแบบของ Styled Component ให้เรา install package เพิ่ม

`npm install --save @emotion/styled`

จากนั้นให้เรา `import styled from '@emotion/styled'` แล้วเริ่มเขียน styled component ได้เลย

เราจะสร้าง Styled Component ของ button กัน

```js
import styled from "@emotion/styled";

const StyledButton = styled.button`
  border-radius: 5px;
  background-color: khaki;
  height: 30px;
  width: 100px;
  color: crimson;
`;

// Skipped code

export default App;
```

จากนั้นเราจะเปลี่ยนปุ่ม Edit, Delete ให้กลายเป็น StyledButton ของเราที่สร้างไว้

```js
function App() {
  return (
    // Skipped codes
    <div className="post-list">
      <div className="post">
        <h3>Title: Post app</h3>
        <p>Post content</p>
        <div className="post-footer">
          <span>Author: John</span>
          <div className="post-footer-buttons">
            <StyledButton>Edit</StyledButton>
            <StyledButton>Delete</StyledButton>
          </div>
        </div>
      </div>
    </div>
  );
}
```

**เราสามารถส่ง Props เข้าไปใน Styled Component ได้ด้วย**

```js
<StyledButton primary={true}>Edit</StyledButton>
<StyledButton>Delete</StyledButton>
```

ตัว StyledButton ของเราจะสามารถรับ Props ผ่าน String template literal ได้ จากนั้นเราจะเขียน Condition ขึ้นมาว่าถ้า primary เป็น true ก็จะให้แสดงสี crimson แต่ถ้าไม่เป็น true ให้แสดง cornflowerblue

```js
const StyledButton = styled.button`
  border-radius: 5px;
  background-color: khaki;
  height: 30px;
  width: 100px;
  color: ${(props) => (props.primary ? "crimson" : "cornflowerblue")};
`;
```

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
