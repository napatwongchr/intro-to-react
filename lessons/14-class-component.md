# Class Component

Class Component เป็นรูปแบบการเขียน Component อีกแบบที่ใช้ Class Syntax ของ JS ปัจจุบันส่วนใหญ่คนหันมาเขียน Component อยู่ในรูปแบบ Function กันค่อนข้างเยอะ แต่ก็ยังมี code base บางที่ก็ยังมี Class Component อยู่ เราลองมาเขียน Class Component กัน

```js
class PostList extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      posts: []
    }
  }

  componentDidMount() {

  }

  render() {
    return ()
  }
}

```

- เราจะเริ่มเขียน class ตามด้วยชื่อ component จากนั้นเราจะ extends `React.Component`
- เราจะเขียน constructor function เพื่อสร้าง object ขึ้นมาตามที่เราเรียนมาจากเรื่อง this และ prototype
- ภายใน constructor เราจะ assign state object เข้าไปใน `this.state`
- สิ่งที่สำคัญในการเขียน class component คือ render method จะเป็นตัวที่ render element ของเราออกไปแสดงผลบนหน้าเว็บ
- ภายใน class component เราจะมี lifecycle methods ที่ชื่อ `componentDidMount` ซึ่งจะถูก call หลังจาก element ถูก mount เข้าไปใน DOM เรียบร้อยแล้ว และ call ได้ครั้งเดียวเท่านั้น

<br><hr><br>

## Function Component vs Class Component
