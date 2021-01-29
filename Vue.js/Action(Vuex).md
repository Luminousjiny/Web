# 🎐 Action    
> - Mutations : 순차적인 로직들만 선언     
> - Actions : 비 순차적 또는 비동기 처리 로직들을 선언   

### ❔ 왜 처리 로직의 성격에 따라 나눠서 등록해야하는가 ❔     
> 👉 Mutations 의 역할 자체가 State 관리임     
> 👉 상태관리 자체가 한 데이터에 대해 여러 개의 컴포넌트가 관여하는 것을 효율적으로 관리하기 위함    
> 👉 Mutations 에 비동기 처리 로직들이 포함되면 같은 값에 대해 여러 개의 컴포넌트에서 변경을 요청했을 때, 그 변경 순서 파악이 어려움     
> 👉 이러한 문제를 방지하기 위해 비동기 처리 로직은 Actions 에, 동기 처리 로직은 Mutations 에 나눠 구현함     
> 👩‍🦰 따라서 setTimeout() 이나 서버와의 http 통신 처리 같이 __결과를 받아올 타이밍이 예측되지 않은 로직은 Actions 에 선언__     

---   
## 🔹 ACtion 등록     
> actions 를 선언하고 action method 를 추가    
```javascript 
// store.js
export const store = new Vuex.Store({
  // ...
  mutations: {
    addCounter: function (state, payload) {
      return state.counter++;
    }
  },
  actions: {
    addCounter: function (context) {
      // commit 의 대상인 addCounter 는 mutations 의 메서드를 의미한다.
      return context.commit('addCounter');
    }
  }
});
```    
```text
상태가 변화하는 것을 추적하기 위해서는 actions는 mutations의 메서드 호출(commit)하는 구조 
```   

> HTTP get 요청이나 setTimeout 과 같은 비동기 처리 로직들은 actions 에 선언    
```javascript
// store.js
export const store = new Vuex.Store({
  actions: {
    getServerData: function (context) {
      return axios.get("sample.json").then(function() {
        // ...
      });
    },
    delayFewMinutes: function (context) {
      return setTimeout(function () {
        commit('addCounter');
      }, 1000);
    }
  }
});
```   

---   
## 🔹 Actions 사용    
> - mutations 를 이용하여 counter 를 하나씩 늘렸음     
> - 이것을 actions 를 이용하면 -> actions 를 호출할 때는 아래와 같이 dispatch() 를 이용    
```javascript
// App.vue
methods: {
  // Mutations 를 이용할 때
  addCounter() {
    this.$store.commit('addCounter');
  }
  // Actions 를 이용할 때
  addCounter() {
    this.$store.dispatch('addCounter');
  }
},

```   

### ✔ dispatch 동작    
![image](https://user-images.githubusercontent.com/72757829/106277848-15234880-627d-11eb-983a-6afad2c717f8.png)

---    
## 🔹 Actions 에 인자 값 넘기기    
> Mutations 와 유사     
```html
<!-- by 와 duration 등의 여러 인자 값을 넘길 경우, 객체안에 key - value 형태로 여러 값을 넘길 수 있다 -->
<button @click="asyncIncrement({ by: 50, duration: 500 })">Increment</button>
```   
```javascript
export const store = new Vuex.Store({
  actions: {
    // payload 는 일반적으로 사용하는 인자 명
    asyncIncrement: function (context, payload) {
      return setTimeout(function () {
        context.commit('increment', payload.by);
      }, payload.duration);
    }
  }
})
```   

---   

# 🎐 mapAction   
> mapGetters, mapMutations 헬퍼 함수들과 마찬가지로 mapActions 도 동일한 방식으로 사용가능   
```javascript
import {mapActions} from 'vuex';

export default {
  methods: {
    ...mapActions([
      'asyncIncrement',
      'asyncDecrement'
    ])
  },
}

```   



