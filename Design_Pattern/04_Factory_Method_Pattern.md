# Factory Method Pattern
> [Design Pattern Code](https://github.com/Junikarp/Design-Patterns)

## 팩토리 메서드 패턴이란?
* 클래스의 인스턴스를 만드는 일을 서브 클래스에 위임하는 패턴 (`new` 키워드를 호출해 객체를 생성하는 역할을 위임)
* 인스턴스를 만드는 방법을 상위 클래스 측에서 결정하지만 구체적인 클래스명을 결정하지는 않는다.
* 구체적인 내용은 하위 클래스 측에서 수행함 (팩토리 메서드 패턴은 객체를 만드는 공장을 만드는 것)

## 구조
* 제품은 인터페이스를 선언하고, 인터페이스는 생성자와 자식 클래스들이 생성할 수 있는 모든 객체에 공통
* 구상 제품들은 제품 인터페이스의 구현이다.
* 크리에이터(creator) 클래스는 새로운 제품 객체들을 반환하는 팩토리 메서드를 선언한다.(반환 유형이 제품 인터페이스와 동일 해야함)
* 구상 크리에이터 들은 기초 팩토리 메서드를 오버라이드 하여 다른 유형의 제품을 반환하게 한다.
![Factory_Method_01.png](image%2FFactory_Method_01.png)

## 예제
* MilkFactory.java
```java
public interface MilkFactory {
    Milk orderMilk() {
        Milk milk = createMilk();
        milk.complete();
        return milk;
    }
    Milk createMilk();
}
```
* StrawberryMilkFactory.java
```java
public class StrawberryMilkFactory implements MilkFactory {
    @Override
    public Milk createMilk() {
        return new StrawberryMilk();
    }
}
```
* BananaMilkFactory.java
```java
public class BananaMilkFactory implements MilkFactory {
    @Override
    public Milk createMilk() {
        return new BananaMilk();
    }
}
```
* Milk.java
```java
public interface Milk {
    void complete();
    void drink();
}
```
* StrawberryMilk.java
```java
public class StrawberryMilk implements Milk{
    @Override
    public void complete() { 
        System.out.println("딸기우유 완성");
    }
    @Override
    public void drink() { 
        System.out.println("딸기우유 냠냠"); 
    }
}
```
* BananaMilk.java
```java
public class BananaMilk implements Milk{
    @Override
    public void complete() { 
        System.out.println("바나나우유 완성"); 
    }
    @Override
    public void drink() {
        System.out.println("바나나우유 냠냠");
    }
}
```
* Make.java
```java
public class Make {
    public static void main(String[] args){
        StrawberryMilkFactory strawberryMilkFactory = new StrawberryMilkFactory();
        Milk milk1 = strawberryMilkFactory.orderMilk();
        milk1.drink();

        BananaMilkFactory bananaMilkFactory = new BananaMilkFactory();
        Milk milk2 = bananaMilkFactory.orderMilk();
        milk2.drink();
    }
}
```
* 실행결과
```java
딸기우유 완성
딸기우유 냠냠
바나나우유 완성
바나나우유 냠냠
```
---

### 참조
* [팩토리 패턴 종류/개념/예제](https://cjw-awdsd.tistory.com/54)
* [팩토리 메소드 패턴(Factory Method Pattern)](https://jdm.kr/blog/180)