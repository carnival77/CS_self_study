# Spring Data JPA

> JPA(Java Persistence API)는 자바 언어를 통해서 데이터베이스와 같은 영속 계층을 처리하고자 하는 스펙

## ORM와 JPA

![image](https://github.com/user-attachments/assets/d202518f-065a-4280-904f-4914b63454e9)

### **관계형 데이터베이스(RDB)**

- 데이터가 **행과 열이 있는 테이블**로 구성되는 집합 이론 모델
  - 관계형 데이터베이스는 강력하고 효율적인 데이터 저장 및 검색 기능을 제공하지만 복잡한 객체 지향 개념을 모델링(상속, 다형성, 레퍼런스, 오브젝트)하는 데 적합하지 않습니다.
  - 객체에 접근할 때마다 DB상에 어떤 테이블과 연결시켜줘야되고 객체의 상태, 상속 정보가 바뀔 때마다 이를 수정해줘야 한다.

### **ORM(Object Relational Mapping)** 

- **객체와 RDB 테이블이 매핑을 이뤄 테이블을 객체지향적으로 사용하는 기술**
  - 즉, 내가 코드 상에서 생성한 객체가 DB상에 어떤 테이블과 연결이 된다는 것을 의미한다. 이렇게 되면 내가 객체를 조작함으로써 DB를 조작할 수 있게 된다.

### **JPA(Java Persistence API)**

![image](https://github.com/user-attachments/assets/1aa60d13-e89f-4484-8ead-41c0343393cd)

- ORM을 자바 언어에 맞게 사용하는 스펙

- **자바 어플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스**

- JPA는 영속성 컨텍스트인 **EntityManager**를 통해 Entity를 관리하고 이러한 Entity가 DB와 매핑되어 사용자가 Entity에 대한 CRUD를 실행을 했을 때 Entity와 관련된 테이블에 대한 적절한 SQL 쿼리문을 생성하고 이를 관리하였다가 필요시 JDBC API를 통해 DB에 날리게 된다

  - 프로세스

    - JPA는 영속성 컨테스트를 사용하여 db와의 통신을 효율적으로 관리한다.

    - 이러한 영속성 컨텍스트에 대한 JPA상에서 구현체를 **EntityManger**라고 한다.

    - 이러한 EntityManger는 Entity에 대한 생명주기를 관리하고 db와의 연결정보를 저장해둔다.

    - Entity에 대한 쿼리는 연결정보를 바탕으로 JPA가 자동으로 생성해준다.

    - 이러한 쿼리문은 EntityManger가 관리를 하다가 필요시 JDBC API를 통해 DB에 날리게 된다.

  - **Persistence Context** : Entity를 저장하는 비휘발성 환경

    - 사용 이유 : **중복되는 쿼리로 인한 오버헤드 줄이고 DB와의 통신 횟수나 방식을 효율적으로 관리**하여 **서버 사용 효율성 증진**
    - **1차 캐시** : Entity를 캐싱해놓기 때문에 쿼리 중복으로 인한 불필요한 DB와의 통신 감소
    - **쓰기 지연** : 반복적이고 동일한 DB write 작업을 Entity에 저장해두었다가 한 번에 처리
    - **Dirty Checking** : 영속성 컨텍스트에서 관리하는 **Entity에 대한 db상의 실제 업데이트**는 영속성 컨텍스트에서 **commit이나 flush**할 때 **Entity에 대한 값**이 **조회할 때를 기준으로 변경되었는지 확인**한 후 **바뀐 부분에 대해서 한꺼번에 db에 대한 업데이트를 지원**하기 때문에 여러 비지니스 로직상에서 db상에 값이 꼬이는 경우를 방지

  - **EnitityManagerFactory** : WAS가 시작되는 시점에 만들어지고 종료되는 시점에 없어지면서 EntityManager를 관리하는 Object

  - **EntityManager** : Entity를 생명주기를 관리하는 context로 Persistence Context 역할을 수행

    

**자문자답**

- **Q) 그럼 언제 EntityManger를 생성할까?**
  - A : Transaction 단위를 수행할 때마다 생성한다. 즉, 고객의 요청이 올 때마다 사용했다가 닫는다. 따라서 Thread당 생성이 되고 이에 따라 Thread당 공유가 되지 않는다.
- **Q: 그러면 JPA는 모두 트랜잭션일 때 사용이 가능한가요 ?**
  - A: 아니다. Spring에서 트랜잭션 없이 JPA를 사용할 수 있지만 일반적으로 데이터 일관성과 무결성을 보장하기위해 트랜잭션을 활성화하는 것이 좋다.
- **Q: 그러면 거의 모든 CRUD 서비스 단에서는 트랜잭션을 활성화 해야겠네?**
  - A: 맞습니다. 대부분 CRUD 작업을 수행할 때 **데이터 일관성, 무결성**을 보장하기 위해 트랜잭션이 필요합니다. 하지만 Read 와 같이 읽기만 하는 경우 **@Transactional**(readOnly = *true*) 사용하여 불필요한 과정을 스킵할 수 있다.

### **Hibernate** 

- Hibernate는 자바 언어를 위한 ORM 프레임워크
- **JPA의 구현체**로, **JPA 인터페이스를 구현**하며, JPA에서 넘겨받은 정보들을 표준화 해서 JDBC에게 넘겨준다.
  - JPA도 JDBC와 마찬가지로 인터페이스이기 때문에 구현체가 필요하고, 그 구현체 중 하나가 **Hibernate**이다.

![image](https://github.com/user-attachments/assets/dc4efebd-40dc-4bf6-b813-069d4a88b29d)

![image](https://github.com/user-attachments/assets/bd12556e-7e96-4a41-9b38-64924c90d5bf)

- 위 사진은 JPA와 Hibernate의 상속 및 구현 관계를 나타낸 것이다.
  - JPA의 핵심인 `EntityManagerFactory`, `EntityManager`, `EntityTransaction`을 Hibernate에서는 각각 `SessionFactory`, `Session`, `Transaction`으로 상속받고 각각 `Impl`로 구현하고 있음을 확인할 수 있다.
- **JPA를 사용하기 위해서 반드시 Hibernate를 사용할 필요는 없다**

### **Spring Data JPA**

![image](https://github.com/user-attachments/assets/ff8211dc-d1c7-450b-b7f6-ab75c2993b3d)

- JPA를 더 쉽게 사용하기 위해 JPA 위에 구축된 상위 프레임워크
- **JPA를 한 단계 추상화시킨** `Repository`**라는 인터페이스를 제공**하며, 이를 통해 **엔티티 객체들을 처리하고 메서드 이름 규칙을 기반으로 JPA 쿼리를 자동으로 생성**
  - 사용자가 `Repository` 인터페이스에 정해진 규칙대로 메소드를 입력하면, Spring이 알아서 해당 메소드 이름에 적합한 쿼리를 날리는 구현체를 만들어서 Bean으로 등록해준다.

### **JDBC(Java Database Connectivity)** 

- **데이터베이스에 연결 및 작업을 하기 위한 자바 표준 인터페이스**
- DBMS의 종류에 상관없이 하나의 JDBC API를 이용해서 하나의 문법으로 통일시켜 데이터베이스 작업을 처리

![image](https://github.com/user-attachments/assets/fc3e78d6-c6ce-4a18-86ac-0e06691812e0)

## 엔티티 클래스와 JpaRepository

### @Entity

- 엔티티 클래스에 추가하는 어노테이션
- 해당 클래스가 엔티티를 위한 클래스이며, 해당 클래스의 인스턴스들이 JPA로 관리되는 엔티티 객체라는 것을 의미
- @Entity 가 붙은 클래스는 옵션에 따라 자동으로 테이블을 생성 가능. 이 경우 해당 클래스의 멤버 변수에 따라 자동으로 칼럼 생성

### @Table

- @Entity 어노테이션과 같이 사용할 수 있는 어노테이션
- 데이터베이스 상에서 엔티티 클래스를 어떠한 테이블로 생성할 것인지에 대한 정보를 담기 위한 어노테이션
- 테이블 뿐만 아니라 인덱스 등 생성도 가능

### @Id와 @GeneratedValue

- @Entity가 붙은 클래스는 Primary Key에 해당하는 특정 필드를 @Id로 지정해야 한다.
- @Id와 함께 자동으로 생성되는 번호를 사용하기 위해 @GeneratedValue 어노테이션 활용

- @GeneratedValue(strategy = GenerationType.키 생성 전략) 방식으로 아래와 같은 키 생성 전략 설정 가능
  - AUTO(default) : JPA 구현체(스프링 부트에서는 하이버네이트) 가 생성 방식 결정
  - IDENTITY : 사용하는 데이터베이스가 키 생성 결정. MySQL이나 MariaDB의 경우 auto increment 사용
  - SEQUENCE : 데이터베이스의 sequence 이용하여 키 생성. @SequenceGenerator와 같이 사용
  - TABLE : 키 생성 전용 테이블을 생성해서 키 생성. @TableGenerator와 함께 사용

### @Column

- @Column 어노테이션을 활용해 다양한 속성 지정
- 주로 nullable, name, length 등을 이용해 데이터베이스의 컬럼에 필요한 정보 제공

### 엔티티 클래스 설정

```java
@Getter
@Builder
@AllArgsConstructor
@NoArgsConstructor
@ToString
@Entity
public class Posts extends BaseTime {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String content;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String ref;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String imageUrl;
    
    }
}

```

- @Builder를 사용해서 객체를 생성할 수 있게 처리
- @Builder를 이용하기 위해서는 @AllArgsConstructor 와 @NoArgsConstructor를 항상 같이 처리해야 컴파일 에러 발생 X

### Spring Data JPA를 위한 스프링 부트 설정 

```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://000.000.000.000:3306/spring_boot_ex?useSSL=false&useUnicode=true&serverTimezone=Asia/Seoul
spring.datasource.username=0---
spring.datasource.password=9---

spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.show-sql=true
```

- spring.jpa.hibernate.ddl-auto : 프로젝트 실행 시에 자동으로 DDL을 생성할 것인지 결정
  - create, update(변경이 필요한 경우 alter,  테이블이 없는 경우 create), create-drop, validate
- spring.jpa.properties.hibernate.format_sql : 실제 JPA의 구현체인 하이버네이트가 동작하면서 발생하는 SQL을 포맷팅해서 출력
- spring.jpa.show-sql : JPA 처리 시에 발생하는 SQL을 보여줄 것인지 결정

### JpaRepository 인터페이스

![image](https://github.com/user-attachments/assets/f4057314-13a1-4b9a-89ea-edafaa89d3d8)

- Spring Data JPA에는 여러 종류의 인터페이스의 기능을 통해 JPA 관련 작업을 별도 코드 없이 처리할 수 있게 지원
- CRUD, 페이징/정렬 등의 처리도 인터페이스의 메서드를 호출하는 형태로 처리. 기능에 따라서 상속 구조로 추가적인 기능 제공
- 



**Reference**

- [Spring - ORM, JPA, Hibernate, JDBC 총정리](https://velog.io/@murphytklee/Spring-ORM-JPA-Hibernate-JDBC-%EC%B4%9D%EC%A0%95%EB%A6%AC****)