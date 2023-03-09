# Adapter Pattern (어댑터 패턴)
> [Design Pattern Code](https://github.com/Junikarp/Design-Patterns)

## 어댑터 패턴이란
* 클라이언트의 요구 타입과 반환 타입이 다를지라도 중간에 둘을 연결지어주는 패턴
* 기능상 문제없이 동작하는 코드가 단지 인터페이스 차이 때문에 사용할 수 없을 경우 많이 응용함

## 기본 설계
   * Adaptee 에 정의된 기능을 Adapter 를 통해서 요구사항에 맞춰 변경하여 사용한다.
![adapter_01.png](image%2Fadapter_01.png)

## 요구 사항
* 두 수에 대한 다음 연산을 수행하는 객체를 만드세요.
   * 수의 두 배의 수를 반환 - twiceOf(Float): Float
   * 수의 반(1/2)의 수를 반환 = halfOf(Float): Float
* 구현 객체의 이름은 'Adapter'
* Math 클래스에서 두 배와 절반을 구하는 함수는 이미 구현되어있음 (매개변수, 리턴타입 double 형)

## 설계
![adapter_02.png](image%2Fadapter_02.png)

## 구현
* 기존에 보유하고 있는 알고리즘
   * Math.java
```java
public class Math {
    
    public static double twoTime(double num) {
        return num * 2;
    }
    
    public static double half(double num) {
        return num / 2;
    }
}
```
* Adapter.java
```java
public interface Adapter {
    public Float twiceOf(Float f);
    public Float halfOf(Float f);
}
```
* AdapterImpl.java
```java
public class AdapterImpl implements Adapter {
    
    @Override
    public Float twiceOf(Float f) {
        return (float) Math.twoTime(f.doubleValue());
    }

    @Override
    public Float halfOf(Float f) {
        return (float) Math.half(f.doubleValue());
    }
}
```
* main.java
```java
public class main {
    public static void main(String[] args) {
        Adapter adapter = new AdapterImpl();
        System.out.println(adapter.twiceOf(100f));
        System.out.println(adapter.halfOf(50f));
    }
}
```
* 실행 결과
```agsl
200.0
25.0

Process finished with exit code 0
```
* 결론적으로 알고리즘에 대한 변경은 인터페이스 구현체에서 받아 커스텀, 메인에서 인터페이스에 접근하여 사용하는 구조이다.



---
### 참조
[자바 디자인 패턴의 이해 - 어댑터 패턴](https://www.youtube.com/watch?v=gJDZ7pcvlAU&t=244s)
[자바 디자인 패턴의 이해 - Gof Design ](https://catsbi.oopy.io/344dbe7b-9774-48fc-9c95-b554e9c1c4bc)
