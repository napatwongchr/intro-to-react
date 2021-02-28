# Custom Hook

สมมุติว่าหน้า Single Post Page ต้องการที่จะดึงข้อมูล Post List ด้วยเช่นเดียวกัน เราจะทำยังไงดีนะ ?​ สิ่งแรกที่เราคิดออกเลยคือก็ Copy and Paste เลยสิ 🤓 แน่นอนว่ามันทำงานได้ แต่ว่ามันก็จะรู้สึกแปลก ๆ เนอะเพราะว่า code มันซ้ำซ้อน

## Creating Custom Hook

ให้เราสร้างไฟล์ใหม่ `src/utilities/posts` จากนั้นสร้าง usePosts function ขึ้นมา ซึ่งเราจะย้าย logic การ fetch ข้อมูล posts จาก server มาอยู่ใน usePosts พร้อมทั้ง posts state และ isFetchingError state

```js
import { useEffect, useState } from "react";

export function usePosts() {
  const [posts, setPosts] = useState([]);
  const [isFetchingError, setIsFetchingError] = useState(null);

  useEffect(() => {
    getPosts();
  }, []);

  async function getPosts() {
    try {
      let response = await fetch("http://localhost:8000/posts");
      let posts = await response.json();
      setPosts(posts.data);
    } catch (error) {
      setIsFetchingError(true);
    }
  }

  return { posts, isFetchingError };
}
```

จากนั้นให้เราไปเรียกใช้ usePosts ที่ HomePage component

```js
import { usePosts } from "../utilities/posts";

export default function HomePage() {
  let { posts, isFetchingError } = usePosts();

  // Rest of codes
}
```

เราจะได้ error ว่า `'setPosts' is not defined` error นี้จะเกิดขึ้นตรง function ในการ delete post เนื่องจากว่าเราย้าย code ส่วน setPosts ไปอยู่ใน usePosts เรียบร้อยแล้ว ดังนั้นเราจะย้าย deletePost function เข้าไปข้างใน usePosts แล้ว return ออกมา

```js
export function usePosts() {
  const [posts, setPosts] = useState([]);
  const [isFetchingError, setIsFetchingError] = useState(null);

  // Skipped code

  async function deletePost(postId) {
    let url = "http://localhost:8000/posts/" + postId;
    let response = await fetch(url, { method: "DELETE" });

    if (response.ok) {
      let newPosts = posts.filter((post) => {
        return post.id !== postId;
      });

      setPosts(newPosts);
    } else {
      console.log("Delete failed !");
    }
  }

  return { posts, isFetchingError, deletePost };
}
```

จากนั้นเราก็สามารถนำ usePosts ไป import ใช้ได้ในที่ ๆ เราอยากจะใช้ เช่น เมื่อตอนต้นเราบอกว่าเราจะเอาไปใช้ในหน้า Single Post Page

```js
import { usePosts } from "../utilities/posts";

function SinglePostPage() {
  const { posts } = usePosts();

  // Skipped codes
}

export default SinglePostPage;
```

## Bonus Exercises 🏅

ให้แสดง Post List ที่หน้า Single Post Page ด้วย Custom Hook
