> 2강 학습

[[토크ON세미나] JPA 프로그래밍 기본기 다지기 2강 - JPA 기초와 매핑 | T아카데미](https://youtu.be/egVZusxSeKw)

# JPA 기초와 매핑

## 📑 환경설정

### ✔ H2 데이터베이스

- 최고의 실습용 DB
- 가볍다
- 웹용 쿼리툴 제공
- MySQL, Oracle DB 시뮬레이션 가능
- 시퀀스, auto increment 기능 기원

### ✔ **메이븐 설정**

- 자바 라이브러리, 빌드 관리
- 라이브러리 자동 다운로드 및 의존성 관리

### ✔ persistence.xml 파일

JPA 설정 파일

- `/META-INF/persistence.xml` 위치
- `javax.persistence`로 시작: JPA 표준 속성
- `hibernate`로 시작: 하이버네이트 전용 속성

## 📑 객체 매핑하기

- **@Entity**(엔티티): JPA가 관리할 객체
- **@Id**: DB PK와 매핑할 필드

```java
@Entity
public class Member{

		@Id
		private Long id;
		private String name;
		...
}
```

```java
create table Member(
    id bigint not null,
    name varchar(255),
    primary key (id)
)
```

## 📑 데이터베이스 방언
![image](https://user-images.githubusercontent.com/72757829/116091974-5abaaa80-a6e0-11eb-813c-11834bf80abc.png)

- JPA는 특정 데이터베이스에 종속적이지 않은 기술
- 각각의 데이터베이스가 제공하는 SQL문법과 함수는 조금씩 다르다
    - 가변 문자: MySQL은 VARCHAR, Oracle은 VARCHAR2
    - 문자열을 자르는 함수: SQL표준은 SUBSTRING(), Oracle은 SUBSTR()
- 방언: SQL 표준을 지키지 않거나 특정 데이터베이스만의 고유한 기능
- `hibernate.dialect` 속성에 지정
    - H2: `org.hibernate.dialect.H2Dialect`
    - Oracle 10g: `org.hibernate.dialect.Oracle10gDialect`
    - MySQL: `org.hibernate.dialect.MySQL5InnoDBDialect`
- 하이버네이트는 45가지 방언 지원

# 애플리케이션 개발
![image](https://user-images.githubusercontent.com/72757829/116092109-7cb42d00-a6e0-11eb-8705-75e98fc28575.png)

## 💻 실습

1. [H2.sh](http://h2.sh) 접속 

    → IP 다르면 그냥 localhost:8082로 바꾸기

2. H2에서 DB테이블 생성 
3. STS에서 Maven Project 생성
    - Create a simple project 체크
    - Group Id, Artifact Id 아무거나 쓰면 됨
4. **pom.xml**에 dependencies 추가 

    ```java
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>hello.jpa</groupId>
      <artifactId>hello.jpa</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      
      <dependencies>
      	<dependency>
      		<groupId>org.hibernate</groupId>
      		<artifactId>hibernate-entitymanager</artifactId>
      		<version>5.3.7.Final</version> 
      	</dependency>
      	<dependency>
      		<groupId>com.h2database</groupId>
      		<artifactId>h2</artifactId>
      		<version>1.4.197</version>
      	</dependency>
      </dependencies>
    </project>
    ```

5. src/main/java → **Main.java**생성

    ```java
    package hellojpa;

    import javax.persistence.EntityManager;
    import javax.persistence.EntityManagerFactory;
    import javax.persistence.EntityTransaction;
    import javax.persistence.Persistence;

    import hellojpa.entity.Member;

    public class Main {
    	public static void main(String[] args) {

    		EntityManagerFactory emf = Persistence.createEntityManagerFactory("hello"); 
    		// persistence.xml에 있는 persistence-unit name과 같게 
    		//-> hello 라는 이름으로 설정정보 로딩

    		EntityManager em = emf.createEntityManager(); // 엔티티매니저 생성
    		EntityTransaction tx = em.getTransaction(); // 트랜잭션을 얻음
    		tx.begin(); // db에 접근해서 커넥션 가져와서 실제 트랜잭션 시작

    		try {
    			Member member = new Member();
    			member.setId(100L);
    			member.setName("안녕하세요");

    			em.persist(member); // 영구 저장
    			tx.commit();

    		} catch (Exception e) {
    			tx.rollback();
    		} finally {
    			em.close(); // 엔티티매니저 종료
    		}

    		emf.close(); // 엔티티매니저 종료
    	}
    }
    ```

6. src/main/java → **Member.java** 생성

    ```java
    package hellojpa.entity;

    import javax.persistence.Entity;
    import javax.persistence.Id;

    @Entity
    public class Member {
    	
    	@Id
    	private Long id;
    	private String name;
    	
    	public Long getId() {
    		return id;
    	}
    	
    	public void setId(Long id) {
    		this.id = id;
    	}
    	public String getName() {
    		return name;
    	}
    	public void setName(String name) {
    		this.name = name;
    	}

    }
    ```

7. src/main/resources → META_INF 폴더 생성 → **persistence.xml** 생성

    ```java
    <?xml version="1.0" encoding="UTF-8"?>
    <persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.2">
    	<persistence-unit name="hello">
    		<properties>
    		
    			<!-- 필수 속성 -->
    			<property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
    			<property name="javax.persistence.jdbc.user" value="sa"/>
    			<property name="javax.persistence.jdbc.password" value=""/>
    			<property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>
    			<property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/>
    			
    			<!-- 옵션 -->
    			<property name="hibernate.show_sql" value="true"/>
    			<property name="hibernate.format_sql" value="true"/>
    			<property name="hibernate.user_sql_comments" value="true"/>
    			
    			<!-- <property name="hibernate.hbm2ddl.auto" value="create"/>-->
    		</properties>
    	</persistence-unit>
    </persistence>
    ```

### 결과
- spring 콘솔     
![image](https://user-images.githubusercontent.com/72757829/116092227-96ee0b00-a6e0-11eb-988a-46c4a9b33dc0.png)     

- h2 화면     
![image](https://user-images.githubusercontent.com/72757829/116092290-a3726380-a6e0-11eb-81bf-ea359690e0bb.png)      



---

## ✔ 주의
- 엔티티 매니저 팩토리는 반드시 하나만 생성해서 애플리케이션 전체에서 공유해야함
- 엔티티 메니저는 쓰레드간에 공유하면 안된다(사용하고 버려야한다.)
- JPA의 모든 데이터 변경은 트랜잭션 안에서 실행해야함
