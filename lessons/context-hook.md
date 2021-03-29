# Context Hook

โดยปกติแล้ว React จะมีปัญหาเรื่องของ **“Prop drilling”** คือ การที่เรามี Parent แล้วมี Child ที่ต้องการข้อมูลจาก Parent ห่างลงไปอีกหลาย ๆ ชั้นทำให้เราต้อง Pass props ลงไปผ่านทุก ๆ ชั้น

![Props Drilling Problem](./images/props-drilling-1.png)

**React Context เกิดมาแก้ไขปัญหานี้** ทำให้เราเหมือนสร้างวาร์ปให้กับข้อมูลส่งไปให้ Child ที่อยู่ชั้นลึก ๆ ได้เลย​โดยไม่ต้องส่งผ่านมาเรื่อย ๆ

![Context API](./images/props-drilling-2.png)

เราจะสร้าง Context ขึ้นมาเพื่อเก็บ values ของ counter แล้วโยน ข้ามเข้าไปใน HomePage component

ให้เราสร้าง file `src/contexts/counter.js` ขึ้นมา

```js
import React, { useReducer } from "react";

const CounterContext = React.createContext();

const INITIAL_STATE = {
  counter: 0,
};

function counterReducer(state, action) {
  switch (action.type) {
    case "add_counter":
      return { counter: state.counter + 1 };
    case "subtract_counter":
      return { counter: state.counter - 1 };
    case "reset_counter":
      return { counter: 0 };
    default:
      return state;
  }
}

function CounterProvider(props) {
  const [state, dispatch] = useReducer(counterReducer, INITIAL_STATE);

  const counterContextValue = {
    state,
    dispatch,
  };

  return (
    <CounterContext.Provider value={counterContextValue}>
      {props.children}
    </CounterContext.Provider>
  );
}

function useCounter() {
  const context = useContext(CounterContext);
  if (context === undefined) {
    throw new Error("useCounter must use under CounterProvider");
  }
  return context;
}

export { CounterProvider, useCounter };
```

จากนั้นให้เรา import CounterProvider มาครอบ Component ที่เราอยากจะใช้ values ของ counter ที่อยู่ใน context

```js
import { CounterProvider } from "./contexts/Counter";
import "./App.css";

function App() {
  return (
    <div>
      <CounterProvider>
        <BrowserRouter>
          <Switch>
            <Route path="/counter" component={CounterPage} />
            <Route path="/post/:postId" component={SinglePostPage} />
            <Route path="/addpost" component={AddPostPage} />
            <Route path="/" component={HomePage} />
          </Switch>
        </BrowserRouter>
      </CounterProvider>
    </div>
  );
}
```

ต่อไปเราจะไปเรียกใช้ values จาก context ใน component ที่ไหนก็ได้ที่อยู่ภายใต้ CounterProvider

```js
import { useCounter } from "../contexts/Counter";

function CounterPage() {
  const [toggle, setToggle] = useState(true);
  const { state, dispatch } = useCounter();

  // skipped code
}
```

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
