# Template Method Pattern
> [Design Pattern Code](https://github.com/Junikarp/Design-Patterns)

## 템플릿 메서드 패턴이란
* 알고리즘의 구조를 메서드에 정의하고 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 재정의 하는 패턴
* GOF 디자인 패턴에서의 정의는 아래와 같다.
> 템플릿 메서드 패턴은 다음과 같은 목적을 가진다.
> 작업에서 알고리즘의 골격을 정의하고 일부 단계를 하위 클래스로 연기합니다.
> 템플릿 메서드를 사용해 하위 클래스에서 전체 구조를 변경하지 않고 알고리즘의 특정 단계를 재정의 할 수 있습니다.

## 사용처
* 일정한 프로세스를 가진 요구사항을 템플릿 메서드 패턴을 이용하여 구현 가능하다.
* 예시로 아래와 같은 경우에서 이용가능하다.
   * Spring Security 의 인증 및 인가 과정
   * 애노테이션 프로세서의 라운드 구조
   * 로직의 완성까지의 로직이 순차적인 일정한 단계가 있는 경우 등..

## 구조
* Abstract Class
   * 템플릿 메서드를 정의하는 클래스
   * 하위 클래스에 공통 알고리즘을 정의하고, 하위 클래스에서 구현될 기능을 hook 메서드 등으로 정의하는 클래스이다.
* ConcreteClass
   * 물려받은 primitive 메서드 또는 hook 메서드를 구현하는 클래스
   *  상위 클래스에 구현된 템플릿 메서드의 일반적인 알고리즘에서 하위 클래스에 적합하게 hook 메서드 등을 오버라이드 하는 클래스이다.
![Template_Method_01.png](image%2FTemplate_Method_01.png)

## 구현 
* 딸기 우유와 바나나 우유 만드는 법을 비교한다고 가정해본다.

|  딸기 우유  |  바나나 우유  |
|:-------:|:--------:|
| 우유를 산다  |  우유를 산다  |
| 우유를 끓인다 | 우유를 끓인다  |
| 딸기를 넣는다 | 바나나를 넣는다 |
|   식힌다   |   식힌다    |
* StrawberryMilk.java
```java
public class StrawberryMilk {
    public void makeStrawberryMilk() {
        buyMilk();
        boilMilk();
        putStrawberry();
        coolDown();
    }
    private void buyMilk() {
        System.out.println("우유를 삽니다.");
    }
    private void boilMilk() {
        System.out.println("우유를 끓입니다.");
    }
    private void putStrawberry() {
        System.out.println("딸기를 넣습니다.");
    }
    private void coolDown() {
        System.out.println("완성품을 식힙니다.");
    }
}
```
* BananaMilk.java
```java
public class BananaMilk() {
    public void makeBananaMilk() {
        buyMilk();
        boilMilk();
        putBanana();
        coolDown();
    }
    private void buyMilk() {
        System.out.println("우유를 삽니다.");
    }
    private void boilMilk() {
        System.out.println("우유를 끓입니다.");
    }
    private void putBanana() {
        System.out.println("바나나를 넣습니다.");
    }
    private void coolDown() {
        System.out.println("완성품을 식힙니다.");
    }
}
```
* MakeMilk
```java
public class MakeMilk { 
    public static void main(String[] args) {
        StrawberryMilk strawberrymilk = new StrawberryMilk();
        BananaMilk bananamilk = new BananaMilk();
        
        strawberrymilk.makeStrawberryMilk();
        Bananamilk.makeBananaMilk();
    }
}
```
위의 코드를 살펴보면 딸기우유와 바나나우유를 만드는 두가지의 코드에 중복되는 부분이 많은 것을 확인할 수 있다.






---
### 참조
* [자바 디자인 패턴의 이해 - Gof Design Pattern](https://catsbi.oopy.io/344dbe7b-9774-48fc-9c95-b554e9c1c4bc)
