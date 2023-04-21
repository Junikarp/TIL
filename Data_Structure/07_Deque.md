# Deque

## 데크(Deque)
> Double-Ended Queue 의 줄임말인 데크는 스택과 큐가 결합한 형태로 양쪽 끝에서 자료의 삽입과 삭제가 가능한 자료구조이다.
> 한쪽으로만 입력 가능하도록 설정한 데크를 `스크롤(scroll)`이라고 하며, 한쪽으로만 출력 가능하도록 설정한 데크를 `셸프(shelf)`라고 한다.

![Deque_1.jpg](image%2FDeque%2FDeque_1.jpg)

### Java 라이브러리를 이용하여 Deque 사용하기
> 데크 자료구조의 여러 연산들을 정의한 Deque 인터페이스가 있고 이를 구현한 `ArrayDeque`, `LinkedBlockingDeque`, `ConcurrentLinkedDeque`, `LinkedList` 등의 클래스가 있다.

* Deque 생성
```java
Deque<String> deque = new ArrayDeque<>();
Deque<String> deque = new LinkedBlockingDeque<>();
Deque<String> deque = new ConcurrentLinkedDeque<>();
Deque<String> deque = new LinkedList<>();
```

* Deque 메서드

![Deque_2.png](image%2FDeque%2FDeque_2.png)

![Deque_3.png](image%2FDeque%2FDeque_3.png)

|                 메서드                 |           설명            |
|:-----------------------------------:|:-----------------------:|
| addFirst(item)<br/>offerFirst(item) |  데크의 앞쪽에 item 을 삽입한다.   |
|      add(item)<br/>offer(item)      |    데크의 뒤쪽에 item 을 삽입    |
|    removeFirst()<br/>pollFirst()    | 데크의 앞쪽에서 item 을 반환 후 제거 |
|         remove()<br/>poll()         | 데크의 뒤쪽에서 item 을 반환 후 제거 |
|      getFirst()<br/>peekFirst       |  데크의 앞쪽에서 item 을 반환한다.  |
|          get()<br/>peek()           |  데크의 뒤쪽에서 item 을 반환한다.  |
|               size()                |       데크의 크기를 반환        |
|   isEmpty()    | HashSet 이 비어있다면 true, 아닐경우 false 반환 |




---
### 참조
* [Deque(덱/데크) 자료구조](https://soft.plusblog.co.kr/24)
* [Deque(덱/데크) 사용법 및 예제](https://hbase.tistory.com/128)