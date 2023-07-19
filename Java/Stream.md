# Stream (스트림)

## 스트림이란?
> * 배열을 포함한 컬렉션의 저장요소를 하나씩 참조
> * 람다식으로 처리할 수 있도록 해주는 반복자

### 반복자와 스트림

* 반복자
```java
List<String> list = Arrays.asList("정대만", "채치수", "서태웅");
Iterator<String> iterator = list.iterator();
while(iterator.hasNext()) {
    String name = iterator.next();
    System.out.println(name)
}
```

* 스트림으로 변환
```java
List<String> list = Arrays.asList("정대만", "채치수", "서태웅");
Stream<String> stream = list.stream();
stream forEach(name -> System.out.println(name));
```

### 스트림의 특징
> * Iterator 와 비슷한 역할을 하는 반복자
> * 람다식으로 요소 처리 코드 제공
>    * 대부분의 요소처리 메소드 함수적 인터페이스 매개 타입 
> * 내부 반복자 사용 -> 병렬처리가 쉬움
>    * 컬렉션 내부에서 요소들 반복시킴
>    * 개발자는 요소당 처리해야할 코드만 제공


## 스트림의 종류
> java.util.stream 패키지에 스트림 API가 있음