# Dynamic Programming (동적 계획법)

## 동적 계획법
> * 동적 계획법은 어떤 문제가 여러 단계의 반복되는 부분 문제로 이루어져 있을 때, 각 단계에 있는 부분 문제의 답을 기반으로 전체 문제의 답을 구하는 방법이다.
> * 동적 계획법은 분할 정복과 달리 한 번 푼 적이 있는 부분 문제의 답을 다시 풀지 않도록 테이블 등에 저장한다.

### 동적 계획법 사용 조건
1. 겹치는 부분 문제
   * `동일한 작은 문제들이 반복`되는 형태의 문제여야 한다.
2. 최적 부분 구조
   * 최적 부분 구조란 `전체 문제의 최적해가 부분 문제의 최적해로부터 만들어지는 구조`를 말한다.

### 동적 계획법 동작방식
1. 문제를 부분 문제로 나눈다.
2. 가장 작은 부분 문제부터 해를 구한 뒤 테이블에 저장한다.
3. 테이블에 저장된 부분 문제의 해를 이용하여 점차적으로 상위 부분 문제의 최적해를 구한다.

### Top-Down 과 Bottom-Up
> DP 의 구현 방식에는 Top-Down 과 Bottom-Up 방식이 있다.
> 메모를 위해서 `dp`라는 배열을 만들었고 이것이 1차원이라 가정했을 때, `dp[0]`가 기저 상태이고 `dp[n]`을 목표 상태라고 가정한다.

* Top-Down 방식
   * `dp[n]`의 값을 찾기 위해 위에서 부터 바로 호출을 시작하여 `dp[0]`의 상태까지 내려간 다음 해당 결과 값을 재귀를 통해 전이시켜 재활용하는 방식이다.
   * 이전에 계산을 완료한 값은 저장된 내역을 꺼내서 활용하면 되며, 이 값을 `Memoization` 이라고 한다.
* Bottom-Up
   * 아래에서부터 계산을 수행하고 누적시켜서 전체 큰 문제를 해결하는 방식이다.
   * `dp[0]`부터 시작하여 반복문을 통해 점화식으로 결과를 내서 `dp[n]`까지 그 값을 전이시켜 재활용하는 방식이다.

### 피보나치 수 구하기
> 피보나치 수는 선행되는 수를 구해야만 다음 수를 구할 수 있으므로 최적 부분 구조를 갖추고 있다고 할 수 있다.

* 점화식

![Dynamic_Programming_1.png](image%2FDynamic_Programming%2FDynamic_Programming_1.png)

* 구현

![Dynamic_Programming_2.png](image%2FDynamic_Programming%2FDynamic_Programming_2.png)

위의 트리에서 확인 가능하듯이 트리의 하위 노드들이 중복되는 내용이 있다. 따라서 중복되는 부분해를 별도의 테이블에 저장하는 형태로 구현할 수 있다.

```java
public class fibonacci {
    public static int fib(int n) {
        if (n <= 1)
            return n;
        else
            return fib(n - 2) + fib(n - 1);
    }
    public static void main(String[] args) {
        System.out.println(fib(5));
    }
}
```
### LCS
> LCS 는 LCS는 주로 최장 공통 부분수열(Longest Common Subsequence)을 말하지만, 최장 공통 문자열(Longest Common Substring)을 의미하기도 한다.

![Dynamic_Programming_3.png](image%2FDynamic_Programming%2FDynamic_Programming_3.png)

### 최장 공통 문자열(LCS : Longest Common Substring)
> 두 문자열이 존재할 때 두 문자열의 연속된 공통 문자열 중에서 가장 긴 문자열을 의미한다.

#### 점화식
```java
if (i == 0 || j == 0) {
    LCS[i][j] = 0;
}
else if (str1.charAt(i) == str2.charAt(j)) {
    LCS[i][j] = LCS[i-1][j-1] + 1;
}
else {
    LCS[i][j] = 0;
}
```
#### 동작 방식
1. `문자열 A`와 `문자열 B`를 한글자 씩 비교해본다.
2. 두 문자가 다르다면 `LCS[i][j]`에 0을 표시한다.
3. 두 문자가 같다면 `LCS[i-1][j-1]`값을 찾아 `+1`을 해준다.
4. 두 문자열을 모두 비교할 때까지 위의 과정을 반복한다.
   * 비교가 모두 끝나고 가장 큰 값을 갖는 구간이 최장 공통 문자열이다.

    
### 최장 부분 공통 수열(LCS : Longest Common Subsequence)
> 두 문자열을 비교했을 때 공통적으로 나타나는 순서들 중에서 가장 긴 수열을 의미하며 최장 길이 문자열과 달리 연속하지 않아도 순서만 맞다면 상관없다.

#### 점화식

![Dynamic_Programming_4.png](image%2FDynamic_Programming%2FDynamic_Programming_4.png)

```java
if (i == 0 || j == 0) {
    LCS[i][j] = 0;
}
else if (str1.charAt(i) == str2.charAt(j)) {
    LCS[i][j] = LCS[i-1][j-1] + 1;
} 
else {
    LCS[i][j] = Math.max(LCS[i - 1][j], LCS[i][j - 1]);
}
```

#### 동작 방식
#### 최장 공통 부분수열의 길이 구하기
1. `문자열 A`와 `문자열 B`를 한글자 씩 비교해본다.
2. 두 문자가 다르다면 `LCS[i-1][j]`과 `LCS[i][j-1]` 중에 큰값을 표시한다.
3. 두 문자가 같다면 `LCS[i-1][j-1]`값을 찾아 `+1`을 해준다.
4. 두 문자열을 모두 비교할 때까지 위의 과정을 반복한다.

#### 최장 공통 부분수열 찾기
1. LCS 배열의 가장 마지막 값에서 시작한다.
   * 결과값을 저장할 `result` 배열을 준비한다.
2. `LCS[i-1][j]`과 `LCS[i][j-1]` 중 현재 값과 같은 값을 찾는다.
   * 현재 값과 같은 값이 있다면 해당 값으로 이동한다.
   * 현재 값과 같은 값이 없다면 `result`배열에 해당 문자를 넣고 LCS[i-1][j-1]로 이동한다.
3. `단계 2`를 반복하다가 `0`으로 이동하게 되면 종료한다. `result` 배열의 역순이 LCS 이다.

![Dynamic_Programming_5.png](image%2FDynamic_Programming%2FDynamic_Programming_5.png)

---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [다이나믹 프로그래밍](https://velog.io/@corone_hi/%EB%8B%A4%EC%9D%B4%EB%82%98%EB%AF%B9-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)
* [알고리즘 - Dynamic Programming(동적 계획법)](https://hongjw1938.tistory.com/47)
* [[알고리즘] 그림으로 알아보는 LCS 알고리즘 - Longest Common Substring와 Longest Common Subsequence](https://velog.io/@emplam27/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-LCS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Longest-Common-Substring%EC%99%80-Longest-Common-Subsequence)
* [가장 긴 공통 부분 수열 (LCS - Longest Common Subsequence) 알고리즘](https://aerocode.net/253)