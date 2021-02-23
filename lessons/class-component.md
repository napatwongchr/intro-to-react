# Class Component

Class Component เป็นรูปแบบการเขียน Component อีกแบบที่ใช้ Class Syntax ของ JS ปัจจุบันส่วนใหญ่คนหันมาเขียน Component อยู่ในรูปแบบ Function กันค่อนข้างเยอะ แต่ก็ยังมี code base บางที่ก็ยังมี Class Component อยู่ เราลองมาเขียน Class Component กัน

```js
import React from "react";

class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0,
    };
  }

  handleAddCounter = () => {
    this.setState(function (state) {
      return {
        counter: state.counter + 1,
      };
    });
    console.log("Add counter");
  };

  handleSubtractCounter = () => {
    this.setState(function (state) {
      return {
        counter: state.counter - 1,
      };
    });
    console.log("Subtract counter");
  };

  handleResetCounter = () => {
    this.setState(function () {
      return {
        counter: 0,
      };
    });
    console.log("Reset counter");
  };

  render() {
    return (
      <div>
        <h1>Counter: {this.state.counter}</h1>
        <button onClick={this.handleAddCounter}>Add</button>
        <button onClick={this.handleSubtractCounter}>Subtract</button>
        <button onClick={this.handleResetCounter}>Reset</button>
      </div>
    );
  }
}

export default Counter;
```

- เราจะเริ่มเขียน class ตามด้วยชื่อ component จากนั้นเราจะ extends `React.Component`
- เราจะเขียน constructor function เพื่อสร้าง object ขึ้นมาตามที่เราเรียนมาจากเรื่อง this และ prototype
- ภายใน constructor เราจะ assign state object เข้าไปใน `this.state`
- สิ่งที่สำคัญในการเขียน class component คือ render method จะเป็นตัวที่ render element ของเราออกไปแสดงผลบนหน้าเว็บ

<br><hr><br>

## Function Component vs Class Component

TBD

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
