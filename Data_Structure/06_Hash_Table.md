# Hash Table

## 해시 테이블(Hash Table)
> * 키(Key)를 특정 해시 함수(Hash Function)를 통해 해싱한 후 나온 테이블 내의 주소(인덱스)에 데이터(Value)를 담는 자료구조.
> * 데이터를 입력할 여유공간이 많이 필요하지만 인덱스를 통한 빠른 탐색이 가능하다.

![Hash_Table_1.png](image%2FHash_Table%2FHash_Table_1.png)

## 해시 함수의 충돌
> 해시 함수가 서로 다른 입력값에 대해 동일한 해시 테이블 주소를 반환하는 것을 `충돌`이라고 부른다.

### 충돌 해결 기법

#### 1. 체이닝
> 해시 함수가 서로 다른 키에 같은 주소값을 반환하여 충돌이 일어나면 각 데이터를 해당 주소의 링크드 리스트에 삽입하는 방법

![Hash_Table_2.png](image%2FHash_Table%2FHash_Table_2.png)

#### 2. 개방 주소법
> 개방 주소법은 충돌 발생 시 해시 함수로 만들어진 주소가 아닌 다른 주소를 사용하는 것을 허용하여 충돌을 피하는 방법이다.

#### 2-1. 선형 탐사
* 선형 탐사는 충돌 발생 시 현재 주소에서 고정폭으로 주소를 이동하여 저장하는 방법이다.
* 충돌할 뻔한 데이터들이 한 곳으로 모이는 클러스터 현상이 많이 발생한다.
* 클러스터 현상은 새로운 주소를 찾는 탐사 시간을 늘리므로, 해시 테이블의 성능을 저하시킨다.

![Hash_Table_3.png](image%2FHash_Table%2FHash_Table_3.png)

#### 2-2. 제곱 탐사
* 제곱 탐사는 충돌 발생 시 이동폭이 제곱수로 늘어난다 (Ex. 1, 4, 9, 16,...)
* 서로 다른 해시값을 가진 데이터에 대해서는 어느정도 클러스터가 형성되지 않도록 하는 효과가 있다.
* 같은 해시값을 가진 데이터에 대해서는 2차 클러스터를 형성하는 문제를 갖고 있다.

![Hash_Table_4.png](image%2FHash_Table%2FHash_Table_4.png)

#### 2-3. 이중 해싱
* 하나의 해시 함수에서 충돌이 발생할 시 2차 해시 함수를 통해 이동폭을 얻는 방법 
* 캐시 효율은 떨어지지만 클러스터링에 영향을 거의 받지 않는다.

![Hash_Table_5.png](image%2FHash_Table%2FHash_Table_5.png)

### 재해싱
> 해시 테이블은 테이블의 공간 사용률이 70% ~ 80% 에 이르면 성능 저하가 나타나기 시작한다.
> 재해싱은 이러한 성능저하를 방지하기 위해 테이블의 크기를 늘리고, 새로운 테이블의 크기에 맞춰 기존의 데이터를 다시 해싱하는 것을 의미한다.

![Hash_Table_6.png](image%2FHash_Table%2FHash_Table_6.png)

### Java 라이브러리를 이용하여 HashSet 과 HashMap 사용하기 

#### 1. HashSet
> 객체 자체를 데이터로 저장하는 Set 인터페이스의 구현체로 중복을 허용하지 않는다.

* HashSet 생성
```java
HashSet<Type> hset = new HashSet<>();
```

* HashSet 메서드

|      메서드       |                 설명                  |
|:--------------:|:-----------------------------------:|
|   add(item)    |              item 을 삽입              |
|  remove(item)  |         HashSet 에서 item 삭제          |
|     size()     |      HashSet 에 저장된 원소의 개수를 반환       |
|   isEmpty()    | HashSet 이 비어있다면 true, 아닐경우 false 반환 |
|    clear()     |         HashSet 의 모든 요소를 삭제         |
| contains(item) |   item 이 HashSet 에 포함된 경우 true 반환   |


#### 2. HashMap
> Key-Value 쌍 형태로 데이터를 저장하는 Map 인터페이스 구현체로 HashTable 과 유사한 자료구조로 데이터를 저장한다.

* HashMap 생성
```java
HashMap<Type, Type> hmap = new HashMap<Type, Type>();
```

* HahsMap 메서드

|          메서드           |                                     설명                                      |
|:----------------------:|:---------------------------------------------------------------------------:|
|        get(key)        |                           key 값과 매핑되는 value 값 반환                            |
|    put(key, value)     | 주어진 key = value 쌍을 HashMap 에 추가<br/>이미 key 가 존재할 경우 나중에 put 된 value 가 들어간다. |
|      remove(key)       |                   key 값과 매핑되는 value 반환 후 key = value 쌍 삭제                   |
|  replace(key, value)   |           기존에 존재하던 key = value 쌍을 반환하고, 새로운 key = value 쌍으로 바꾼다.            |
|       isEmpty()        |                     HashMap 이 비어있다면 true, 아닐경우 false 반환                     |
|        clear()         |                             HashMap 의 모든 요소를 삭제                             |
| containsKey/Value(key) |                    Key/Value 가 HashMap 에 포함된 경우 true 반환                     |



---
### 참조
* [해시 테이블(Hash Table)](https://dev-kani.tistory.com/1)
* [HashMap, HashSet 이란? - (5) HashMap과 HashSet의 차이](https://siahn95.tistory.com/96)
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
