# Library and Module (자바 라이브러리와 모듈)

## 라이브러리 vs 모듈
* 라이브러리
   * 라이브러리는 프로그램 개발 시 활용할 수 있는 `클래스와 인터페이스들을 모아놓은 것`을 말한다.
   * 일반적으로 `JAR(Java ARchive)` 압축파일 형태로 존재한다.
   * 개발 시 라이브러리를 이용하려면 JAR 파일을 `ClassPath(클래스를 찾기 위한 경로)` 에 추가해야 한다.
* 모듈
   * 모듈은 `패키지 관리 기능까지 포함`된 라이브러리이다.
   * 일반 라이브러리는 내부에 포함된 모든 패키지에 `외부 프로그램에서의 접근이 가능`하지만, 모듈은 `일부 패키지를 은닉`하여 접근하지 못하게 할 수 있다.
   * 모듈은 자신이 실행할 때 필요로 하는 `의존 모듈을 모듈 기술자에 기술 가능`하다. (의존 관계 쉽게 파악 가능)

## java.base 모듈
> java.base 는 모든 모듈이 의존하는 기본 모듈로, 모듈중 유일하게 `requires`하지 않아도 사용 가능하다.

### java.base 주요 패키지

|     패키지     |                    용도                    |
|:-----------:|:----------------------------------------:|
|  java.lang  |             자바 언어의 기본 클래스 제공             |
|  java.util  |          자료 구조와 관련된 컬렉션 클래스 제공           |
|  java.text  |  날짜 및 숫자를 원하는 형태의 문자열로<br/> 만들어 주는 포맷 클래스 제공  |
|  java.time  |        날짜 및 시간을 조작하거나 연산하는 클래스 제공        |
|   java.io   |              입출력 스트림 클래스 제공              |
|  java.net   |           네트워크 통신과 관련된 클래스 제공            |
|  java.nio   |    데이터 저장을 위한 Buffer 및<br/> 새로운 입출력 클래스 제공    |

### Object 클래스
> 자바의 모든 클래스는 Object 의 자식이거나 자손 클래스이며, 클래스 선언시 다른 클래스를 상속하지 않으면 암시적으로 java.lang.Object 클래스를 상속한다.

* Object 주요 메소드

|             메소드             |               용도                |
|:---------------------------:|:-------------------------------:|
| boolean equals(Object obj)  |       객체의 번지를 비교하고 결과를 리턴       |
|       int hashCode()        |           객체의 해시코드 리턴           |
|       String toString       | 객체 문자 정보 리턴<br/>(클래스명@16진수해시코드) |

Object 는 최상위 클래스이므로 위의 메소드는 모든 객체에서 사용가능하다.

### System 클래스
> System 클래스의 정적 멤버와 메소드를 이용하면 운영체제의 일부 기능을 이용할 수 있다.

* System 클래스 필드

|  필드   |       용도        |
|:-----:|:---------------:|
|  out  |   콘솔에 문자를 출력    |
|  err  |  콜솔에 에러 내용을 출력  |
|  in   |     키보드 입력      |

* System 클래스 메소드

|          메소드          |                      용도                      |
|:---------------------:|:--------------------------------------------:|
|   exit(int status)    | 프로세스를 종료<br/>(정상 종료 `0`, 비정상 종료 `1` 또는 `-1`) |
|  currentTimeMillis()  |          현재 시간을 밀리초 단위의 long 값으로 리턴          |
|      nanoTime()       |          현재 시간을 나노초 단위의 long 값으로 리턴          |
|     getProperty()     |               운영체제와 사용자 정보 제공                |
|       getenv()        |              운영체제의 환경 변수 정보 제공               |

### 문자열 클래스

#### 1. String 클래스
> * 문자열을 저장하고 조작할 때 사용한다.
> * 문자열 리터럴은 자동으로 String 객체로 생성되지만, String 클래스의 다양한 생성자를 이용해 직접 객체 생성도 가능하다.

#### 2. StringBuilder 클래스
> * 내부 버퍼에 문자열을 저장해두고 그 안에서 추가, 삭제, 수정 작업을 하기 위한 클래스
> * String 을 이용하면 새로운 객체를 생성하는 것밖에 못하므로 잦은 문자열 변경을 해야한다면 효율성이 좋다.

* StringBuilder 조작 메소드

|     리턴 타입      |       메소드(매개 변수)       |        설명        |
|:--------------:|:----------------------:|:----------------:|
| StringBuilder  |      append(문자열)       |   문자열을 끝부분에 추가   |
| StringBuilder  |    insert(위치, 문자열)     |  문자열을 지정 위치에 삽입  |
| StringBuilder  |  delete(시작 위치, 끝 위치)   |    문자열 일부를 삭제    |
| StringBuilder  |  replace(시작 위치, 끝 위치)  |    문자열 일부를 대체    |
|     String     |       toString()       |    완성된 문자열 리턴    |

* 사용 예시
```java
public class StringBuilderExample {
  public static void main(String[] args) {
    String data = new StringBuilder();
    data.append("def");        // def
    data.insert(0, "abc");     // abcdef
    data.delete(3, 4);         // abcef
    data.toString();
  }
}
```
```agsl
abcef
```

#### 3. StringTokenizer 클래스
> 문자열이 구분자로 연결되어 있을 경우, 이를 분리하기 위해 사용 가능하다.

* split() 메소드를 이용한 구분
```java
String data = "강백호&채치수,서태웅-정대만";
String[] names = data.split("&|,|-");
```

* StringTokenizer 클래스를 이용한 구분
```java
String data = "강백호/채치수/서태웅";
StirngTokenizer st = newStringTokenizer(data, "/");
```

* StringTokenizer 조작 메소드

|   리턴 타입   |     메소드(매개변수)     |          설명          |
|:---------:|:-----------------:|:--------------------:|
|    int    |   countTokens()   |  분리할 수 있는 문자열의 총 갯수  |
|  boolean  |  hasMoreTokens()  |  남아 있는 문자열이 있는지 여부   |
|  String   |    nextToken()    |     문자열을 하나씩 가져옴     |

### Wrapper 클래스 (포장 클래스)
> 자바는 기본 타입의 값을 갖는 객체를 생성할 수 있는데 이러한 객체를 포장 객체라고 한다. 

|   기본 타입   |   포장 클래스    |
|:---------:|:-----------:|
|   byte    |    Byte     |
|   char    |  Character  |
|   short   |    Short    |
|    int    |   Integer   |
|   long    |    Long     |
|   float   |    Float    |
|  double   |   Double    |
|  boolean  |   Boolean   |

위와 같이 기본 타입에는 대응되는 포장 클래스가 있으며, 포장 객체는 포장하고 있는 기본 타입의 값을 변경할 수 없고, 단지 객체로 생성하는 것에만 목적이 있다.

#### 박싱과 언박싱
> * 기본 타입의 값을 포장 객체로 만드는 것을 `박싱(boxing)`, 포장 객체에서 기본 타입의 값을 얻어내는 것을 `언박싱(unboxing)`이라고 한다.
> * 박싱은 포장 클래스 변수에 기본 타입 값이 대입될 때, 언박싱은 기본 타입 변수에 포장 객체가 대입될 때 발생한다.

![Library_and_Module_1.png](image%2FLibrary_and_Module%2FLibrary_and_Module_1.png)

```java
Integer obj = 123;    // 박싱
int value = obj       // 언박싱
int value = obj + 123 // 언박싱 후 연산
```

#### 문자열을 기본 타입 값으로 변환
> 대부분의 포장 클래스에는 문자열을 기본 타입 값으로 변환하기 위한 `parse + 기본타입`명으로 된 정적 메소드가 있다.

#### 포장 값의 비교
> 포장 객체는 내부 값을 비교할 때 `==`과 `!=`이  아닌 `equals`를 사용하도록 한다. 전자는 내부 값을 비교하는 것이 아니라 객체 번지를 비교하기 때문이다.

### Math 클래스 (수학 클래스)
> 수학 클래스는 이름 그대로 수학 계산에 사용 가능한 메소드를 제공하며, 모든 메소드는 정적이므로 수학 클래스로 바로 사용이 가능하다.

|       메소드       |        리턴값        |
|:---------------:|:-----------------:|
|   Math.abs()    |        절대값        |
|   Math.ceil()   |        올림값        |
|  Math.floor()   |        버림값        |
|   Math.max()    |        최대값        |
|   Math.min()    |        최소값        |
|  Math.random()  |  랜덤값<br/>(0.0<=x<1.0)  |
|  Math.round()   |       반올림값        |

### 리플렉션 (reflection)
> * 자바는 클래스와 인터페이스의 `패키지 정보`, `타입 정보`, `멤버(생성자, 필드, 메소드) 정보` 등을 Class 객체로 관리하며, 이를 `메타 정보`라고 부른다
> * 메타 정보를 프로그램에서 읽고 수정하는 행위를 리플렉션이라고 한다.

* Class 객체 얻는 방법
```java
// 클래스로부터 얻는 방법
Class clazz = 클래스이름.class;
Class clazz = Class.forName("패키지...클래스이름");

// 객체로 부터 얻는 방법
Class clazz = 객체참조변수.getClass();
```

#### 패키지와 타입정보 얻기

| 메소드                    | 용도                |
|------------------------|-------------------|
| Package getPackage()   | 패키지 정보 얻기         |
| String getSimpleName() | 패키지를 제외한 타입 이름    |
| String getName()       | 패키지를 포함한 전체 타입 이름 |

#### 멤버 정보 얻기

| 메소드                                     | 용도        |
|-----------------------------------------|-----------|
| Constructor[] getDeclaredConstructors() | 생성자 정보 읽기 |
| Field[] getDeclaredFields()             | 필드 정보 읽기  |
| Method[] getDeclaredMethods()           | 메소드 정보 읽기 |

#### 리소스 경로 얻기

| 메소드                                          | 용도                     |
|----------------------------------------------|------------------------|
| URL getResource(String name)                 | 리소스 파일의 URL 리턴         |
| InputStream getResourceAsStream(String name) | 리소스 파일의 InputStream 리턴 |

## 어노테이션 (Annotation)
> 코드에서 `@`으로 작성되는 요소를 `어노테이션`이라고 하며, 어노테이션은 클래스 또는 인터페이스를 컴파일하거나 실행 시 어떻게 처리해야 할 것인지 알려주는 설정 정보이다.

#### 어노테이션의 용도
1. 컴파일 시 사용하는 정보를 전달
2. 빌드 툴이 코드를 자동으로 생성할 때 사용하는 정보를 전달
3. 실행 시 특정 기능을 처리할 때 사용하는 정보를 전달

---
### 참조
* [이것이 자바다(한빛미디어)](http://www.yes24.com/Product/Goods/112208302)