> 1강 학습

[[토크ON세미나] JPA 프로그래밍 기본기 다지기 1강 - JPA 소개 | T아카데미](https://youtu.be/WfrSN9Z7MiA)

# 📑 JPA 실습 준비

### ✔ STS IDE 설치

- File -> New -> Spring Starter Project
- Type: Maven 선택 후 Next
- H2, JPA 선택 후 Finish

### ✔ H2 데이터 베이스 설치

- h2폴더/bin/h2.sh (윈도우 h2.bat) 실행
- http://localhost:8082 접속
- 드라이버 클래스: org.h2.Driver
- JDBC URL: jdbc:h2:tcp://localhost/~/text
- 사용자명: sa, 비밀번호 생략 후 연결

# 📑 SQL 중심적 개발의 문제

- CRUD *반복적임, 지루한 코드*
- 필드 추가하면 찾아서 업데이트 해야함
- 엔티티 신뢰 문제
- 진정한 의미의 계층분할이 어려움
- SQL은 의존적 개발을 피하기 어려움

# 📑 객체 VS 관계형 데이터베이스

- **객체** : OOP.. 어떻게 추상화 해서 객체를 관리할까에 초점
- **관계형 데이터베이스** : 데이터를 어떻게 정규화할까에 초점

객체와 관계형 데이터베이스를 억지로 매핑해서 일을 처리해야함

### ✔ **차이점**

1. 상속
    - 객체는 상속관계 O
    - 관계형 DB는 상속관계 X
2. **연관관계 →** 둘의 차이가 중요!! 
    - 객체는 **참조**를 사용 → 방향성 O
    - 테이블은 **외래키**를 사용  → 방향성 X
3. 데이터타입
4. 데이터 식별방법
 

# 📑 JPA(Java Persistaence API) → 영구 저장

> 객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수 없을까? **JPA 등장       
> ⇒ 객체와 RDB 두 기둥위에 있는 기술**        

- 자바 진영의 **ORM** 기술 표준

    **ORM**(Object-relational mapping : 객체 관계매핑)
    - 객체는 객체대로 설계
    - 관계형 DB는 DB대로 설계
    - ORM 프레임워크가 중간에서 매핑
    - 대중적 언어에는 대부분 ORM 기술 존재

- 발전

    EJB(엔티티 빈-자바표준)  —→ 하이버네이트(오픈소스) ——> JPA(자바표준)

- **애플리케이션과 JDBC 사이에서 동작**

**[ 동작과정 ]**     
```
    개발자가 JPA를 사용하면, JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신한다.
    즉, 개발자가 직접 JDBC API를 쓰는 것이 아니다.
```        


**[ 저장과정 ]**      
```
    Ex) MemberDAO에서 객체를 저장하고 싶을 때
    개발자는 JPA에 Member 객체를 넘긴다.
    JPA는
    1) Member 엔티티를 분석한다.
    2) INSERT SQL을 생성한다.
    3) JDBC API를 사용하여 SQL을 DB에 날린다.
 ```     
 
**[ 조회과정 ]**     
```
    Ex) Member 객체를 조회하고 싶을 때
    개발자는 member의 pk 값을 JPA에 넘긴다.
    JPA는
    1) 엔티티의 매핑 정보를 바탕으로 적절한 SELECT SQL을 생성한다.
    2) JDBC API를 사용하여 SQL을 DB에 날린다.
    3) DB로부터 결과를 받아온다.
    4) 결과(ResultSet)를 객체에 모두 매핑한다.
    쿼리를 JPA가 만들어 주기 때문에 Object와 RDB 간의 패러다임 불일치를 해결할 수 있다.
```
---

# 📑 JPA 사용 이유

### 1. SQL중심적인 개발에서 **객체 중심으로 개발**

### 2. **생산성 - JPA와 CRUD**

- 저장: `jpa.persist(member)`
- 조회: `Member member = jpa.find(memberId)`
- 수정: `member.setName("변경할 이름")`
- 삭제: `jpa.remove(member)`

### 3. **유지보수**

- 기존에는 필드 변경 시 모든 SQL수정해야함
- JPA는 필드만 추가하면 됨 → SQL은 JPA가 알아서 처리
- 신뢰할 수 있는 엔티티, 계층

### 4. 패러다임의 불일치를 해결

---     
# 📑 **JPA의 성능 최적화 기능**

1. **1차 캐시와 동일성(identity) 보장**

    → 같은 트랜잭션 안에서는 같은 엔티티 반환

    → 약간의 조회 성능 향상

2. **트랜직션을 지원하는 쓰기 지연 - insert**
    - 트랜잭션을 커밋할때까지 `INSERT SQL`을 모음
    - `JDBC BATCH SQL`기능을 사용해서 한번에 `SQL` 전송

    ```java
    transaction.begin(); //트랜잭션 시작
    em.persist(memberA);
    em.persist(memberB);
    em.persist(memberC);
    //여기까지 INSERT SQL를 데이터베이스에 보내지 않는다.

    //커밋하는 순간 데이터베이스에 INSERT SQL를 모아서 보낸다.
    transaction.commit(); //트랜잭션 커밋
    ```

3. **지연 로딩**과 즉시 로딩
    - 지연로딩 : 객체가 실제 사용될 때 로딩
        - 이때 필드에 있는 객체는 가짜(프록시) 객체임
    - 즉시 로딩: `JOIN SQL`로 한번된 연관된 객체까지 미리 조회
4. **동일한 트랜잭션에서 조회한 에티티는 같음을 보장**     
---     
> 참고자료

[[JPA] JPA란 - Heee's Development Blog](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html)
