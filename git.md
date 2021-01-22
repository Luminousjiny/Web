# Ⓜ GIT 

> https://ssafyprj.github.io/git/?locale=ko  튜토리얼 학습 후 정리할 것    
## GIT branch 목록보기   
#### - 로컬 저장소의 Branch 목록 보기    
```text
git branch
```   

#### - 원격 저장소의 Branch 목록 보기   
```text
git branch -r
```    

#### - 모든 Branch 목록 보기       
```text
git branch -a
```     
---    
## GIT branch 관리하기 
#### - 현재 위치에서 새로운 Branch 생성하기   
```text
git branch 생성할 Branch 이름
```     

#### - 다른 branch로 이동하기
```text
git checkout 이동할 Branch 이름
```   

#### - branch 이름 변경하기    
```text 
git branch -m 기존 Branch 이름 새로운 Branch 이름
```   

#### - branch 삭제하기   
```text   
git branch -d 삭제할 Branch 이름
```     

---    

## 원격 저장소의 branch 관리하기    
#### - 원격저장소 branch 삭제하기   
> push를 사용한다는 점 기억 !!      
```text 
git push --delete 원격저장소 별칭 원격 Branch 이름
```
> 예시 : git push --delete origin test     


#### - 원격 저장소의 특정 Branch를 로컬 저장소의 새로운 Branch로 가져오기     
> 원격 저장소에 Push를 시도했는데 Reject당한 경우,      
> 원격 저장소의 대상 Branch를 로컬 저장소의 임시 Branch로 가져온 뒤,      
> 병합이나 재정렬을 하고 다시 Push를 하는 순서로 작업을 진행     
```text
git checkout -b {새로운 로컬 Branch 이름} {원격 저장소 별칭}/{원격 Branch 이름}
git checkout {새로운 로컬 Branch 이름}
git pull origin {원격 Branch 이름}
```      
> git checkout -b temp origin/master    
> git checkout temp    
> git pull origin master     

---    
[참고] https://www.tuwlab.com/ece/22216     


