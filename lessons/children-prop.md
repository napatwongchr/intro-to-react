# Children Prop

เนื่องจากเรามีการใช้ Button บ่อยมากในหลาย ๆ ที่เราจะทำการสร้าง Component ขึ้นมาเพื่อความง่ายในการจัดการแก้ไข code ในอนาคต

เราจะทำการสร้างไฟล์ `Button.js` ภายใต้ `src/components/Button.js`

```js
import styled from "@emotion/styled";

const StyledButton = styled.button`
  border-radius: 5px;
  background-color: khaki;
  height: 30px;
  width: 100px;
  color: ${(props) => {
    return props.primary ? "crimson" : "cornflowerblue";
  }};
`;

function Button(props) {
  return (
    <StyledButton primary={props.primary} onClick={props.onClick}>
      {props.children}
    </StyledButton>
  );
}

export default Button;
```

จากโค้ด

- Component Button จะรับ Props ทั้งหมด 2 ตัว คือ primary และ onClick
- ระหว่าง Tag StyledButton เราจะใช้ **children prop** ในการแสดงผลข้อความของตัว Button ซึ่ง children prop นั้นเป็น prop พิเศษที่เรามองไม่เห็น ซึ่งมาจากการใส่ Element เข้าไประหว่าง Component ที่เราเรียกใช้งานใน JSX

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
