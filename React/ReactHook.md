# 📑 ReactHook

> **use로 시작하는 함수들**     
> function으로 구현하여도 class처럼 사용가능하도록 도와줌
- `useState` 를 이용하여 state사용

    → 실제 state 값과 업데이트를 할 수 있는 함수를 리턴함

    → 업데이트된 state 값을 항상 기억하고 있음 

    ⇒ 함수가 계속 호출되어도 괜찮다

```jsx
const [ count, setCount ] = useState(0);
// count : 실제 state 값
// setCount : 업데이트 할 수 있는 함수
// useState(초기값);
```

- `useRef`

    → createRef 처럼 매번 새로운 것을 만드는 것이 아닌 한번만 만들고 메모리에 저장 후 재사용

    ```jsx
    const spanRef = useRef();
    ```

- `useEffect`

    → 컴포넌트가 마운트 되었을 때, 업데이트 될 때 마다 호출

    → componentDidMount와 componentDidUpdate 결합 ( 중복 ↓ )

    - 기존 state나 props가 변경될 때 호출

        ```jsx
        useEffect(() => {
              //code
            });
        ```

    - 해당 데이터가 변경될 때만 호출

        ```jsx
        useEffect(() => {
              //code
            }, [count, age]);
        // count, age가 변경될 때만 호출되도록 해줌
        ```

    - 마운트 되었을 때만 호출 → 처음에만 호출됨 !

        ```jsx
        useEffect(() => {
              //code
            }, []);
        ```
