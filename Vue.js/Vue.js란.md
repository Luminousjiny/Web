# 🔰 Vue.js란 무엇인가?   
> 사용자 인터페이스를 만들기 위한 프로그레시브 프레임 워크
### ✅ 특징
``` 
1. 접근성   
2. 유연성   
3. 고성능   
```   

### ✅ Model + View + View Model   
![image](https://user-images.githubusercontent.com/72757829/107958362-3c03ad80-6fe5-11eb-9fed-20655c7fd1ca.png)


```
<!DOCTYPE html>
<html>
  <head>
    <title>Vue.js Sample</title>
  </head>
  <body>
    <div id="app">
      {{ message }}
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        data: {
          message: "Hello Vue.js!"
        }
      });
    </script>
  </body>
</html>
```
