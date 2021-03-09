# 📑 Class로 컴포넌트 생성
- react에서 제공하는 Component 라는 class를 extends 하여 사용
- 내 컴포넌트에 state가 있고, 주기적인 업데이트가 필요할 때 사용
- lifecycle-methods가 있음   

```jsx
import React, { Component } from 'react';

class test extends Component {
    state = {
        count: 0,
    };
    render() {
        return (
            <div>
                {this.state.count}
            </div>
        );
    }
}

export default test;
```

> **state에서 데이터의 변경이 일어나면 자동으로 render 함수 반복 호출**     
→ Virtual DOM Treee에서 실질적으로 필요한 부분만 업데이트하여 성능에 크게 영향 X         

![image](https://user-images.githubusercontent.com/72757829/110482697-46205400-812c-11eb-8f72-631e68e5fe06.png)

