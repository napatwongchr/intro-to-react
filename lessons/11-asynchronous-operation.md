# Asynchronous Operation

จากหน้า Post Home Page เรามีการแสดงข้อมูลของ Post เราจะทำการดึงของมูลของ Post จากตัว Server ที่มีการเตรียมไว้ให้เรียบร้อยแล้ว

เปิด CMD หรือ Termial ขึ้นมาแล้วพิมพ์คำสั่ง `docker run -dit -p 8000:8000 --rm --name mypostapp napatwongchr/postapp` เพื่อทำการให้ Docker Generate Post App Server ขึ้นมาให้

<br><hr><br>

## API Document

เรามาดู API Document กันสักหน่อยว่ามีอะไรให้เราเรียกใช้บ้าง

**API Endpoint:** localhost:8000

| Method | Path       | Description       |
| ------ | ---------- | ----------------- |
| GET    | /posts     | Get all posts     |
| GET    | /posts/:id | Get post by id    |
| POST   | /posts     | Create post       |
| PUT    | /posts/:id | Update post by id |
| DELETE | /posts/:id | Delete post by id |

API ที่เราจะเรียกใช้ก็คือ GET /posts เพราะว่าเราอยากจะได้ Posts ทั้งหมด มาแสดงผลที่หน้าเว็บของเรา

<br><hr><br>

## Effect

เวลาเราจะทำการ fetch ข้อมูลจาก Server ให้เราเรียกใช้ `fetch()` ภายใน `useEffect` เท่านั้น `useEffect` เป็น Function ของ React ที่จะทำให้เราสามารถทำ **Side Effects** ได้ภายใน Function Component

```js
import { useEffect } from "react";

function App() {
  useEffect(() => {
    getPosts();
  }, []);

  async function getPosts() {
    let response = await fetch("http://localhost:8000/posts");

    if (response.ok) {
      let data = await response.json();
    } else {
      console.log("Handle Response Not OK");
    }
  }

  return (
    <div className="postapp-header">
      <h1>Post App</h1>
      <button className="postapp-header-add-button">Add Post</button>
    </div>
  );
}
```

- จากโค้ด เราเขียน function getPosts ขึ้นมาใหม่เพื่อดึงข้อมูล Posts จากนั้นข้างในเราจะใช้ `fetch` ในการต่อกับ Server และทำการขอข้อมูล Posts ผ่าน Endpoint `http://localhost:8000/posts` ด้วย `let response = await fetch("http://localhost:8000/posts");`

- เมื่อ response ok แล้วให้เราทำการ parse JSON response ออกมาเป็น Object ให้สามารถใช้งานได้ใน JS Application ด้วย `await response.json()`

- จากนั้นให้เราทำการนำ Posts ไปเก็บไว้ในตัวแปร State ด้วย `useState` (จากที่เรา Design กันจำได้มั้ยว่า Posts เป็น State ตัวนึงใน App ของเรา) 🤓

```js
import { useState, useEffect } from "react";

function App() {
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
    <div className="postapp-header">
      <h1>Post App</h1>
      <button className="postapp-header-add-button">Add Post</button>
    </div>
  );
}
```

<br><hr><br>

## Render Array Items

ยังมีอีกหนึ่งอย่างที่เราจะต้องทำต่อ คือ การ Render Posts จาก State ที่เราเก็บไว้ เราจะใช้ `Array.map()` ที่เราเรียนกันเข้ามาช่วย

```js
import { useState, useEffect } from "react";

function App() {
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
    <div className="postapp-header">
      <h1>Post App</h1>
      <button className="postapp-header-add-button">Add Post</button>
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
  );
}
```

<br><hr><br>

## Fetch Alternatives

Fetch เป็น Function Built-in ใน Web Browser แต่ยังมี Tools ตัวอื่น ๆ ที่นิยม และทำหน้าที่ เหมือนกันกับ fetch เช่น **[axios](https://github.com/axios/axios)**

วิธีการใช้ axios

1. ให้เราทำการ install package ด้วย npm

`npm install axios`

2. จากนั้นทำการ `import axios from 'axios'`

3. ทำการ Refactor getPosts function ได้เลย

```js
async function getPosts() {
  try {
    let response = await axios.get("http://localhost:8000/posts");
    setPosts(response.data);
  } catch (error) {
    console.log("Handle Response Not OK");
  }
}
```
