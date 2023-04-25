# Topology Sort(위상 정렬)

## 위상 정렬
> 위상 정렬은 순서가 있는 작업을 차례로 수행할 때 순서를 정해주기 위해 사용하는 알고리즘이다.

### DAG (Directed Acyclic Graph)

![Topology_Sort_1.png](image%2FTopology_Sort%2FTopology_Sort_1.png)

모든 그래프를 위상 정렬 할 수 있는 것은 아니며, 위상을 정렬하려면 아래의 두가지 조건을 만족한 그래프가 있어야만 한다.

1. 그래프에 방향성이 있어야한다.
2. 그래프내에 사이클이 존재하지 않아야 한다.

위의 두가지 조건을 만족한 그래프를 DAG 라고 부른다.

### 위상 정렬 동작방식
1. 리스트를 하나 준비한다. 
2. 그래프에서 진입 간선이 없는 정점을 리스트에 추가하고 해당 정점 자신과 진출 간선을 제거한다. (진입 간선이 없는 정점은 큐에 넣어 관리한다.) 
3. 모든 정점에 대해 `단계 2`를 반복하고 그래프 내에 정점이 남아 있지 않으면 정렬을 종료한다. 이때 리스트에는 위상정렬된 그래프가 저장된다.

이 때 정점으로 들어가는 간선을 `진입 간선`, 정점에서 나오는 간선을 `진출 간선`이라고 부른다.

![Topology_Sort_2.png](image%2FTopology_Sort%2FTopology_Sort_2.png)


---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [[알고리즘] 위상 정렬(Topological Sort)이란](https://gmlwjd9405.github.io/2018/08/27/algorithm-topological-sort.html)


