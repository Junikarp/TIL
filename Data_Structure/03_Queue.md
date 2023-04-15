# Queue

---

## 큐(Queue)란?
> 입력 창구와 출력 창구가 따로 존재하고 먼저 들어간 데이터가 먼저 나오는 선입선출(First In First Out) 자료구조이다.
> 보통 enqueue 가 일어나는 쪽을 `rear`, dequeue 가 일어나는 쪽을 `front` 라고 부른다.

![Queue_1.png](image%2FQueue%2FQueue_1.png)

* 큐의 기본연산
   * enqueue(item) : 큐에 데이터 item 을 삽입 
   * dequeue() : 큐의 맨 앞에 저장된 데이터를 제거하며, 반환
   * peek() : 큐의 맨 앞에 저장된 데이터를 반환
   * size() : 큐에 들어있는 데이터 원소의 개수를 반환
   * isEmpty : 현재 큐가 비어있다면 `true`, 비어있지 않다면 `false` 반환

## 순환 큐
> 배열을 기반으로 구현된 큐로, 배열의 크기가 유한하므로 큐의 크기가 다 차버리면 사용 불가하다.

* CircularQueue.java
```java
public class CircularQueue {
    private int[] queue; // 큐를 구현할 배열
    private int front; // 큐의 맨 앞 위치
    private int rear; // 큐의 맨 뒤 위치
    private int size; // 큐의 크기

    public CircularQueue(int size) {
        queue = new int[size];
        front = 0;
        rear = 0;
        this.size = size;
    }

    public void enqueue(int item) { // 큐에 데이터 추가
        if (isFull()) {
            System.out.println("큐가 가득참");
            return;
        }
        queue[rear] = item;
        rear = (rear + 1) % size; // rear 위치 조정
    }

    public int dequeue() { // 큐에서 데이터 삭제
        if (isEmpty()) {
            System.out.println("큐가 비어있음");
            return -1;
        }
        int item = queue[front];
        front = (front + 1) % size; // front 위치 조정
        return item;
    }

    public boolean isEmpty() { // 큐가 비어있는지 확인
        return front == rear;
    }

    public boolean isFull() { // 큐가 꽉 차 있는지 확인
        return (rear + 1) % size == front;
    }
}
```

## 링크드 큐(연결형 큐)
> 링크드 큐는 크기의 제한이 없고, 삽입과 삭제가 편리하다는 장점이 있다.

* LinkedQueue.java
```java
public class LinkedQueue {
    private Node front; // 큐의 맨 앞 노드
    private Node rear;  // 큐의 맨 뒤 노드

    public Queue() { // 큐 생성자
        front = null;
        rear = null;
    }

    public void enqueue(int data) { // 큐에 데이터 추가
        Node newNode = new Node(data);
        if (isEmpty()) {
            front = newNode;
            rear = newNode;
        } else {
            rear.next = newNode;
            rear = newNode;
        }
    }

    public int dequeue() { // 큐에서 데이터 삭제
        if (isEmpty()) {
            System.out.println("큐가 비어있음");
            return -1;
        } else {
            int data = front.data;
            front = front.next;
            if (front == null) {
                rear = null;
            }
            return data;
        }
    }

    public boolean isEmpty() { // 큐가 비어있는지 확인
        return front == null;
    }

    private static class Node { // 노드 정의
        int data; // 데이터 필드
        Node next; // 다음 노드 참조 필드

        public Node(int data) { // 노드 생성자
            this.data = data;
            this.next = null;
        }
    }
}
```

## java 라이브러리를 이용하여 큐 사용하기

* 큐 생성
```java
Queue<T> queue = new LinkedList<>(); // T 자료형 큐 생성
```

* 메서드

|            메서드             |                   결과                   |
|:--------------------------:|:--------------------------------------:|
| offer(item)<br/>add(item)  |              item 을 큐에 삽입              |
|    poll()<br/>remove()     |       가장 먼저 큐에 삽입된 데이터 반환하면서 삭제        |
|        peek()<br/>         |      element() 가장 먼저 큐에 들어간 요소 반환      |
|         isEmpty()          |  큐가 비어있다면 `true`, <br/>비어있지 않다면 `false` 반환  |
|           size()           |           큐에 들어있는 요소의 개수 반환            |

이 때 `add`,`remove`,`element` 는 문제 상황에서 예외를 발생시키지만, `offer`,`poll`,`peek` 는 `null` 또는 `false` 를 반환하는 차이점이 있으며, 기능적으로는 동일하다.


---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [큐(Queue) 이해하고 구현해보기](https://oh-potato.tistory.com/6)