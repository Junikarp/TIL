# Graph

## 그래프(Graph)
  * 그래프는 연결되어 있는 원소간의 관계를 표현한 자료구조로 연결할 객체를 나타내는 `정점(Vertext)`과 정점을 연결하는 `간선(Edge)`의 집합으로 구성된다.
  * 간선으로 연결된 두 정점을 `인접(이웃 관계)`했다고 말하며, 이웃 관계인 정점이 만드는 길을 `경로`, 어느 경로가 하나의 정점을 두번 이상 거친다면 `사이클`이라고 부른다.

![Graph_1.png](image%2FGraph%2FGraph_1.png)

### 그래프의 종류

![Graph_2.png](image%2FGraph%2FGraph_2.png)

1. 무방향성 그래프
   * 간선의 방향이 없는 그래프이다.
2. 방향성 그래프
   * 무방향성 그래프와 반대로 간선의 방향이 있는 그래프이다.
3. 가중치 그래프
   * 간선에 가중치값이 존재하는 그래프이다.
4. 루트없는 트리
   * 간선을 통해 정점 간에 이어지는 방법이 한가지뿐인 그래프를 의미한다.
5. 이분 그래프
   * 그래프의 정점을 겹치지 않도록 두 그룹으로 나눈 후 다른 그룹끼리만 간선이 존재하도록 분할 가능한 그래프이다.
6. 사이클이 없는 방향 그래프
   * 정점에서 출발해 자기 자신으로 돌아오는 사이클이 없는 그래프이다.

### 그래프의 표현방법

#### 1. 인접 행렬
> 인접 행렬은 정점끼리의 인접 관계를 나타내는 행렬로 그래프의 정점 수를 N 이라고 했을 때 N x N 크기의 행렬을 만들어 한 정점과 다른 정점이 인접시 행렬의 각 원소를 1로 표시하고 그렇지 않다면 0으로 표시하는 방법이다.

![Graph_3.png](image%2FGraph%2FGraph_3.png)

방향성 그래프의 경우 행렬에서 `(출발 정점, 도착 정점)`의 위치를 1로 바꾸어주면 된다.
위의 그래프를 예시로 들면 정점 `1`에서 연결된 `(1,2)`, `(1,3)`, `(1,4)`, 정점 `2`에서 연결된 `(2,3)`, 정점 `4`에서 연결된 `(4,3)` 을 1로 바꾸어주면 된다.

![Graph_4.png](image%2FGraph%2FGraph_4.png)

무방향성 그래프의 경우에는 양쪽 방향으로 향하는 위치를 1로 바꿔준다고 생각하면 간단하다. 또한 좌상단에서 우하단으로 향하는 대각선에 대해서 대칭인 성질을 가지고있다.

* 구현
```java
public class Graph {
   private int N; // 노드의 수
   private int[][] Matrix; // 인접 행렬

   public Graph(int N) {
      this.N = N;
      Matrix = new int[N][N];
   }

   // 그래프에서 노드 u와 v를 연결
   public void addEdge(int u, int v) {
      Matrix[u][v] = 1;
      Matrix[v][u] = 1; // 무방향성 그래프에서만 사용 (빙향성 그래프에서는 없어도 됨)
   }

   // 인접 행렬 출력
   public void printMatrix() {
      for (int i = 1; i < N; i++) {
         for (int j = 1; j < N; j++) {
            System.out.print(Matrix[i][j] + " ");
         }
         System.out.println();
      }
   }

   public static void main(String[] args) {
      Graph g = new Graph(5);
      g.addEdge(1, 2);
      g.addEdge(1, 3);
      g.addEdge(1, 4);
      g.addEdge(2, 3);
      g.addEdge(4, 3);

      g.printMatrix();
   }
}
```
* 출력결과
```agsl
0 1 1 1 
1 0 1 0 
1 1 0 1 
1 0 1 0 
```

#### 2. 인접 리스트
> 인접 리스트는 그래프 내 각 정점의 인접 관계를 표현하는 리스트로 각 정점이 자신과 인접한 모든 정점의 목록을 리스트로 관리하도록 하는 기법이다.

![Graph_5.png](image%2FGraph%2FGraph_5.png)

방향성 그래프의 경우 출발 정점 위치에 연결된 정점들을 리스트 형태로 연결하면 된다.

![Graph_6.png](image%2FGraph%2FGraph_6.png)

무방향성 그래프의 경우 인접 행렬 때와 마찬가지로 양방향으로 연결되어 있다고 생각하면 간단하게 인접 리스트를 만들 수 있다.

* 구현
```java
public class Graph {
   private int N; // 노드의 수
   private List<List<Integer>> adjList; // 인접 리스트

   public Graph(int N) {
      this.N = N;
      adjList = new ArrayList<>(N);

      for (int i = 0; i < N; i++) {
         adjList.add(new ArrayList<>());
      }
   }

   // 그래프에서 노드 u와 v를 연결
   public void addEdge(int u, int v) {
      adjList.get(u).add(v);
      adjList.get(v).add(u); // 무방향성 그래프에서만 사용 (빙향성 그래프에서는 없어도 됨)
   }

   // 인접 리스트를 출력
   public void printList() {
      for (int i = 1; i < N; i++) {
         System.out.print(i + ": ");
         for (int j = 0; j < adjList.get(i).size(); j++) {
            System.out.print(adjList.get(i).get(j) + " ");
         }
         System.out.println();
      }
   }

   public static void main(String[] args) {
      Graph g = new Graph(5);
      g.addEdge(1, 2);
      g.addEdge(1, 3);
      g.addEdge(1, 4);
      g.addEdge(2, 3);
      g.addEdge(4, 3);

      g.printList();
   }
}
```
* 출력 결과
```agsl
1: 2 3 4 
2: 1 3 
3: 1 2 4 
4: 1 3 
```

#### 인접 행렬 vs 인접 리스트
 * 인접 행렬은 정점 간의 인접 여부를 빠르게 알 수 있다는 장점이 있지만, 인접 관계를 행렬형태로 저장하기 위해 사용하는 메모리의 양이 `정점의 크기 x N^2` 만큼 커진다는 단점이 존재한다.
 * 인접 리스트는 간선의 삽입이 빠르고 리스트에 사용되는 메모리가 적다는 장점이 있지만, 정점 간의 인접 여부를 알아내기 위해 인접 리스트를 순차탐색해야 한다는 단점이 있다.

### 참조
* [[자료구조 1] 그래프(Graph) 이해하기](https://laboputer.github.io/ps/2017/09/29/graph/)
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [[그래프] 인접 행렬과 인접 리스트](https://sarah950716.tistory.com/12)
