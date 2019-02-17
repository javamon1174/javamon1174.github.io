---
title: "[Advanced OOP] 네번째, 고급 객체지향 프로그래밍 정리"
excerpt: "(4)고급 객체지향 프로그래밍 용어 정리"
date: 2019-02-11
categories:
  - oop
  - book
tags:
  - 객체지향
  - OOP
  - 고급
  - 프로그래밍
  - 용어
  - 정리
  - 객체
  - 다형성
  - 캡슐화
  - 상속
  - 추상클래스
  - 인터페이스
  - 예외처리
  - 고급 객체지향 프로그래밍
---
# 네번째, 책 고급 프로그래밍 요점 및 정의 정리

## 인터페이스(Interface)

### 일반적인 인터페이스
두 개의 서로 다른 요소들이 서로 상호작용하기 위해 한 요소에서 제공되는 기능을 명세한 것을 인터페이스라 한다.

> 대표적으로 USB 포트이며, 컴퓨터에 외부기기를 연결하는 인터페이스로 활용된다.

#### 소프트웨어 인터페이스
    - 그래픽 사용자 인터페이스(Graphic User Interfacem GUI) : 사용자가 GUI를 통해 컴퓨터의 특정 기능을 실행 시킬 수 있다.
    - API(Application Programming Interface) : 한 컴포넌트가 제공할 수 있는 기능을 명세한 것이다.
    
### 객체지향에서의 인터페이스
    - 서로 다른 클래스들(상속 구조를 갖지 않는)이 상호작용하기 위해 외부로 노출되어 다른 클래스에게 제공 될 수 있는 기능을 명세한 것이 인터페이스다.
    - 객체지향 패러다임에서는 공통 기능을 나타내는 매소드에 대한 구현 없이, 시그니처만 정의하여 구성한 클래스를 인터페이스라 한다.
    - 즉, 인터페이스만 보면 해당 클래스가 어떤 기능을 제공하는지를 알 수 있다.
    - 인터페이스는 '명세 수준의 공통성'으로만 구성 된다.

#### 기능 공통성 수준과 인터페이스

![interface](/images/interface.png){: .align-center}

#### 인터페이스를 포함한 상속구조 예제

![structure](/images/interface-structure.png){: .align-center}

    - '수업보조' 클래스는 '조교'의 서브클래스이지만, '임시'라는 인터페이스를 구현하여 일시적으로 임금을 받는 대학원생을 나타낸다.
    - '방문수업' 클래스는 '교수'의 서브클래스이지만, '임시'라는 인터페이스를 통해 일시적으로 학교에 고용된 교수를 나타낸다.
    - '수업보조'와 '방문수업' 클래스들을 이용하여 임금을 지불하는 기능을 구현하려고 할 때, computeTotalPay()에 대한 
       세부 내용을 알 필요 없이 '임시' 인터페이스에서 선언된 메소드만 호출하면 된다.
    - '임시' 인터페이스를 구현한 모든 클래스의 computeTotalPay() 메소드를 호출할 수 있게 된다.
    
> 인터페이스는 서로 유사성이 없는 클래스들 간의 공통 기능성을 명세하기 위해 주로 사용된다.


### 추상클래스와의 차이점
    - 상속 관계 적용 유무
    
    - 구현된 메소드 제공 유무
    인터페이스는 일반 메소드를 가질 수 없다.
    
    - 변수 정의 가능성 유무
    인터페이스는 속성을 가질 수 없으며, 오직 상수만 정의할 수 있다.
    
    - 다중 상속 가능성 유무
    java에서는 클래스 다중 상속을 지원하지 않지만, 인터페이스 활용하여 다중 상속을 지원한다.
    

### 인터페이스 장점
    - 관련 없는 클래스 간의 유사성 표현 가능
    인터페이스는 관련이 없는 클래스간 유사한 기능성 명세를 기술할 수 있는 유용한 장치이다.
    
    - 메소드 표준화 가능
    인터페이스의 정의된 메소드는 추상 메소드이므로, 인터페이스를 구현한 클래스는 모두 같은 메소드 시그니쳐를 가진 메소드를 구현해야 한다.
    
    - 메소드 선언과 구현 분리
    이 특징은 객체지향 패러다임, CBD, SOA로 재사용 패러다임이 발전함으로써 보다 광범위 하게 활용되고 있다.
    

## 제네릭 클래스(Generic Class)
유사성이 높은 오퍼레이션 집합을 가지지만 속성의 데이터 타입의 다양한 객체들을 위한 클래스

### 제네릭 클래스 활용
    1. 제네릭 클래스 정의
    데이터 타입이 정해지지 않은 일부 속성들과 이와 연관된 오퍼레이션들을 정의한다.
    => 파라미터를 통해 어떤 종류의 데이터 타입으로 지정할 지 결정한다.
    
    2. 특정 데이터 타입에 의존적인 알고리즘을 구현하지 않는다.
    
    3. 특정 타입의 클래스 생성
    특정 타입 클래스가 선언되면 지정된 데이터 타입만을 지원 할 수 있고, 지정된 타입과 다른 데이터 타입이 사용되는 경우 오류가 발생한다.
    
    4. 객체 생성
    
    
### 제네릭 클래스 장점
    1. 데이터 타입에 따른 별도의 구현이 필요없이 재사용이 가능하다.
    2. 컴파일 시점에 데이터 타입 검사를 통해 속성의 타입 안전성을 보장한다.
    

### cpp 제네릭 클래스 장치

```cpp
// cpp 에서 'template' 키워드 사용 예
// T는 타입을 의미한다.
template <class T>

T max(T x, T y)
{
    return x < y ? y : x;
}
```

> vector, map과 같은 자료 구조는 int, string 등 데이터 타입에 상관없이 동일한 로직이 적용 될 수 있기에,
일반적으로 자료 구조를 정의 할 때 제네릭 클래스를 많이 활용한다.


### 제네릭 클래스의 활용
    - 자료 구조의 구현
    - 데이터 타입과 관련없는 공통 기능 구현
    

> 제네릭 클래스에 대해서는 다른 포스트에서 더 상세히 다룰 예정입니다.