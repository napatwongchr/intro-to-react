# Component Refactoring

สังเกตไหม ว่า post app header เราซ้ำกันอยู่ทั้งสองที่ และแววว่าเราจะนำไปใช้ในหน้าอื่น ๆ ด้วย

```html
<div className="postapp-header">
  <h1>Post App</h1>
  <button className="postapp-header-add-button">Add Post</button>
</div>
```

**เมื่อมี code ที่ซ้ำ ๆ กันเราทำยังไงนะ ?​**

คำตอบคือ แยกออกมาสร้างเป็น component ใหม่ เราจะมาแยก post app header ออกมาเป็น component ใหม่กัน ให้เราสร้างไฟล์ `Header.js` ไว้ใน `src/components/Header.js` จากนั้นก็ให้เขียน Component ขึ้นมา

```js
function Header() {
  return (
    <div className="postapp-header">
      <h1>Post App</h1>
      <button className="postapp-header-add-button">Add Post</button>
    </div>
  );
}
```

จากนั้นให้เรา import Header component นี้ไปใช้ใน AddPostPage component แล้วทำการเรียกใช้

```js
// AddPostPage.js
import Header from "../components/Header";

function AddPostPage() {
  // Skipped codes
  return (
    <div className="postapp-add-post-container">
      <Header />
    </div>
  );
}
```

จากนั้นให้เรานำ Header component ไปใช้ใน HomePage ด้วย **แต่ !** เราจะสังเกตว่า HomePage มีการแสดงผลของ Header เป็นอีกแบบ ซึ่งจะมีปุ่ม Add Post ด้วย เราจะเขียน Component ให้ support รูปแบบทั้ง 2 แบบ

```js
// Header.js
import "./Header.css";

function Header(props) {
  const { title, rightSectionItem } = props;
  return (
    <div className="postapp-header">
      <div className="postapp-header-title">
        <h1>{title}</h1>
      </div>
      {rightSectionItem && (
        <div className="postapp-header-right-section">{rightSectionItem}</div>
      )}
    </div>
  );
}

export default Header;
```

เมื่อเราเขียน Header component เสร็จเรียบร้อยแล้ว สิ่งที่เราต้องทำต่อไปคือเอาไปใช้ใน HomePage และ AddPostPage Components

```js
// AddPostPage.js
import Header from "../components/Header";

function HomePage() {
  // Skipped codes
  return (
    <div>
      <Header
        title="Post App"
        rightSectionItem={
          <button
            className="postapp-add-post-button"
            onClick={handleAddPostClick}
          >
            Add Post
          </button>
        }
      />
    </div>
  );
}
```

```js
// AddPostPage.js
import Header from "../components/Header";

function HomePage() {
  // Skipped codes
  return (
    <div className="postapp-add-post-container">
      <Header title="Post App" />
    </div>
  );
}
```

<br><hr><br>

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
