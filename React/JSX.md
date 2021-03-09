# 📑 JSX
> 자바스크립트 코드 위에 간단하게 html 처럼 할 수 있도록 만들어 진 것     
> → JavaScript 코드 내에서 UI로 작업 할 때 시각적 인 도움으로 유용     

- 변수나 함수를 중괄호로 감싸서 사용

```jsx
const name = 'Josh Perez';
const element = <h1>Hello, {name} </h1>; 

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

- 문자열 → 두 표현식은 동일

```jsx
<MyComponent message="hello world" />
<MyComponent message={'hello world'} />
```

- 값을 전달하지 않으면 true →  두 표현식은 동일

```jsx
<MyTextBox autocomplete />
<MyTextBox autocomplete={true} />
```

- 여러개의 태그를 이용 할 시, **`<React.Fragment>`** 태그 이용
- 단, 의미가 필요하다면 `<div>`, `<li>`, `<ol>` 등 사용 가능

```jsx
render() {
        return (
            **<React.Fragment>**
                <span className="habit-name">Reading</span>
                <span className="habit-count">2</span>
            **</React.Fragment>**
        );
    }
```

#### 스프레드 속성
> 이미 props객체로 가지고 있고 JSX에서 전달하려는 경우 **"spread"연산자(...)**로 사용하여 전체 props 객체를 전달     

```jsx
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = {firstName: 'Ben', lastName: 'Hector'};
  return <Greeting {...props} />;
}
```

- JSX 자식 → **`props.children`**

```jsx
// Calls the children callback numTimes to produce a repeated component
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```
