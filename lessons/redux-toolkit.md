# Redux Toolkit

การ Setup Redux และใช้งาน เป็นอะไรที่ค่อนข้างเหนื่อย และซับซ้อน เนื่องจากขั้นตอนเยอะ แถมเวลาใช้งานมันเพิ่มความซับซ้อนให้กับ Code ของเราประมาณนึงเลย

ทีมพัฒนา Redux เลยคิด Tool ขึ้นมาช่วยในการ Setup และใช้งานที่มีชื่อว่า [Redux Toolkit](https://redux-toolkit.js.org/)

Redux Toolkit เกิดมาขึ้นเพื่อทำให้เรา Setup และใช้งาน Redux ได้ง่ายมากยิ่งขึ้น

🌟 **ทีมพัฒนา Redux แนะนำการใช้ Redux Toolkit กับ Production App**

<hr><br><hr>

## Getting Start With Redux Toolkit

เราจะ Install package redux toolkit `npm install @reduxjs/toolkit react-redux` จากนั้นเราจะเริ่ม Setup Redux

**1. สร้าง Redux Store ก่อน**

- ให้สร้างไฟล์ไว้ที่ที่ `app/store.js`
- Store ของ redux-toolkit สามารถใช้ redux-thunk และ redux devtools extension ได้เราไม่ต้องไป setup เพิ่มเอง

```js
import { configureStore } from "@reduxjs/toolkit";

export default configureStore({
  reducer: {},
});
```

**2. เชื่อมต่อ Store เข้าไปใน React App**

```js
import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import store from "./app/store";
import { Provider } from "react-redux";

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```

**3. สร้าง Redux State Slice**

- Redux State Slice เป็นตัวที่จะรับ actions เข้ามาแล้วทำการ update app states ตาม actions ที่เข้ามา

```js
import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

**4. เพิ่ม Slice Reducers เข้าไปใน Store**

```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

**5. เรามาลองใช้ State และ Dispatch Action ใน Component กัน**

```js
import React, { useState } from "react";
import { useSelector, useDispatch } from "react-redux";
import { decrement, increment } from "./counterSlice";
import styles from "./Counter.module.css";

export function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <div>
      <div>
        <button
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          Increment
        </button>
        <span>{count}</span>
        <button
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </button>
      </div>
    </div>
  );
}
```
