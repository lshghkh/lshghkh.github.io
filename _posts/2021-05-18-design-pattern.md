---
layout: post
title: 디자인 패턴
subtitle: 주요 디자인 패턴
tags: [OOP, Design Pattern, SE]
comments: true
---

###### 목차


---

## 디자인 패턴

소프트웨어 공학에서 소프트웨어 디자인 패턴이란 소프트웨어를 디자일할 때 자주 발생할 수 있는 문제들에 대한 일반적이고 재사용 가능한 해결방법이다. 디자인 패턴은 완벽히 구체화된 설계도가 아니다. 즉, 그 즉시 소스코드로 바로 작성될 수 있는 것이 아니다. 디자인 패턴은 애플리케이션이나 시스템을 설계할 때 발생할 수 있는 일반적인 문제에 대해 사용할 수 있는 공식화되어 있는 모범 예시에 가깝다. 디자인 패턴들은 생성, 구조, 행동, 동시실행 패턴으로 크게 4가지로 분류할 수 있다. 이 포스트에서는 대표적인 생성, 구조, 행동 패턴에 대해서 서술하고자 한다.

---

## 생성 패턴 (Creational patterns)

1. 싱글톤 패턴 Singleton pattern
클래스에 인스턴스가 하나만 있도록 하고, 이에 대한 글로벌 액세스 지점을 제공한다.

1. 팩토리-메서드 패턴 Factory Method pattern
단일 개체를 만들기 위한 인터페이스를 정의하되, 인스턴스화는 해당 클래스의 하위 클래스에서 결정하도록 한다. 이 패턴을 사용하면 클래스가 인스턴스화를 하위 클래스에게 전담시킬 수 있다.

1. 추상 팩토리 패턴 Abstract Factory pattern
구체적인 클래스를 지정하지 않고, 관련된 객체나 종속 객체를 생성할 수 있는 인터페이스를 제공한다.

---

## 구조 패턴 (Structural patterns)

1. 어댑터 패턴 Adapter(Wrapper) pattern
외부 클래스의 인터페이스를 클라이언트가 기대하는 형태의 다른 인터페이스로 변환한다. 어댑터는 호환되지 않는 인터페이스를 위한 징검다리 역할을 하여, 기존의 클래스와 함께 작동하도록 한다.

1. 프록시 패턴 Proxy pattern
다른 객체에 대한 엑세스를 제어할 대리자 혹은 place holder를 제공한다. 

1. 퍼사드 패턴 Facade pattern


1. 데코레이터 패턴 Decorator pattern


1. 컴포짓 패턴 Composite pattern


---

## 행동 패턴 (Behavioural patterns)

1. 전략 패턴 Strategy pattern


1. 상태 패턴 State pattern


1. 커맨드 패턴 Command pattern


1. 템플릿 메서드 패턴 Template Method pattern


1. 중재자 패턴 Mediator pattern



---

## 참고자료
- [Wikipedia: Software design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)
- 
