# Sorting (정렬 알고리즘)
> * simple, slow
>    * [Selection sort (선택 정렬)](#selection-sort--선택-정렬-)
>    * [Bubble sort (버블 정렬)](#bubble-sort--버블-정렬-)
>    * [Insertion sort (삽입 정렬)](#insertion-sort--삽입-정렬-)
> * fast
>    * [Quick sort (퀵 정렬)](#quick-sort--퀵-정렬-)
>    * Merge sort (합병 정렬)
>    * Heap sort (힙 정렬)
> * O(n)
>    * Radix sort

## Selection sort (선택 정렬)
선택 정렬은 현재 위치에 들어갈 값을 찾아 정렬하는 배열로, 현재 위치에 저장 될 값의 크기가 작은지, 큰지에 따라서 최소 선택 정렬(Min-Selection sort)와 최대 선택 정렬(Max-Selection sort)로 구분된다.

 * 기본 로직
   1. 정렬되지 않은 index 의 맨 앞에서 부터, 이를 포함한 그 이후의 배열값 중 가장 작은 값을 찾아간다.
   2. 가장 작은 값을 찾으면, 그 값을 현재 인덱스의 값과 바꾼다.
   3. 하나의 원소만 남을 때까지 다음 인덱스에서 위 과정을 반복한다.

* 시간 복잡도
    * T(n) = (n-1)+(n-2)+ ··· +2+1 = O(n<sup>2</sup>)
    * 최악, 최선, 평균 항상 n(n-1)/2번의 비교 연산을 수행하므로 O(n<sup>2</sup>)

* 구현
```java
public class Selection {
    private static int[] input = {1, 2, 3, 4, 5};
    
    private static void Min_Selection_sort(int[] input, int length){
        int min;
        int tmp;
        for (int i = 0; i < length - 1; i++) {
            if (input[j] < input[min])
                min = j;
        }
        tmp = input[i];
        input[i] = input[min];
        input[min] = tmp;
    }
    private static void Max_Selection_sort(int[] input, int length) {
        int max;
        int tmp;
        for (int i = length - 1; i > 0; i--) {
            max = i;
            for (int j = i - 1; j >= 0; j--) {
                if (input[j] > input[max])
                    max = j;
            }
            tmp = input[i];
            input[i] = input[max];
            input[max] = tmp;
        }
    }
    public static void main(String[] args) {
        Min_Selection_sort(input, input.length);
        for (int a : input) {
            System.out.print(a + " ");
        }
        
        System.out.println();
        
        Max_Selection_sort(input, input.length);
        for (int a : input) {
            System.out.print(a + " ");
        }
    }
}
```
* 결과값
```java
1 2 3 4 5
5 4 3 2 1        
        
Process finished with exit code 0
```

## Bubble sort (버블 정렬)
버블 정렬은 매번 연속된 두개의 인덱스를 비교하여, 정한 기준의 값을 뒤로 넘겨 정렬하는 방법이다.

* 기본 로직
  1. 삽입 정렬은 두 번째 인덱스부터 시작하며, 현재 인덱스 값과, 바로 이전의 인덱스 값을 비교한다.
  2. 만약 이전 인덱스가 더 크면, 현재 인덱스와 바꿔준다.
  3. 현재 인덱스가 더 크면, 교환하지 않고 다음 두 연속된 배열값을 비교한다.
  4. 이를 (전체 배열의 크기 -  현재까지 순환한 바퀴 수)만큼 반복한다.

* 시간 복잡도
   * T(n) = (n-1)+(n-2)+ ··· +2+1 = O(n<sup>2</sup>)
   * 최악, 최선, 평균 항상 n(n-1)/2번의 비교 연산을 수행하므로 O(n<sup>2</sup>)

* 구현
```java
public class Bubble_sort {
    private static int[] input = {1, 2, 3, 4 ,5}
            bubble_sort(input, input.length);


    private static void bubble_sort(int[] input, int length) {
        int tmp;
        for (int i = length - 1; i > 0; i--)
            for (int j = 0; j < i; j++) {
                if (input[j] > input[j + 1]) {
                    tmp = input[j];
                    input[j] = input[j + 1];
                    input[j + 1] = tmp;
                }
            }
    }
}
```
* 결과값
```java
1 2 3 4 5
        
Process finished with exit code 0
```

## Insertion sort (삽입 정렬)
삽입 정렬은 현재 위치에서, 그 이하의 배열들을 비교하여 자신이 들어갈 위치를 찾아, 그 위치에 삽입하는 배열 알고리즘이다.

* 기본 로직
   1. 삽입 정렬은 두 번째 인덱스부터 시작한다. 현재의 인덱스는 별도의 변수에 저장해주고, 비교 인덱스를 현재 인덱스의 -1로 잡는다.
  2. 별도로 저장해 둔 삽입을 위한 변수와, 비교 인덱스의 배열값을 비교한다.
  3. 삽입 변수의 값이 더 작으면 현재 인덱스로 비교 인덱스의 값을 저장해주고, 비교 인덱스를 -1 하여 비교를 반복한다.
  4. 만약 삽입 변수가 더 크면, 비교 인덱스의 +1 위치에 삽입 변수를 저장한다.

* 시간 복잡도
   * 최악의 경우(역으로 정렬되어 있는 경우) 시간 복잡도는 T(n) = (n-1)+(n-2)+ ··· +2+1 = O(n<sup>2</sup>)
   * 최선의 경우(이미 정렬되어 있는 경우) O(n)의 시간 복잡도
* 구현
```java
public class Insertion_sort {
    private static int[] input = {1, 2, 3, 4, 5};

    public static void main(String[] args) {
        insertion_sort(input, input.length);
        for (int a : input) {
            System.out.print(a + " ");
        }
    }
    
    private static void insertion_sort(int[] input, int length) {
        int tmp;
        for(int i = 1; i < length; i++) {
            for(int j = i; j > 0; j--) {
                if(input[j-1] > input[j]){
                    tmp = input[j - 1];
                    input[j - 1] = input[j];
                    input[j] = tmp;
                }
            }
        }
    }
}
```
* 결과값
```java
1 2 3 4 5

Process finished with exit code 0
```

## Quick sort (퀵 정렬)
* 퀵 정렬은 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행속도를 자랑하는 정렬방법이다.
* 합병 정렬과 달리 리스트를 비균등하게 분할하는 방법이다. 

* 기본 로직
  1. 리스트 안에 있는 한 요소를 선택한다. 이 때 고른 원소를 피벗(pivot) 이라고 한다
  2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고, 피벗보다 큰 요소들은 모두 피벗의 오른 쪽으로 옮겨진다.
  3. 피벗을 제외한 왼쪽, 오른쪽 리스트를 다시 정렬한다
     * 분할된 부분 리스트에 대하여 순환 호출을 이용해 정렬을 반복한다.
     * 부분 리스트에서도 새로 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.
  4. 부분 리스트들이 더이상 분할이 불가능할 때까지 반복한다.
     * 리스트의 크기가 0이나 1이 될 때까지 반복한다.

* 시간 복잡도
   * 최선은 항상 절반으로 분할되는 경우이다.
      * T(n) = 2T(n/2) + Θ(n) = Θ(nlog<sub>2</sub>n) 
   * 최악은 항상 한 쪽은 0개, 다른 쪽은 n-1개로 분할되는 경우와 이미 정렬된 입력 데이터의 마지막 원소를 피벗으로 선택하는 경우이다.
      * T(n) = Θ(n<sup>2</sup>) 
   * 평균 시간 복잡도 O(nlog<sub>2</sub>n)

* 구현

```java
public class Quick_sort {
  private static void quicksort(int[] arr, int start, int end) {
    int part = divide(arr, start, end);
    if (start < part - 1) {
      quicksort(arr, start, part - 1);
    }
    if (end > part) {
      quicksort(arr, part, end);
    }
  }

  private static int divide(int[] arr, int start, int end) {
    int pivot = arr[(start + end) / 2];
    while (start <= end) {
      while (arr[start] < pivot) {
        start++;
      }
      while (arr[end] > pivot) {
        end--;
      }
      if (start <= end) {
        swap(arr, start, end);
        start++;
        end--;
      }
    }
    return start;
  }

  private static void swap(int[] arr, int start, int end) {
    int tmp = arr[start];
    arr[start] = arr[end];
    arr[end] = tmp;
  }

  public static void main(String[] args) {
    int[] arr = {4,2,5,1,6,8,7,3};
    quicksort(arr,0,arr.length-1);
    for(int v : arr){
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

---
참조
* [기본 정렬 알고리즘(Sorting Algoritm) 요약 정리](https://hsp1116.tistory.com/33)
* [권오흠 교수님의 (알고리즘) 제3강 기본적인 정렬 알고리즘](https://www.youtube.com/watch?v=0dG7xTt5IfQ&list=PL52K_8WQO5oUuH06MLOrah4h05TZ4n38l&index=9)
* [퀵 정렬(Quick sort) 이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)