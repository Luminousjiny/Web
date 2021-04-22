# esLint경고해결 및 포트번호 변경   

> 오류사항     
```javascript
Module Warning (from ./node_modules/eslint-loader/index.js):
```    

> 해결         
   
=> 루트 경로는 프로젝트 최상위 위치인 `package.json`과 같은 경로에 `vue.config.js` 파일 생성 후 code 추가     
![image](https://user-images.githubusercontent.com/72757829/115680387-79dad480-a38e-11eb-94dd-eb40b3e69c3c.png)

- vue.config.js    
```javascript

module.exports = {
    lintOnSave: false, // esLint경고해결
    devServer: {
        // 사용자 정의 환경 변수에서 VUE_APP_PORT가 있으면 사용하고
        // 없으면 8000 포트로 개발서버를 실행합니다.
        port: process.env.VUE_APP_PORT || 8000
    }
}

```     

---     
[포트번호 변경_ 참고자료] https://velog.io/@skyepodium/vue-%EC%8B%A4%ED%96%89-%EB%AA%A8%EB%93%9C%EC%99%80-%ED%99%98%EA%B2%BD-%EB%B3%80%EC%88%98-%EC%84%A4%EC%A0%95     
