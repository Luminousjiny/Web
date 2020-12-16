# 😈 Mybatis
1. 객체 지향 언어인 자바의 관계형 데이터베이스 프로그래밍을 보다 쉽게 도와주는 프레임워크
2. 자바에서는 관계형 데이터베이스 프로그래밍을 하기위해 JDBC를 제공
  ```
  - JDBC(Java Data Connectivity): 자바 프로그래밍이 데이터베이스와 연결되어 데이터를 주고 받을 수 있게 해주는 프로그래밍 인터페이스
   (DriverClass, Connection, PerparedStatement, ResultSet etc..)
  - JDBC는 다양한 관계형 데이터베이스 프로그래밍을 위해 API 제공.
  ```
> 즉, MyBatis는 JDBC를 보다 편하게 사용하기 위해 개발됨
---
## 📌 특징
1. SQL문이 코드로부터 완전히 분리
  - Mapper파일에 SQL코드를 입력해 놓고 DAO파일에서 필요할 때마다 가져와서 사용
  - XML, 애노테이션 방식으로 SQL 문을 별도로 처리하는 작업이 가능
2. 생산성 -> 코드가 짧아짐
3. Spring과의 연동으로 자동화된 처리
4. 유지보수성 향상
---
## 📌 구성
1. MyBatis 환경설정 파일(SqlSessionConfig.xml): MyBatis가 JDBC코드를 실행하는데 필요한 전반에 걸친 세팅
  - TypAlias 설정: 사용할 모델 클래스에 대한 별칭 설정.\<typeAlias>
  - DB연동을 위한 설정: DataBase에 어떻게 접속할 것인지에 대한 설정. \<environment>
  - Mapper설정 파일 등록: 매핑 설정이 어디있는지. \<mapper>
2. Mapper 설정 파일(member.xml, company.xml): sql문과 관련된 설정을 하는 파일, MyBatis설정파일(SqlSessionConfig.xml)에 등록
  ```
  [ 주요 구성 요소 ]
  - SQL문 등록 태그
      - SQL문 태그의 구성요소: Parameter, Result, SQL문 등록
      - SQL태그: insert, delete, update, select
      - 공통 SQL문 설정 태그: \<sql>
  - select 결과 처리 설정
      - \<resultMap>
  ```
---
▶ 참고 : https://velog.io/@wimes/2.-%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95-Spring-MyBatis-MySQL%EC%9D%98-%EC%84%A4%EC%A0%95-2zk4cf5gof
