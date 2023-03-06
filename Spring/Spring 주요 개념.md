
# Spring

**:book: Contents**

- [Spring](#spring)
    - [MVC 패턴](#mvc-패턴)
    - [3계층 아키텍쳐](#3계층-아키텍쳐)
    - [프런트 컨트롤러 디자인 패턴](#프런트-컨트롤러-디자인-패턴)
    - [POJO](#pojo)
    - [프레임워크란](#프레임워크란)
    - [스프링 프레임워크란](#스프링-프레임워크란)
    - [Container란](#container란)
    - [IoC(Inversion of Control, 제어의 역전)](#iocinversion-of-control-제어의-역전)
      - [Spring에서의 IoC](#spring에서의-ioc)
    - [DI(Dependency Injection. 의존성 주입) 관련 개념 정리](#didependency-injection-의존성-주입-관련-개념-정리)
      - [빈(Bean)](#빈bean)
      - [빈 팩토리(Bean Factory)](#빈-팩토리bean-factory)
      - [애플리케이션 컨텍스트(Application Context)](#애플리케이션-컨텍스트application-context)
      - [설정 메타정보(Configuration metadata)](#설정-메타정보configuration-metadata)
      - [Bean 등록 어노테이션](#bean-등록-어노테이션)
      - [Bean 등록 및 의존관계 설정 어노테이션](#bean-등록-및-의존관계-설정-어노테이션)
      - [Bean 생명주기](#bean-생명주기)
      - [Bean 초기화 방법 3가지](#bean-초기화-방법-3가지)
      - [Bean 소멸 방법 3가지](#bean-소멸-방법-3가지)
        - [권장하는 방법](#권장하는-방법)
      - [Bean Scope](#bean-scope)
    - [DI(Dependency Injection, 의존성 주입)](#didependency-injection-의존성-주입)
      - [의존성(Dependency)](#의존성dependency)
    - [DAO와 DTO의 차이](#dao와-dto의-차이)
    - [스프링 프론트 컨트롤러 패턴](#스프링-프론트-컨트롤러-패턴)
    - [단위 테스트](#단위-테스트)
      - [JUnit](#junit)
    - [AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)](#aopaspect-oriented-programming-관점-지향-프로그래밍)
    - [Spring vs Spring Boot](#spring-vs-spring-boot)
    - [Filter와 Interceptor 차이](#filter와-interceptor-차이)
      - [Filter, Interceptor](#filter-interceptor)
      - [Filter, Interceptor 흐름](#filter-interceptor-흐름)
      - [Filter 특징](#filter-특징)
      - [Interceptor 특징](#interceptor-특징)
        - [Filter, Interceptor 차이점 요약](#filter-interceptor-차이점-요약)
  - [Reference](#reference)
  - [:house: Home](#house-home)

  

---

### MVC 패턴
- 정의
	- 애플리케이션을 모델(Model), 뷰(View), 컨트롤러(Controller) 로 구분하여 작업을 분리하는 디자인 패턴
- 구분
	- 뷰
		- 클라이언트와 서버 간의 인터페이스 역할을 하는 영역으로서 클라이언트로부터 요청 받거나 처리된 결과를 보여주는 기능
		- 구현 방법 : HTML, CSS, JSP
	- 컨트롤러
		- 뷰와 모델을 연결하는 중계 역할. 클라이언트가 전달한 파라미터를 추출하여 모델로 전달하고, 처리 결과를 페이지로 보여주는 기능
		- 구현 방법 : JSP, 서블렛
	- 모델
		- 서비스와 데이터베이스 처리를 담당하는 역할. 비즈니스 로직 처리, DB 질의 처리 기능
		- 구현 방법 : POJO(Plain Old Java Object). 일반 평범한 자바 객체
		- 구분
			- Service/Business 객체 : 서비스 처리 담당.
			- DAO(Data Access Object) : 데이터베이스 처리 담당.
- 장점
	- 서로 간의 결합도를 최소화
	- 유지보수성 높임
	- 개발자들의 각각 맡은 영역에만 집중할 수 있게 하여 개발의 효율성을 극대화

### 3계층 아키텍쳐
웹 애플리케이션을 개발할 때 디자인 패턴은 MVC 디자인 패턴을 사용하며, 구조적인 측면에서 3계층 아키텍처를 사용한다. 각 레이어는 독립된 역할을 갖는다.
![3 Layered Architecture - Blogs](https://www.ecanarys.com/sites/default/files/anant.patil-50/3lyrs2.jpg)
- 정의
	- 프레젠테이션 계층(Presentation tier/Layer)
		- 구성 : 뷰, 컨트롤러
		- 최상위에 위치하는 영역으로써, 사용자와 애플리케이션 간 상호작용 위한 인터페이스, 사용자의 요청을 비즈니스 계층에 전달하거나, 처리 결과를 뷰 페이지로 이동하는 기능
		- 프런트엔드
	- 비즈니스 계층(Business tier) = 서비스 영역(Business Logic Layer)
		- 실제 클라이언트가 요청한 서비스를 처리하는 비즈니스 로직 구현
		- 미들웨어, 백엔드
	- 영속 계층(Persistent tier) = 데이터 영역(Data Access Layer)
		- 데이터베이스 서버나 파일 시스템에 접근하여 데이터를 생성/관리하는 기능 담당
		- 백엔드

### 프런트 컨트롤러 디자인 패턴
대표 컨트롤러(Front Controller)을 두고 뷰에서 들어오는 모든 요청을 담당하게 하여 애플리케이션을 실행하는 모든 요청을 일괄적으로 처리.

![프론트 컨트롤러 패턴](https://velog.velcdn.com/images/jmjmjames/post/a5a31ce2-9764-4d89-9c85-ed8223c1beff/image.png)

- 프런트 컨트롤러 구현 방법
	- 프런트 컨트롤러 지정 및 URL 패턴 지정 : web.xml에 서블렛으로 FrontController 및 url-pattern 으로 /*을 설정하여 모든 요청을 받을 수 있게 한다.
	- 그 후 실제 요청한 서비스를 처리할 서브 컨트롤러를 구현한다.
- 프런트 컨트롤러 기능
  - 어떤 컨트롤러가 요청을 실행할 지 결정
  - 렌더링할 뷰를 결정
- 장점
  - 각 요청을 적절한 곳으로 위임해줌으로써 개발과 유지보수의 효율성이 증가
  - 모든 요청에 대해 보안, 국제화, 라우팅 및 로그와 같은 일반적인 기능을 한 곳에서 캡슐화

### POJO

**객체지향 원리에 따라 만들어진 자바 언어의 기본에 충실하게 비즈니스 로직을 구현**, 즉 프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않는 단순한 클래스.

- 특징

  - Java에서 제공하는 API 외에 종속되지 않음

  - 특정 규약, 환경에 종속되지 않음

  - 환경에 종속되지 않는 것의 장점

  - 코드의 간결함 (비즈니스 로직과 특정 환경/low 레벨 종속적인 코드를 분리하므로 단순)

  - 비즈니스 로직과 특정 환경이 분리되므로 단순함

  - 자동화 테스트에 유리 (환경 종속적인 코드는 자동화 테스트가 어렵지만, POJO는 테스트가 매우 유연)

  - 객체지향 설계의 자유로운 사용

### 프레임워크란
-   정의
    -   비기능적 요구사항(보안, 확장성, 안정성 등)을 만족하는 구조와 구현된 기능을 안정적으로 실행하도록 제어해주는 잘 만들어진 구조의 라이브러리 덩어리. '반제품'을 의미한다.
-   목표
    -   애플리케이션들의 최소한의 공통점을 찾아 하부 구조를 제공함으로써 개발자가 Application 개발에 집중할 수 있도록 한다.
-   장점
    -   개발 기간 단축
    -   성능 향상
    -   유지보수성 향상
   
### 스프링 프레임워크란

* 자바 엔터프라이즈 개발을 편하게 해주는 경량급 오픈소스 애플리케이션 프레임워크
* 목표 : **POJO 기반의** Enterprise Application 개발을 쉽고 편하게 할 수 있도록 한다.
* Java Application을 개발하는데 필요한 하부구조(Infrastructure)를 포괄적으로 제공한다. Spring이 하부구조를 처리하기 때문에 개발자는 Application 개발에 집중할 수 있다.
* 특징
	* 컨테이너 역할
		* 자바 객체의 라이프사이클을 관리하며, 필요한 객체를 제공한다.
	* DI(의존관계 주입) 지원
		* xml 설정파일이나 어노테이션을 통해 객체 간의 의존 관계를 설정할 수 있다.
	* AOP 지원
		* 스프링은 트랜잭션이나 로깅, 보안과 같이 공통적으로 필요로 하는 모듈들을 실제 핵심 모듈에서 분리해서 적용할 수 있다.
	* POJO(Plain Old Java Object) 지원
		* 스프링 컨테이너에 저장되는 자바 객체는 특정한 인터페이스를 구현하거나, 특정 클래스를 상속 받지 않아도 된다.
	* 트랜잭션 처리를 위한 일관된 방법을 지원
		* JDBC, JTA 등 어떤 트랜잭션을 사용하던 설정을 통해 정보를 관리하므로 트랜잭션 구현에 상관없이 동일한 코드 사용 가능
	* 영속성과 관련된 다양한 API 지원
		* Spring은 MyBatis, Hibernate 등 데이터베이스 처리를 위한 ORM(Object Relational Mapping) 프레임워크들과의 연동 지원  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [https://gmlwjd9405.github.io/2018/10/26/spring-framework.html](https://gmlwjd9405.github.io/2018/10/26/spring-framework.html)
  



### Container란

- 컨테이너(Container)는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것이라 할 수 있다. 다시 말해, 컨테이너란 당신이 작성한 코드의 처리과정을 위임받은 독립적인 존재라고 생각하면 된다. 컨테이너는 적절한 설정만 되어있다면 누구의 도움없이도 프로그래머가 작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸을 컨트롤해준다.

- Spring 프레임워크는 다른 프레임워크들과 달리 컨테이너 기능을 제공하고 있다. 이와 같은 컨테이너 기능을 제공하는 것이 가능하도록 하는 것이 IoC 패턴이다.

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [http://limmmee.tistory.com/13](http://limmmee.tistory.com/13)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)

  

### IoC(Inversion of Control, 제어의 역전)

- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것, 즉 제어 권한을 자신이 아닌 다른 대상에게 위임하는 것이다.

- 개발자는 프레임워크에 필요한 부품을 개발하고 조립하는 방식의 개발을 하게 된다.

- 이렇게 조립된 코드의 최종 호출은 개발자에 의해서 제어되는 것이 아니라 프레임워크의 내부에서 결정된 대로 이뤄지게 되는데, 이러한 현상을 "제어의 역전"이라고 표현한다.

#### Spring에서의 IoC

- Spring 프레임워크에서 지원하는 Ioc Container는 POJO(Plain Old Java Object)의 생성과 의존성, 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공한다.

- 라이브러리와 프레임워크의 차이

  - IoC의 개념이 적용되었나의 차이, 즉 애플리케이션 흐름을 어떤 것이 제어하는가의 차이다.

  - 라이브러리를 사용할 경우, 애플리케이션 코드가 라이브러리를 활용하여 능동적으로 애플리케이션 흐름을 직접 제어한다.

  - 반면에 프레임워크를 사용할 경우, 프레임워크가 애플리케이션 흐름을 제어한다. 보통 프레임워크 위에 개발자가 개발한 클래스를 등록해두고, 프레임워크가 흐름을 주도하는 중에 이것을 사용하는 방식이다.

  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=3664](http://wiki.javajigi.net/pages/viewpage.action?pageId=3664)

> - [http://limmmee.tistory.com/13](http://limmmee.tistory.com/13)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)

### DI(Dependency Injection. 의존성 주입) 관련 개념 정리

#### 빈(Bean)

* 스프링 IoC 컨테이너가 관리하는 객체
* 스프링이 직접 생성과 제어를 담당
* @Bean 을 사용하거나 xml 설정을 통해 일반 객체를 Bean으로 등록할 수 있고, Bean으로 등록된 객체는 쉽게 주입하여 사용 가능

#### 빈 팩토리(Bean Factory)

* 스프링의 IoC를 담당하는 핵심 컨테이너
* Bean을 등록, 생성, 조회, 반환하는 기능 담당

#### 애플리케이션 컨텍스트(Application Context)
* 빈 팩토리를 확장한 IoC 컨테이너
* 스프링이 제공하는 각종 부가 서비스를 추가로 제공
* 주로 사용됨

#### 설정 메타정보(Configuration metadata)
* 애플리케이션 컨텍스트 또는 빈 팩토리가 IoC를 적용하기 위해 사용하는 메타정보
* IoC 컨테이너에 의해 관리되는 빈 객체를 생성/구성

#### Bean 등록 어노테이션
* @Compoment : 스프링 빈을 정의하는 일반적인 방법. 개발자가 작성한 class를 기반으로 실행 시점에 인스턴스 객체를 1회(싱글톤) 생성
* @Bean : 개발자가 작성한 method를 기반으로 메서드에서 반환하는 객체를 인스턴스 객체로 1회(싱글톤) 생성
* @Repository : 퍼시스턴스 레이어의 데이터베이스 관련 클래스를 정의
* @Service : 서비스 레이어의 비즈니스 로직을 가진 클래스 정의
* @Controller : 프레젠테이션 레이어의 웹 어플리케이션의 요청/응답을 처리하는 클래스 정의

#### Bean 등록 및 의존관계 설정 어노테이션

* @Configuration
  * 스프링 IoC 컨테이너가 해당 클래스를 빈 정의 설정 용도로 사용하게끔 한다.

* @ComponentScan
  * @Component를 통해 자동으로 빈을 등록하고, @Autowired로 의존 관계를 주입 받는 어노테이션을 클래스에서 선언하여 사용했을 경우, 해당 클래스가 위치한 특정 패키지를 Scan하여 빈과 의존 관계를 식별한다.
  * xml 파일에 설정하는 것도 가능하다.

* @Autowired
  * 선언된 해당 변수에 자동으로 빈을 매핑
  * 변수, setter 메서드, 생성자, 일반 메서드에 적용 가능
  * 의존 객체 주입 시 주로 Type 이용

* @Resource
  * 어플리케이션에서 필요로 하는 자원을 자동 연결
  * 변수, setter 메서드에 적용 가능
  * 의존 객체 주입 시 주로 Name 이용

* @Value
  * 단순 값 주입용

* @Qualifier
  * @Autowired 어노테이션과 같이 사용된다.
  * 동일한 타입의 빈 객체가 여러 개 존재할 때 특정 빈을 찾는 용도
* @Primary
  * 특정 의존 관계를 오토와이어링할 수 있는 후보가 둘 이상 있을 때, 이 어노테이션을 사용한 빈이 호출된다.


#### Bean 생명주기

- 객체 생성 -> 의존 설정 -> 초기화 -> 사용 -> 소멸

- 스프링 컨테이너에 의해 생명주기 관리

- 스프링 컨테이너 초기화 시 빈 객체 생성, 의존 객체 주입 및 초기화

- 스프링 컨테이너 종료 시 빈 객체 소멸

  

#### Bean 초기화 방법 3가지

1. 빈 초기화 메소드에 ```@PostConstruct``` 사용

- 빈 정의 xml에 ```<context:annotation-config></context:annotation-config>``` 추가

2.  ```InitializingBean``` 인터페이스의 ```afterPropertiesSet()``` 메소드 오버라이드

3. 커스텀 init() 메소드 정의

- 빈 정의 xml에 ```init-method``` 속성으로 메소드 이름 지정

- 또는 빈 초기화 메소드에 ```@Bean(init-method="init")``` 지정

  

#### Bean 소멸 방법 3가지

1. 빈 소멸 메소드에 ```@PreDestroy``` 사용

- 빈 정의 xml에 ```<context:annotation-config></context:annotation-config>``` 추가

2.  ```DisposableBean``` 인터페이스의 ```destroy()``` 메소드 오버라이드

3. 커스텀 destroy() 메소드 정의

- 빈 정의 xml에 ```destroy-method``` 속성으로 메소드 이름 지정

  

##### 권장하는 방법

- 1번 방법 (권장)

  - 사용 방법이 간결하며 코드에서 초기화 메소드가 존재함을 쉽게 파악 가능하여 xml 설정 방법보다 직관적

- 2번 방법 (지양)

  - 빈 코드에 스프링 인터페이스가 노출되어 권장하지 않으며 간결하지 않은 방법

- 3번 방법

  - 빈 코드에 스프링 인터페이스는 노출되지 않지만, 코드만으로 초기화 메소드 호출 여부를 알 수 없는 단점

  

#### Bean Scope

*  **singleton (default)**

   * 애플리케이션에서 Bean 등록 시 singleton scope로 등록

   * Spring IoC 컨테이너 당 한 개의 인스턴스만 생성

   * 컨테이너가 Bean 가져다 주입할 때 항상 같은 객체 사용

   * 메모리나 성능 최적화에 유리

*  **prototype**

   * 컨테이너에서 Bean 가져다 쓸 때 항상 다른 인스턴스 사용

   * 모든 요청에서 새로운 객체 생성

   * gc에 의해 Bean 제거

* request

  * Bean 등록 시 하나의 HTTP request 생명주기 안에 단 하나의 Bean만 존재

  * 각각의 HTTP 요청은 고유 Bean 객체 보유

  * Spring MVC Web Application에서 사용

* session

  * 하나의 HTTP Session 생명주기 안에 단 하나의 Bean만 존재

  * Spring MVC Web Application에서 사용

* global session

  * 하나의 global HTTP Session 생명주기 안에 한 개의 Bean 지정

  * Spring MVC Web Application에서 사용

* application

  * ServletContext 생명주기 안에 한 개의 Bean 지정

  * Spring MVC Web Application에서 사용

  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [[Spring] IOC(Inversion Of Control): 제어 역전](https://velog.io/@max9106/Spring-IOC%EB%AF%B8%EC%99%84)

> - [[Spring] Spring Bean의 개념과 Bean Scope 종류](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)

> - [Spring 빈/컨테이너 생명주기 (Lifecycle)](https://flowarc.tistory.com/entry/Spring-%EB%B9%88%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-Lifecycle)

> - [SpringMVC :: 스프링 컨테이너의 생명주기, 빈의 생명주기 (Life cycle), InitialzingBean, DisposableBean, @PreDestroy, @PostConstruct](https://hongku.tistory.com/106)

> - [[Spring] 빈(bean)생명주기 메소드](https://cornswrold.tistory.com/100)


### DI(Dependency Injection, 의존성 주입)

- Spring 프레임워크에서 지원하는 IoC의 형태이다.

- 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동적으로 연결해주는 것을 말한다. 개발자들은 제어를 담당할 필요없이 빈 설정 파일에 의존관계가 필요하다는 정보만 추가해주면 된다.

- 컨테이너가 실행 흐름의 주체가 되어 애플리케이션 코드에 의존 관계를 주입하고, 이로 인해 실행 시에 동적으로 의존 관계가 생성된다.

#### 의존성(Dependency)

- 현재 객체가 다른 객체와 상호작용(참조)하고 있다면 다른 객체들을 현재 객체의 의존이라 한다.

- 의존성이 위험한 이유

  - 모듈 간 결합도가 높아져 강한 결합이 된다.(다른 클래스를 직접적으로 사용하여 클래스 간 의존성이 높아진다.)
    - 코드 유연성과 재사용성을 줄이고, 코드 변경을 어렵게 한다.
      - 하나의 모듈이 바뀌면 의존한 다른 모듈까지 변경되야 한다.
    - 시험 가능성을 지연시킨다.
      - 다른 모듈로부터 독립적으로 테스트할 수 없기에 단위 테스트 작성이 어렵다.

- DI의 장점

  - 모듈 간 결합도가 제거되어 느슨한 결합이 가능하다.(클래스 간 의존성을 줄인다.)
    - 코드 유연성과 재사용성을 높이고, 코드 변경 가능성을 높인다.
    - 다른 클래스와 독립적으로 클래스를 단위 테스트 할 수 있다.
  
  - SRP(Single Responsibility Principle)를 준수할 수 있다.
    - 애플리케이션의 각 클래스와 컴포넌트가 명확하게 정의된 특정 책임을 갖도록 설계할 수 있다.

  - 코드가 단순해진다.

- DI의 세가지 방법

  - Contructor Injection : 생성자 주입
    - 의존성을 입력 받는 생성자를 만들고 이를 통해 의존성을 주입한다.

  - Method(Setter) Injection : 메소드 매개 변수 주입
    - 필요한 의존성을 포함하는 클래스의 생성자를 만들고 이를 통해 의존성을 주입한다.
    - 변수에 @Autowired를 지정하면 스프링은 자동으로 setter 주입을 사용한다.

  - Field Injection : 멤버 변수 주입
    - 의존성을 입력 받는 일반 메서드를 만들고 이를 통해 의존성을 주입한다.

  - 생성자 주입 vs setter 주입
    - 불변 객체에는 생성자 주입 사용
      - setter 주입 사용 시 생성 중 오브젝트 상태가 변경되기 때문
    - 클래스에 많은 의존 관계가 있다는 것을 숨길 시 setter 주입 사용
      - 생성자 주입 사용 시 생성자의 크기가 증가하므로 이것이 드러남

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [http://www.nextree.co.kr/p11247/](http://www.nextree.co.kr/p11247/)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)

> - [http://tony-programming.tistory.com/entry/Dependency-의존성-이란](http://tony-programming.tistory.com/entry/Dependency-의존성-이란)


### DAO와 DTO의 차이

-  **DAO(Data Access Object)**

   - DB의 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체를 말한다.

   - DB에 접근을 하기위한 로직과 비즈니스 로직을 분리하기 위해서 사용

-  **DTO(Data Transfer Object)**

   - 계층간 데이터 교환을 위한 Bean을 말한다.

   - 여기서 말하는 계층은 Controller, View, Business Layer, Persistent Layer 이다.

   - 일반적인 DTO는 로직을 갖고 있지 않는 순수한 데이터 객체이며, 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스이다.

- VO(Value Object)

  - DTO와 동일한 개념이지만 read only 속성을 가진다.

  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [https://jungwoon.github.io/common%20sense/2017/11/16/DAO-VO-DTO/](https://jungwoon.github.io/common%20sense/2017/11/16/DAO-VO-DTO/)



### 스프링 프론트 컨트롤러 패턴
  - 디스패처 서블릿(Dispacher Servlet)이 Bean으로 등록되어 package를 scan하고 @Controller, @RestController 애노테이션을 확인하여 어떠한 요청이 들어왔을 때 적절한 Handler Method에 위임

![image](https://user-images.githubusercontent.com/52997401/223123839-7c5a9e7d-78bd-4e3a-ab97-a8ebebb24a61.png)

1.	디스패처 서블릿이 클라이언트로부터 요청을 받으면, 이를 요청할 핸들러 이름을 알기 위해 핸들러 맵핑에게 물어봅니다.
2.	핸들러 맵핑은 요청 URL을 보고 핸들러 이름을 디스패처 서블릿에게 알려줍니다. 이때 핸들러를 실행하기 전/후에 처리할 것을 인터셉터로 만듭니다.
3.	디스패처 서블릿은 해당 핸들러에게 제어권을 넘겨주고, 이 핸들러는 응답에 필요한 서비스를 호출하고 렌더링해야 하는 뷰 이름을 판단하여 디스패처 서블릿에게 전송해줍니다.
4.	디스패처 서블릿은 받은 뷰 이름을 뷰 리졸버에게 전달해 응답에 필요한 뷰를 만들라고 명령합니다.
5.	이때 해당하는 뷰는 디스패처 서블릿에게 받은 모델과 컨트롤러를 활용해 원하는 응답을 생성해서 다시 보내줍니다.
6.	디스패처 서블릿은 뷰로부터 받은 것을 클라이언트에게 응답해줍니다.


### 단위 테스트

- 개념 : 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차. 즉, 모든 함수와 메소드에 대한 테스트 케이스를 작성하는 절차.
- 목적 : 배포된 전체 애플리케이션을 테스트하는 대신, 각 클래스와 메소드의 책임에 자동화된 테스트를 작성한다.
- 장점
  - 미래 결함에 대비한 안전망
  - 결함의 조기 발견이 가능
  - TDD 가 더 나은 디자인을 만든다
  - 잘 작성된 테스트는 코드와 기능의 문서화 역할을 한다.

#### JUnit
- 자바에서 독립된 단위테스트를 지원해주는 프레임워크

- Spring-Test에서 테스트를 지원하는 어노테이션
  - @RunWith(SpringJUnit4ClassRunner.class)
    - SpringJUnit4ClassRunner라는 클래스를 지정해주면 jUnit 이 테스트를 진행하는 중에 ApplicationContext 를 만들고 관리하는 작업을 진행해 준다
    - RunWith 어노테이션은 각각의 테스트 별로 객체가 생성되더라도 싱글톤의 ApplicationContext 를 보장한다.
  - @ContextConfiguration
    - 스프링 빈 설정 파일의 위치를 지정


### AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)

어떤 로직을 기준으로 핵심 관점과 부가 관점을 나누고, 관점을 기준으로 모듈화하는 것

- 핵심 관점은 주로 핵심 비즈니스 로직

- 부가 관점은 핵심 로직을 실행하기 위한 데이터베이스 연결, 로깅, 파일 입출력 등

* AOP 목적

  - 소스 코드에서 여러 번 반복해서 쓰는 코드(= 흩어진 관심사, Concern)를 Aspect로 모듈화하여 핵심 로직에서 분리 및 재사용

  - 개발자가 핵심 로직에 집중할 수 있게 하기 위함

  - 주로 부가 기능을 모듈화

* AOP 주요 용어

  -  **Aspect**

     - 흩어진 관심사를 모듈화 한 것

     - Advice + PointCut

-  **Target**

- A spect를 적용하는 곳(클래스, 메소드 등)

-  **Advice**

   - 실질적으로 수행해야 하는 기능을 담은 구현체

-  **JoinPoint**

   - Advice가 적용될 위치

     - ex. 메소드 진입 시, 생성자 호출 시, 필드에서 값 꺼낼 때 등

-  **PointCut**

   - JoinPoint의 상세 스펙 정의

     - 더욱 구체적으로 Advice가 실행될 지점 지정

-  **Weaving**

   - PointCut에 의해 결정된 Target의 JoinPoint에 Advice를 삽입하는 과정

* AOP 적용 방법

  1. 컴파일 시 적용

     - AspectJ가 사용하는 방법

     - 자바 파일을 클래스 파일로 만들 때 Advice 소스가 추가되어 조작된 바이트 코드 생성하는 방법

  2. 로드 시 적용

     - AspectJ가 사용하는 방법

     - 컴파일 후 컴파일 된 클래스를 로딩하는 시점에 Advice 소스를 끼워넣는 방법

  3. 런타임 시 적용

    -  **Spring AOP**가 사용하는 방법

    - 스프링은 런타임 시 Bean 생성

    - A라는 Bean 만들 때 A라는 타입의 프록시 Bean도 생성하고, 프록시 Bean이 A의 메소드 호출 직전에 Advice 소스를 호출한 후 A의 메소드 호출

  

* Spring AOP 특징

  - [프록시 패턴](https://velog.io/@max9106/Spring-%ED%94%84%EB%A1%9D%EC%8B%9C-AOP-xwk5zy57ee) 기반의 AOP 구현체

  - Target 객체에 대한 프록시를 만들어 제공

  - Target을 감싸는 프록시는 런타임 시 생성

  - 접근 제어 및 부가 기능 추가를 위해 프록시 객체 사용

  - 프록시가 Target 객체의 호출을 가로채 Advice 수행 전/후 핵심 로직 호출

  - 스프링 Bean에만 AOP 적용 가능

  - 메소드 조인 포인트만 지원하여 메소드가 호출되는 런타임 시점에만 Advice 적용 가능

  - 모든 AOP기능을 제공하지는 않으며 스프링 IoC와 연동하여 엔터프라이즈 애플리케이션의 각종 문제(중복 코드, 프록시 클래스 작성의 번거로움, 객체 간 관계 복잡도 증가)에 대한 해결책 지원 목적

  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [[Spring] 스프링 AOP (Spring AOP) 총정리 : 개념, 프록시 기반 AOP, @AOP](https://engkimbs.tistory.com/746)

> - [[Spring] AOP란?](https://velog.io/@max9106/Spring-AOP%EB%9E%80-93k5zjsm95)

> - [Spring AOP, Aspect 개념 특징, AOP 용어 정리](https://shlee0882.tistory.com/206)

  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [http://limmmee.tistory.com/8?category=654011](http://limmmee.tistory.com/8?category=654011)


### Spring vs Spring Boot

* Spring
* Spring Boot

  
  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [http://blog.naver.com/PostView.nhn?blogId=sthwin&logNo=221271008423&parentCategoryNo=&categoryNo=50&viewDate=&isShowPopularPosts=true&from=search](http://blog.naver.com/PostView.nhn?blogId=sthwin&logNo=221271008423&parentCategoryNo=&categoryNo=50&viewDate=&isShowPopularPosts=true&from=search)


  

### Filter와 Interceptor 차이

  

#### Filter, Interceptor

* 애플리케이션에서 자주 사용되는 기능(공통 부분)을 분리하여 관리할 수 있도록 Spring이 제공하는 기능

  

#### Filter, Interceptor 흐름

  

![filterInterceptor](./images/filterInterceptor.jpg)

1. 서버 실행 시 Servlet이 올라오는 동안 init 후 doFilter 실행

2. Dispatcher Servlet을 지나쳐 Interceptor의 preHandler 실행

3. 컨트롤러를 거쳐 내부 로직 수행 후, Interceptor의 postHandler 실행

4. doFilter 실행

5. Servlet 종료 시 destroy

  

#### Filter 특징

* Dispatcher Servlet 이전에 수행되고, 응답 처리에 대해서도 변경 및 조작 수행 가능

* WAS 내의 ApplicationContext에서 등록된 필터가 실행

* WAS 구동 시 FilterMap이라는 배열에 등록되고, 실행 시 Filter chain을 구성하여 순차적으로 실행

* Spring Context 외부에 존재하여 Spring과 무관한 자원에 대해 동작

* 일반적으로 web.xml에 설정

* 예외 발생 시 Web Application에서 예외 처리

* ex. 인코딩 변환, XSS 방어 등

* 실행 메소드

* init() : 필터 인스턴스 초기화

* doFilter() : 실제 처리 로직

* destroy() : 필터 인스턴스 종료

  

#### Interceptor 특징

* Dispatcher Servlet 이후 Controller 호출 전, 후에 끼어들어 기능 수행

* Spring Context 내부에서 Controller의 요청과 응답에 관여하며 모든 Bean에 접근 가능

* 일반적으로 servlet-context.xml에 설정

* 예외 발생 시 @ControllerAdvice에서 @ExceptionHandler를 사용해 예외 처리

* ex. 로그인 체크, 권한 체크, 로그 확인 등

* 실행 메소드

* preHandler() : Controller 실행 전

* postHandler() : Controller 실행 후

* afterCompletion() : view Rendering 후

  

##### Filter, Interceptor 차이점 요약

* Filter는 WAS단에 설정되어 Spring과 무관한 자원에 대해 동작하고, Interceptor는 Spring Context 내부에 설정되어 컨트롤러 접근 전, 후에 가로채서 기능 동작

* Filter는 doFilter() 메소드만 있지만, Interceptor는 pre와 post로 명확하게 분리

* Interceptor의 경우 AOP 흉내 가능

* handlerMethod(@RequestMapping을 사용해 매핑 된 @Controller의 메소드)를 파라미터로 제공하여 메소드 시그니처 등 추가 정보를 파악해 로직 실행 여부 판단 가능

  
  

> :arrow_double_up:[Top](#9-spring) :leftwards_arrow_with_hook:[Back](https://github.com/WeareSoft/tech-interview#9-spring) :information_source:[Home](https://github.com/WeareSoft/tech-interview#tech-interview)

> - [[Spring] Filter, Interceptor, AOP 차이 및 정리](https://goddaehee.tistory.com/154)

> - [[Spring] Filter, Interceptor, AOP 차이](https://velog.io/@sa833591/Spring-Filter-Interceptor-AOP-%EC%B0%A8%EC%9D%B4-yvmv4k96)

> - [Spring Filter와 Interceptor](https://jaehun2841.github.io/2018/08/25/2018-08-18-spring-filter-interceptor/#spring-request-flow)

> - [(Spring)Filter와 Interceptor의 차이](https://supawer0728.github.io/2018/04/04/spring-filter-interceptor/)

  

---

  

## Reference

> - []()

  
  

## :house: [Home](https://github.com/WeareSoft/tech-interview)