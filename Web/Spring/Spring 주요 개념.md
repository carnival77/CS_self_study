# Spring

**:book: Contents**

- [Spring](#spring)
  - [Spring Framework](#spring-framework)
    - [프레임워크란](#프레임워크란)
    - [스프링 프레임워크란](#스프링-프레임워크란)
    - [POJO](#pojo)
    - [Container란](#container란)
    - [IoC(Inversion of Control, 제어의 역전)](#iocinversion-of-control-제어의-역전)
      - [Spring에서의 IoC](#spring에서의-ioc)
    - [DI(Dependency Injection, 의존성 주입)](#didependency-injection-의존성-주입)
      - [의존성(Dependency)](#의존성dependency)
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
    - [단위 테스트](#단위-테스트)
      - [JUnit](#junit)
    - [AOP(Aspect Oriented Programming, 관점 지향 프로그래밍)](#aopaspect-oriented-programming-관점-지향-프로그래밍)
      - [관점의 구분](#관점의-구분)
      - [AOP 목적](#aop-목적)
      - [AOP 주요 용어](#aop-주요-용어)
      - [Weaving 구분](#weaving-구분)
      - [AOP 프레임워크](#aop-프레임워크)
      - [Spring AOP의 구현 방식](#spring-aop의-구현-방식)
      - [Advice 종류](#advice-종류)
      - [Spring AOP 특징](#spring-aop-특징)
    - [스프링으로 작업 스케쥴링하기](#스프링으로-작업-스케쥴링하기)
      - [@Scheduled로 작업 스케쥴링하기](#scheduled로-작업-스케쥴링하기)
      - [@Async를 사용해 비동기식으로 작업 실행하기](#async를-사용해-비동기식으로-작업-실행하기)
      - [작업 실행자](#작업-실행자)
  - [Spring MVC](#spring-mvc)
    - [3계층 아키텍쳐](#3계층-아키텍쳐)
    - [DAO와 DTO의 차이](#dao와-dto의-차이)
    - [MVC 패턴](#mvc-패턴)
    - [프런트 컨트롤러 디자인 패턴](#프런트-컨트롤러-디자인-패턴)
    - [스프링 프론트 컨트롤러 패턴](#스프링-프론트-컨트롤러-패턴)
      - [Spring MVC 애플리케이션 설정법](#spring-mvc-애플리케이션-설정법)
      - [Spring MVC의 주요 구성 요소](#spring-mvc의-주요-구성-요소)
      - [스프링 프론트 컨트롤러 패턴 실행 흐름](#스프링-프론트-컨트롤러-패턴-실행-흐름)
      - [컨트롤러를 위한 핵심 어노테이션](#컨트롤러를-위한-핵심-어노테이션)
      - [@ExceptionHandler 어노테이션의 사용](#exceptionhandler-어노테이션의-사용)
  - [REST](#rest)
    - [RESTful 웹서비스](#restful-웹서비스)
      - [HTTP Method](#http-method)
      - [Spring MVC 기반 RESTful 웹서비스 구현 절차](#spring-mvc-기반-restful-웹서비스-구현-절차)
      - [RESTful Controller를 위한 핵심 어노테이션](#restful-controller를-위한-핵심-어노테이션)
  - [SpringBoot](#springboot)
    - [스프링 부트 장점](#스프링-부트-장점)
    - [스프링 부트의 목표](#스프링-부트의-목표)
    - [스프링 프레임워크 기반 프로젝트 구축 vs 스프링부트 기반 프로젝트 구축](#스프링-프레임워크-기반-프로젝트-구축-vs-스프링부트-기반-프로젝트-구축)
    - [스프링부트 기반 프로젝트 구축 관련 주요 개념](#스프링부트-기반-프로젝트-구축-관련-주요-개념)
      - [spring-boot-starter-parent](#spring-boot-starter-parent)
      - [스타터 프로젝트](#스타터-프로젝트)
      - [spring-boot-maven-plugin](#spring-boot-maven-plugin)
      - [스프링 부트 launch 클래스 생성](#스프링-부트-launch-클래스-생성)
      - [스프링 부트 기반 애플리케이션 실행 시 특징](#스프링-부트-기반-애플리케이션-실행-시-특징)
    - [자동 설정](#자동-설정)
    - [애플리케이션 구성 외부화](#애플리케이션-구성-외부화)
      - [application.properties를 통한 프레임워크 사용자 정의](#applicationproperties를-통한-프레임워크-사용자-정의)
      - [애플리케이션별로 사용자 정의 속성 정의하기](#애플리케이션별로-사용자-정의-속성-정의하기)
      - [다른 환경에 프로파일 생성하기](#다른-환경에-프로파일-생성하기)
        - [액티브 프로파일을 기반으로 동적 빈 구성하기](#액티브-프로파일을-기반으로-동적-빈-구성하기)
    - [YAML 구성](#yaml-구성)
    - [임베디드 서버](#임베디드-서버)
      - [전통적인 자바 애플리케이션 배포 vs 임베디드 서버 활용 배포](#전통적인-자바-애플리케이션-배포-vs-임베디드-서버-활용-배포)
      - [JAR대신 기존 WAR 파일 빌드](#jar대신-기존-war-파일-빌드)
    - [개발자 도구를 사용해 생산성 향상](#개발자-도구를-사용해-생산성-향상)
      - [주요 기능](#주요-기능)
      - [장점](#장점)
      - [브라우저에서 실시간 리로드 활성화](#브라우저에서-실시간-리로드-활성화)
    - [애플리케이션 모니터링에 스프링 부트 액추에이터 사용하기](#애플리케이션-모니터링에-스프링-부트-액추에이터-사용하기)
      - [애플리케이션 모니터링](#애플리케이션-모니터링)
      - [HAL 브라우저를 사용해 액추에이터 엔드포인트 찾기](#hal-브라우저를-사용해-액추에이터-엔드포인트-찾기)
      - [액추에이터로 확인 가능한 주요 사항](#액추에이터로-확인-가능한-주요-사항)
- [Reference](#reference)

---

## Spring Framework

### 프레임워크란

- 정의
  - 비기능적 요구사항(보안, 확장성, 안정성 등)을 만족하는 구조와 구현된 기능을 안정적으로 실행하도록 제어해주는 잘 만들어진 구조의 라이브러리 덩어리. '반제품'을 의미한다.
- 목표
  - 애플리케이션들의 최소한의 공통점을 찾아 하부 구조를 제공함으로써 개발자가 Application 개발에 집중할 수 있도록 한다.
- 장점
  - 개발 기간 단축
  - 성능 향상
  - 유지보수성 향상

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

> - [https://gmlwjd9405.github.io/2018/10/26/spring-framework.html](https://gmlwjd9405.github.io/2018/10/26/spring-framework.html)

### POJO

**객체지향 원리에 따라 만들어진 자바 언어의 기본에 충실하게 비즈니스 로직을 구현**, 즉 프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않는 단순한 클래스.

- 특징
  
  - Java에서 제공하는 API 외에 종속되지 않음
  
  - 특정 규약, 환경에 종속되지 않음
  
  - 코드의 간결함 (비즈니스 로직과 특정 환경/low 레벨 종속적인 코드를 분리하므로 단순)
  
  - 자동화 테스트에 유리 (환경 종속적인 코드는 자동화 테스트가 어렵지만, POJO는 테스트가 매우 유연)
  
  - 객체지향 설계의 자유로운 사용

### Container란

- 컨테이너(Container)는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 하는 것이라 할 수 있다. 다시 말해, 컨테이너란 당신이 작성한 코드의 처리과정을 위임받은 독립적인 존재라고 생각하면 된다. 컨테이너는 적절한 설정만 되어있다면 누구의 도움 없이도 프로그래머가 작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸을 컨트롤해준다.

- Spring 프레임워크는 다른 프레임워크들과 달리 컨테이너 기능을 제공하고 있다. 이와 같은 컨테이너 기능을 제공하는 것이 가능하도록 하는 것이 IoC 패턴이다.

> - [http://limmmee.tistory.com/13](http://limmmee.tistory.com/13)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)

### IoC(Inversion of Control, 제어의 역전)

- 객체의 생성에서부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것, 즉 제어 권한을 자신이 아닌 다른 대상에게 위임하는 것이다.

- 개발자는 프레임워크에 필요한 부품을 개발하고 조립하는 방식의 개발을 하게 된다.

- 이렇게 조립된 코드의 최종 호출은 개발자에 의해서 제어되는 것이 아니라 프레임워크의 내부에서 결정된 대로 이뤄지게 되는데, 이러한 현상을 "제어의 역전"이라고 표현한다.

#### Spring에서의 IoC

- Spring 프레임워크에서 지원하는 Ioc Container는 POJO(Plain Old Java Object)의 생성과 의존성, 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능들을 제공한다.

- 라이브러리와 프레임워크의 차이
  
  - **라이브러리** : 특정 기능에 대한 도구들의 집합
  
  - **프레임워크** : 비기능적 요구사항(보안, 확장성, 안정성 등)을 만족하는 구조와 구현된 기능을 안정적으로 실행하도록 제어해주는 잘 만들어진 구조의 라이브러리 덩어리
  
  - 우선, 프레임워크가 라이브러리를 포함한다.
  
  - 또한, IoC의 개념이 적용되었나의 차이, 즉 애플리케이션 흐름을 어떤 것이 제어하는가의 차이다.
  
  - 라이브러리를 사용할 경우, 사용자가 애플리케이션 코드를 짜며 능동적으로 라이브러리를 호출하여 애플리케이션 흐름을 직접 제어한다.
  
  - 반면에 프레임워크를 사용할 경우, 프레임워크가 애플리케이션 흐름을 제어한다. 보통 프레임워크 위에 개발자가 개발한 클래스를 등록해두고, 프레임워크가 흐름을 주도하는 중에 이것을 사용하는 방식이다.
  
  ![image](https://user-images.githubusercontent.com/52997401/223724639-9e424a82-d865-44c4-af49-e9b05b06254f.png)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=3664](http://wiki.javajigi.net/pages/viewpage.action?pageId=3664)

> - [http://limmmee.tistory.com/13](http://limmmee.tistory.com/13)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)
> - [프레임워크와 라이브러리의 차이점](https://mangkyu.tistory.com/4)

### DI(Dependency Injection, 의존성 주입)

- Spring 프레임워크에서 지원하는 IoC의 형태이다.

- 클래스 사이의 의존관계를 빈 설정 정보를 바탕으로 컨테이너가 자동적으로 연결해주는 것을 말한다. 개발자들은 제어를 담당할 필요없이 빈 설정 파일에 의존관계가 필요하다는 정보만 추가해주면 된다.

- 컨테이너가 실행 흐름의 주체가 되어 애플리케이션 코드에 의존 관계를 주입하고, 이로 인해 실행 시에 동적으로 의존 관계가 생성된다.

#### 의존성(Dependency)

현재 객체가 다른 객체와 상호작용(참조)하고 있다면 다른 객체들을 현재 객체의 의존이라 한다.

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

> - [http://www.nextree.co.kr/p11247/](http://www.nextree.co.kr/p11247/)

> - [http://wiki.javajigi.net/pages/viewpage.action?pageId=281](http://wiki.javajigi.net/pages/viewpage.action?pageId=281)

> - [http://tony-programming.tistory.com/entry/Dependency-의존성-이란](http://tony-programming.tistory.com/entry/Dependency-의존성-이란)

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
2. ```InitializingBean``` 인터페이스의 ```afterPropertiesSet()``` 메소드 오버라이드

3. 커스텀 init() 메소드 정의
- 빈 정의 xml에 ```init-method``` 속성으로 메소드 이름 지정

- 또는 빈 초기화 메소드에 ```@Bean(init-method="init")``` 지정

#### Bean 소멸 방법 3가지

1. 빈 소멸 메소드에 ```@PreDestroy``` 사용
- 빈 정의 xml에 ```<context:annotation-config></context:annotation-config>``` 추가
2. ```DisposableBean``` 인터페이스의 ```destroy()``` 메소드 오버라이드

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

* **singleton (default)**
  
  * 애플리케이션에서 Bean 등록 시 singleton scope로 등록
  
  * Spring IoC 컨테이너 당 한 개의 인스턴스만 생성
  
  * 컨테이너가 Bean 가져다 주입할 때 항상 같은 객체 사용
  
  * 메모리나 성능 최적화에 유리

* **prototype**
  
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

> - [[Spring] IOC(Inversion Of Control): 제어 역전](https://velog.io/@max9106/Spring-IOC%EB%AF%B8%EC%99%84)

> - [[Spring] Spring Bean의 개념과 Bean Scope 종류](https://gmlwjd9405.github.io/2018/11/10/spring-beans.html)

> - [Spring 빈/컨테이너 생명주기 (Lifecycle)](https://flowarc.tistory.com/entry/Spring-%EB%B9%88%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-Lifecycle)

> - [SpringMVC :: 스프링 컨테이너의 생명주기, 빈의 생명주기 (Life cycle), InitialzingBean, DisposableBean, @PreDestroy, @PostConstruct](https://hongku.tistory.com/106)

> - [[Spring] 빈(bean)생명주기 메소드](https://cornswrold.tistory.com/100)

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

애플리케이션에서의 관심사의 분리(기능의 분리)를 구현, 즉 핵심 기능에서 부가 기능을 분리하고, 분리한 부가 기능을 Aspect라는 모듈로 만들어 설계/개발한다.

#### 관점의 구분

- 핵심 관점 : 비즈니스 로직

- 부가 관점 : 핵심 로직을 실행하기 위한 부가 기능(데이터베이스 연결, 로깅, 파일 입출력 등)

#### AOP 목적

- 소스 코드에서 여러 번 반복해서 쓰는 코드(= 흩어진 관심사, Concern)를 Aspect로 모듈화하여 핵심 로직에서 분리 및 재사용

- 개발자가 핵심 로직에 집중

#### AOP 주요 용어

- **Aspect**
  
  - Advice + PointCut
  - 부가 기능을 정의한 코드인 어드바이스(Advice)와 어드바이스를 어디에 적용할지를 결정하는 포인트컷(PointCut)을 합친 개념
  - 구분된 애스팩트를 런타임 시 필요한 위치에 동적으로 실행

- **Target**
  
  - Aspect를 적용하는 곳(클래스, 메소드 등)

- **Advice**
  
  - 타겟에 제공할 수행 기능을 담은 구현체

- **JoinPoint**
  
  - Advice가 적용될 위치
    
    - 타겟 겟체가 구현한 인터페이스의 모든 메소드는 조인 포인트의 후보다.
    
    - 조인포인트를 사용해 메소드의 세부 정보(이름과 인수)를 얻을 수 있다.
      
      - ex. 메소드 진입 시, 생성자 호출 시, 필드에서 값 꺼낼 때 등

- **PointCut**
  
  - JoinPoint의 상세 스펙 정의
    
    - 어드바이스를 적용할 타겟의 메소드를 선별하는 정규표현식
      - 더욱 구체적으로 Advice가 실행될 지점 지정
      - execution으로 시작하고, 메소드의 Signature를 비교하는 방법 주로 이용
    
    ![image](https://user-images.githubusercontent.com/52997401/223365184-53e2cee3-8025-4d0d-b112-5e178caa864d.png)

- **Weaving**
  
  - PointCut에 의해 결정된 Target의 JoinPoint에 Advice를 삽입하는 과정

#### Weaving 구분

1. 컴파일 타임 위빙
   
   1. 자바 파일을 클래스 파일로 만들 때 Advice 소스가 추가되어 조작된 바이트 코드 생성하는 방법
   2. 입력은 소스 코드고 출력은 위빙이 있는 컴파일된 클래스이다.
   3. AspectJ가 사용하는 방법

2. 바이너리 위빙
   
   1. 컴파일 후 컴파일 된 클래스를 로딩하는 시점에 Advice 소스를 끼워넣는 방법
   2. 코드가 컴파일된 후에 수행된다.
   3. 입력은 컴파일된 클래스 파일 또는 jar 파일이고 출력은 위빙이 있는 컴파일된 클래스나 jar 파일이다.
   4. AspectJ가 사용하는 방법

3. 런타임 위빙
   
   1. 클래스가 JVM에 로드되기 직전에 수행된다.
   2. **Spring AOP**가 사용하는 방법
   3. 스프링은 런타임 시 Bean 생성
   4. A라는 Bean 만들 때 A라는 타입의 프록시 Bean도 생성하고, 프록시 Bean이 A의 메소드 호출 직전에 Advice 소스를 호출한 후 A의 메소드 호출

#### AOP 프레임워크

- AspectJ
  - 컴파일 타임 위빙을 제공한다.
  - 위빙을 수행하기 위해 AspectJ 컴파일러를 빌드 프로세스에 추가할 수 있다.
- 스프링 AOP
  - AspectJ와 자체의 몇 가지 기본 AOP 기능과의 통합을 제공한다.
  - 런타임 위빙을 수행한다.
  - 스프링 빈에서 메소드 호출만 인터셉트할 수 있다.

스프링 빈으로 작업 중이고 스프링 빈에서 메소드 호출을 인터셉트하려는 경우, 스프링 AOP면 충분하다. 

스프링 컨테이너에 의해 관리되지 않는 객체의 메소드 호출을 가로채려면 AspectJ를 사용해야 한다.

#### Spring AOP의 구현 방식

- XML 기반 POJO 클래스 이용
  - 부가기능 제공하는 어드바이스 클래스 작성
  - XML 설정 파일에 <aop:config>를 이용해서 애스펙트 설정
- @Aspect 어노테이션을 이용한 구현
  - @Aspect 어노테이션을 이용하여 부가 기능 제공하는 애스펙트 클래스를 어드바이스를 구현하는 메서드와 포인트컷을 포함하여 작성
  - XML 설정 파일에 <aop:aspectj-autoproxy /> 설정

#### Advice 종류

- @Around
  - 타겟의 메소드가 호출되기 이전/이후 시점에 모두 처리해야 할 부가기능 정의
  - 조인포인트 앞/뒤에서 실행되는 어드바이스
- @Before
  - 타겟의 메소드가 호출되기 이전 시점에 모두 처리해야 할 부가기능 정의
  - 조인포인트 앞에서 실행되는 어드바이스
- @After
  - 타겟의 메소드가 호출되기 이후 시점에 모두 처리해야 할 부가기능 정의
  - 조인포인트 뒤에서, 즉 메소드 실행 후, 메소드가 예외를 발생시키더라도 실행된다.
- @After Returning
  - 타겟의 메소드가 실행된 이후 시점에 모두 처리해야 할 부가기능 정의
  - 조인포인트 실행 종료된 이후 실행되는 어드바이스
- @After Throwning
  - 타겟의 메소드가 예외를 발생한 이후 시점에 모두 처리해야 할 부가기능 정의 
  - 예외가 던져질 때 실행되는 어드바이스

#### Spring AOP 특징

- [프록시 패턴](https://velog.io/@max9106/Spring-%ED%94%84%EB%A1%9D%EC%8B%9C-AOP-xwk5zy57ee) 기반의 AOP 구현체
  
  ![image](https://user-images.githubusercontent.com/52997401/223365874-9f205e18-3c97-4929-aa6a-519951bcec6d.png)
  
  - Target 객체에 대한 프록시를 만들어 제공
  
  - Target을 감싸는 프록시는 런타임 시 생성
  
  - 프록시는 어드바이스를 타겟 객체에 적용하면서 생성되는 객체

- 프록시가 Target 객체의 호출을 가로채 핵심 로직 호출 전/후 Advice 수행
  
  ![image](https://user-images.githubusercontent.com/52997401/223366151-6974f3ed-d12c-4206-addb-15fdb25c9346.png)

- 스프링 Bean에만 AOP 적용 가능

- 스프링은 메소드 조인 포인트만 지원하여, 메소드가 호출되는 런타임 시점에만 Advice 적용 가능

- 모든 AOP기능을 제공하지는 않으며 스프링 IoC와 연동하여 엔터프라이즈 애플리케이션의 각종 문제(중복 코드, 프록시 클래스 작성의 번거로움, 객체 간 관계 복잡도 증가)에 대한 해결책 지원 목적

> - [[Spring] 스프링 AOP (Spring AOP) 총정리 : 개념, 프록시 기반 AOP, @AOP](https://engkimbs.tistory.com/746)

> - [[Spring] AOP란?](https://velog.io/@max9106/Spring-AOP%EB%9E%80-93k5zjsm95)

> - [Spring AOP, Aspect 개념 특징, AOP 용어 정리](https://shlee0882.tistory.com/206)

### 스프링으로 작업 스케쥴링하기

스프링은 정기적으로 빈 메소드를 실행할 수 있는 스케쥴링 기능을 제공한다.

#### @Scheduled로 작업 스케쥴링하기

빈 컴포넌트의 특정 메소드에 @Scheduled 어노테이션을 추가하고, 스프링 부트 애플리케이션 클래스에 @EnableScheduling 어노테이션을 추가해 작업을 스케쥴링할 수 있다.

```java
@Component
public class Task {

    private static final Logger log = LoggerFactory.getLogger(Task.class);

    @Scheduled(fixedRate = 10000)
    //fixedDelay=10000
    //initialDelay=20000
    //cron="*/5 * * * * MON-FRI") //CRON EXPRESSION
    public void execute() {
        log.info("The time is now {}", new Date());
    }
}

@EnableScheduling
public class TaskSchedulingApplication implements CommandLineRunner{}
```

빈이 스프링 컨테이너에 의해 관리되면 @Scheduled(fixedRate = 10000)는 execute 메소드가 10000ms 마다 한 번씩 실행되도록 한다.

#### @Async를 사용해 비동기식으로 작업 실행하기

빈 컴포넌트의 특정 메소드에 @Async 어노테이션을 추가하고, 스프링 부트 애플리케이션 클래스에 @EnableAsync 어노테이션을 추가해 작업을 스케쥴링할 수 있다.

```java
@Component
public class AsyncTask {

    private Logger logger = LoggerFactory.getLogger(this.getClass());

    @Async
    void doThisAsynchronously() {
        IntStream.range(1, 100).forEach(x -> logger.info("AsyncTask {}",x));
    }

    @Async
    Future<Long> doThisAsynchronouslyAndReturnAValue() {
        IntStream.range(1, 100).forEach(x -> logger.info("AsyncTask With Return Value {}",x));        

        long sum = IntStream.range(1, 100).sum();

        return new AsyncResult<>(sum);
    }
}

@EnableAsync
public class TaskSchedulingApplication implements CommandLineRunner{}
```

#### 작업 실행자

스프링 프레임워크에서 사용되는 디폴트 작업 실행자는 SimpleAsyncTaskExecutor다.

## Spring MVC

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

### DAO와 DTO의 차이

- **DAO(Data Access Object)**
  
  - DB의 데이터를 조회하거나 조작하는 기능을 전담하도록 만든 객체를 말한다.
  
  - DB에 접근을 하기 위한 로직과 비즈니스 로직을 분리하기 위해서 사용

- **DTO(Data Transfer Object)**
  
  - 계층 간 데이터 교환을 위한 Bean을 말한다.
  
  - 여기서 말하는 계층은 Controller, View, Business Layer, Persistent Layer 이다.
  
  - 일반적인 DTO는 로직을 갖고 있지 않는 순수한 데이터 객체이며, 속성과 그 속성에 접근하기 위한 getter, setter 메소드만 가진 클래스이다.

- VO(Value Object)
  
  - DTO와 동일한 개념이지만 read only 속성을 가진다.

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
  - 개발자들이 각각 맡은 영역에만 집중할 수 있게 하여 개발의 효율성을 극대화

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

### 스프링 프론트 컨트롤러 패턴

디스패처 서블릿(Dispacher Servlet)이 web.xml에 설정되어 클라이언트로부터의 모든 요청을 받는다.  어떠한 요청이 들어왔을 때 적절한 Handler Method에 요청을 전달하고, 리턴한 결과값을 뷰에게 전달하여 알맞은 응답을 생성한 후 클라이언트에게 보낸다.

#### Spring MVC 애플리케이션 설정법

1. 스프링 MVC 의존 관계 추가
   1. spring-webmvc
2. web.xml에 디스패쳐 서블릿 추가
   1. 서블렛으로 디스패쳐 서블릿 및 url-pattern 으로 "/*"을 설정하여 모든 요청을 받을 수 있게 한다.
3. Spring Bean Configuration 파일(beans-web.xml) 설정
   1. default-servlet-handler 설정
      1. DispatcherServlet은 url pattern 을 "/" 와 같이 설정하게 되면서 tomcat 의 web.xml 에 정의되어 있는 url pattern "/" 을 무시하게 된다. 결국 DispatcherServlet url pattern 을 재정의하게 되어서 DefaultServlet 은 더 이상 동작할 수 없게 된 것이다. Spring에서는 이를 해결하기 위해서 <mvc:default servlet handler /> 설정을 지원한다.
   2. annotation driven 태그 설정
      1. <mvc:annotation-driven />
      2. Spring MVC에 필요한 Bean 들을 자동으로 등록해주는 태그
4. 스프링 컨텍스트 설정
   1. 컴포넌트 스캔으로 package를 scan하고 패키지 내 @Bean, @Controller, @RestController 애노테이션 등의 어노테이션을 확인하여 빈과 컨트롤러가 생성되고 오토와이어링 된다.

#### Spring MVC의 주요 구성 요소

- Dispatcher Servlet : 어떠한 요청이 들어왔을 때 적절한 Handler Method에 요청을 전달하고, 리턴한 결과값을 뷰에게 전달하여 알맞은 응답을 생성한 후 클라이언트에게 보낸다.
- HanderMapping : URL과 요청 정보를 기준으로 어떤 핸들러 메소드를 사용할 지 결정하는 객체이며, 디스패처 서블릿은 하나 이상의 핸들러 매핑을 가질 수 있다.
- Controller : 클라이언트의 요청을 처리한 뒤, Model을 호출하고 그 결과를 디스패처 서블릿에게 알려 줌.
- ModelAndView : 컨트롤러가 처리한 데이터 및 화면에 대한 정보를 보유한 객체
- View : 컨트롤러의 처리 결과 화면에 대한 정보를 보유한 객체
- ViewResolver : 컨트롤러가 리턴한 뷰 이름을 기반으로 컨트롤러 처리 결과를 생성할 뷰를 결정

#### 스프링 프론트 컨트롤러 패턴 실행 흐름

![image](https://user-images.githubusercontent.com/52997401/223123839-7c5a9e7d-78bd-4e3a-ab97-a8ebebb24a61.png)

1. 디스패처 서블릿이 클라이언트로부터 요청을 받는다.
2. 요청 URL를 기준으로 이를 처리할 핸들러 이름을 알기 위해 핸들러 맵핑과 통신한다.
3. 핸들러 맵핑은 요청 URL을 보고 핸들러 이름을 디스패처 서블릿에게 알려줍니다. 이때 핸들러를 실행하기 전/후에 처리할 것을 인터셉터로 만듭니다.
4. 디스패처 서블릿은 해당 핸들러 메소드에게 제어권을 넘겨주고, 이 핸들러는 응답에 필요한 모델과 뷰(ModelAndView)를 디스패처 서블릿에게 반환합니다.
5. 디스패처 서블릿은 받은 논리적 뷰 이름을 뷰 리졸버에게 전달해 응답에 필요한 물리적 뷰 이름을 만들라고 명령합니다.
6. 뷰 리졸버는 논리적 뷰 이름을 물리적 뷰 이름에 매핑한 후 반환한다.
7. 디스패처 서블릿은 해당 뷰를 실행하며, 해당 뷰에서 모델을 사용할 수 있게 한다.
8. 뷰는 원하는 응답을 생성해서 반환합니다.
9. 디스패처 서블릿은 응답을 클라이언트에게 전달합니다.

#### 컨트롤러를 위한 핵심 어노테이션

- @RequestMapping : HTTP 요청 URL을 처리할 컨트롤러 클래스 또는 메소드 정의. 메소드를 특정 요청 메소드(GET, POST 등)에 매핑할 수 있다.
- @RequestParam : HTTP 요청에 포함된 파라미터 참조 시 사용
- @ModelAttribute : HTTP 요청에 포함된 파라미터를 모델 객체로 바인딩
- @PathVariable : 파라미터를 URL 형식으로 받을 수 있게 해 줌

#### @ExceptionHandler 어노테이션의 사용

- 컨트롤러의 메서드에 ExceptionHandler 어노테이션을 설정하여 컨트롤러의 메서드에서 예외가 발생했을 때 예외 처리를 할 수 있음.
- 예외가 발생했을 때 예외 Type 과 Message 를 보여주는 JSP 페이지를 작성해야 함.

## REST

### RESTful 웹서비스

![image](https://user-images.githubusercontent.com/52997401/223404545-db53e548-1643-48b1-9be3-d6d90385a6ca.png)

- ROA(Resource Oriented Architecture) 개념을 실현하기 위한 리소스 중심의 표현, 전달, 접근 방식의 기술.
- REST(Representational State Transfer) 기반의 웹 서비스로서, HTTP의 기본 기능만으로 원격 정보에 접근 가능.
  - REST : HTTP URI + HTTP Method
    - HTTP URI를 통해 제어할 자원(Resource)을 명시하고, HTTP Method(GET, POST, PUT, DELETE)를 통해 해당 자원을 제어하는 명령을 내리는 방식의 아키텍쳐
- 서버와 클라이언트로만 분리되어 있다.
- 클라이언트에서 XML, JSON, 텍스트, 이미지 등 원하는 형식으로 표현 가능
  - 이러한 표현 형식은 HTTP의 accept 헤더 값이나 URI 파라미터로 지정

#### HTTP Method

[self_study/HTTP 메소드.md at main · carnival77/self_study · GitHub](https://github.com/carnival77/self_study/blob/main/Web/HTTP%20%EB%A9%94%EC%86%8C%EB%93%9C.md)

#### Spring MVC 기반 RESTful 웹서비스 구현 절차

1. RESTful 웹서비스를 처리할 RestfulController 클래스 작성 및 @RestController 어노테이션(@ResponseBody + @Controller) 선언하여 Bean으로 등록
2. 요청을 처리할 메서드에 @RequestMapping, @RequestBody, @ResponseBody 어노테이션 선언

#### RESTful Controller를 위한 핵심 어노테이션

- 스프링 MVC에서는 클라이언트에서 전송한 XML이나 JSON 데이터를 컨트롤러에서 자바 객체로 변환해서 수신할 수 있다.
  - @RequestBody : HTTP Request Body(요청 몸체)를 자바 객체로 전달 받을 수 있다.
- 자바 객체를 XML이나 JSON으로 변환해서 송신할 수 있다.
  - @ResponseBody : 자바 객체를 HTTP Request Body(응답 몸체)로 전송할 수 있다.

## SpringBoot

### 스프링 부트 장점

개발자는 마이크로서비스의 비즈니스 논리에 집중할 수 있다. 스프링 부트의 목표는 마이크로서비스 개발에 관련된 모든 기술적 세부사항을 관리하는 것이기 때문이다.

### 스프링 부트의 목표

- 기본 목표
  - 스프링 기반 프로젝트를 빠르게 구축할 수 있다.
  - 일반적인 설정이 기본으로 적용된다. 기본값과의 차이를 처리하는 설정 옵션은 제공한다.
  - 코드 생성과 많은 XML 설정의 사용을 피한다.
  - 다양한 비기능적 특징을 제공한다.
- 비기능적 특성
  - 광범위한 프레임워크, 서버와 스펙의 버젼 관리 및 설정에 관한 기본 처리
  - 애플리케이션 시큐리티를 위한 기본 옵션
  - 확장 옵션이 있는 기본 애플리케이션 매트릭스
  - 상태 체크로 기본 애플리케이션 모니터링
  - 외부 설정의 여러 옵션

### 스프링 프레임워크 기반 프로젝트 구축 vs 스프링부트 기반 프로젝트 구축

스프링 MVC로 애플리케이션을 구축하고 JPA(하이버네이트로 구현)를 사용해 데이터베이스에 연결한다고 가정하자.

**스프링 프레임워크 기반 프로젝트 구축 단계**

1. 사용할 스프링 MVC, JPA 및 하이버네이트 버젼을 결정한다.
2. 모든 다른 레이어를 연결하는 스프링 컨텍스트를 설정한다.
3. 스프링 MVC를 사용해 웹 레이어를 설정한다.
   1. DispatcherServlet, handler, resolvers, 뷰 리졸버 등의 빈 설정
4. 데이터 레이어에서 하이버네이트를 설정한다.
   1. SessionFactory, 데이터 소스 등의 빈 설정
5. 다양한 환경에 따라 애플리케이션 설정을 저장하는 방법을 정하고 구현한다.
6. 단위 테스트를 어떻게 할 것인지 결정한다.
7. 트랜잭션 관리 전략을 결정하고 구현한다.
8. 시큐리티를 구축하는 방법을 결정하고 구현한다.
9. 로깅 프레임워크를 설정한다.
10. 프로덕션 환경에서 애플리케이션을 모니터링 할 방법을 결정하고 구현한다.
11. 애플리케이션의 통계를 제공하기 위해 매트릭스 관리 시스템을 정하고 구현한다.
12. 웹 또는 애플리케이션 서버에 애플리케이션을 배포하는 방법을 결정하고 구현한다.

```
비즈니스 로직 구축을 시작하려면 위에 언급된 단계 중 최소 몇 가지는 완료해야 하며, 이것은 적어도 몇 주는 소요되는 작업이다.
```

**스프링부트 기반 프로젝트 구축**

1. pom.xml 파일에 spring-boot-starter-parent 구성
2. 요구되는 스타터 프로젝트(spring-boot starter web, spring-boot-starter-test 등)로 pom.xml 파일 구성
3. 애플리케이션을 실행할 수 있도록 spring-boot-maven-plugin 구성
4. 첫 번째 스프링 부트 launch 클래스 생성

또는, **스프링 이니셜라이저(http:/start/spring.io)** 사용

1. 빌드 도구(Maven 또는 Gradle)을 선택
2. 사용할 스프링 부트 버젼 선택
3. 컴포넌트의 그룹 ID와 아티팩트 ID 설정
4. 프로젝트에 원하는 스타터(의존 관계) 선택
5. 컴포넌트 패키지 방법 선택(JAR 또는 WAR)
6. 자바 버젼 선택
7. JVM 언어 선택

### 스프링부트 기반 프로젝트 구축 관련 주요 개념

#### spring-boot-starter-parent

- 스프링 부트 기반의 애플리케이션의 의존 관계 및 플러그인 관리를 제공하는 상위 POM이다.
- 사용할 자바 기본 버젼, 스프링 부트가 사용하는 의존 관계 기본 버젼, 메이븐 플러그인의 기본 설정이 포함된다.
- 스프링 버젼을 변경하면 다른 모든 의존 관계가 새 스프링 버젼과 호환되는 버젼으로 업그레이드된다. 개발자가 마주한 의존관계 간 호환성 이슈를 해결해준다.

#### 스타터 프로젝트

- 스타터는 여러 목적으로 사용자 정의가 단순화된 의존 관계 설명자다.
  - 스프링 부트 스타터 웹(spring-boot starter web)은 웹 애플리케이션을 구축하는 데 필요한 모든 프레임워크와 함께 제공된다. 스프링 및 스프링 MVC 프레임워크를 사용해 RESTful API를 포함한 웹 애플리케이션을 구축하는 데 사용된다.
    - 스프링 MVC
    - jackson-databind(바인딩용), hibernate-validator(폼 유효성 검사용)의 호환 가능 버젼
    - spring-boot-starter-tomcat(톰캣을 위한 스타터 프로젝트)
- spring-boot-starter-test
  - 단위 테스트에 필요한 테스트 프레임워크를 제공
    - JUnit : 기본 단위 테스트 프레임워크
    - 모키토 : 모킹용
    - 스프링 테스트 : 스프링 컨텍스트 기반 애플리케이션을 위한 단위 테스트 프레임워크

#### spring-boot-maven-plugin

- spring-boot-maven-plugin을 추가하면 스프링 부트 애플리케이션을 실행할 수 있다.
- 아래 두 개의 상황 모두를 위한 기능을 제공한다.
  - JAR 또는 WAR을 작성하지 않고 애플리케이션 실행
  - 나중에 배포할 수 있도록 JAR과 WAR을 빌드

#### 스프링 부트 launch 클래스 생성

- SpringApplication 클래스의 정적 run 메소드를 사용한다.
  
  ```java
  @SpringBootApplication
  public class Application {
    public static void main(String[] args) {
      ApplicationContext ctx = SpringApplication.run(Application.class, args);
    }
  }
  ```

- SpringApplication 클래스로 자바 main 메소드에서 스프링 애플리케이션을 다음과 같은 단계로 부트 스트랩하고 실행할 수 있다.
1. 스프링의 ApplicationContext 인스턴스를 생성한다.

2. 명령행 인수를 허용하고 스프링 속성으로 표시하는 기능을 활성화한다.

3. 설정에 따라 모든 스프링 빈을 로드한다.
- @SpringBootApplication 어노테이션은 세 가지 어노테이션의 바로가기다.
  - @Configuration : 스프링 애플리케이션 컨텍스트 구성 파일이라는 것을 나타낸다.
  - @EnableAutoConfiguration : 스프링 부트의 중요한 기능인 자동 설정을 활성화한다.
  - @ComponentScan : 클래스의 패키지와 모든 하위 패키지에서 스프링 빈을 스캔한다.

#### 스프링 부트 기반 애플리케이션 실행 시 특징

1. 톰캣 서버는 포트 8080에서 시작된다.
2. 디스패처 서블릿이 구성된다. 스프링 MVC 프레임워크가 요청을 수락할 준비가 되었음을 의미한다.
3. characterEncodingFilter, hiddenHttpMethodFilter, httpPutFormContentFilter, requestContextFilter 이 네 가지 필터가 기본적으로 사용된다.
4. 오류 페이지가 기본으로 설정된다.
5. WebJar가 자동 설정된다.
   1. 이것은 부트 스트랩, 쿼리와 같은 정적 의존 관계의 의존 관계 관리를 가능하게 한다.

**간단한 pom.xml 파일과 하나의 자바 클래스(Application.java)를 사용해 이 모든 기능이 포함된 스프링 MVC 애플리케이션을 시작할 수 있다.**

### 자동 설정

- 스프링 부트 프로젝트의 의존 관계에 맞게 빈을 자동으로 설정한다.
- spring-bootautoconfigure-{version}.jar에서 대부분이 제공된다.
- 모든 자동 설정 로직은 스프링 부트 애플리케이션이 시작될 때 실행된다.
- 특정 의존 관계나 스타터 프로젝트의 특정 클래스를 클래스 패스에서 사용할 수 있는 경우, 자동 설정 클래스가 실행된다. 자동 설정 클래스는 이미 빈이 구성돼 있는지 확인한다.
- 기존 빈에 기초해 기본 빈을 작성할 수 있다.

### 애플리케이션 구성 외부화

**application.properties**

구성 값이 선택되는 기본 파일이다. 스프링 부트는 클래스 패스 어디서나 application.properties 파일을 선택할 수 있다.

#### application.properties를 통한 프레임워크 사용자 정의

1. 로깅 구성
   1. 로깅 구성 파일의 위치
   2. 로그 파일의 위치
   3. 로깅 레벨
2. 임베디드 서버 구성 사용자 정의
   1. 서버 포트
   2. SSL 지원과 구성
   3. 접속 로그 구성
3. 스프링 MVC 설정
4. 스프링 스타터 시큐리티 구성
5. 데이터 소스, JDBC와 JPA 사용자 정의
6. 기타 구성 옵션
   1. 프로파일
   2. HTTP 메시지 변환기(JSON/Jackson)
   3. 트랜잭션 관리
   4. 국제화

#### 애플리케이션별로 사용자 정의 속성 정의하기

스프링 부트는 강력한 형식의 ConfigurationProperties 기능을 통해 애플리케이션 구성에 더 나은 접근 방식을 제공한다.

- 사전 정의된 빈 구조에 모든 특성을 보유한다.
- 빈은 모든 애플리케이션 속성의 중앙 저장소 역할을 한다.
- 구성 빈은 애플리케이션 구성이 필요한 모든 곳에 자동 연결될 수 있다.

구성 빈의 예시

```java
@Component
@ConfigurationProperties("application")
public class ApplicationConfiguration {

    private boolean enableSwitchForService1;
    private String service1Url;
    private int service1Timeout;

    public boolean isEnableSwitchForService1() {
        return enableSwitchForService1;
    }

    public void setEnableSwitchForService1(boolean enableSwitchForService1) {
        this.enableSwitchForService1 = enableSwitchForService1;
    }

    public String getService1Url() {
        return service1Url;
    }

    public void setService1Url(String service1Url) {
        this.service1Url = service1Url;
    }

    public int getService1Timeout() {
        return service1Timeout;
    }

    public void setService1Timeout(int service1Timeout) {
        this.service1Timeout = service1Timeout;
    }
}
```

- 주목해야 할 사항
  - @ConfigurationProperties("application") : 외부화된 구성의 어노테이션이다. 어노테이션을 모든 클래스에 추가해 외부 속성에 바인딩할 수 있다. "application"은 빈에 외부 구성을 바인딩하는 동안 접두사로 사용된다.
  - 빈에서 여러 구성 가능한 값을 정의한다.
  - 바인딩은 자바 빈 속성 설명자를 통해 발생하므로 getter와 seter가 필요하다.

application.properties을 이용해 애플리케이션별로 구성 가능하다.

```java
application.enableSwitchForService1=true
application.service1Url=http://abc-dev.service.com/somethingelse
application.service1Timeout=250
```

- 주목해야 할 사항
  - application : 접두사는 구성 빈을 정의하는 동안 @ConfigurationProperties("application")의 일부로 정의된다.
  - 값은 속성 이름에 접두사를 추가해 정의한다.

ApplicationConfiguration을 빈에 자동 연결해 다른 빈에서 구성 등록 정보를 사용할 수 있다.

```java
import com.mastering.spring.springboot.configuration.ApplicationConfiguration;

@Component
public class SomeOtherDataService {
    @Autowired
    private ApplicationConfiguration configuration;

    public String retrieveSomeData() {
        // Logic using the url and getting the data
        System.out.println(configuration.getService1Timeout());
        System.out.println(configuration.getService1Url());
        System.out.println(configuration.isEnableSwitchForService1());

        return "data from service";
    }
}
```

#### 다른 환경에 프로파일 생성하기

다른 환경에서 같은 속성에 다른 값을 갖게 하고자 한다.

프로파일을 사용하면 환경마다 다른 구성을 제공할 수 있다.

아래와 같이 액티브 프로파일을 구성한다.

```java
spring.profiles.active=dev
```

액티브 프로파일이 구성되면 appication-{profile-name}.properties에서 해당 프로파일에 고유한 특성을 정의할 수 있다.

```java
// application-dev.properties

application.enableSwitchForService1=true
application.service1Url=http://abc-dev.service.com/somethingelse
application.service1Timeout=250
```

액티브 프로파일이 dev이면 application-dev.properties 의 값이 application.properties 의 기본 구성을 대체한다.

##### 액티브 프로파일을 기반으로 동적 빈 구성하기

@Component나 @Configuration으로 표시된 모든 클래스는 추가로 @Profile 어노테이션을 표시해 빈이나 구성이 사용 가능한 프로파일을 지정할 수 있다.

예를 들어 애플리케이션마다 다른 환경에서 사용할 수 있는 다른 캐시가 필요하다. dev 환경에서는 매우 간단한 캐시를 사용하며, 프로덕션 환경에서는 분산 캐시를 사용하고자 한다. 프로파일을 사용해 구현할 수 있다.

```java
@Configuration
public class DevSpecificConfiguration {

    @Profile("dev")
    @Bean
    public String cache() {
        return "Dev Cache Configuration";
    }
}
```

```java
@Configuration
public class ProdSpecificConfiguration {

    @Profile("prod")
    @Bean
    public String cache() {
        return "Production Cache Configuration - Distributed Cache";
    }
}
```

구성된 액티브 프로파일에 따라 각 구성이 선택된다.

### YAML 구성

- YAML은 'YAML Ain't Markup Language'의 줄임말로 사람이 읽을 수 있는 구조화된 형식의 파일이며, 보통 설정 파일에 사용된다.
- 더 나은 속성 그룹화를 허용하므로 application.properties 보다 훨씬 읽기 쉽다.
- 단일 구성 파일에서 여러 프로파일의 구성을 할 수 있다는 장점이 있다.

### 임베디드 서버

#### 전통적인 자바 애플리케이션 배포 vs 임베디드 서버 활용 배포

**전통적인 자바 애플리케이션 배포**
자바 웹 애플리케이션을 사용해 WAR(Web Application Archive)나 EAR를 빌드해 웹 서버나 애플리케이션 서버, 그리고 자바가 설치된 서버에 배포한다.

순서 : 

1. APP.WAR
2. 톰캣
3. 자바
4. 리눅스 인스턴스

**임베디드 서버**
스프링 부트는 웹 서버가 애플리케이션 배포 가능한 JAR의 일부인 임베디드 서버 개념을 도입한다. 임베디드 서버를 사용해 애플리케이션을 배포하려면 서버에 자바가 설치되어 있어야 한다.

순서 : 

1. APP.JAR와 그 안의 임베디드 톰캣
2. 자바
3. 리눅스 인스턴스

스프링 부트로 모든 애플리케이션을 빌드할 때의 기본값은 JAR를 빌드하는 것이다.

해당 명령어는 다음과 같다.

```bash
mvn clean install
```

#### JAR대신 기존 WAR 파일 빌드

pom.xml의 패키지를 war로 변경한다.

```xml
<pachaging>war</pachaging>
```

톰캣 서버가 WAR 파일의 의존 관계로 포함되지 않도록 하고 싶다면 임베디드 서버의 의존 관계를 수정한다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-tomcat</artifactId>
  <scope>provided</scope>
</dependency>
```

이후 WAR로 WAS나 톰캣과 같은 웹 서버에 배포할 수 있다.

### 개발자 도구를 사용해 생산성 향상

스프링 부트 개발자 도구를 사용하려면 다음 의존 관계를 포함해야 한다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <optional>true</optional>
</dependency>
```

#### 주요 기능

- 뷰 템플릿 및 정적 파일 캐싱을 비활성화하는데, 이로써 변경 사항을 즉시 확인할 수 있다.
- 클래스 패스의 파일이 변경될 때 자동으로 애플리케이션이 다시 시작한다.
  - 컨트롤러나 서비스 클래스를 변경할 때
  - 속성 파일을 변경할 때

#### 장점

- 개발자는 매번 애플리케이션을 중지하고 재시작할 필요가 없다. 애플리케이션은 변경되는 즉시 자동으로 재시작된다.
- 이때 새롭게 개발된 클래스만 리로드한다. 이것은 애플리케이션의 콜드-스타트보다 훨씬 빠르다.

#### 브라우저에서 실시간 리로드 활성화

브라우저에 표시된 페이지나 서비스의 코드가 바뀌면 새로운 내용으로 자동 새로고침된다.

### 애플리케이션 모니터링에 스프링 부트 액추에이터 사용하기

#### 애플리케이션 모니터링

- 서비스가 다운되거나 느려지는 경우 즉시 알 수 있다.
- 서버에 충분한 여유 공간이나 메모리가 있는지 즉시 확인 가능하다.

스프링 부트 액추에이터를 사용하려면 다음 의존 관계를 포함해야 한다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

application.properties의 속성을 구성해 모든 액추에이터 URL을 활성화할 수 있다.

```java
management.endpoints.web.exposure.include=*
```

#### HAL 브라우저를 사용해 액추에이터 엔드포인트 찾기

액추에이터는 방대한 양의 데이터는 노출시키는 많은 엔드포인트를 노출시킨다.

정보를 더 잘 시각화하기 위해 애플리케이션에 HAL 브라우저를 추가한다.

```xml
<dependency>
  <groupId>org.springframework.data</groupId>
  <artifactId>spring-data-rest-hal-browser</artifactId>
</dependency>
```

스프링 부트 액추에이터는 스프링 부트 애플리케이션 및 환경에서 캡처된 모든 데이터에 REST API를 제공한다.

HAL 브라우저를 사용하면 스프링 부트 액추에이터 API를 시각적으로 표현할 수 있다.

#### 액추에이터로 확인 가능한 주요 사항

- 애플리케이션 구성 속성
  - configprops 엔드포인트는 애플리케이션 등록 정보를 통해 구성할 수 있는 구성 옵션의 정보를 제공한다.
- 환경 세부 정보
  - 환경(env) 엔드포인트는 운영체제, JVM 설치, 클래스 패스, 시스템 환경 변수, 다양한 애플리케이션 특성 파일에 구성된 값의 정보를 제공한다.
- 애플리케이션 상태 모니터링
  - 상태 서비스는 애플리케이션의 상태를 제공한다.
- 매핑 정보 얻기
  - 매핑 엔드포인트는 애플리케이션에 노출되는 여러 서비스 엔드포인트의 정보를 제공한다.
    - URI
    - 요청 메소드
    - 빈
    - 서비스를 노출시키는 컨트롤러 메소드
- 빈 구성으로 디버깅하기
  - 빈 엔드포인트는 스프링 컨텍스트에 로드된 빈의 세부 사항을 제공한다. 스프링 컨텍스트와 관련된 문제를 디버깅할 때 유용하다.
    - 빈의 이름 및 별명
    - 빈의 스코프
    - 빈의 종류
    - 빈이 작성되는 클래스의 정확한 위치
    - 빈의 의존 관계
- 중요한 매트릭스 탐색하기
  - 서버 : 프리 메모리, 프로세서, 가동 시간 등
  - JVM : 힙, 스레드, 가비지 컬렉션, 세션 등의 세부 정보
  - 애플리케이션 서비스에서 제공하는 응답
- 디버깅
  - /application/heapdump : 힙 덤프를 제공한다.
  - /application/httptrace : 애플리케이션에서 처리한 마지막 몇 가지 요청을 추적한다.
  - /application/threaddump : 스레드 덤프를 제공한다.

---

# Reference

> - [tech-interview](https://github.com/carnival77/tech-interview/blob/master/contents/spring.md#filter%EC%99%80-interceptor-%EC%B0%A8%EC%9D%B4)
> - [스프링 5 마스터 2/e](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=250634950)