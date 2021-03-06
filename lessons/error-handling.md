# Error Handling

สิ่งที่เรายังไม่ได้คิดต่อคือเรื่องของการ Handle ถ้าตัว App ของเราไม่สามารถที่จะ fetch ข้อมูลจาก Server ไม่สำเร็จ

<br><hr><br>

## Displaying Error

การ Handle Case Error จากการ Fetch ข้อมูล เราจะมี state ที่เรียกว่า `isError` และเราจะ set isError ให้เป็น null ตั้งแต่แรกเนื่องจากว่าเรายังไม่รู้ผลลัพธ์ของการ fetch

```js
function App() {
  const [posts, setPosts] = useState([]);
  const [isError, setIsError] = useState(null);

  // Rest of codes
}
```

จากนั้นเราจะทำการแก้ไข `getPosts` function จำได้มั้ยว่าเรา console.log ติดไว้อยู่ถ้า code ในบล็อกของ try มี error ออกมา มันจะเข้า catch บล็อกทันที จากนั้นมันจะ **setIsError** เข้าไปเป็น **true**

```js
async function getPosts() {
  try {
    let response = await fetch("http://localhost:8000/posts");
    let { data } = await response.json();
    setPosts(data);
  } catch (error) {
    setIsError(true);
  }
}
```

เมื่อเกิด error เราอยากให้มันมีข้อความแจ้งเตือนสักหน่อยที่หน้าเว็บ เราจะมาเขียน logic การแสดงผลเพิ่มกัน

```js
return (
  <div className="postapp-header">
    <h1>Post App</h1>
    <button className="postapp-header-add-button">Add Post</button>

    {isError && <h2>Fetching data error. Please try again.</h2>}

    {!isError &&
      posts.map((post) => {
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
```

<br><hr><br>

## Error Boundaries

มันจะมี Error บางชนิดที่จะทำให้หน้าเว็บของเราไม่สามารถใช้งานต่อได้เลย React มีวิธีการรับมือกับเหตุการณ์แบบนี้ เราเรียกตัวนี้ว่า [Error Boundaries](https://github.com/bvaughn/react-error-boundary) ให้เราทำการ `npm install react-error-boundary`

ตัวอย่างการใช้งาน

```js
import { ErrorBoundary } from 'react-error-boundary'

function App() {
  return (
    <ErrorBoundary FallbackComponent={ErrorFallback}>
      <ComponentThatMayError />
    </ErrorBoundary>;
  )
}

function ErrorFallback() {
  return <h3>There are some serious error happened !</h3>;
}
```

<br><hr><br>

[Table of Contents](https://github.com/napatwongchr/intro-to-react/blob/main/README.md)
