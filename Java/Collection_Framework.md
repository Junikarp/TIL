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
> List 컬렉션은 객체를 인덱스로 관리하며, 객체를 저장하면 인덱스가 부여되고 인덱스로 객체를 검색, 삭제하는 기능을 제공한다.

### List 메소드

* 객체 추가 

|               메소드                | 기능                       |
|:--------------------------------:|:-------------------------:|
|         boolean add(E e)         | 주어진 객체를 맨 끝에 추가          |
|  void add(int index, E element)  | 주어진 인덱스에 객체 추가           |
|    set(int index, E element)     | 주어진 인덱스의 객체를 새로운 객체로 교체  |

* 객체 검색

|             메소드              |          기능           |
|:----------------------------:|:---------------------:|
|  boolean contains(Object o)  |  주어진 객체가 저장되어 있는지 여부  |
|       E get(int index)       |  주어진 인덱스에 저장된 객체 리턴   |
|          isEmpty()           |     컬렉션이 비어있는지 조사     |
|          int size()          |  저장되어 있는 전체 객체수를 리턴   |

* 객체 삭제

|            메소드             |          기능          |
|:--------------------------:|:--------------------:|
|        void clear()        |     저장된 모든 객체 삭제     |
|    E remove(int index)     |  주어진 인덱스에 저장된 객체 삭제  |
|  boolean remove(object o)  |      주어진 객체를 삭제      |

### ArrayList
> List 컬렉션에서 가장 많이 사용하는 컬렉션으로 객체 추가 시 내부 배열에 객체가 저장된다. 일반 배열과 다르게 객체를 제한없이 추가 가능하며 List 컬렉션은 객체의 번지를 저장한다.

#### ArrayList 생성
```java
List<E> list = new ArrayList<E>(); // E에 지정된 타입의 객체만 저장
List<E> list = new ArrayList<>();  // E에 지정된 타입의 객체만 저장
List list = new ArrayList();       // 모든 타입의 객체 저장
```

### Vector
> `ArrayList` 와 동일한 내부 구조를 가지고 있지만 동기화된 메소드로 구성되어 있어 멀티 스레드가 동시에 `Vector()` 메소드를 실행 불가하다.

#### Vector 생성
```java
List<E> list = new Vector<E>(); // E에 지정된 타입의 객체만 저장
List<E> list = new Vector<>();  // E에 지정된 타입의 객체만 저장
List list = new Vector();       // 모든 타입의 객체 저장
```

### LinkedList
> `ArrayList`와 사용 방법은 동일하지만 인접 객체를 체인처럼 연결해서 관리한다는 차이점이 존재한다. 빈번한 객체 삽입, 삭제 작업이 필요 시 성능면에서 유리하다.

#### LinkedList 생성
```java
List<E> list = new ArrayList<E>(); // E에 지정된 타입의 객체만 저장
List<E> list = new ArrayList<>();  // E에 지정된 타입의 객체만 저장
List list = new ArrayList();       // 모든 타입의 객체 저장
```

## Set 컬렉션
> * List 와 달리 저장 순서를 유지하지 않는 집합
> * 객체 중복 저장 불가, 하나의 null 만 저장 가능

### Set 메소드

* 객체 추가

|               메소드               |                      기능                       |
|:-------------------------------:|:---------------------------------------------:|
|        boolean add(E e)         |  객체를 성공적으로 저장시 true 리턴,<br/>중복 객체라면 false 리턴  |

* 객체 검색

|             메소드              |             기능              |
|:----------------------------:|:---------------------------:|
|  boolean contains(Object o)  |     주어진 객체가 저장되어 있는지 여부     |
|          isEmpty()           |        컬렉션이 비어있는지 조사        |
|          int size()          |     저장되어 있는 전체 객체수를 리턴      |
|    Iterator<E> iterator()    |  저장된 객체를 한 번 씩 가져오는 반복자 리턴  |

* 객체 삭제

|            메소드             |          기능          |
|:--------------------------:|:--------------------:|
|        void clear()        |     저장된 모든 객체 삭제     |
|  boolean remove(object o)  |      주어진 객체를 삭제      |

### HashSet
> Set 컬렉션에서 가장 많이 사용하는 형태이다.

#### HashSet 생성
```java
Set<E> set = new HashSet<E>(); // E에 지정된 타입의 객체만 저장
Set<E> set = new HashSet<>();  // E에 지정된 타입의 객체만 저장
Set set = new HashSet();        // 모든 타입의 객체 저장
```

## Map 컬렉션
> * Map 컬렉션은 `키(key)`와 `값(value)`으로 구성된 엔트리 객체를 생성한다.
> * 키는 중복 저장 불가능하지만 값은 중복 저장 할수 있다.
> * 기존에 저장된 키와 동일한 키로 값 저장시 기존 값이 새로운 값으로 대체된다.

* 객체 추가
 
|          메소드           |       기능        |
|:----------------------:|:---------------:|
| V put(K key, V value)  | 주어진 키로 값을 저장한다  |

* 객체 검색
  
|                 메소드                 |                     기능                      |
|:-----------------------------------:|:-------------------------------------------:|
|   boolean containsKey(Object key)   |              주어진 키가 있는지 여부 파악               |
| boolean containsValue(Object value) |              주어진 값이 있는지 여부 파악               |​
|   Set<Map.Entry<K, V>> entrySet()   | 키와 값의 쌍으로 구성된 모든 Map.entry 객체를 Set 에 담아서 반환 |
|          V get(Object key)          |                주어진 키의 값을 리턴                 |
|          boolean isEmpty()          |                컬렉션이 비어있는지 여부                |
|           Set<K> KeySet()           |            모든 키를 Set 객체에 담아서 리턴             |
|             int size()              |               저장된 키의 총 수를 리턴                |
|       Collection<V> values()        |        저장된 모든 값 Collection 에 담아서 리턴         |

### HashMap
> 키로 사용할 객체가 `hashCode()` 메소드의 리턴값이 같고 `equal()` 메소드가 true 를 리턴할 경우 동일 키로 보고 중복 저장을 허용하지 않는다.

#### HashMap 생성
```java
Map<K,V> map = new HashMap<K,V>();  // 키와 값의 타입을 지정
Map map = new HashMap();            // 거의 사용하지 않는 방식
```

### Hashtable
> * `HashMap` 과 동일한 내부구조를 가지고 있다.
> * `Hashtable` 은 동기화 메소드로 구성되어 있으므로 멀티스레드가 동시에 `Hashtable` 메소드를 실행 할 수 없다.
> * 멀티 스레드 환경에서도 안전하게 객체를 추가, 삭제 가능하다.

#### Hashtable 생성
```java
Map<K,V> map = new Hashtable<K,V>();  // 키와 값의 타입을 지정
Map<K,V> map = new Hashtable<K,V>();  // 키와 값의 타입을 지정(뒤 쪽 생략)
Map map = new HashMap();              // 거의 사용하지 않는 방식
```

### Properties
> * `Properties` 는 `Hashtable` 의 자식 클래스로 키와 값을 `String` 타입으로 제한한 컬렉션이다.
> * 프로퍼티 파일은 키와 값이 `=`기호로 연결되어 있는 텍스트 파일이다.
> * Properties 는 프로퍼티 파일의 내용을 코드에서 쉽게 읽을 수 있도록 한다.

#### 프로퍼티 파일

* database.properties

```java
driver=oracle.jdbc.OracleDriver
        ...
admin=\uD64D\uAE38\uB3D9
```


#### Properties 생성
```java
Properties properties = new Properties();
```

#### 프로퍼티 파일 내용 로드
```java
properties.load(Xxx.class.getResourceAsStream("database.properties"))
```

## 검색 기능 강화 컬렉션
> 컬렉션 프레임워크가 제공하는 검색 기능 강화 컬렉션에는 `TreeSet`과 `TreeMap`이 있다.

### TreeSet
> `TreeSet`은 이진 트리 기반의 Set 컬렉션이다.

#### TreeSet 생성
```java
TreeSet<E> treeSet = new TreeSet<E>();
TreeSet<> treeSet = new TreeSet<>();
```


#### TreeSet 메소드
|          메소드           |                           설명                            |
|:----------------------:|:-------------------------------------------------------:|
|        first()         |                      제일 낮은 객체를 리턴                       |
|         last()         |                      제일 높은 객체를 리턴                       |
|       lower(E e)       |                  주어진 객체보다 바로 아래 객체를 리턴                  |
|      higher(E e)       |                  주어진 객체보다 바로 위 객체를 리턴                   |
|       floor(E e)       |  주어진 객체와 동등한 객체가 있다면 리턴,<br/>없다면 주어진 객체의 바로 아래의 객체를 리턴  |
|      ceiling(E e)      | 주어진 객체와 동등한 객체가 있으면 리턴,<br/>만약 없다면 주어진 객체의 바로 위의 객체를 리턴 |
|      pollFirst()       |                 제일 낮은 객체를 꺼내오고 컬렉션에서 제거                 |
|       pollLast()       |                 제일 높은 객체를 꺼내오고 컬렉션에서 제거                 |
|  descendingIterator()  |                 내림차순으로 정렬된 Iterator 리턴                  |
|    descendingSet()     |               내림차순으로 정렬된 NavigableSet 리턴                |


### TreeMap
> TreeMap 은 이진 트리를 기반으로 한 Map 컬렉션으로 TreeSet 과 달리 키와 값이 저장된 Entry 를 저장한다.

#### TreeMap 생성
```java
TreeMap<K, V> treeMap = new TreeMap<K, V>();
TreeMap<K, V> treeMap = new TreeMap<>();
```

#### TreeMap 메소드
|         메소드          |                                    설명                                    |
|:--------------------:|:------------------------------------------------------------------------:|
|     firstEntry()     |                           제일 낮은 `Map.Entry` 리턴                           |
|     lastEntry()      |                           제일 높은 `Map.Entry` 리턴                           |
|  lowerEntry(K key)   |                       주어진 키보다 바로 아래 `Map.Entry` 리턴                       |
|  higherEntry(K key)  |                       주어진 키보다 바로 위 `Map.Entry` 리턴                        |
|  floorEntry(K key)   | 주어진 키와 동등한 키가 있다면 해당 `Map.Entry` 리턴,<br/>없다면 주어진 키 바로 위의 `Map.Entry` 리턴  |
| ceilingEntry(K key)  | 주어진 키와 동등한 키가 있다면 해당 `Map.Entry` 리턴,<br/>없다면 주어진 키 바로 아래의 `Map.Entry` 리턴 |
|   pollFirstEntry()   |                    제일 낮은 `Map.Entry`를 꺼내오고 컬렉션에서 제거함                     |
|   pollLastEntry()    |                    제일 높은 `Map.Entry`를 꺼내오고 컬렉션에서 제거함                     |
|  descendingKeySet()  |                     내림차순으로 정렬된 키의 `NavigableSet`을 리턴                     |
|   descendingMap()    |               내림차순으로 정렬된 `Map.Entry`의 `NavigableMap` 을 리턴                |

### Comparable & Comparator
> * TreeSet 과 TreeMap 에 저장되는 키 객체는 저장과 동시에 오름차순으로 정렬되는데, 객체가 Comparable 인터페이스를 구현하고 있어야 가능하다.
> * Integer, Double, String 타입은 모두 Comparable 을 구현하고 있지만, 사용자 정의 객체는 따로 Comparable 을 구현하고 있어야 한다.

|  리턴 타입  |       메소드       |                                 설명                                 |
|:-------:|:---------------:|:------------------------------------------------------------------:|
|   int   | compareTo(T o)  |  주어진 객체와 같으면 0 리턴,<br/>주어진 객체보다 적으면 음수 리턴,<br/> 주어진 객체보다 크면 양수 리턴  |

비교 기능이 있는 Comparable 구현 객체를 TreeSet 에 저장하거나 TreeMap 의 키로 저장하는 것이 원칙이지만, 비교 기능이 없는 Comparable 비구현 객체를 저장하고 싶다면 TreeSet 과 TreeMap 을 생성할 때 비교자를 아래와 같이 제공하면 된다.

```java
TreeSet<E> treeSet = new TreeSet<E>(new ComparatorImpl());
TreeMap<K,V> treeMap = new TreeMap<K,V>(new ComparatorImpl());
```

|  리턴 타입  |         메소드          |                                              설명                                              |
|:-------:|:--------------------:|:--------------------------------------------------------------------------------------------:|
|   int   |  compare(T o1,T o2)  | `o1`과 `o2`가 동등하다면 0 리턴,<br/>`o1`이 `o2`보다 앞에 오게 하려면 음수 리턴,<br/> `o1`이 `o2`보다 뒤에 오게 하려면 양수 리턴  |

## LIFO & FIFO

### Stack
> Stack 에 대한 내용은 링크 -> [Stack](https://github.com/Junikarp/TIL/blob/main/Data_Structure/02_Stack.md)

#### Stack 생성
```java
Stack<E> stack = new Stack<E>;
Stack<E> stack = new Stack<>;  // 타입 생략 가능
```

#### Stack 메소드

|  리턴 타입  |      메소드       |         설명          |
|:-------:|:--------------:|:-------------------:|
|    E    |  push(E item)  |  주어진 객체를 스택에 삽입한다.  |
|    E    |     pop()      |  스택의 맨 위 객체를 빼낸다.   |

### Queue
> Queue 에 대한 내용은 링크 -> [Queue](https://github.com/Junikarp/TIL/blob/main/Data_Structure/03_Queue.md)

#### Queue 생성
```java
Queue<E> queue = new LinkedList<E>;
Queue<E> queue = new LinkedList<>;  // 타입 생략 가능
```

#### Queue 메소드

|  리턴 타입  |    메소드     |       설명        |
|:-------:|:----------:|:---------------:|
| boolean | offer(E e) | 주어진 객체를 큐에 넣는다. |
|    E    |   poll()   |  큐에서 객체를 빼낸다.   |

## 동기화된(Synchronized) 컬렉션
> * 비동기화된 컬렉션을 멀티스레드 환경에서 사용할 경우 동기화된 컬렉션으로 래핑하여 사용하는 것이 안전하다.
> * `ArrayList`, `HashSet`, `HashMap` 은 멀티스레드 환경에서 안전하지 않으므로 컬렉션을 Thread-safe 로 만들기 위해서는 `Collections.synchronizedXxx()`메소드를 이용해야 한다.

### 비동기화된 컬렉션을 동기화된 컬렉션으로 래핑

#### List 컬렉션
> `ArrayList` 를 `Collections` 클래스의 정적 메소드를 통해서 래핑하면 `ThreadSafe` 한 컬렉션을 만들 수 있다.
```java
List<T> list = Collections.synchronizedList(new ArrayList<T>());
```

* 비동기화된 컬렉션인 `ArrayList`를 `Collections`클래스의 정적메소드를 통해서 래핑시켜주면 `ThreadSafe`한 컬렉션을 만들 수 있다.\

#### Set 컬렉션
```java
Set<E> set = Collections.synchronizedSet(new HashSet<E>);
```

* 비동기화된 컬렉션인 `HashSet`를 `Collections`클래스의 정적메소드를 통해서 래핑시켜주면 `ThreadSafe`한 컬렉션을 만들 수 있다.

#### Map 컬렉션
```java
Map<K, V> map = Collections.synchronizedMap(new HashMap<K, V>));
```
* 
* 비동기화된 컬렉션인 `HashMap`를 `Collections`클래스의 정적메소드를 통해서 래핑시켜주면 `ThreadSafe`한 컬렉션을 만들 수 있다.


---
### 참조
* [이것이 자바다(한빛미디어)](http://www.yes24.com/Product/Goods/112208302)
* [[Java] 컬렉션 프레임워크](https://devbox.tistory.com/entry/Java-%EC%BB%AC%EB%A0%89%EC%85%98-%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)
