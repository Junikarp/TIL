# final and constant

## final 키워드
> final 은 해당 entity 가 오로지 한 번 할당될 수 있음을 의미한다.
* final 필드
   * 해당 변수가 한 번만 초기화가 가능함을 의미함(상수를 만들 때 응용)
* final 메서드
   * 해당 메서드를 Override 하거나 숨길수 없음
* final 클래스
   * 해당 클래스는 상속할 수 없으며, 상속 계층에서 마지막 클래스
   * 보안과 효율성을 얻기위해 자바 표준 라이브러리 클래스에서 사용 가능
## final 필드
* final 필드 선언
```java
final 타입 필드명 [=초기값];
```
* 필드 선언 시 초기값을 주는 방법은 두가지 방법이 있다.
   * 필드 선언 시에 초기화
      * 단순 값이라면 필드 선언시 초기화를 하는 방법이 간단하다. 
   * 생성자에서 초기화 
      * 복잡한 초기화 코드가 필요하거나 객체 생성시 외부 데이터로 초기화 해야한다면, 생성자에서 초기값 지정
      * 초기화 되지 않은 final 필드가 있으면 컴파일 에러 발생

* 예시 코드
```java
public class Person {
    final String nation = "Korea"; // 필드 선언 & 초기값 지정
    final String age;
    String name;
    
    public Person(String age, String name) {
        this.age = age;
        this.name = name;
    }
}
```
```java
public class Person_final {
    public static void main(String[] args) {
        Person person = new Person("22", "karp");
        
        System.out.println(person.nation); // Koera
        System.out.println(person.age);  // 22
        System.out.println(person.name); // karp
        
        person.nation = "Japan"; // final 값을 수정 불가이므로 컴파일 에러
        person.name = "Juni"; // 인스턴스 필드는 수정 가능
    }
}
```
## final 클래스
* final 클래스 선언
```java
접근제어자 final class 클래스명;
```
* 예시 코드
```java
public final class Person {
    public int age;
    
    public void setAge(int age){
        this.age = age;
    }
} 
```
```java
public class Student extends Person {  // final 클래스는 상속 불가이므로 에러 발생
    public int age;
    public int getAge(){
        return age;
    }
}
```
## final 메서드
* 선언 방식
```java
public final 리턴타입 메서드명(){...}
```
* 예시 코드
```java
public class Person {
    public int age;

    public final void setAge(int age){
        this.age = age;
    }
} 
```
```java
public class Student extends Person{
    public final void setAge(int age){
        // final 메서드는 오버라이딩 불가이므로 에러 발생
    }
}
```

## Static 키워드
> static 은 해당 데이터의 메모리 할당을 컴파일 시간에 할 것임을 의미합니다.
* static 멤버 변수
   * 클래스 변수라고도 부르며, 모든 해당 클래스는 같은 메모리를 공유함
   * 특정한 인스턴스에 종속되지 않으며, 인스턴스를 만들지 않고 사용 가능
* static 메서드
   * 클래스 메서드라고도 부르며, 오버라이드가 불가
   * 상속 클래스에서 보이지 않음
* static 블록
   * 클래스 내부에 만들 수 있는 초기화 블록
   * 클래스가 초기화 될 때 실행되며, main()보다 먼저 수행됨
* static 클래스
   * 일반 적인 클래스, top-level 클래스에 적용하면 문법 오류
   * 중첩 클래스에만 사용 가능
   * 부모클래스의 멤버필드 중에는 static 필드에만 접근 가능
   * 사실상 일반적인 top-level 클래스와 동일하게 동작하지만, 그 위치가 하나의 top-level 클래스 안에 들어있는 것
* static import
   * 다른 클래스에 존재하는 static 멤버를 불러올 때 사용
   * 멤버 메서드를 곧바로 사용가능

## 상수 (static final)
>* 불변의 값을 저장하는 필드는 상수(constant)라고 한다.
>* 불변의 값은 객체마다 저장할 필요가 없는 공용성을 띄며, 여러가지 값으로 초기화가 불가(오직 하나의 값을 가진다).
>* final 필드는 객체마다 저장되고, 생성자의 매개값을 통해 여러가지 값을 가지는 것이 가능하다.(상수가 되는 것이 불가능)
>* 상수는 static(공용성)이면서 final(수정 불가)이어야 하며, static final 필드는 객체마다 저장되지 않고, 클래스에만 포함되며, 한번 초기화시 변경 불가하다.
* 상수 선언 방식
```java
static final 타입 상수 [=초기값];
```
```java
static final 타입 상수;

static {            
    상수 = 초기값;  // 복잡한 초기화의 경우 정적 블록에서 초기화 가능
}
```
상수의 이름은 모두 대문자이며, 단어 혼합 시 _ 기호로 이어준다.
```java
static final double PI = 3.141592;
static final double TOM_JERRY;
```
* 예시 코드
```java
public class Earth {
    static final double EARTH_RAD = 6400;
    static final double EARTH_SURFACE_AREA;
    
    static {
        EARTH_SURFACE_AREA = 4 * MATH.PI * EARTH_RAD * EARTH_RAD;
    }
}
```
```java
public class Earthis {
    public static void main(String[] args) {
        system.out.println("Earth.EARTH_RAD");
        system.out.println("Earth.EARTH_SURFACE_AREA");
    }
}
```

### 참조
* [자바 - final 필드와 상수](https://kephilab.tistory.com/51)
* [왜 자바에서 final 멤버 변수는 관례적으로 static을 붙일까?](https://djkeh.github.io/articles/Why-should-final-member-variables-be-conventionally-static-in-Java-kor/)
* [final 클래스, final 메소드](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=highkrs&logNo=220213143536)