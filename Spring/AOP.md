- [1. AOP의 개요와 용어](#1-aop의-개요와-용어)
  - [1.1. 핵심 기능과 부가 기능](#11-핵심-기능과-부가-기능)
  - [1.2. AOP(Aspect Oriented Programming)의 개요](#12-aopaspect-oriented-programming의-개요)
    - [1.2.1. 애스펙트 (Aspect)](#121-애스펙트-aspect)
    - [1.2.2. AOP 용어](#122-aop-용어)
- [2. Spring AOP의 특징](#2-spring-aop의-특징)
  - [2.1. Spring 은 프록시 (Proxy) 기반 AOP 를 지원한다.](#21-spring-은-프록시-proxy-기반-aop-를-지원한다)
  - [2.2. 프록시가 호출을 가로챈다(Intercept)](#22-프록시가-호출을-가로챈다intercept)
  - [2.3. Spring AOP 는 메서드 조인 포인트만 지원한다.](#23-spring-aop-는-메서드-조인-포인트만-지원한다)
- [3. Spring AOP 의 구현](#3-spring-aop-의-구현)
    - [3.0.1. Spring AOP 의 구현 방식](#301-spring-aop-의-구현-방식)
    - [3.0.2. Spring AOP 의 구현(XML)](#302-spring-aop-의-구현xml)
- [4. PointCut 표현식](#4-pointcut-표현식)
  - [4.1. PointCut 표현식 문법](#41-pointcut-표현식-문법)
  - [4.2. PointCut 표현식 예시](#42-pointcut-표현식-예시)
- [5. Spring AOP 의 구현 (Annotation)](#5-spring-aop-의-구현-annotation)
  - [5.1. @Aspect 어노테이션](#51-aspect-어노테이션)
    - [Aspect 클래스 정보](#aspect-클래스-정보)
    - [Advice를 정의하는 어노테이션](#advice를-정의하는-어노테이션)

## 1. AOP의 개요와 용어

### 1.1. 핵심 기능과 부가 기능
- 핵심 기능(Core Concerns) : 업무(Biz) 로직을 포함하는 기능
- 부가기능(Cross cutting Concerns) : 핵심기능을 도와주는 부가적인 기능(로깅, 보안 등)
- 객체지향의 기본 원칙을 적용하여도 핵심기능에서 부가기능을 분리해서 모듈화하는 것은 매우 어렵다.

### 1.2. AOP(Aspect Oriented Programming)의 개요
AOP는 애플리케이션에서의 **관심사의 분리 기능의 분리** 즉, 핵심적인 기능에서 부가적인 기능을 분리한다.
분리한 부가 기능을 애스펙트(Aspect)라는 독특한 모듈 형태로 만들어서 설계하고 개발하는 방법이다.

OOP를 적용하여도 핵심기능에서 부가기능을 쉽게 분리된 모듈로 작성하기 어려운 문제점을 AOP가 해결해 준다고 볼 수 있다.

AOP는 부가기능을 애스펙트로 정의하여, 핵심기능에서 부가기능을 분리함으로써 핵심기능을 설계하고 구현할 때 객체지향적인 가치를 지킬 수 있도록 도와주는 개념이다.

#### 1.2.1. 애스펙트 (Aspect)
애스펙트는 부가기능을 정의한 코드인 어드바이스(Advice)와 어드바이스를 어디에 적용하지를 결정하는 포인트컷(PointCut)을 합친 개념이다.

`Advice + PointCut = Aspect`

- AOP 개념을 적용하면 핵심기능 코드 사이에 침투된 부가기능을 독립적인 애스펙트로 구분해 낼 수 있다 .
- 구분된 부가기능 애스펙트를 런타임 시에 필요한 위치에 동적으로 참여하게할 수 있다.

#### 1.2.2. AOP 용어
- 타겟(Target) : 핵심 기능을 담고 있는 모듈로, 부가 기능을 부여할 대상이다.
- 어드바이스(Advice) : 타겟에 제공할 부가 기능을 담고 있는 모듈이다.
- 조인 포인트(Join Point) : 어드바이스가 적용될 수 있는 위치이다. 즉, 타겟 객체가 구현한 인터페이스의 모든 메서드는 조인 포인트가 된다.
- 포인트컷(Pointcut) : 어드바이스를 적용할 타겟의 메서드를 선별하는 정규표현식이다. 포인트컷 표현식은 execution으로 시작하고, 메서드의 Signature를 비교하는 방법을 주로 이용한다.
- 애스펙트(Aspect) : AOP의 기본 모듈이다. 싱글톤 형태로 객체로 존재하며, 어드바이스 + 포인트컷이다.
- 어드바이저(Advisor) : 어드바이스 + 포인트컷
- 위빙(Weaving) : 위빙은 포인트컷에 의해서 결정된 타겟의 조인 포인트에 부가기능 어드바이스를 삽입하는 과정을 뜻한다.
위빙은 AOP가 핵심기능 타겟의 코드에 영향을 주지 않으면서 필요한 부가기능(어드바이스)을 추가할 수 있도록 해주는 핵심적인 처리과정이다.

    ![image](https://user-images.githubusercontent.com/52997401/166419831-e4f65d10-8957-452e-8d9c-0e194c448f4c.png)

## 2. Spring AOP의 특징

### 2.1. Spring 은 프록시 (Proxy) 기반 AOP 를 지원한다.
- Spring은 타겟 (target) 객체에 대한 프록시를 만들어 제공한다
- 타겟을감싸는 프록시는 실행시간 (런타임) 에 생성된다
- 프록시는 어드바이스를 타겟 객체에 적용하면서 생성되는 객체이다.
    ![image](https://user-images.githubusercontent.com/52997401/166420247-8a2970f3-966e-4a3b-b28e-afd8611f1dad.png)

### 2.2. 프록시가 호출을 가로챈다(Intercept)
- 프록시는 타겟 객체에 대한 호출을 가로챈 다음 어드바이스의 부가기능 로직을 수행하고 난 후에 타겟의 핵심기능 로직을 호출한다.(전처리 어드바이스)
- 또는 타겟의 핵심기능 로직 메서드를 호출한 후에 부가 기능(어드바이스)을 수행하는 경우도 있다(후처리 어드바이스)
    ![image](https://user-images.githubusercontent.com/52997401/166420612-fcf30e5c-bc85-4764-a217-82f94b01a602.png)

### 2.3. Spring AOP 는 메서드 조인 포인트만 지원한다.
- Spring은 동적 프록시를 기반으로 AOP 를 구현하므로 메서드 조인 포인트만 지원한다. 즉 핵심기능 타겟의 메서드가 호출되는 런타임 시점에만 부가기능(어드바이스)을 적용할 수 있다 .
- 반면에 AspectJ 같은 고급 AOP 프레임워크 를 사용하면 객체의 생성 , 필드값의 조회와 조작 , static 메서드 호출 및 초기화 등의 다양한 작업에 부가기능을 적용할 수 있다.

## 3. Spring AOP 의 구현

#### 3.0.1. Spring AOP 의 구현 방식

1. XML 기반의 POJO 클래스를 이용한 AOP 구현
   1. 부가기능을 제공하는 Advice 클래스를 작성한다
   2. XML 설정 파일에 ```<aop:config>``` 를 이용해서 애스펙트를 설정한다 .(즉 , 어드바이스와 포인트컷을 설정함 )
2. @Aspect 어노테이션을 이용한 AOP 구현
   1. @Aspect 어노테이션을 이용해서 부가기능을 제공하는 Aspect 클래스를 작성한다. 이때 Aspect 클래스는 어드바이스를 구현하는 메서드와 포인트컷을 포함한다
   2. XML 설정 파일에 ```<aop:aspectj autoproxy/>>``` 를 설정한다.

#### 3.0.2. Spring AOP 의 구현(XML)
1. Advice의 종류
   1. Around 어드바이스
      1.  타겟의 메서드가 호출되기 이전 (before) 시점과 이후 (after) 시점에 모두 처리해야 할 필요가 있는 부가기능을 정의한다
      2. Joinpoint 앞과 뒤에서 실행되는 Advice
   2. Before 어드바이스
      1.  타겟의 메서드가 실행되기 이전 (before) 시점에 처리해야 할 필요가 있는 부가기능을 정의한다
      2. Joinpoint 앞에서 실행되는 Advice
   3.  AfterReturning 어드바이스
       1.  타겟의 메서드가 정상적으로 실행된 이후 (after) 시점에 처리해야 할 필요가 있는 부가기능을 정의한다
       2.  Jointpoint 메서드 호출이 정상적으로 종료된 뒤에 실행되는 Advice
   4. AfterThrowing 어드바이스
      1.  타겟의 메서드가 예외를 발생된 이후 (after) 시점에 처리해야 할 필요가 있는 부가기능을 정의한다
      2.  예외가 던져질 때 실행되는 Advice
2.  Advice를 정의하는 태그
   ![image](https://user-images.githubusercontent.com/52997401/166421765-0bf006d1-3629-47e8-a4c5-d157ac600eac.png)
3. Advice 클래스 작성
    ![image](https://user-images.githubusercontent.com/52997401/166421947-2cfdc05e-7060-44c0-9622-cc50297fc31b.png)
4. JoinPoint 인터페이스
    ![image](https://user-images.githubusercontent.com/52997401/166422193-4c8d5bff-2747-4460-a639-207c2d09c694.png)
5. AOP 설정에 대한 설명
    ![image](https://user-images.githubusercontent.com/52997401/166422325-0e23bba8-176e-40a9-b410-e186e2083e3d.png)

## 4. PointCut 표현식
### 4.1. PointCut 표현식 문법
![image](https://user-images.githubusercontent.com/52997401/166422479-65ba9c87-9c4a-4981-ac83-2b64ceb62273.png)
### 4.2. PointCut 표현식 예시
![image](https://user-images.githubusercontent.com/52997401/166422634-0afeb60c-d4f2-43bd-81b2-a3765cd6b114.png)
![image](https://user-images.githubusercontent.com/52997401/166422820-98e8f354-ab8b-4ea4-93ca-a13d6bbfa8fc.png)
![image](https://user-images.githubusercontent.com/52997401/166422862-44d89227-af21-4ced-88d0-8b78ed150ea7.png)

## 5. Spring AOP 의 구현 (Annotation)
### 5.1. @Aspect 어노테이션
- Aspect 클래스 선언할 때 @Aspect 어노테이션을 사용한다
- AspectJ5 버전에 새롭게 추가된 어노테이션이다
- @Aspect어노테이션을 이용할 경우 XML 설정 파일에 어드바이스와 포인트컷을 설정하는 것이 아니라 클래스 내부에 정의할 수 있다
- ```<aop:aspectj autoproxy >``` 태그를 설정파일에 추가하면 Aspect 어노테이션이 적용된 Bean 을 Aspect 로 사용 가능하다.
#### Aspect 클래스 정보
![image](https://user-images.githubusercontent.com/52997401/166423233-4485e3b4-8ca4-4679-9618-b9b86e771d2d.png)
#### Advice를 정의하는 어노테이션
![image](https://user-images.githubusercontent.com/52997401/166423424-f971ef5f-9a7d-4571-8a34-2e841c5ff2c5.png)
![image](https://user-images.githubusercontent.com/52997401/166423489-0e16bf26-5b8f-4c8e-804e-fe3bfe7c5586.png)
