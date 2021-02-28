# URL Parameters

เราลองมาดูหน้า View Post Page กันว่าเราจะทำหน้านี้ยังไง

ขั้นตอนแรกให้เราไปที่ App.js เพื่อไปสร้าง Route ขึ้นมาอีก 1 หน้า เราจะใส่ Route path เป็น `/post` Component เป็น SinglePostPage จากนั้นให้เราไปสร้าง SinglePostPage แล้ว import มาใช้

```js
import SinglePostPage from "./pages/SinglePostPage";

function App() {
  return (
    <div>
      <BrowserRouter>
        <Switch>
          <Route path="/add" component={AddPostPage} />
          <Route path="/home" component={HomePage} />
          <Route path="/post" component={SinglePostPage} />
        </Switch>
      </BrowserRouter>
    </div>
  );
}
```

จากนั้นเวลาเรากดที่ Post title ในแต่ละ Post จะต้อง Link ไปที่หน้า SinglePostPage เราจะเขียน function viewPost ขึ้นมาแล้วใช้ `history.push` เพื่อย้่ายไปยังหน้า page นั้น ๆ

```js
function viewPost(postId) {
  history.push("/post");
}
```

จากนั้นเราจะเรียกใช้ viewPost พร้อมกับส่ง post.id เข้าไปจังหวะที่ event click เกิดขึ้นที่ h3 ซึ่งมี handleViewPost handler

```js
// Skipped codes
{
  !isFetchingError &&
    posts.map((post) => {
      return (
        <div key={post.id} className="postapp-postitem">
          <h3
            className="postitem-title"
            onClick={function handleViewPost() {
              viewPost(post.id);
            }}
          >
            {post.title}
          </h3>
        </div>
      );
    });
}
// Skipped codes
```

ถ้าเราสามารถคลิกแต่ละ post แล้วเข้าไปหน้า SinglePostPage ได้แล้วให้เราลองคิดต่อว่าเวลาเราจะออกแบบ SinglePostPage ยังไง ?​

- สิ่งนี้คือ SinglePostPage
- สิ่งนี้แสดง Post detail
- สิ่งนี้มีข้อมูล Post title และ Post content

การที่จะแสดงข้อมูลได้เราก็ต้องไป fetch ข้อมูลมาจาก server เราถูกต้องมั้ยครับ แต่การที่เราจะดึงข้อมูล post detail นั้น ๆ มาได้เราจะต้องรู้ id ของ post นั้น ๆ ก่อน สิ่งที่เราต้องทำคือเราจะปรับ path ที่แสดงผลหน้า SinglePostPage ด้วยการใส่ parameter **:id** ต่อเข้าไปที่ path

```js
<Route path="/post/:id" component={SinglePostPage} />
```

จากนั้นแก้ไข viewPost ให้ย้ายไปที่ path `/post/:id`

```js
function viewPost(postId) {
  history.push("/post/" + postId);
}
```

เราจะทำการ get parameter id จาก url path ด้วย **useParams** function จาก react-router-dom

```js
import { useParams } from "react-router-dom";

function SinglePostPage() {
  const [post, setPost] = useState({});
  let params = useParams();

  console.log(params);
  // Rest of codes
}
```

เมื่อเราได้ id จาก params แล้ว ให้เรา fetch ข้อมูล post ด้วย id ได้เลย ให้กลับไปดู api doc ว่า endpoint ในการดึงข้อมูล post ด้วย id นั้นใช้ endpoint อะไร จากนั้นเราจะทำการ สร้าง getPostById function แล้ว fetch ข้อมูลตาม code ด้านล่าง

```js
useEffect(() => {
  async function getPostById() {
    let response = await fetch("http://localhost:8000/posts/" + params.postId);
    let post = await response.json();
    console.log(post);
  }

  getPostById();
}, []);
```

เมื่อเราได้ข้อมูล post มาแล้วให้เราทำการสร้าง state variable มาแล้ว set post เข้าไปใน state variable

```js
const [post, setPost] = useState({});

useEffect(() => {
  async function getPostById() {
    let response = await fetch("http://localhost:8000/posts/" + params.postId);
    let post = await response.json();
    setPost(post);
  }

  getPostById();
}, []);
```
