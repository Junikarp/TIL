# Stack

---

## Stack 이란?
> * 요소의 삽입과 삭제가 한쪽 끝에서만 이루어지는 자료구조로 가장 마지막에 들어간 데이터가 제일 먼저 나오고, 가장 먼저 들어간 데이터가 가장 나중에 나오는 특징을 가진다.
> * 스택 ADT 의 주요 기능은 `삽입(push)`과 `제거(pop)` 연산이 있다.

![Stack_1.png](image%2FStack%2FStack_1.png)

* 기본 연산
    * push(item) : item 을 스택에 삽입
    * pop() : 스택의 가장 위에 있는 항목 제거
    * peek() : 스택의 가장 위에 있는 항목 반환
    * isEmpty() : 스택이 비어있다면 true 반환
 
## 배열 기반 스택
> 배열 기반의 스택은 용량을 동적으로 변경하는 비용이 크지만, 구현이 간단하다는 장점이 있다.

* ArrayStack.java
```java
class ArrayStack<T> { 
    private int top;
    private Object[] stack;
    private int size;
    
    ArrayStack(int size) {
        this.top = -1;
        this.stack = new Object[size];
        this.size = size;
    }
    
    boolean isEmpty() {
        return this.top < 0;
    }
    
    T peek() {
        return isEmpty() ? null : (this).stack[top];
    }
    
    void push(T value) {
        if (++top >= size) {
            return;
        }
        stack[top] = value;
    }
    
    T pop() {
        if (isEmpty()) {
            return null;
        } else {
            return (T) stack[top--];
        }
    }
}
```


## 링크드 리스트 기반 스택
> 링크드 리스트 기반 스택은 스택 용량에 제한을 두지 않아도 된다는 장점이 존재한다.

* StackNode.java
```java
class StackNode<T> {
    T value;
    StackNode<T> next;
    
    StackNode(T value) {
        this.value = value;
        this.next = null;
    }
}
```

* LinkedStack.java
```java
class LinkedStack<T> {
    private StackNode<T> list = null;
    
    boolean isEmpty() {
        return list == null;
    }
    
    void push(T value) {
        StackNode<T> node = new StackNode<>(value);
        node.next = list;
        list = node;
    }
    
    T pop() {
        if (isEmpty()) {
            return null;
        }
        else {
            StackNode ret = list;
            list = list.next;
            return (T)ret.value;
        }
    }
    T peek() {
        if(isEmpty()) {
            return null;
        } 
        else {
            return list.value;
        }
    }
}
```

---
### 참조
* [Stack(스택) - Array 기반 / LinkedList 기반](https://hoehen-flug.tistory.com/4)
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)