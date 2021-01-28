# 🎆 Vuex   
> Vue.js의 __상태관리__ 를 위한 패턴이자 라이브러리     
> 뷰의 반응성 체계를 효율적으로 활용하여 화면을 업데이트 함    

## 🤷‍♀️ 상태 관리란?
> 컴포넌트간 통신이나 데이터 전달을 좀더 유기적으로 관리할 필요성이 생김... ➰상태관리 필요    
> 여러 컴포넌트간의 데이터 전달과 이벤트 통신을 한 곳에서 관리하는 패턴을 의미한다.    
> 앱의 규모가 커지면서 생기는 문제를 해결하기 위해 모든 데이터 통신을 한곳에 __중앙집중식__ 으로 관리하는 것     
```text
[ 규모가 커지면서 생기는 문제점 ]   
1. 뷰의 컴포넌트 통신 방식인 props, event emit 때문에 중간에 거쳐할 컴포넌트가 많아지거나    
2. 이를 피하기 위해 Event Bus를 사용하여 컴포넌트 간 데이터 흐름을 파악하기 어려운 것     
```     

### ☑ Vuex 전체 흐름도       
![image](https://user-images.githubusercontent.com/72757829/106002491-8c79a080-60f4-11eb-8007-e7973b1e7310.png)     

----       

## 🤷‍♀️ 상태관리 구성요소   
1. __state__ : 컴포넌트 간에 공유할 data     
2. __view__ : 데이터가 표현될 template     
3. __actions__ : 사용자의 입력에 따라 반응할 methods     

```javascript
new Vue({
  // state
  data() {
    return {
      counter: 0
    };
  },
  // view
  template: `
    <div>{{ counter }}</div>
  `,
  // actions
  methods: {
    increment() {
      this.counter++;
    }
  }
});

```     
### ☑ 동작 흐름     
![image](https://user-images.githubusercontent.com/72757829/106003233-58eb4600-60f5-11eb-9ae9-032765b3fa8f.png)     
---   
[참고자료] https://joshua1988.github.io/web-development/vuejs/vuex-start/
