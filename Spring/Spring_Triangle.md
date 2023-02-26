## 스프링 트라이앵글 (Spring Triangle)
> 1. IoC (Inversion of Control) : 제어의 역전
>   * [IoC (Inversion of Control) 이란](#ioc-inversion-of-control-이란)
>   * [DI (Dependency injection) 이란](#di-dependency-injection-이란)
> 2. AOP (Aspect Oriented Programming) : 관점 지향 프로그래밍
>    * [AOP (Aspect Oriented Programming) 이란](#aop-aspect-oriented-programming-이란)
>    * [AOP 의 주요 개념](#aop-의-주요-개념)
>    * [Spring AOP 의 특징](#spring-aop-의-특징)
> 3. PSA (Portable Service Abstraction) : 일관성 있는 서비스 추상화
>    * [PSA (Portable Service Abstraction) 이란](#psa-portable-service-abstraction-이란)

### 1. IOC (Inversion of Control) : 제어의 역전
#### **IoC (Inversion of Control) 이란**
* 메소드나 객체의 호출작업을 개발자가 결정하는 것이 아닌, 외부에서 결정되는 것을 의미
* 제어의 흐름을 사용자가 컨트롤하지 않고, Spring 에게 맡겨 작업을 처리

#### **DI (Dependency injection) 이란**
* Spring 이 제공하는 의존 관계 주입 기능
   * 주입이란, 외부로부터 객체의 주소값을 전달 받아 객체가 참조되어지는 방식
   * Spring 에서는 객체를 Bean 이라고 부르며, 프로젝트가 실행될 때 객체의 생성과 소멸과 관련된 작업을 자동으로 수행하며 객체가 생성되는 곳을 Bean 컨테이너라고 부름  
* 객체를 직접 생성하지 않고, 외부에서 생성한 후 주입 시켜주는 방식
* DI를 통해 모듈 간의 결합도를 낮추고 유연성을 높일 수 있음

### 2. AOP (Aspect Oriented Programming) : 관점 지향 프로그래밍 
#### **AOP (Aspect Oriented Programming) 이란**
* 소스 코드 상에서 다른 부분에 반복적으로 쓰는 코드들을 흩어진 관심사 (Crosscutting Concerns)라고 부름.
* 흩어진 관심사를 Aspect 로 모듈화하고 핵심적인 비즈니스 로직에서 분리하여 재사용하겠다는 것이 AOP 의 취지

#### **AOP 의 주요 개념**
* Aspect
   * 흩어진 관심사(공통 부분 코드)를 모듈화 한 것
   * 주로 부가기능들을 모듈화 함
* Target
   * Aspect 가 적용되는 곳 (클래스, 메서드 등 )
* Advice
   * Aspect 에서 실질적인 기능에 대한 구현체
* Join Point
   * Advice 가 Target 에 적용되는 시점
   * 메서드 진입 시점, 생성자 호출 시점, 필드에서 값을 꺼내올 때 등 다양한 시점에 적용 가능
* PointCut
   * Joint Point 의 상세한 스펙을 정의 한 것
   * 더욱 구체적으로 Advice 가 실행될 지점을 정할 수 있음

#### **Spring AOP 의 특징**
* Spring Bean 에서만 AOP 가 적용 가능
* 프록시 패턴 기반의 AOP 구현체, 프록시 객체를 쓰는 이유는 접근 제어 및 부가기능을 추가하기 위해서임
* 중복 코드, 프록시 클래스 작성의 번거로움 등에 대한 해결책을 제시하는 것이 목적

### 3. PSA (Portable Service Abstraction) : 일관성 있는 서비스 추상화
#### **PSA (Portable Service Abstraction) 이란**
* 추상화 계층을 사용하여 어떤 기술을 내부에 숨기고 개발자에게 편의성을 제공하는 것을 서비스 추상화(Service Abstaraction)라고 함
* 하나의 추상화로 여러 서비스를 묶어둔 것을 Spring 에서 PSA 라고 함
   * PSA는 환경의 변화와 관계없이 일관된 방식의 기술로의 접근환경을 제공하는 추상화 구조임
   * Spring 은 Spring Web MVC, Spring Transaction, Spring Cache 등의 다양한 PSA 를 제공

    
 



   




### reference
Ioc
https://medium.com/@jang.wangsu/di-inversion-of-control-container-%EB%9E%80-12ecd70ac7ea
https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/
https://velog.io/@gillog/Spring-DIDependency-Injection

AOP
https://engkimbs.tistory.com/746
https://catsbi.oopy.io/fb62f86a-44d2-48e7-bb9d-8b937577c86c

PSA
https://sabarada.tistory.com/127
