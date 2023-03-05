# Generic

## 제네릭(Generic)이란?
* 클래스나 메서드에서 사용할 내부 데이터 타입을 컴파일시에 미리 지정하는 방법
* 특정 타입을 미리 지정해주는 것이 아닌 필요에 의해 지정할 수 있도록 하는 일반(Generic)타입

## 제네릭(Generic)의 장점
* 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
* 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다.(편한 관리 가능)
* 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.
```java
ArrayList list = new ArrayList();
list.add("hello")
String str = (String) list.get(0);
```
위와 같이 제네릭을 사용하지 않을 경우 타입변환이 필요하지만,
```java
ArrayList<String> list2 = new ArrayList();
list.add("hello");
str = list2.get(0);
```
제네릭을 사용할 경우 타입변환이 필요없다.

## 제네릭(Generic) 사용방법
### (1) 클래스 및 인터페이스 선언
   * 클래스 또는 인터페이스 이름 뒤에 < >부호가 붙고 사이에 타입 파라미터가 위치한다.
   * T 타입은 해당 블럭 {...} 안에서까지 유효하다.
```java
public class 클래스명 <T> {...}
public Interface 인터페이스명 <T> {...}
```

### (2) 제네릭 클래스
```java
class ClassName<T> {
    
    private T type;  // 제네릭 타입 변수
    
    void set(T type) {  // 제네릭 파라미터 메소드
        this.type = type;
    }
    
    T get() {  // 제네릭 타입 반환 메소드
        return type;
    }
}
```
위와 같이 클래스를 설계할 때 타입파라미터로 넣어두었다가 실제 클래스 사용 시 구체적인 타입을 지정하면서 사용하면 타입 변환을 최소화 시키는 것이 가능하다.
```java
class Main {
    public static void main(String[] args) {
        ClassName<String> a = new ClassName<String>();
        ClassName<Integer> b = new ClassName<Integer>();
```
위와 같은 코드처럼 타입 지정 시
* a 객체의 ClassName 의 T 제네릭 타입은 모두 String 으로 변환된다.
* b 객체의 ClassName 의 T 제네릭 타입은 모두 Integer 로 변환된다.

### (3) 제네릭 인터페이스
* 인터페이스 또한 클래스처럼 제네릭으로 설정해두고 활용 가능하다.
```java
interface InterfaceName<T> {
    T type();
}

class ExGenetic implements InterfaceName<String> {
    
    @Override
    public String example() {
        return null;
    }
}
```

### (4) 멀티 타입 파라미터
* 두개 이상의 멀티 타입 파라미터 사용 시, 각 타입 파라미터를 콤마로 구분한다.
```java
class ClassName<K, V> {
    private K first; // K 타입 (제네릭)
    private V second; // V 타입 (제네릭)
    
    void set(K first, V second) {
        this.first = first;
        this.second = second;
    }

    K getFirst() {
        return first;
    }

    V getSecond() {
        return second;
    }
}

class Main {
    public static void main(String[] args) {

        ClassName<String, Integer> a = new ClassName<String, Integer>();
    }
}
```

### (5) 제네릭 메서드
* 클래스에서 지정한 제네릭 유형과는 별도로 메소드에서 독립적으로 제네릭 유형을 선언하여 사용하는 방법
* 제네릭이 사용되는 메소드를 정적 메소드로 두고 싶다면 제네릭 클래스와 별도로 독립적인 제네릭이 사용되어야 함.
```java
public <T> T genericMethod(T o) {	// 제네릭 메소드
        ...
}
```
일반적으로 제네릭 메서드는 위와 같이 선언 가능하다.
```java
class ClassName<E> {
    private E element;
    
    void set(E element) {
        this.element = element;
    }
    
    E get() {
        return element;
    }
    
    static <E> E genericMethod1(E o) {
        return o;
    }

    static <T> T genericMethod1(T o) {
        return o;
    }
}
```
위의 코드와 같이 제네릭 메소드는 제네릭 클래스 타입과 별도로 지정되며, 메소드의 E 타입은 제네릭 클래스의 E 타입과 다른 독립적인 타입이다.

## 제한된 제네릭(Generic)과 와일드카드

### (1) 상한 경계 (제네릭 타입 < extends 상위타입 >)
extends 뒤에 오는 타입이 최상위 타입으로 한계가 정해진다.

```java
public class ClassName <K extends Number> {...}
```
* Number 와 이를 상속하는 Integer, Short, Double 등의 타입이 지정될 수 있다.
* 객체 혹은 메소드 호출 시 K 는 지정된 타입으로 변환된다.
```java
public class ClassName <? extends T> {...}
```
* T 와 이를 상속하는 Integer, Short, Double 등의 타입이 지정될 수 있다.
* 객체 혹은 메소드 호출 시 지정되는 타입이 없어 타입 참조가 불가능하다.
```java
public class ClassName <K extends Number> { 
	... 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<Double> a1 = new ClassName<Double>();	// 정상 작동
 
		ClassName<String> a2 = new ClassName<String>(); // 에러 발생
	}
}
```
* 위와 같은 경우 Integer 는 Number 클래스를 상속받는 클래스라 가능하지만, String 은 별개의 클래스이기 때문에 에러가 발생한다. 
### (2) 하한 경계 (제네릭 타입 < super 상위타입 >)
super 뒤에 오는 타입이 최하위 타입으로 한계가 정해진다.
대표적으로 해당 객체가 업 캐스팅(Up Casting) 되어야 할 때 사용하는데, 하위 타입의 자료들을 상위 타입으로 보고 조작해야 할 때 사용 가능하다.

* 제네릭 타입에 대한 객체 비교
```java
public class SaltClass <E extends Comparable<E>> { ... }	// 에러 가능성 있음
public class SaltClass <E extends Comparable<? super E>> { ... }	// 안전성이 높음

public class Person {...}

public class Student extends Person implements Comparable<Person> {
    @Override
    public int compareTo(Person o) { ... };
}

public class Main {
    public static void main(String[] args) {
        SaltClass<Student> a = new SaltClass<Student>();
    }
}
```
* Comparable 에서 보다 상위 타입을 비교하는 것을 방지하기 위해서 <? super E> 를 사용해 미리 방지
* 즉, <E extends Comparable<? super E>>는 E타입 혹은 E 타입의 super 클래스가 Comparable 을 의무적으로 구현해야 한다.
* 이를 통해 Up Casting 의 안정성을 보장받는다. (타입 파라미터보다 더 높은 상위 타입 객체로 가는 것을 방지)


### (3) 와일드 카드 (제네릭 타입 <?>)
와일드 카드 <?> 은 <? extends Object>와 마찬가지로 아래의 코드와 같은 의미이다.
```java
public class ClassName extends Object {...}
```
* 어떤 타입을 리턴받아도 상관없다는 의미이다.
* 보통 데이터가 아닌 기능의 사용에만 관심이 있는 경우에 사용한다.

---
### 참조
* [제네릭의 개념](http://www.tcpschool.com/java/java_generic_concept)
* [자바 - 제네릭(Generic)의 이해](https://st-lab.tistory.com/153)
* [제네릭(Generic) 사용법 & 예제 총정리](https://coding-factory.tistory.com/573)
