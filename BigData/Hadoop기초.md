
# 📑 하둡이란

**빅데이터 처리를 위한 자바기반 오픈소스 프레임워크**

## 🖍 하둡요소

- **분산저장(HDFS)** : 데이터를 어떻게 나누어 저장, 관리할 것인가
- **분산처리(MapReduce)** : 응용에 맞데 데이터를 어떻게 나누어 처리할 것인가

---

## 🖍 RDBMS  VS  NoSQL

```
☑ RDBMS -> 수직적 확장
- 행과 열로 이루어진 테이블 형태의 데이터 구조와 그 데이터 구조와 그 데이터들 간에 연결을 정의한 모델
- 스키마 : 데이터베이스의 구조와 제약조건에 관해 전반적 명세
	✔ 단점 : 개발속도 저하, 능동적인 데이터 저장의 어려움, 반/비정형 데이터 저장의 어려움
- 관계 : 데이터를 여러 테이블, 개체로 구분하고 저장, 이들의 관계를 정의
 
☑ NoSQL -> 수평적 확장
- 비정형 데이터를 보다쉽게 저장하는 분산처리 시스템 필요
- 대표적으로 JSON형태의 파일을 다루는 MongoDB
- 확장성, 유연성, 고성능
```

☑ **SQL 사용**

- 관계를 맺고 있는 데이터가 자주 변경되는 애플리케이션 → NoSQL에서는 데이터들 중복이 있으므로 여러문서 모두 수정
- ACID(원자성, 일관성, 고립성, 지속성)가 중요한 데이터를 다룰 때 ex) 금융

☑ **NoSQL 사용**

- 정확한 데이터 구조를 알수 없거나 유연하게 데이터를 저장할 경우
- Read는 자주! Update는 X ... 갱신에 불리

---

## 🖍 RDBMS VS 하둡
![image](https://user-images.githubusercontent.com/72757829/107115496-6d2b0200-68b0-11eb-98cd-aaf8dd4e0161.png)
- RDBMS와 하둡의 경계는 모호해지고 있다.
- 하둡 시스템이 RDBMS를 모방하여 한계를 극복 → HiveQL

☑ **RDBMS** 

- 적은 양의 데이터를 낮은 지연시간에 추출하고 변경
- 특정 쿼리 및 데이터 변경에 적합
- 지속적 변경이 필요한 데이터셋
- 데이터 무결성
- ex> 금융, 온라인 결제

☑ **하둡(맵리듀스)**

- 비정형 데이터 분석과 같이 일괄처리(batch)방식
- 한번 쓰고 여러번 읽는 응용
- 고속의 순차적 읽기, 쓰기
- ex> 웹서버의 로그
