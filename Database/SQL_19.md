# SQL_19

## delete
> delete 는 테이블에서 데이터를 삭제할 때 사용하는 DML 명령어이다.

## delete 사용 방법
update 실습 때 사용했던 테이블을 사용하여 실습해본다.

![SQL_19_1.png](image%2FSQL_19%2FSQL_19_1.png)

* 사용법
```sql
delete from 테이블명 where 조건문 and 추가조건...;
```

* 실습
```sql
delete from insert_test where seq = 7;
```

![SQL_19_2.png](image%2FSQL_19%2FSQL_19_2.png)

위의 사진과 같이 `seq` 값이 7인 데이터가 삭제된 것을 확인 가능하다.

```sql
delete from insert_test where seq in(4,5,6);
```

![SQL_19_3.png](image%2FSQL_19%2FSQL_19_3.png)

위와 같이 `in`과 같은 연산자를 where 절에 사용해도 정상적으로 삭제 가능한 모습이다.

## 테이블 내 모든 데이터 삭제
테이블 내의 모든 데이터를 삭제하고 싶다면 아래와 같이 sql 문을 작성하면 된다.
```sql
delete from insert_test;
delete from insert_test where 1=1; 
```
이 때 `where 1=1`은 모든 조건을 참으로 인식하겠다는 뜻이며 select 문에서도 사용이 가능하다.

![SQL_19_4.png](image%2FSQL_19%2FSQL_19_4.png)

위와 같이 테이블 내의 모든 데이터가 삭제된 모습을 확인 가능하다.

## select 한 결과 delete
다른 테이블을 select 하여 조건을 불러와서 또 다른 테이블의 데이터를 삭제하는 방식이다.

* 실습
<br>실습을 위해 테이블을 2개 준비한다.

![SQL_19_5.png](image%2FSQL_19%2FSQL_19_5.png)

![SQL_19_6.png](image%2FSQL_19%2FSQL_19_6.png)

```sql
delete from insert_test where seq in (sleect seq from insert_test2);
```

위의 SQL 문은 `insert_test2`테이블에 있는 `seq`와 `insert_test`에 있는 `seq`값이 동일한 데이터를 삭제하게 한다.

![SQL_19_7.png](image%2FSQL_19%2FSQL_19_7.png)

위의 사진과 같이 `seq`값이 1,2,3 인 데이터들이 삭제된 것을 확인할 수 있다.

---
### 참조
* [https://stricky.tistory.com/282](https://stricky.tistory.com/282)
