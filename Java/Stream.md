# Stream (스트림)

## 스트림이란?
> * 배열을 포함한 컬렉션의 저장요소를 하나씩 참조
> * 람다식으로 처리할 수 있도록 해주는 반복자

### 반복자와 스트림
```java
List<String> list = Arrays.asList("정대만", "채치수", "서태웅");
Iterator<String> iterator = list.iterator();
while(iterator.hasNext()) {
    String name = iterator.next();
    System.out.println(name)
}
```