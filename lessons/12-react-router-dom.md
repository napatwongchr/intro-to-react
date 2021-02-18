# React Router Dom

ต่อไปเราจะทำให้สามารถที่จะ click ที่ปุ่ม **"Add Post"** แล้วไปที่หน้า Add Post Page ตามที่เราออกแบบกันไว้

<br><hr><br>

## Let's Build Page Router

1. ให้เราทำการ install package ที่ชื่อว่า **react-router-dom** ให้ไปที่ CMD หรือ Terminal จากนั้น Run คำสั่ง

`npm install react-router-dom`

2. เมื่อ Install เสร็จเรียบร้อยแล้วเราจะทำการ refactor code ด้วยการสร้าง Component ใหม่ขึ้นมาชื่อว่า `HomePage` ชื่อไฟล์ว่า `HomePage.js` ภายใต้ Folder `src/pages/HomePage.js` แล้วให้ย้าย code ทั้งหมดที่เกี่ยวกับ Post App ในหน้านี้ไปที่ไฟล์ `HomePage.js`

```js
// src/pages/HomePage.js
import { useState, useEffect } from "react";

export default function HomePage() {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    getPosts();
  }, []);

  async function getPosts() {
    let response = await fetch("http://localhost:8000/posts");
    if (response.ok) {
      let { data } = await response.json();
      setPosts(data);
    } else {
      console.log("Handle Response Not OK");
    }
  }

  return (
    <div>
      <div className="postapp-header">
        <h1>Post App</h1>
        <button className="postapp-header-add-button">Add Post</button>
      </div>
      <div className="postapp-postlist">
        {posts.map((post) => {
          return (
            <div className="postapp-postitem">
              <h3 className="postitem-title">{post.title}</h3>
              <p className="postitem-content">{post.content}</p>
              <button className="postitem-edit-button">Edit</button>
              <button className="postitem-delete-button">Delete</button>
            </div>
          );
        })}
      </div>
    </div>
  );
}
```

3. ภายใน `App.js` เราจะทำการ import components จาก react-router-dom ทั้งหมดสามตัวคือ **BrowserRouter, Switch, Route** จากนั้นทำการ Import HomePage ที่เราแยกไฟล์ออกไปมาใช้งานด้วย แล้วทำการสร้าง router ตาม code ด้านล่าง

```js
import { BrowserRouter, Switch, Route } from "react-router-dom";

import HomePage from "./pages/HomePage";

import "./App.css";

function App() {
  return (
    <div>
      <BrowserRouter>
        <Switch>
          <Route path="/home" component={HomePage} />
        </Switch>
      </BrowserRouter>
    </div>
  );
}

export default App;
```

มาดูการทำงานเพิ่มเติมนิดนึง

- **BrowserRouter** เป็นตัว ที่ทำให้หน้า UI ของเรา Sync เข้าไป Path ที่เราเข้า
- **Route** เป็นตัวที่บอกว่า URL Path ไหนให้แสดงผล Page Component อะไร ซึ่งเราจะต้องส่ง Props สองตัวเข้าไปที่ Route Component
  - ซึ่งก็คือ path เป็นตัวบอก URL ของเว็บ
  - component เป็น Page Component ที่เราจะ render
- **Switch** เป็นตัวที่ทำให้ Component ที่จะแสดงผลใน URL นั้น ๆ สลับหน้ากัน

เมื่อ refactor code เสร็จเรียบร้อย ให้เราทำการเข้า `http://localhost:3000/home` ( ⚠️ **อย่าลืม /home นะ เพราะเรา set path ไว้ใน** `<Route />`)

<br><hr><br>

## Link The Page

เราสามารถที่จะ Link จาก Page นึงไปอีก Page นึงได้หลายวิธี

- Link ด้วย `useHistory`
- Link ด้วย Link Component

<br><hr><br>

## useHistory

เราจะทำการ Import useHistory function มาจาก react-router-dom

```js
import { useHistory } from "react-router-dom";

// Rest of codes ...
```

จากนั้นให้คิดต่อว่าเราทำการเปลี่ยน Page ตอนไหน ?​ ตอนที่เรา click ปุ่ม **"Add Post"** ให้เราทำการเขียน function `handleAddPostClick` ภายใต้ Component

```js
function handleAddPostClick() {
  history.push("/add");
}
```

แล้วนำไปใส่ใน onClick prop ของ ปุ่ม Add Post

```js
<button className="postapp-header-add-button" onClick={handleAddPostClick}>
  Add Post
</button>
```

Code สุดท้ายจะได้หน้าตาประมาณแบบนี้

```js
import { useState, useEffect } from "react";
import { useHistory } from "react-router-dom";

export default function HomePage() {
  let history = useHistory();
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    getPosts();
  }, []);

  async function getPosts() {
    let response = await fetch("http://localhost:8000/posts");
    if (response.ok) {
      let { data } = await response.json();
      setPosts(data);
    } else {
      console.log("Handle Response Not OK");
    }
  }

  function handleAddPostClick() {
    history.push("/add");
  }

  return (
    <div>
      <div className="postapp-header">
        <h1>Post App</h1>
        <button className="postapp-header-add-button">Add Post</button>
      </div>
      <div className="postapp-postlist">
        {posts.map((post) => {
          return (
            <div className="postapp-postitem">
              <h3 className="postitem-title">{post.title}</h3>
              <p className="postitem-content">{post.content}</p>
              <button className="postitem-edit-button">Edit</button>
              <button className="postitem-delete-button">Delete</button>
            </div>
          );
        })}
      </div>
    </div>
  );
}
```

<br><hr><br>

## Link Component

TBD
