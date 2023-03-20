# DDD

- [DDD](#ddd)
  - [Domain이란 ?](#domain이란-)
  - [DDD란? Domain Driven Design](#ddd란-domain-driven-design)
- [Reference](#reference)

## Domain이란 ?

1) 사전적 의미는 '영역', '집합'입니다.

2) DDD에서 말하는 Domain은 비즈니스 Domain입니다.

3) 비즈니스 Domain은 유사한 업무의 집합입니다.(MPRS-마케팅,구매,연구,영업)

4) 어플리케이션은 비즈니스 Domain별로 나누어 설계 및 개발 될 수 있습니다.

## DDD란? Domain Driven Design

1) 비즈니스 Domain별로 나누어 설계하는 방식입니다. 

   기존의 어플리케이션 설계가 비즈니스 Domain에 대한 이해가 부족한 상태에서 설계 및 개발되었다는 반성에서 출발하였습니다. DDD에서는 기존의 현업에서 IT로의 일방향 소통구조를 탈피하여 현업과 IT의 쌍방향 커뮤니케이션을 매우 중요하게 생각합니다.

2) DDD의 핵심 목표는 "Loosly coupling", "High cohesion"입니다.
  (어플리케이션 또는 그 안의 모듈간의 결합도는 최소화하고, 응집도는 최대화)
  - 결합도(Coupling)는 다른 모듈과의 의존성 정도
  - 응집도(Cohesion)는 모듈에 포함된 내부 요소들이 하나의 책임/목적을 위해 연결되어 있는 연관된 정도.

# Reference

> - [DDD 핵심만 빠르게 이해하기](https://happycloud-lee.tistory.com/94)