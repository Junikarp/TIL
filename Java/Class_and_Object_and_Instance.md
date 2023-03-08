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
클래스를 통해 생성된 객체 하나하나를 해당 클래스의 인스턴스라고 부른다.

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
