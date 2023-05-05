# Backtracking (백트래킹)

## 백트래킹
> * 백트래킹은 여러 후보해 중에서 특정 조건을 충족시키는 모든 해를 찾는 알고리즘이다. 
> * 다시말해 해를 찾는 도중에 해가 아니라면, 되돌아가서 다시 해를 찾아가는 방법이다.
> * 백트래킹에서는 해를 찾는 비용을 줄이기 위해 방문할 노드의 수를 최소화하는 것이 중요하다.

![Backtracking_1.png](image%2FBacktracking%2FBacktracking_1.png)

### 백트래킹 동작방식
> 백트래킹 문제들은 다양한 후보해를 가지며, 이 후보해들은 부분해로 이루어져 있어 트리 형태로 표현 가능하다.

1. 해를 찾아가는 과정은 뿌리에서 시작한다.
   * 이 때 뿌리도 하나의 부분해이다.
2. 현재 위치한 부분해에서 선택 가능한 다음 부분해의 목록을 얻는다.
3. `단계 2`에서 얻은 목록의 부분해들을 하나씩 방문한다.
4. 방문한 부분해가 `해가 될 수 있는 조건`을 만족시키는지 확인한다.
   * 만족시킨다면 그자리에서 `단계 2`와 `단계 3`을 수행한다.
   * 만족시키지 못한다면 그 이전 부분해로 돌아 나와 다른 부분해를 시도한다.
5. 최종해를 얻을 때까지 또는 모든 경우의 수를 확인해도 해가 없음을 확인할 때까지 `단계 2`에서 `단계 4`를 반복한다.

### N-Queen 문제
> 백트래킹으로 풀이 가능한 대표적인 문제 중의 하나로 `N*N`체스판에 N개의 퀸을 서로 공격할 수 없도록 배치하는 문제이다.

![Backtracking_2.png](image%2FBacktracking%2FBacktracking_2.png)

#### N-Queen 구현
구현에서는 실제 체스판과 같이 N값을 8로 설정하였다.

```java
public class NQueen {
	static int N;
	static int map[][];
	static boolean visit[][];
	static int result = 0;

	static int queen[]; // queen[행] = 열

	public static void main(String[] args) {
		
        N = 8;
		queen = new int[N];
		backTracking(0);
		System.out.println(result);
	}
    
	private static void backTracking(int idx) {
		if (idx == N ) {
			result++;
			return;
		}
		for (int i = 0; i < N; i++) {
			queen[idx] = i;
			if (idx == 0 || check(idx))
				backTracking(idx + 1);
		}
	}

	public static boolean check(int check) {
		for (int j = 0; j < check; j++) {
			if (queen[j] == queen[check] ||check - j == Math.abs(queen[j] - queen[check]))
				return false;
		}
		return true;
	}
}
```
* 결과값
```java
92
```

---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [N-Queen 알고리즘](http://sooyoung32.github.io/dev/2016/03/14/n-queen-algorithm.html)