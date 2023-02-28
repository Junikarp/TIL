# Dependency Injection
* [강한 결합](#강한-결합)
* [느슨한 결합](#느슨한-결합)
* 의존성 주입(DI)은 어떻게 하는걸까?
   * [필드 주입(Field Injection)](#1-필드-주입--field-injection-)
   * [수정자 주입(Setter Injection)](#2-수정자-주입--setter-injection-)
   * [생성자 주입(Constructor Injection)](#3-생성자-주입--constructor-injection-)

### 강한 결합

이전에 있던 객체간의 의존성 설정은 A 클래스 내의 B 객체를 new 키워드를 사용하여 생성하거나, B 클래스에서 싱글톤 패턴을 이용해 자신의 객체를 생성해둔 것을 A 클래스 안에서 getInstatnce() 등의 메서드 등을 통해 생성하였다.
```java
class A {
    Object_B b;
    
    public A() {
        this.b = Object_B.getInstance();
    }
}
```
위와 같은 코드에서 Object_B 객체를 Object_B2 클래스의 인스턴스로 바꾸기 위해서는 아래와 같이 A 클래스를 직접 수정해야한다.
```java
class A {
    Object_B b;
    
    public A() {
        this.b = Object_B2.getInstance();
    }
}
```
이러한 구조는 객체 간 높은 결합도를 갖게하며, Spring 에서는 객체 간의 관계 설정을 클래스가 직접 하는 방식 대신, Spring Container 를 이용해 외부에서 객체를 생성하고, 객체를 주입하는 의존성 주입(DI) 방식을 사용하고 있다.

### 느슨한 결합

객체를 주입 받는다는 것은 외부에서 생성된 객체를 이넡페이스를 통해서 넘겨받는 것이다. 이를 통해 결합도를 낮출 수 있고. 런타임 시 의존관계가 결정되기 때문에 유연한 구조를 가진다.

### 의존성 주입(DI)은 어떻게 하는걸까?
의존성 주입을 하는 방법은 아래의 3가지 방법이 존재한다.
* 필드 주입(Field Injection)
* 수정자 주입(Setter Injection)
* 생성자 주입(Constructor Injection)

### 1. 필드 주입(Field Injection)
변수 선언부에 @Autowired Annotation 을 붙이는 방식으로 아래와 같은 순서로 이루어진다.
1. 주입받으려는 빈의 생성자를 호출하여 빈을 찾거나 빈 팩토리에 등록
2. 생성자 인자에 사용하는 빈을 찾거나 생성
3. 필드에 주입
```java
@Controller
public class A_Controller {
   
    @Autowired
    private A_Repository a_repository;
}
```
필드 주입 방식에는 아래와 같은 장점과 단점이 존재한다.
* 장점
   * 의존성을 주입하기가 쉽다. (@Autowired 선언 아래 무한으로 추가 가능)
* 단점
   * 의존 관계가 눈에 잘 보이지 않아 추상적이고, 이로 인해 의존성 관계가 과도하게 복잡해 질 수 있다.
   * 생성자 주입 방식과 다르게 final 을 선언할 수 없으므로, 객체가 변할 수 있다.
   * SRP(단일 책임 원칙)에 반하는 안티 패턴이다.
   * DI Container 와의 강한 결합으로 단위테스트 시 의존성 주입이 용이하지 않다.

### 2. 수정자 주입(Setter Injection)
setter 메서드에 @Autowired annotation 을 선언하여 주입받는 방식으로 아래와 같은 순서로 이루어진다.
1. 주입받으려는 빈의 생성자를 호출하여 빈을 찾거나 빈 팩토리에 등록
2. 생성자 인자에 사용하는 빈을 찾거나 생성
3. 주입하려는 빈 객체의 수정자를 호출하여 주입
```java
@Controller
public class A_Controller {
    
    private A_Repository a_repository;
    
    @Autowired
    public void setA_repository(A_Repository a_repository) {
        this.a_repository = a_repository;
    }
}
```
수정자 주입 방식에는 아래와 같은 장점과 단점이 존재한다.
* 장점
   * 의존성이 선택적으로 필요한 경우 유용하다.
   * 생성자에 모든 의존성을 기술하면 과도하게 복잡해질 수 있는 것을 선택적으로 나눠 주입 할 수 있도록 부담을 덜어준다.
* 단점
   * 의존성 주입 대상 필드가 final 선언 불가하다.

### 3. 생성자 주입(Constructor Injection)
생성자 주입은 생성자에 의존성 주입을 받고자 하는 field 를 나열하는 방법으로 아래와 같은 순서로 이루어진다.
1. 생성자의 인자에 사용되는 빈을 찾거나 빈 팩토리에서 생성
2. 찾은 인자 빈으로 주입하려는 생성자를 호출
```java
@controller
public class A_controller {
    
    private final A_Repository a_Repository;
    
    @Autowired
    public A_controller(A_Repository a_repository){
        this.a_Repository = a_Repository;
    }
}
```
생성자 주입 방식에는 아래와 같은 장점과 단점이 존재한다.
* 장점
   * 필수적으로 사용해야하는 의존성 없이는 Instance 를 만들지 못하도록 강제할 수 있다.
   * Spring 4.3 부터는 Class 를 완벽하게 DI Framework 로부터 분리할 수 있다.
   * 단일 생성자에 한해 @Autowired 를 붙이지 않아도 된다.
      * 생성자가 하나이고 그 생성자로 주입받을 객체가 Bean 으로 등록되어 있다면 @Autowired 생략 가능
   * null 을 주입하지 않는 한 NullPointerException 이 발생하지 않는다.
   * final 을 사용할 수 있다.
      * final 의 장점은 객체가 불변하도록 만든다는 점으로, 누군가가 Controller 내부에서 Service 객체를 바꿔치는 것을 막는다.
   * 순환 의존성을 알 수 있다.
* 단점
   * 어쩔 수 없는 순환 참조는 생성자 주입으로 해결하기 어렵다.
      * 이 경우 나머지 주입 방법을 사용하도록 한다. (순환 참조가 발생하지 않도록 하는 것이 가장 중요)  




참조
* [의존성 주입 3가지 방법, @Autowired 란?](https://hyewon-study-log.tistory.com/169#:~:text=%EB%8C%80%ED%91%9C%EC%A0%81%EC%9C%BC%EB%A1%9C%20%EC%83%9D%EC%84%B1%EC%9E%90%20%EC%A3%BC%EC%9E%85%2C%20setter,%EC%9D%B4%EB%A0%87%EA%B2%8C%203%EA%B0%80%EC%A7%80%EA%B0%80%20%EC%9E%88%EC%8A%B5%EB%8B%88%EB%8B%A4.)
* [DI, IoC 그리고 의존성 주입(DI)의 3가지 방법](https://nect2r.tistory.com/58)
* [DI(Dependency Injection), 3가지 방법](https://velog.io/@gillog/Spring-DIDependency-Injection-%EC%84%B8-%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95)
