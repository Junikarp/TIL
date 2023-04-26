# Minimum Spanning Tree(최소 신장 트리)

## 최소 신장 트리
> `신장 트리`는 가장 적은 간순 수로 그래프의 모든 정점을 연결하는 트리를 의미한다. 간선에 가중치가 주어질 때 여러 간선 중 가중치의 합이 최소가 되는 간선만 남긴 신장 트리를 `최소 신장 트리`라고 부른다.

![Minimum_Spanning_Tree_1.png](image%2FMinimum_Spanning_Tree%2FMinimum_Spanning_Tree_1.png)

위와 같이 최소 신장트리는 각 구성요소가 연결되어 있고, 간선에 가중치가 실려있는 `연결된 가중치 그래프`로부터 만들어진다.

### 최소 신장 트리 알고리즘
> 최소 신장 트리를 만들기 위한 알고리즘에는 `프림 알고리즘`과 `크루스칼 알고리즘`이 있다.

#### 프림 알고리즘
1. 그래프와 최소 신장 트리를 준비한다. 
   * 이 때의 최소 신장 트리는 노드가 하나도 없는 상태이다.
2. 그래프에서 임의의 정점을 시작 정점으로 선택하여 최소 신장 트리의 뿌리 노드로 삽입한다.
3. 최소 신장 트리에 삽입된 정점들과 이 정점들의 모든 인접 정점 사이에 있는 간선의 가중치를 조사한다.
   * 간선 중에 가장 가중치가 작은 것을 골라 이 간선에 연결된 인접 정점을 최소 신장 트리에 삽입한다.
   * 새로 삽입되는 정점은 최소 신장 트리에 삽입된 기존 노드와 사이클을 형성해서는 안된다.
4. `단계 3`을 반복하다가 최소 신장 트리가 그래프의 모든 정점을 연결하게 되면 알고리즘을 종료한다.

![Minimum_Spanning_Tree_2.png](image%2FMinimum_Spanning_Tree%2FMinimum_Spanning_Tree_2.png)














---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [[알고리즘] Prim 알고리즘 이란](https://gmlwjd9405.github.io/2018/08/30/algorithm-prim-mst.html)
* [[알고리즘] Kruskal 알고리즘 이란](https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html)