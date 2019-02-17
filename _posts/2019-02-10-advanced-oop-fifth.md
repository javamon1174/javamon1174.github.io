---
title: "[Advanced OOP] 다섯번째, 고급 객체지향 프로그래밍 정리"
excerpt: "(5)고급 객체지향 프로그래밍 용어 정리"
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
# 다섯번째, 책 고급 프로그래밍 요점 및 정의 정리

## 객체지향 예외 처리(Exception Handling)

### 예외 처리
    - 예외는 프로그램 기능을 수행하는 도중 발생할 수 있는 비정상적인 상황을 의미한다.
    - 프로그램에서는 일반적으로 3가지 흐름이 있으며, 1)일반적인 흐름 2)대체 흐름 3)에러 흐름으로 나뉜다.
    - 일반적인 흐름 : 가장 보편적인 흐름이며, 프로그램을 정상 종료를 위한 흐름이다.
    - 대체 흐름 : 정상 종료를 위한 흐름이지만, 일반적인 흐름과는 다른 방법의 흐름이다.
    - 에러 흐름 : 사용자가 의도했던 결과값을 전달하지 못하고 의도치 않게 프로그램이 종료되는 흐름이다.
    - 예외 상황을 잘 처리하면 대체 흐름으로 진행되며, 에러 흐름과 대체흐름을 혼돈하여서는 안된다.
    
### 예외 vs 에러
    - 프로그램이 런타임에 실행되는 도중 발생할 수 있는 문제를 에러라고 한다.
    - 예외는 정확히 예외 이벤트로, 비정상 종료가 날 수 있는 에러 흐름을 발생시키는 이벤트를 의미한다.
    - 예외는 비정상으로 프로그램이 종료될 수 잇지만 개발자에 의해 정상 흐름으로 되돌아 갈 수 있는 이벤트지만, 에러는 런타임에 발생하여 비정상으로 종료될 수 있는 문제이다.
    
    
### cpp에서 사용자 정의 예외 타입을 사용한 예제
```cpp
// exception 클래스를 상속받으면서 what() 메소드를 오버라이딩하여 에러 메세지를 정의한 예제이다.
class UserDefinedException: public exception {

public:
    UserDefinedException() {}
    const char* what() const throw() {
        return "Throw User Defined Exception!!"
    }
}
```

### 예외를 처리하는 방법
    - try...catch 블록을 이용하여 발생한 메소드 내에서 예외 처리
    - throws를 이용하여 예외가 발생한 메소드를 호출한 쪽에서 예외 처리

```cpp 
// cpp에서 try...catch 블록을 이용한 예외 처리 
    
    // 메소드 내에 위치하는 예외블록
    try {
    // 예외가 발생할 수 있음
    string year = birthDay.substr(0, 4);
    string month = birthDay.substr(4, 4);
    string day = birthDay.substr(2, 4);

    } catch(out_of_range e) {
        cout << "the birthday is invalid" << endl;
    }
```

```java
// java에서 throws를 이용한 예제

public class DivisionCalculator {
    private int result;
    
    // ArithmeticException이 발생할 수 있지만, 이를 여기서 처리하지 않고
        이 메소드를 호출한 곳에서 Exception을 처리하게 함.
        
    public int divideNumber(int numerator, int denominator) throws
        ArithmeticException {
            return result = numerator / denominator;
        }
}
```

### 예외를 발생시키는 법
    1. 운영체제나 자바 가성머신이 직접 발생키는 상황 외에 다른 경우에 예외를 발생시키고자 할 때
    2. 사용자 정의 외예 타입을 발생시키려고 할 때
    java) throw new [예외 타입];
    cpp) throw [예외 타입];

여기서 중요한 점은 throw와 throws 키워드를 혼돈하면 안된다. 둘은 스펠링은 유사하지만 의미와 활용도는 확연한 차이가 있다.<br/>
throw는 프로그램 내에서 임의로 예외를 발생시킬 때 사용하지만, throws는 발생한 예외에 대한 처리를 해당 메소드를 호출한 쪽으로 위임하는 역할을 한다.<br/>
즉, 하나는 예외를 발생시키는 키워드 이며, 다른 하나는 발생한 예외를 처리하는 키워드이다.<br/>


### 예외 관련 링크
#### [Exception Handling](https://neil.fraser.name/writing/exception/)
#### [Checked/UnChecked Exception](https://close852.tistory.com/47)

## 리플렉션(Reflection)
    - 전산학에서의 리플렉션은 컴파일된 프로그램의 구조를 런타임에 확인하고 조작하는 기법을 의미한다.
    
### 리플렉션에 관련된 내용은 "고급 객체지향 프로그래밍" 에서 확인하시길 바랍니다.