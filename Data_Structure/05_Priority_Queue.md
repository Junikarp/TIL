# Priority Queue

## 우선순위 큐(Priority Queue)
> 데이터에 우선순위를 부여하여 큐에 삽입하고, 들어간 순서와 상관없이 가장 높은 우선순위를 가진 요소부터 빠져나오게 하는 자료구조

## 힙(Heap)
> 힙은 우선순위 큐를 위해 고안된 완전 이진 트리 형태의 자료구조이다.

### 힙의 특징
* 완전 이진 트리의 형태로 이루어져있다.
* 이진 탐색 트리와 다르게 중복된 값을 허용한다.
* 부모 노드와 서브 트리간의 대소 관계가 성립한다.

### 힙의 종류

#### 1. 최대 힙
최대 힙은 완전 이진 트리이면서, 루트 노드로 올라갈수록 저장된 값이 커지는 구조이다.

![Priority_Queue_1.png](image%2FPriority_Queue%2FPriority_Queue_1.png)

#### 2. 최대 힙
최소 힙은 완전 이진 트리이면서, 루트 노드로 올라갈수록 저장된 값이 작아지는 구조이다.

![Priority_Queue_2.png](image%2FPriority_Queue%2FPriority_Queue_2.png)

### 힙의 연산

#### 1. 삽입 연산
1. 힙의 최고 깊이 가장 우측에 새 노드를 추가한다. 이때 힙은 완전 이진 트리를 유지해야 한다.
2. 삽입한 노드를 부모 노드와 비교한다.
   * 삽입한 노드가 부모 노드보다 크다면 연산을 종료한다.
   * 삽입한 노드가 부모 노드보다 작다면 다음 단계를 진행한다.
3. 삽입한 노드가 부모 노드보다 작다면 위치를 서로 변경한다.
4. 바꾼 후에는 다시 2번 단계를 진행한다.

#### 2. 삭제 연산
1. 뿌리 노드를 삭제한다.
2. 힙의 최고 깊이 가장 우측의 노드를 뿌리 노드로 옮겨와 힙 순서 복원을 시작한다.
3. 옮겨온 노드의 양쪽 자식을 비교하여 크기가 더 작은 노드와 위치를 교환한다.
4. 옮겨온 노드가 더 이상 자식이 없는 잎 노드가 되거나, 양쪽 자식보다 크기가 더 작은 경우 연산을 종료한다. 그렇지 않으면 2번 단계를 반복한다.

### heap 의 표현
* 힙은 배열의 형태로 정리하는 것이 가능하며 이 때의 성질은 아래와 같다.
    * 왼쪽 자식 노드 인덱스 = 부모노드 인덱스 * 2 + 1
    * 오른쪽 자식 노드 인덱스 = 부모노드 인덱스 * 2 + 2
    * 부모노드 인덱스 = (자식 노드 인덱스 - 1) / 2

![Priority_Queue_3.png](image%2FPriority_Queue%2FPriority_Queue_3.png)

### 힙 구현
아래의 코드와 같이 최소힙을 구현 가능하다.

```java
public class MinHeap {
    private int[] heap; // 배열로 힙 구현
    private int capacity; // 힙의 크기
    private int size; // 현재 힙에 저장된 요소의 개수

    public MinHeap(int capacity) {
        this.capacity = capacity;
        this.size = 0;
        this.heap = new int[capacity + 1]; // 0번 인덱스는 사용하지 않음
    }

    // 삽입 연산
    public void insert(int element) {
        if (size == capacity) {
            throw new RuntimeException("힙이 가득참");
        }
        size++;
        heap[size] = element;
        int idx = size;

        // 부모 노드보다 값이 작으면 교환
        while (idx > 1 && heap[idx] < heap[idx / 2]) { 
            swap(idx, idx / 2);
            idx = idx / 2;
        }
    }

    // 삭제 연산
    public int delete() {
        if (size == 0) {
            throw new RuntimeException("힙이 비어있음");
        }
        int deleted = heap[1];
        heap[1] = heap[size];
        size--;
        int idx = 1;
        while (idx * 2 <= size) { // 자식 노드와 비교하며 하향식으로 정렬
            int leftChild = idx * 2;
            int rightChild = idx * 2 + 1;
            int smallerChild;
            if (rightChild > size || heap[leftChild] < heap[rightChild]) {
                smallerChild = leftChild;
            } else {
                smallerChild = rightChild;
            }
            if (heap[idx] > heap[smallerChild]) {
                swap(idx, smallerChild);
                idx = smallerChild;
            } else {
                break;
            }
        }
        return deleted;
    }

    // 두 개의 노드 위치를 교환
    private void swap(int i, int j) {
        int temp = heap[i];
        heap[i] = heap[j];
        heap[j] = temp;
    }
}
```

## java 라이브러리를 이용하여 우선순위 큐 사용하기

### 우선순위 큐 생성
```java
PriorityQueue<참조 타입> pq = new PriorityQueue<>();
```
기본값으로 최소 힙 기반의 우선순위 큐가 생성된다.

### 우선순위 큐 메서드

|            메서드            |                설명                 |
|:-------------------------:|:---------------------------------:|
| add(item)<br/>offer(item) |         우선순위 큐에 item 을 삽입         |
|          poll()           |      우선순위가 가장 높은 원소를 반환하고 삭제      |
|          peek()           |        우선순위가 가장 높은 원소를 반환         |
|          size()           |      우선순위 큐에 저장된 원소의 개수를 반환       |
|         isEmpty()         | 우선순위 큐가 비어있다면 true, 아닐경우 false 반환 |
|         toArray()         |     우선순위 큐에 저장된 원소들을 배열값으로 반환     |
|          clear()          |         우선순위 큐의 모든 요소를 삭제         |
|      contains(item)       |   item 이 우선순위 큐에 포함된 경우 true 반환   |

---
### 참조
* [우선순위 큐와 힙 (Priority Queue & Heap)](https://suyeon96.tistory.com/31)
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [우선순위 큐(Priority Queue)와 힙(heap)](https://chanhuiseok.github.io/posts/ds-4/)