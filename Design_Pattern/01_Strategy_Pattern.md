# Strategy Pattern (전략 패턴)
> [Design Pattern Code](https://github.com/Junikarp/Design-Patterns)

## 전략 패턴이란
* 여러 알고리즘을 하나의 추상적인 접근점(Interface)을 만들어 접근점에서 서로 교환 가능(Deligate)하도록 하는 패턴

## 기본 설계
   * 사용자(Client)는 자신에게 맞는 전략(Strategy)을 취사선택하여 로직을 수행할 수 있게 하는 방법
   * 게임을 예를 들면 캐릭터는 공격이라는 작업을 수행함에 있어 무기를 상황에 맞게 선택, 공격을 위임 가능
![Strategy_01.png](image%2FStrategy_01.png)

## 구현 코드
   * 무기(Weapon)는 공격(Attack)이라는 기능을 가지는 하나의 접근점(Strategy)
   * `setWeapon` 메서드를 통해 무기(접근점)를 변경 가능
   * `weapon.attack()`으로 weapon 에게 공격 기능을 위임
* 클래스 다이어그램
![Strategy_02.png](image%2FStrategy_02.png)
* main.java
```java
public class main {
    
    public static void main(String[] args) {
        
        GameCharacter character = new GameCharacter();
        character.attack();

        character.setWeapon(new Knife());
        character.attack();

        character.setWeapon(new Sword());
        character.attack();
    }
}
```
* GameCharacter.java
```java
public class GameCharacter {
    //접근점
    private Weapon weapon;

    //교환 가능
    public void setWeapon(Weapon weapon) {
        this.weapon = weapon;
    }
    public void attack(){
        if (weapon == null) {
            System.out.println("맨손 공격");
        } else {
            //위임(Delegate)
            weapon.attack();
        }
    }
}
```
* Weapon.java
```java
public interface Weapon {
    public void attack();
}
```
* Knife.java
```java
public class Knife implements Weapon{

    @Override
    public void attack() {
        System.out.println("칼 공격");
    }
}
```

* Sword.java
```java
public class Sword implements Weapon{
   
    @Override
    public void attack() {
        System.out.println("검 공격");
    }
}
```
위와 같이 Weapon 이라는 인터페이스를 통해 접근점을 만들고, attack 메서드 기능 무기마다 따로 구현하여 setter 를 통해 무기의 교환을 가능하게 만든다.

## 유지 보수
   * 무기에 총을 추가하고 싶다면...
   * 다른 코드의 변경을 할 필요없이, Gun 을 추가하고 사용하는 것이 가능하다.
```java
public class Gun implements Weapon {
    
    @Override
    public void attack() {
        System.out.println("탕탕 총 공격");
    }
}
```
---
### 참조
* [자바 디자인 패턴의 이해 - Gof Design Pattern](https://catsbi.oopy.io/344dbe7b-9774-48fc-9c95-b554e9c1c4bc)