# 📑 function으로 작성

### ✅ 표현법

```jsx
import React from 'react';

const HabitAddForm = (props) => (
            
    );

export default HabitAddForm;
```

```jsx
import React from 'react';

function HabitAddForm (props) {
    
}

export default HabitAddForm;
```
### ✅ class로 구현한 것과 function으로 구현한 것 비교      
- class 이용하여 구현

```jsx
import React, { PureComponent } from 'react';

class HabitAddForm extends PureComponent {
    formRef = React.createRef(); 
    inputRef = React.createRef(); // 멤버변수 정의 

    onSubmit = event => {
        event.preventDefault(); //새로고침 방지
        // console.log(this.inputRef.current.value); // 입력이 콘솔에 찍임
        const name = this.inputRef.current.value;
        name && this.props.onAdd(name); // 이름 전달 

        // this.inputRef.current.value = ''; // input 칸 초기화 (방법 1)
        this.formRef.current.reset(); // (방법 2)
    };

    render() {
        return (
            <form ref={this.formRef} className = "add-form" onSubmit = {this.onSubmit}>
                <input ref={this.inputRef} type="text" className="add-input" placeholder="Habit"></input> 
                <button className = "add-button">Add</button>
            </form>
        );
    }
}

export default HabitAddForm;
```

- function 이용하여 표현
> this. 이 필요 없음

```jsx
import React from 'react';

const HabitAddForm = (props) => {
    const formRef = React.createRef(); 
    const inputRef = React.createRef(); // 멤버변수 정의 

    const onSubmit = event => {
        event.preventDefault(); //새로고침 방지
        const name = inputRef.current.value;
        name && props.onAdd(name); // 이름 전달 
        formRef.current.reset(); 
    };
    return (
        <form ref={formRef} className = "add-form" onSubmit = {onSubmit}>
            <input ref={inputRef} type="text" className="add-input" placeholder="Habit"></input> 
            <button className = "add-button">Add</button>
        </form>
    );
};

export default HabitAddForm;
```

#### class → PureComponent
#### function → memo
---    
# 📑 memo
> class 에서 state나 props에 변화가 없다면 render함수가 불려지지 않는 것과 같은 역할

```jsx
import React, { memo } from 'react';

const HabitAddForm = memo((props) => {
    const formRef = React.createRef(); 
    const inputRef = React.createRef(); // 멤버변수 정의 

    const onSubmit = event => {
        event.preventDefault(); //새로고침 방지
        const name = inputRef.current.value;
        name && props.onAdd(name); // 이름 전달 
        formRef.current.reset(); 
    };
    return (
        <form ref={formRef} className = "add-form" onSubmit = {onSubmit}>
            <input ref={inputRef} type="text" className="add-input" placeholder="Habit"></input> 
            <button className = "add-button">Add</button>
        </form>
    );
});

export default HabitAddForm;
```
