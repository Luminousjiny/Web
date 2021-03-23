# Ⓜ Fork 한 Repository 업데이트      
> __원본 저장소__ : 다른 사람의 저장소       
> __포크 저장소__ : 내 저장소 (다른 사람의 저장소를 내 저장소로 가져옴)     

## 🎫 순서
### 1. 내 로컬 PC에 포크 저장소 Clone    
```bash
$ git clone 포크한 저장소 주소
```     

### 2. Clone 한 프로젝트 디렉토리로 이동     

### 3. 리모트 저장소 확인     
```bash
$ git remote -v
// 결과
origin 포크한 저장소 주소 (fetch)
origin 포크한 저장소 주소 (push)
```    

### 4. remote 저장소에 원본 저장소 추가   
```bash
$ git remote add upstream 원본 저장소 주소
```  

```bash   
$ git remote -v
// 결과
origin	포크한 저장소 주소 (fetch)
origin	포크한 저장소 주소 (push)
upstream	원본 저장소 주소 (fetch)
upstream	원본 저장소 주소 (push)
```     

### 5. 원본 저장소 fetch     
```bash
$ git fetch upstream
```

### 6. 원본 저장소 merge   
```bash
$ git merge upstream/main
``` 

### 7. 포크 저장소로 push   
```bash
git push
```   

---      
#### ✔ 참고자료   
- https://hyunjun19.github.io/2018/03/09/github-fork-syncing/     
- https://velog.io/@k904808/Fork-%ED%95%9C-Repository-%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8-%ED%95%98%EA%B8%B0     
