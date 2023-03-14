# Class, Object, Instance

## Object(객체)
* 객체란 물리적으로 존재하거나 추상적으로 생각 가능한 것 중에서 자신의 속성을 가지고 있으며, 식별 가능한 것을 말한다.
* 한마디로 고유의 특성을 가지는 모든 대상이 객체이다.

## Class(클래스)
클래스는 Java 에서 객체를 생성하기 위한 설계도라고 할 수 있다.

* 구성
   * field(필드) : 객체의 데이터가 저장되는 장소이다.
   * constructor(생성자) : 객체가 실제로 생성될 때 초기화하는 역할을 한다.
   * method(메서드) : 객체의 동작에 해당하는 실행 블록이다.
* 예시
```java
public class Person {
    //field (필드)
    String name;
    int age;
    char sex;
    
    // constructor(생성자)
    Person(String name, int age, char sex) {
        this.name = name;
        this.age = age;
        this.sex = sex;
    }
    
    // method(메서드)
    void eat(){
        System.out.println("냠");
    }

    void sleep(){
        System.out.println("쿨쿨");
    }

    void clap(){
        System.out.println("짝짝");
    }
}
```

## Instance(인스턴스)

* 인스턴스는 같은 클래스에 속하는 개개의 객체로, 하나의 클래스에서 생성된 객체를 말한다.
* 클래스가 객체화되어, 클래스에서 정의된 속성과 성질을 가진 실질적인 객체로 표현된 것을 의미한다.
* 추상적인 개념인 클래스에서 실제 객체를 생성하는 것을 인스턴스화(instantiation)라고 한다.

```java
public class PersonIns{
    public static void main(String[] args) {
        
        // 객체 생성 = 인스턴스
        Person person1 = new Person("Juni","20","Female");
        Person person2 = new Person("Karp", "22","male");
        
        // 메서드 사용
        person1.eat();
        person2.sleep();
    }
}
```
위와 같이 생성자를 통해 객체를 생성하고 초기화하며, 생성된 인스턴스를 통해 메서드를 사용한다.

---
### 참조
* [객체와 클래스, 인스턴스의 차이](https://codybuilder.com/17)

