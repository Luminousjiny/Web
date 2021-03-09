# 📑 Lifecycle      
> 상황에 맞게 구현해 두면 알아서 호출     

![image](https://user-images.githubusercontent.com/72757829/110483058-ae6f3580-812c-11eb-9878-063e2a2d0c82.png)
### ✔️ Mount : 컴포넌트 처음 실행

1. **`context`**, `**defaultProps**`와 **`state`**를 저장
2. **`componentWillMount`** 메소드 호출 

    → props나 state를 바꾸면 안됨(마운트중임)

3. **`render`**
4. **`componentDidMount`**호출

    → 주로 AJAX 요청을 하거나, setTimeout, setInterval같은 것들 함

---

### ✔️ Props Update

1. `componentWillReceiveProps` 호출
2. `shouldComponentUpdate` 호출
3. `componentWillUpdate` 호출
4. `render`
5. `componentDidUpdate` 

    → componentDidUpdate 만 바뀌기 이전의 props에 대한 정보를 가지고 있음

---

### ✔️ State Update

props update와 과정이 같지만, `componentWillReceiveProps` 메소드는 호출되지 않음

1. `shouldComponentUpdate`
2. `componentWillUpdate`
3. `render`
4. `componentDidUpdate`

---

### ✔️ Unmount : 컴포넌트 제거

1. `componentWillUnmount`     


---     
- 가장 많이 쓰는 메소드    
![image](https://user-images.githubusercontent.com/72757829/110483240-df4f6a80-812c-11eb-8bb7-24eb692cbaf1.png)
