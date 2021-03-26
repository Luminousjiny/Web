> React.js 라이브러리 모음

[brillout/awesome-react-components](https://github.com/brillout/awesome-react-components)

> React Router 공식페이지

[React Router: Declarative Routing for React](https://reactrouter.com/web/guides/quick-start)

> 튜토리얼 정리

[[React.JS] 강좌 목록](https://velopert.com/reactjs-tutorials)

---

> **Routing**

어떤 사용자가 요청하는 url링크인 **HTTP 리퀘스트를 요청**했을 때, 어떤 특정 **페이지로 연결**할 것인지 결정하는 것

# React Router

![image](https://user-images.githubusercontent.com/72757829/112650479-c534bc80-8e8e-11eb-87f1-f124466d13af.png)


### 패키지 추가

- yarn add 패키지명

```bash
yarn add react-router-dom 
```

### App.jsx

```jsx
import './App.css';
import { BrowserRouter, Link, Route } from 'react-router-dom';
import Home from './components/home';
import Profile from './components/profile';

function App() {
  return (
    <BrowserRouter>
    <nav>
      <Link to="/">Home</Link>
      <Link to="/profile">Profile</Link>
    </nav>

      <switch>
        <Route path={['/', '/home']} exact> //exact 필수 
          <Home />
        </Route>
        <Route path="/profile">
          <Profile />
        </Route>
      </switch>
    </BrowserRouter>
  );
}

export default App;
```

- `<BrowserRouter>` 태그로 감싸줌
- `switch` → redirect 해줌 (방향을 알려줌)
- switch 밖에서는 `Link`를 사용하면 가능
- `[ '/' , '/home' ]` 과 같이 경로를 두가지로 설정 가능
- `exact` 안붙이면 경로가 포함이 되면 같은 경로라고 생각

    → /home  == /home/profile

    따라서, 붙여줘야함 → 그럼 둘을 다르게 인식! 

### props에 오는 것

![image](https://user-images.githubusercontent.com/72757829/112650615-e695a880-8e8e-11eb-808e-23f692b99981.png)

- **match**는 전달내용에 접근이 가능
- **history** 는 이동을 가능하게 함

    → `useHistory`로 이용

    ```jsx
    // 선언 
    import { useHistory } from 'react-router';

    // 사용 
    const history = useHistory(); 
    history.push('/home');
    ```

### profile.jsx

```jsx
import React from 'react';
import { useHistory } from 'react-router';

const Profile = (props) => {
    const history = useHistory();
    return (
        <>
            <h1>profile</h1>
            <button onClick={ ( ) => {
                history.push('/home');
            }}>Go to Home</button>            
        </>
    );
}

export default Profile;
```

### home.jsx

```jsx
import React from 'react';
import { useHistory } from 'react-router';

const Home = (props) => {
    const history = useHistory();
    return (
        <>
            <h1>Home</h1>
            <button onClick={ ( ) => {
                history.push('/profile');
            }}>Go to profile</button>            
        </>
    );
}

export default Home;
```
