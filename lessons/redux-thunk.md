# Redux Thunk

Redux Thunk ทำให้เราสามารถเขียน Asynchronous Logic ได้ใน redux flow เรามาลองดูกัน

เราจะทำการจัดการ State ของ Posts ด้วย Redux ให้เราสร้าง `src/features/postsSlice.js` ขึ้นมา

```js
import { createSlice } from "@reduxjs/toolkit";

const postsSlice = createSlice({
  name: "posts",
  initialState: {
    posts: [],
    status: "idle",
    error: null,
  },
  reducers: {},
  },
});

export default postsSlice.reducer;
```

- เราจะตั้งชื่อ slice นี้ว่า posts
- initialState ที่เกี่ยวข้องในการจัดการ posts state คือ posts array, status (idle, pending), และ error

จากนั้นให้เรา export reducer ออกไปเอาไปประกอบที่ `src/app/store`

```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";
import postsReducer from "../features/posts/postsSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
    posts: postsReducer,
  },
});
```

จากนั้นเราจะสร้าง function เอาไว้ดึงข้อมูล posts จาก server ชื่อว่า `getPosts`

```js
const getPosts = () => async (dispatch) => {
  dispatch(postsLoading());
  let response = await fetch("http://localhost:8000/posts");
  let posts = await response.json();
  dispatch(postsReceived(posts));
};

export { getPosts };
```

🌟 ให้สังเกตดี ๆ getPosts เป็น function ที่ return function ที่มี parameter เป็น dispatch ตัวนี้เราเรียกว่า **"Thunk"**

ใน Thunk เราสามารถเรียกใช้ dispatch function ได้

ซึ่งเราจะ dispatch `postsLoading` action เพราะว่าเวลาเราดึงข้อมูล posts state แรกที่เราจะเจอคือ loading state

จากนั้นเราจะทำการ fetch ข้อมูล เมื่อ fetch ข้อมูลเสร็จเราจะทำการ dispatch `postsReceived` action แล้วส่ง payload ไปเป็นข้อมูล posts ที่ได้มาจาก server

```js
const postsSlice = createSlice({
  name: "posts",
  initialState: {
    posts: [],
    status: "idle",
    error: null,
  },
  reducers: {
    postsLoading: (state) => {
      if (state.status === "idle") {
        state.status = "pending";
      }
    },
    postsReceived: (state, action) => {
      if (state.status === "pending") {
        state.status = "idle";
        state.posts = action.payload.data;
      }
    },
  },
});

export const { postsLoading, postsReceived } = postsSlice.actions;
```
