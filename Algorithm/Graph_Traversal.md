# Graph Traversal
> [Graph 에 대한 내용](https://github.com/Junikarp/TIL/blob/main/Data_Structure/08_Graph.md)

## 그래프 순회 (Graph Traversal)
> 그래프의 순회는 그래프의 모든 정점을 방문하는 작업으로 대표적으로 `BFS` 와 `DFS` 가 있다.

### 깊이 우선 탐색 (DFS: Depth First Search)
> 깊이 우선 탐색은 길이 나오지 않을 때까지 그래프의 정점을 타고 깊이 들어가다가 더 이상 방문해왔던 정점 이외의 다른 이웃이 없는 정점을 만나면 뒤로 돌아와 다른 경로로 방문을 재개하는 방식이다.

#### DFS 동작 방식
1. 시작 정점을 밟은 후 이 정점을 `방문했음` 상태로 표시한다.
2. 이 정점과 이웃 정점 중에서 아직 방문하지 않은 곳을 선택하여 이를 시작 정점으로 삼고 다시 깊이우선 탐색을 시작한다. (`단계 1`을 반복)
3. 더 이상 방문하지 않은 이웃 정점이 없다면 이전 정점으로 돌아가서 `단계 2`를 수행한다.
4. 이전 정점으로 돌아가도 더 이상 방문할 이웃 정점이 없다면 그래프의 모든 정점을 방문한 것이므로 탐색을 종료한다.

![Graph_Traversal_1.png](image%2FGraph_Traversal%2FGraph_Traversal_1.png)

* DFS 구현
```java
public class DFS {
    public static void dfs(ArrayList<Integer>[] graph, boolean[] visited, int start) {
        visited[start] = true; // 시작 노드를 방문한 것으로 체크
        System.out.print(start + " "); // 현재 노드 출력

        for (int i = 0; i < graph[start].size(); i++) {
            int next = graph[start].get(i);
            if (!visited[next]) {
                dfs(graph, visited, next); // 다음 노드 재귀 호출
            }
        }
    }

    public static void main(String[] args) {
        int n = 5; // 노드 개수
        ArrayList<Integer>[] graph = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<Integer>();
        }

        // 그래프 구성 예시
        graph[0].add(1);
        graph[0].add(2);
        graph[1].add(2);
        graph[2].add(3);
        graph[2].add(4);
        graph[3].add(4);

        boolean[] visited = new boolean[n];
        dfs(graph, visited, 0); // 시작 노드는 0
    }
}
```
* 출력 결과
```asgl
0 1 2 3 4 
```

### 너비 우선 탐색(BFS: Breadth First Search)
> 너비 우선 탐색은 한 단계씩 깊이를 더해가며 해당 깊이의 모든 정점을 방문하다가 더 이상 방문할 정점이 없을때 탐색을 종료하는 탐색 방법이다. 

#### BFS 동작방식
1. 시작 정점을 `방문했음`으로 표시하고 큐에 삽입한다.
2. 큐로부터 정점을 제거하고, 제거한 정점의 인접 정점 중에서 아직 방문하지 않은 곳을 `방문했음`으로 표시하고 큐에 삽입한다.
3. 큐가 비면 탐색이 끝난 것이므로, 큐가 빌 때까지 `단계 2`를 반복한다.

![Graph_Traversal_2.png](image%2FGraph_Traversal%2FGraph_Traversal_2.png)

* BFS 구현
```java
public class BFS {

    public static void main(String[] args) {

        int[][] graph = {
                { 0, 1, 1, 0, 0 },
                { 0, 0, 1, 0, 0 },
                { 0, 0, 0, 1, 1 },
                { 0, 0, 0, 0, 1 },
                { 0, 0, 0, 0, 0}};

        bfs(graph, 0);
    }

    public static void bfs(int[][] graph, int start) {
        int n = graph.length; // 그래프의 정점 개수
        boolean[] visited = new boolean[n]; // 방문 여부를 저장할 배열

        Queue<Integer> queue = new LinkedList<>(); // 큐 생성
        visited[start] = true; // 시작점 방문 표시
        queue.offer(start); // 큐에 시작점 추가

        while (!queue.isEmpty()) { // 큐가 빌 때까지 반복
            int current = queue.poll(); // 큐에서 정점 하나 꺼내기
            System.out.print(current + " ");

            for (int i = 0; i < n; i++) { // 인접 정점 탐색
                if (graph[current][i] == 1 && !visited[i]) { // 인접 정점이면서 방문하지 않은 정점인 경우
                    visited[i] = true; // 방문 표시
                    queue.offer(i); // 큐에 추가
                }
            }
        }
    }
}
```
* 출력 결과
```agsl
0 1 2 3 4
```


---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [[알고리즘] 깊이 우선 탐색(DFS)이란](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
* [[알고리즘] 너비 우선 탐색(BFS)이란](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)