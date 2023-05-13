# String Search (문자열 탐색)

## 문자열 탐색 알고리즘
> 문자열 탐색 알고리즘은 말 그대로 문자열에서 패턴을 찾아내 문자열을 탐색하는 알고리즘이다.

### 고지식한 탐색 알고리즘
> 어떠한 패턴이 있을때 처음부터 끝까지 순차적으로 비교하여 패턴을 찾아내는 탐색 방법이다.

![Stirng_Search_1.png](image%2FString_Search%2FStirng_Search_1.png)

고지식한 탐색은 `본문의 길이를 N`, `패턴의 길이를 M` 이라고 할 때 최악의 경우 `NxM`번의 비교를 수행한다.

### 카프-라빈 알고리즘
> 카프-라빈 알고리즘은 문자열 탐색을 위해 `패턴의 해시값`과 본문 내에 있는 `하위 문자열의 해시값`만 비교하는 문자열 탐색 방법이다.

![String_Search_2.png](image%2FString_Search%2FString_Search_2.png)

위와 같이 하위 문자열의 해시값을 비교하는 방식으로 탐색한다. 

![String_Search_3.png](image%2FString_Search%2FString_Search_3.png)

이 때 i+1 번째 문자열을 해싱할 때, i 번째 문자열을 이용하여 해싱하는 방식을 사용해 기존의 해싱보다 빠른 속도로 탐색이 가능하다.

### KMP 알고리즘
> KMP 알고리즘은 접두부와 접미부를 이용하여 비교하지 않아도 되는 부분은 무시하고 필요한 부분만 비교를 수행하는 탐색 방법이다.

* 접두부와 접미부

![String_Search_4.png](image%2FString_Search%2FString_Search_4.png)

접두부는 문자열의 머리 부분, 접미부는 문자열의 꼬리 부분을 의미한다.

* 경계

![String_Search_5.png](image%2FString_Search%2FString_Search_5.png)

위와 같이 접두부와 접미부가 같은 상황에서 `접두부와 접미부의 쌍`을 `경계`라고 부른다.

#### 동작 순서
    
1. 본문이 되는 문자열과 찾으려는 패턴을 처음에 배치한다.

![String_Search_6.png](image%2FString_Search%2FString_Search_6.png)

2. 불일치한 부분이 있다면, 불일치한 부분을 제외한 직전까지 일치하는 패턴에서 최대 길이의 경계를 찾는다.

![String_Search_7.png](image%2FString_Search%2FString_Search_7.png)

3. 불일치 부분을 제외하고 본문과 일치하는 패턴에서 경계를 찾는다. (경계가 두가지 이상이라면 길이가 최대가 될 때를 선택한다.)

![String_Search_8.png](image%2FString_Search%2FString_Search_8.png)

4. 선택한 경계에서 접두부와 접미부를 파악하고 찾으려는 패턴을 접미부의 시작 문자열까지 이동시킨다.

![String_Search_9.png](image%2FString_Search%2FString_Search_9.png)

그 후 `단계 1`부터 다시 반복한다.

---
### 참조
* [이것이 자료구조 + 알고리즘이다 with C언어(박상현)](http://www.yes24.com/Product/Goods/111362116)
* [문자열 검색 알고리즘 (String Matching Algorithm) : Brute Force ,KMP Algorithm](https://velog.io/@arittung/String-Matching-Algorithm-BruteForce-KMP)