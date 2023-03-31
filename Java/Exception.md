# Exception (예외)

## 예외(Exception)와 오류(Error)
* 오류란?
   * 오류는 시스템이 종료되어야 할 수준의 상황과 같은 수습할 수 없는 심각한 문제
   * 이는 개발자가 미리 예측하여 방지할 수 없는 상황이다.
* 예외란?
   * 개발자가 구현한 로직에서 발생한 실수나 사용자의 영향에 의해 발생한다.
   * 개발자가 미리 예측하여 방지하는 것이 가능하며, 예외처리(Exception Handle)를 해야한다.

## 예외 처리
### (1) try, catch
try 문 안에 있는 문장들에서 예외 발생시 catch 문이 수행된다/
* 기본 구조
```java
try {
    기본 수행 문장;
} catch(예외1) {
    예외 1 발생 시 수행할 문장;
} catch(예외2) {
    예외 2 발생 시 수행할 문장;
}
```
* 예외 처리 예시
```java
int N;
try {
    N = 2 / 0;
}
catch (ArithmeticException e) {
    N = -1;
}
```
위의 예시에서는 `ArithmeticException` 발생 시 N 에 -1이 대입된다. 이 때 `e` 는 `ArithmeticException` 클래스의 객체, 즉 오류 객체이다.   

### (2) finally
* 위의 try, catch 문에서 볼 수 있듯 예외가 발생시 프로그램이 중지되거나 예외 처리에 의해 catch 구문이 시행된다.
* 하지만 어떤 예외가 발생해도 반드시 실행되어야 하는 부분이 있다면 finally 로 처리가능하다.
```java
public class Example {
    public void Run() {
        System.out.println("반드시 수행한다!");
    }
    
    public static void main(String[] args) {
        Example example = new Example();
        int N;
        try {
            N = 2 / 0;
        } catch (ArithmeticException e) {
            N = -1;
        } finally {
            example.Run();
        }
    }
}
```
위와 같은 코드를 실행시킨다면 예외와 상관없이 `example.Run()` 메서드가 실행되어 문장이 출력될 것이다.

### (3) throws
* throws 를 사용하면 메서드를 호출한 곳에서 예외를 처리하도록 한다. (예외 던지기)
```java
throw 예외 객체 //ex) throw new Exception("새로운 예외에요!") 
```
위와 같은 형태로 사용하는 것이 가능하다.
* 예시 코드
```java
public static void divide(int N, int M) throws ArithmeticException {
        if (M == 0) 
            throw new ArithmeticException("예외 발생");
        int K = N/M;
        System.out.println(K);
}
public static void main(String[]args) {
        int N = 2;
        int M = 0;

        try {
        divide(N,M);
        } catch (ArithmeticException e) {
        e.getMessage();
        e.printStackTrace();
        }
}
```
* 실행 결과
```java
java.lang.ArithmeticException: 예외 발생
at main.divide(main.java:5)
at main.main(main.java:14)
```
---
### 참조
* [점프 투 자바 예외처리 (Exception)](https://wikidocs.net/229#finally)
* [Java 의 Error 와 Exception 그리고 예외처리 전략](https://toneyparky.tistory.com/40)
* [이것만 알면 예외(EXCEPTION) 정복 - 예제를 통한 개념과 예외 처리 방법](https://reakwon.tistory.com/155)