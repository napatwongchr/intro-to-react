# How We Write JS on Web

จากที่เราเรียนมาเราเขียน JS ด้วย RunJS App เวลาเราทำงานจริง ๆ เราสามารถเขียน JS ได้สองแบบ

**1. เขียนใต้ `<script>`**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Learn JS</title>
  </head>
  <body>
    <script>
      // Write JS Code Here !
    </script>
  </body>
</html>
```

**2. เขียนแยกไฟล์แล้ว Link เข้ามาใน HTML**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Learn JS</title>
  </head>
  <body>
    <!-- เราสามารถ Link JS ไฟล์เข้ามาผ่าน script tag attribute src -->
    <script src="app.js"></script>
  </body>
</html>
```

<br><hr><br>

## Exercises 🏅

A) ให้ลองเขียน JS ที่แสดงผลลัพธ์บน Browser ทั้งสองแบบ

โค้ด JS

```js
console.log("Hello World !");
```

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
