# 📑 데이터베이스 스키마 자동생성

- DDL을 애플리케이션 실행 시점에 자동생성
- 테이블 중심 → 객체 중심
- 데이터베이스 방언을 활용해서 적절한 DDL 생성 ⇒ **개발 장비에서만 사용**

    (운영서버에서 사용 X 또는 적절히 다듬은 후 사용)

### 🚩 hibernate.hbm2ddl.auto

- `create` : 기존 테이블 삭제 후 다시생성 (drop + create)
- `create-drop` : create와 동일하지만 종료시점에 테이블 drop → 테스트 코드 등에 사용
- `update` : 변경부분만 반영(운영DB에는 사용X)
- `validate` : 엔티티와 테이블이 정상 매핑인지 확인
- `none` : 사용하지 않음

### 🚩 주의

운영 장비에는 절대 `create`, `create-drop`, `update` 사용 금지 

- 개발 초기 단계 : create , update
- 테스트 서버 : update, validate
- 스테이징과 운영서버 : validate, none

# 📑 매핑 어노테이션

```java
@Entity
public class Member {
  @Id
  private Lond id;
  
  @Column(name = "USERNAME", length = 20) // 글자수 제약조건 
  private String name;
  private int age;
  
  @Temporal(TemporalType.TIMESTAMP)
  private Date regDate;
  
  @Enumerated(EnumType.STRING)
  private MemberType memberType;
  
  ...
}
```

### @Column

- 필드명과 DB의 컬럼명이 일치하지 않을 경우

    ex) `@Column(name = “USERNAME”)` 

    :  java에서는 name이라고 했지만 DB에는 username이면 그 둘을 매핑함

- 가장 많이 사용
- insertable, updatable = true/false : 읽기 전용
- nullable = true/false : null/not null 조건, DDL 생성 시 사용
- unique : 유니크 제약 조건, DDL 생성 시 사용
- columnDefinition, length, precision, scale(DDL)

### @Temporal

- 날짜 타입 매핑
- `@Temporal(TemporalType.DATE)`  : 날짜
- `@Temporal(TemporalType.TIMESTAMP)` : 시간
- `@Temporal(TemporalType.TIMESTAMP)` : 날짜와 시간
- 요즘에는 `LocalDate`, `LocalDatetime` 사용

### @Enumerated(EnumType.STRING)

- `@Enumerated(EnumType.ORDINAL)` ⇒ 숫자로 저장해서 추가하면 다 꼬이게 됨 , STRING 으로 하기

### @Lob

- 컨텐츠의 길이가 너무 길 경우 바이너리 파일로 DB에 바로 밀어 넣어야 할 때 사용
- CLOB, BLOB 매핑
- CLOB(Character LOB) : String, char[], java.sql.CLOB
- BLOB(Byte LOB) : byte[], java.sql.BLOB
- @Lob 어노테이션을 String에 붙이면 CLOB, byte에 붙이면 BLOB

```java
@Lob
private String lobString;

@Lob
private byte[] lobByte;
```

### @Transient

- 이 필드는 매핑하지 않는다.
- 애플리케이션에서 DB에 저장하지 않는 필드(객체에서만 들고 있음)
- 웬만하면 쓰지 말기

# 📑 식별자 매핑 어노테이션

### **@Id @GenerateValue(strategy = Generation Type[타입])**

- IDENTITY : 데이터베이스에 위임, MySQL
- SEQUENCE: 데이터베이스 시퀀스 오브젝트 사용, ORACLE
    - `@SequenceGenerator` 필요
- TABLE: 키 생성용 테이블 사용, 모든 DB에서 사용
    - `@TableGenerator` 필요
- AUTO: 방언에 따라 자동 지정, 기본값
    - IDENTITY, SEQUENCE, TABLE 중 Dialect에 맞는 방식으로 자동 적용

### **권장하는 식별자 전략**

- 기본 키 제약조건: Not Null, Unique(유일성), 변하면 안된다(불변)
- 미래까지 이 조건을 만족하는 자연키는 찾기 어렵다.
    - `대체키(대리키)`를 사용하자!
    - ex) 주민등록번호도 기본키로 사용하기에 적절하지 않다.
    - ex) *주민등록번호를 `PK`로 설정하고 다른 테이블과 `FK`참조시 그대로 주민번호가 넘어감. 갑자기 나라에서 개인정보 목적으로 `DB에 주민번호 저장하지 마라`고 하면 끝남…*
- 권장 : **Long + 대체키 + 키 생성전략 사용**
    - 대체키는 전혀 비즈니스랑 관계없는 키 권장`AUTO_INCREMENT`로 PK사용 시 `Int type` 사용X! INT는 최대 10~20억까지이므로 생각보다 빨리 끝나기 때문! → `Long type` 사용하자!
    - 또는 UUID 사용! -> But, 성능 문제는 확인해보고 사용
