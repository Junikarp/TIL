# Collection Framework (컬렉션 프레임워크)

## 컬렉션 프레임워크
> 컬렉션 프레임워크는 자바에서 자료구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 인터페이스와 클래스들을 구현해 놓은 것이다.

![Collection_Framework_1.jpg](image%2FCollection_Framework%2FCollection_Framework_1.jpg)

`List` 와 `Set`은 객체를 추가, 삭제, 검색하는 방법에 공통점이 있어 `Collection` 인터페이스로 정의하고 이것을 상속하고 있다. `Map` 은 키와 값을 하나의 쌍으로 묶어서 관리하는 구조이므로 따로 분류된다.

|  인터페이스 분류  |                  특징                  |                  구현 클래스                   |
|:----------:|:------------------------------------:|:-----------------------------------------:|
|    List    |      순서를 유지하고 저장<br/>중복 저장이 가능       |       ArrayList, Vector, LinkedList       |
|    Set     |    순서를 유지하지 않고 저장<br/>중복 저장이 불가능     |             HashSet, TreeSet              |
|    Map     |  키와 값으로 구성된 엔트리 저장<br/>키는 중복 저장 불가능  |  HashMap, HashTable, TreeMap, Properties  |

## List 컬렉션


---
### 참조
* [이것이 자바다(한빛미디어)](http://www.yes24.com/Product/Goods/112208302)
* [[Java] 컬렉션 프레임워크](https://devbox.tistory.com/entry/Java-%EC%BB%AC%EB%A0%89%EC%85%98-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)
