## POJO 와 JavaBeans

### POJO(Plain Old Java Object)
* 2000년 9월 마틴 파울러, 레베카 파슨스, 조시 맥켄지에 의해 만들어진 용어
* POJO 는 특정 프레임워크에 종속되지 않은 순수한 자바 객체로, 속성과 메서드에 대한 어떠한 네이밍 규칙도 없다.
* Java EE 와 같은 무거운 프레임 워크들이 서비스 시장을 점유했을 때, 해당 프레임워크에 종속된(무거운) 객체를 사용해야 했던 것에 반발해서 나오게 된 개념이다.
* Spring Framework 는 POJO 를 기본 개념으로 채택했다.

> "We wondered why people were so against using regular objects in their systems and concluded that it was because simple objects lacked a fancy name. So we gave them one, and it's caught on very nicely."
> 
> 우리는 왜 사람들이 자기들 시스템에 일반적인 오브젝트를 사용하는 것에 반대하는지 궁금했고, 그 이유는 단순한 오브젝트에 멋진 이름이 없기 때문이라고 결론을 지었습니다. 그래서 우리는 멋진 이름을 지었고, 매우 인기를 얻었습니다.

### POJO 의 조건
* (1) 특정 규약에 종속되지 않는다.
   * 자바 언어와 꼭 필요한 API 외에는 종속되지 말아야 한다.
   * EJB2와 같이 특정 규약을 따라 만들게 하는 경우는 대부분 규약에서 제시하는 특정 클래스를 상속하도록 요구하며, 이 경우 자바의 단일 상속 제한 때문에 더이상 해당 클래스에 객체지향적인 설계 기법을 적용하기가 어려워지는 문제가 생긴다.
* (2) 특정 환경에 종속되지 않는다.
   *  POJO 는 환경에 독립적이어야 하며, 특히 비즈니스 로직을 담은 POJO 클래스는 웹이라는 환경 정보나 웹 기술을 담고 있는 클래스나 인터페이스를 사용해서는 안된다.
* (3) 단일 책임 원칙을 지키는 클래스여야한다.
   * 책임과 역할이 각기 다른 코드는 서로 다른 클래스로 나뉘어야 한다.  

## POJO 의 장점
   * 특정 규약에 종속되지 않아 로우레벨 코드와 비즈니스 코드가 분리되어 깔끔한 코드 작성이 가능하다.
   * 특정 환경에 종속되지 않아 테스트하기 좋다.
   * 객체지향적인 설계를 자유롭게 적용 가능하다.

## POJO 예시 코드
```java
public class Animal {
    String dog;
    public String cat;
    private int legs;

    public Animal(String dog, String cat, int legs) {
        this.dog = dog;
        this.cat = cat;
        this.legs = legs;
    }

    public getDog() {
        return this.dog;
    }
}
```
---
### JavaBeans

JavaBeans 이란 구현 방법에 대해 다음의 컨벤션을 적용한 POJO 이다.

* Fields 는 접근제어자가 private 이어야만 하며 getter 와 setter 를 가져야 한다.
* Fields 는 getter 와 setter 로만 접근되어야 한다.
* constructor 는 argument 를 가져서는 안된다.

## JavaBeans 장·단점
* 장점
   * Bean 의 속성, 이벤트, 메소드는 다른 애플리케이션에 노출 가능하다.
   * Bean 을 구성하는데 도움이 된느 보조 프로그램이 제공될 수 있따.
   * Bean 의 설정 정보는 영속성 저장소에 저장하고 복원할 수 있다.
* 단점
   * 기본 생성자가 있는 클래스는 유요하지 않은 상태에서 인스턴스화 될 수 있다.
       * 수동으로 생성하는 경우 이러한 문제가 생길 수 있으며, 컴파일러가 이러한 문제를 감지할 수 없다.
   * Bean 은 기본적으로 변경 가능하므로, 불변 객체가 제공하는 이점이 없다.
   * 모든 property 에 대해 getter 를 만들고 대부분의 property 에 대해 setter 를 만들어야 한느 경우 많은 양의 코드가 생긴다.
       * Lombok 을 이용해 완화 가능 

## JavaBeans 예시 코드
```java
public class Animal { 
   
    private int legs;
    
    Animal() {
    }
   
    public setLegs(int legs) {
    this.legs = legs;
    }
    
    public getLegs() {
    return legs;
    }
}
```
참조
[POJO란?](https://doing7.tistory.com/81)
[POJO(Plain Old Java Object)와 JavaBean](https://2jinishappy.tistory.com/324)
[POJO 와 Beans 의 차이점](https://sanghye.tistory.com/13)
[POJO](https://www.nowwatersblog.com/springboot/springstudy/POJO)
[JavaBeans 정리](https://velog.io/@dion/what-is-javabeans-and-why-use-javabeans)