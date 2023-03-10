# Lambda

## 람다식(Lambda Expression)
* 함수(메서드)를 간단한 식으로 표현하는 방법
* 익명 함수(이름이 없는 함수, anonymous function)
```java
int max(int a, int b) {
    return a > b ? a : b;
}

// 람다식으로 변환        
(a, b) -> a > b ? a : b
```
* 함수와 메서드는 근본적으로 동일하나 함수는 클래스에 독립적이고, 메서드는 클래스에 종속적이다.
* 자바의 경우 메서드만 있음

## 람다식의 특징
* 람다식 내에서 사용되는 지역변수는 final 이 붙지 않아도 상수로 간주된다.
* 람다식으로 선언된 변수명은 다른 변수명과 중복될 수 없다.

## 람다식 작성하는 법
* (1) 메서드의 이름과 반환 타입을 제거하고 '->'블록{} 앞에 추가한다.
```java
int max (int a, int b) {
    return a > b ? a : b;
}

// (1) 시행
(int a, int b) -> {
    return a > b ? a : b;
}
```
* (2) 반환값이 있는 경우, 식이나 값만 적고 return 문 생략 가능 (끝에 ; 안붙임)
```java
(int a, int b) -> {
    return a > b ? a : b;
}

// (2) 시행
(int a, int b) -> a > b ? a : b
```
* (3) 매개 변수의 타입이 추론 가능하면 생략가능 (대부분 생략 가능)
```java
(int a, int b) -> a > b ? a : b

// (3) 시행
(a, b) -> a > b ? a : b
```
## 람다식 작성 시 주의 사항
* (1) 매개 변수가 하나인 경우, 괄호() 생략 가능(단, 타입이 없을 때만)
```java
(a) -> a * a
(int a) -> a * a

// 괄호 생략
a -> a * a       // OK  
int a -> a * a   // error
```
* (2) 블록 안의 문장이 하나뿐 일 때, 괄호{} 생략가능(끝에 ; 안 붙임)
```java
(int i) -> {
    System.out.println(i)
}

// 괄호 생략
(int i) -> System.out.println(i)
``` 
단, 하나뿐인 문장이 return 문이면 괄호{} 생략 불가 (but, 대부분 return 생략)

## 람다식 작성 예시
```java
int max(int a, int b) {
    return a > b ? a : b;
}

// 람다식 작성
(a, b) => a > b ? a : b
```
```java
int printVar(String name, int i) {
    System.out.println(name+"="+i)
}

// 람다식 작성
(name, i) -> System.out.println(name+"="+i)
```
```java
int square (int x) {
    return x * x;
}

// 람다식 작성
x -> x * x
```
```java
int roll() {
    return (int)(Math.random()*6);
}

// 람다식 작성
() -> (int)(Math.random() * 6) 
```
## 람다식 == 익명 객체
* 람다식은 익명 함수가 아닌 익명 객체
```java
(a, b) -> a > b ? a : b

// 동일
new Object () {
    int max(int a, int b) {
        return a > b ? a : b;
    }
}

int value = obj.max(3,5) // error
```
람다식을 다루기 위한 참조변수가 필요하다.

## 함수형 인터페이스
* 함수형 인터페이스란 단 하나의 추상 메서드만 선언된 인터페이스이다.
```java
interface MyFunction {
    public abstract int max(int a, int b);
}
```
```java
MyFunction f = new MyFunction() {    // 익명 클래스의 선언, 객체 생성을 동시에 함
    public int max(int a, int b) {
        return a > b ? a : b;
        }
};

int value = f.max(3,5) // MyFunction 에 max() 가 있으므로 OK
```
* 함수형 인터페이스 타입의 참조 변수로 람다식 참조 가능
* 함수형 인터페이스의 메서드와 람다식의 **매개변수 개수와 반환타입이 일치**해야함
```java
MyFunction f = (a, b) -> a > b ? a : b
int value = f.max(3,5) // 실제로는 람다식이 호출됨
```
---
참조
* [남궁성님의 자바의 정석](https://www.youtube.com/watch?v=3wnmgM4qK30)