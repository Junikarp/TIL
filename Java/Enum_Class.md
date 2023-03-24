# Enum Class

## 열거체(enumeration type)
* 클래스처럼 보이게 하는 상수
* 서로 관련있는 상수들끼리 모아서 상수를 정의한 것
* enum 클래스 형을 기반으로 한 클래스형 선언

## enum 클래스의 특징
* 열거형으로 선언된 순서에 따라 index 값을 갖는다.(0부터 순차적으로 증가)
* enum 열거형으로 지정된 상수들은 모두 '대문자'로 선언한다.
* 열거형 변수들을 선언한 후 마지막에는 세미콜론(;)을 찍지 않는다.
* 상수와 특정 값을 연결시킬 경우 마지막에 세미콜론(;)을 붙여줘야한다.

## 열거체 정의 및 사용
* 열거체 정의하는 법
```java
enum 열거체 이름{상수이름1, 상수이름2,...}
```
```java
enum Rainbow{
    RED,
    ORANGE,
    YELLOW,
    GREEN,
    BLUE,
    INDIGO,
    VIOLET
}
```

* 열거체 사용방법
```java
열거체이름.상수이름
```
```java
Rainbow.RED
```

* 열거체의 상숫값 정의 및 추가
> 기본적으로 이름만으로 정의도니 열거체의 상숫값은 0부터 설정되며, 순차적으로 1씩 증가한 값을 갖는다.
> <br> 따라서 불규칙적인 값을 상숫값으로 설정하고 싶다면 상수이름 옆에 괄호를 추가하고, 그 안에 원하는 값을 명시한다.
> <br> 이 때, 불규칙한 특정 값을 저장할 수 있는 인스턴스 변수와 생성자를 별도로 추가해야만 한다. 

```java
enum Rainbow {
    RED(3),
    ORANGE(10),
    YELLOW(21),
    GREEN(5),
    BLUE(1),
    INDIGO(-1),
    VIOLET(-11);
    
    private final int value;
    Rainbow(int value) {
        this.value = value;
    }
    public int getValue() {
        return value;
    }
}
```

## enum 메서드
enum 클래스의 메서드는 아래의 표와 같다.

|             메서드              |                          설명                          |
|:----------------------------:|:----------------------------------------------------:|
|       staic E values()       |            해당 열거체의 모든 상수를 저장한 배열을 생성하여 반환            |
| staic E valueOf(String name) | 전달된 문자열과 일치하는 해당 열거체의 상수를 반환<br/>값이 없으면 Exception 발생 |
|        String name()         |               호출된 값의 이름을 String 으로 반환                |
|        int ordinal()         |         해당 값이 enum 에 정의된 순서를 반환(index 값 반환)          |
|     equals(Object other)     |            지정된 객체가 enum 정수와 같은 경우 true 반환            |
|protected void finalize()|           해당 enum 클래스가 final 메서드를 가질 수 없게됨           |

위의 메서드들 중 values(), ordinal(), valueOf() 정도를 주로 사용한다.

---
### 참조
* [Enum 클래스](http://www.tcpschool.com/java/java_api_enum)
* [자바_enum 클래스 (열거형_enumeration type)](https://mine-it-record.tistory.com/204)