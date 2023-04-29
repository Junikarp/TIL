# Divide and Conquer (분할 정복)

## 분할 정복
> 분할 정복은 하나의 문제를 더 이상 나눌 수 없을 때까지 나누고, 나뉜 문제를 각각 풀어 전체 문제의 답을 얻는 기법이다.

![Divide_and_Conquer_1.png](image%2FDivide_and_Conquer%2FDivide_and_Conquer_1.png)

분할 정복은 일반 재귀호출과 비슷해 보이지만 하위 문제를 거의 동일한 크기로 나눠 풀이한다는 점에서 차이가 있다.

### 분할 정복 구성요소
1. 분할(Divide) 
   * 문제가 분할 가능한 경우 2개 이상의 하위 문제로 나눈다.
2. 정복(Conquer) 
   * 하위 문제가 여전히 분할 가능한 상태라면 하위 집합에 대해 `단계 1`을 수행한다.
   * 그렇지 않은 경우 하위 문제를 푼다.
3. 결합(Combine)
   * `단계 2`를 통해 구한 답을 취합한다.

### 병합 정렬
> 병합 정렬은 분할 정복을 이용한 대표적인 정렬방법 중 하나이다.

![Divide_and_Conquer_2.png](image%2FDivide_and_Conquer%2FDivide_and_Conquer_2.png)

#### 구현
* MergeSort.java
```java
public class Mergesort {
    public void mergeSort (int[] arr, int left, int right){
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(arr, left, mid);
            mergtSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }
    public void merge (int[] arr, int left, int mid, int right){
        int L = left;
        int R = mid+1;
        int k = left;
        int[] tmp = new int[arr.length];
        
        while (L <= mid && R <= right) {
            if (arr[L]<=arr[R]) {
                tmp[k++] = arr[L++];
            }
            else {
                tmp[k++] = arr[R++];
            }
        }
        if(L > mid) {
            for (int i = R; i <= right; i++) {
                tmp[k++] = arr[i];
            }
        }
        else {
            for (int i = L; i <= mid; i++) {
                tmp[k++] = arr[i]; 
            }
        }
        for (int i = left; i <= right; i++) {
            arr[i] = tmp[i];
        }
    }
    public static void main(String[] args) {
        int[] arr = {4, 2, 5, 1, 6, 8, 7, 3};
        mergeSort(arr, 0, arr.length-1);
        for(int v : arr) {
            System.out.print(v+" ");
        }
    }
}
```
* 결과값
```agsl
1 2 3 4 5 6 7 8 

Process finished with exit code 0
```

병합 정렬에 대한 더 자세한 내용은 [링크](https://github.com/Junikarp/TIL/blob/main/Algorithm/Sorting.md#merge-sort--%EB%B3%91%ED%95%A9-%EC%A0%95%EB%A0%AC-)를 통해 확인 가능하다.

---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [[종만북] 분할 정복(Divide and Conquer)](https://velog.io/@sossont/%EC%A2%85%EB%A7%8C%EB%B6%81-%EB%B6%84%ED%95%A0-%EC%A0%95%EB%B3%B5Divide-and-Conquer)