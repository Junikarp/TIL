# 01. Linked List

---

## 리스트(List)란?
> * 리스트는 목록 형태로 이루어진 데이터 형식으로, 리스트의 목록을 이루는 개별 요소를 `노드`라고 부른다.
> * 노드 목록에서 첫번째 노드를 `헤드`, 마지막 노드를 `테일`이라고 부른다.

### 리스트 vs 배열
* 배열은 생성 시점에 크기를 정해주어야하며, 생성 후 크기를 변경할 수 없다.
* 이러한 문제를 해결하기위해 유연하게 크기를 조절 가능한 리스트라는 자료구조를 사용한다.

## 링크드 리스트(Linked List)
> * 링크드 리스트는 노드를 연결해서 만든 리스트이다.
> * 링크드 리스트의 노드는 데이터를 보관하는 `필드`, 다음 노드와 연결고리 역할을 하는 `포인터`로 이루어진다.
> * 노드의 추가, 삽입, 삭제 연산은 빠르지만 특정위치에 있는 노드로의 접근이 느리다는 특징이 있다.

![Linked_List_1.png](image%2FLinked_List%2FLinked_List_1.png)

## 더블 링크드 리스트(Double Linked List)
> 링크드 리스트의 탐색 기능을 개선한 자료구조로 링크드 리스트는 헤드에서 테일 방향으로만 탐색이 가능한 것에 비해, 더블 링크드 리스트는 양방향 탐색이 가능하다.

![Linked_List_2.png](image%2FLinked_List%2FLinked_List_2.png)

## 환형 링크드 리스트(Circular Linked List)
> * 헤드와 테일의 노드를 연결하여 헤드의 이전 노드가 테일이고, 테일의 다음 노드가 헤드인 링크드리스트이다.
> * 테일에 접근하는 비용이 작아지며, 뒤에서부터 노드를 찾아가는 루틴을 구현가능하다.

![Linked_List_3.png](image%2FLinked_List%2FLinked_List_3.png)

---
### 참조
* [Difference between Singly linked list and Doubly linked list](https://www.geeksforgeeks.org/difference-between-singly-linked-list-and-doubly-linked-list/)
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)