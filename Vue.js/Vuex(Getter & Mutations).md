# 👀 Vuex     
> 변경된 state 값을 받아오는 ___Getters___ , state 값을 변경하기 위한 메서드를 정의하는 __Mutations__    

## ◽ Getters     
> Vuex의 데이터에 접근할 때 중복된 코드를 반복호출 하게 되는 문제점    
> Vuex에서 수행하도록 하고 각 컴포넌트에서 수행로직을 호출하는 형태    
> __가독성 증가___ , __성능 향상___     

### ✔ Getters 등록    
> Vuex에 getters 추가    
```javascript
// store.js
export const store = new Vuex.Store({
  // ...
  getters: {
    getCounter: function (state) {
      return state.counter;
    }
  }
});
```     

### ✔ Getters 사용    
> 컴포넌트에서 __this.$store__ 를 이용하여 getters 에 접근     
```javascript
// App.vue
computed: {
  parentCounter() {
    this.$store.getters.getCounter;
  }
},

// Child.vue
computed: {
  childCounter() {
    this.$store.getters.getCounter;
  }
},
```     
> computed 의 장점 : 체이닝( Caching )효과    
> 단순히 state 값을 반환하는 것이 아니라, getters 에 선언된 속성에서 filter(), reverse() 등의 추가적인 계산 로직이 들어갈 때 발휘     

### ✔ mapGetters 사용    
> Vuex 에 내장된 helper 함수, mapGetters 로 더 가독성을 올릴 수 있다.        
> 컴포넌트 자체에서 사용할 computed 속성과 함께 사용할 수 없다는 점    
> _해결방안은 ES6 의 문법 ... 을 사용_ 
```javascript
// App.vue
import { mapGetters } from 'vuex'

computed: {
  ...mapGetters([
    'getCounter'
  ]),
  anotherCounter() {
    // ...
  }
}
```     
---    
## ◽ Mutations    
> Vuex 의 데이터, 즉 state 값을 변경하는 로직들을 의미     
> 정의한 로직들이 __순차적__으로 일어나야 각 컴포넌트 반영 여부를 제대로 추적 가능     
> 쉽게 Setters로 이해!   

```text 
- __Getters와 차이점___   
1. 인자를 받아 Vuex에 넘겨줄 수 있음   
2. computed 가 아닌 __methods__ 에 등록
```   
```text 
- __Actions와 차이점___   
1. Mutations 는 __동기적__ 로직을 정의
2. Actions 는 __비동기적__ 로직을 정의
```   

> __commit__ 을 이용하여 state 변경   
![image](https://user-images.githubusercontent.com/72757829/105854564-6091e880-602a-11eb-85e1-633f7c663060.png)


### ✔ Mutations 등록    
> Vuex에 getters 추가    
> Getters와 마찬가지임   
```javascript
// store.js
export const store = new Vuex.Store({
  // ...
  mutations: {
    addCounter: function (state, payload) {
      return state.counter++;
    }
  }
});
```     

### ✔ Mutations 사용    
> 컴포넌트에서 __this.$store.commit__ 를 이용하여 접근     
> this.$store.mutations.addCounter; -> 이렇게 접근 불가능!

```javascript
// App.vue
methods: {
  addCounter() {
    // this.$store.state.counter++;
    this.$store.commit('addCounter');
  }
},

```     

### ✔ Mutations 에 인자 값 넘기기     
> 각 컴포넌트에서 Vuex 의 state 를 조작하는데 필요한 특정 값들을 넘기고 싶을 때는 commit() 에 두 번째 인자를 추가   
```javascript
this.$store.commit('addCounter', 10);
this.$store.commit('addCounter', {
  value: 10,
  arr: ["a", "b", "c"]
});
```    
- Vuex에서 받는 방법   
```javascript
mutations: {
  // payload 가 { value : 10 } 일 경우
  addCounter: function (state, payload) {
    state.counter = payload.value;
  }
}
```   
> _데이터 인자 명은 보통 payload 를 많이 쓴다._   


### ✔ mapMutations 사용    
> mapGetters 와 마찬가지로, Vuex 에 내장된 mapMutations 를 이용하여 코드 가독성을 높일 수 있다.     
```javascript
// App.vue
import { mapMutations } from 'vuex'

methods: {
  // Vuex 의 Mutations 메서드 명과 App.vue 메서드 명이 동일할 때 [] 사용
  ...mapMutations([
    'addCounter'
  ]),
  // Vuex 의 Mutations 메서드 명과 App.vue 메서드 명을 다르게 매칭할 때 {} 사용
  ...mapMutations({
    addCounter: 'addCounter' // 앞 addCounter 는 해당 컴포넌트의 메서드를, 뒤 addCounter 는 Vuex 의 Mutations 를 의미
  })
}

```     
---    
[참고자료]    
- https://joshua1988.github.io/web-development/vuejs/vuex-getters-mutations/   
- https://kamang-it.tistory.com/entry/Vue14vuex-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0    
