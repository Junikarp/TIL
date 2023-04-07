## Recursion

* Recursion 은 자기 자신을 호출하는 함수이다.
---
아래의 코드는 Recursion 함수의 예시이다.
```java
public class Code01{
   public static void main(String [] args) {
      func();
   }

   public static void func() {
      System.out.println("Hello...");
      func();
   }
}
```
위 코드를 실행시켰을 때의 결과값은 Hello...를 끝없이 반복하는 순환형태이다.

```agsl
Hello...
Hello...
Hello...
Hello...
Hello...
```
---
다시 아래의 코드를 한번 살펴보자.

```java
public class Code02 {
    public static void main(String[] args) {
        int n = 4;  
        func(n);
    }
    
    public static void func(int k) {
       if(k<=0)
           return;   // Base case
       else {
           System.out.println("Hello...");
           fucn(k-1); // Recursive case
       }
    }
}
```
```
Hello...
Hello...
Hello...
Hello...

Process finished with exit code 0
```
위의 코드와 같은 적절한 구조의 recursion 을 구성한다면 무한루프에 빠지는 것을 방지 할 수 있으며 아래의 조건이 필요하다.
* Base case : 적어도 하나의 recursion 에 빠지지 않는 경우가 존재하여야 한다.
```java
if(k<=0)
    return;
```
* Recursive case: recursion 을 반복하다 보면 결국 Base case 로 수렴해야 한다.
```java
func(k-1); 
```

---
### 참조

* [권오흠 교수님의 [알고리즘] 제1-1강 Recursion의 개념과 기본 예제들 (1/3) 참조 ](https://www.youtube.com/watch?v=ln7AfppN7mY)
