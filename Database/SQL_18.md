# SQL_18

## update
> 기존의 데이터에서 row 내 특정 칼럼의 값을 수정하기 위한 작업
> 값을 추가하는 insert 와 달리 수정하는 작업이므로 row 수는 변화하지 않는다.

## update 사용 방법
기본적인 사용법은 아래와 같다.
```sql
update 테이블명 
set 컬럼명1 = '변경할 값',
    컬럼명2 = '변경할 값'
where 조건 = 조건값;
```

* 실습
<br>insert 실습 때 사용했던 데이터를 가져온 후 update 해본다.
```sql
select * from insert_test;
```

![SQL_18_1.png](image%2FSQL_18%2FSQL_18_1.png)

```sql
update insert_test set name = '채치수' where seq = 1;
```

![SQL_18_2.png](image%2FSQL_18%2FSQL_18_2.png)

위의 사진과 같이 where 절의 조건에 맞는 row 의 `name` 값이 변화한 것을 확인가능하다.

```sql
update insert_test set name = '채치수';
```

![SQL_18_3.png](image%2FSQL_18%2FSQL_18_3.png)

위의 사진과 같이 조건절을 넣지 않을 경우 set 뒤에 위치한 해당 칼럼값이 일괄 변경되는 것을 확인 가능하다.
<br> 또한 where 절 뒤에 `in`, `like` 와 같은 비교 연산자도 들어갈 수 있다.

```sql
update insert_test set name = '정대만' where seq in (1,2,3);
```

![SQL_18_4.png](image%2FSQL_18%2FSQL_18_4.png)

위와 같이 `in` 을 이용해 `seq` 의 값이 1,2,3 인 로우의 칼럼값만 변경 가능한 것을 확인 가능하다.

## update 문으로 복수의 칼럼값 변경
2개 이상의 칼럼값을 변경하기 위해서는 set 이후에 `,`로 변경할 칼럼값을 추가해주면 된다.

* 실습
```sql
update insert_test set name = '서태웅', cont = '반갑습니다' where seq in(1,2,3);
```

![SQL_18_5.png](image%2FSQL_18%2FSQL_18_5.png)

위의 사진과 같이 `seq` 값이 1,2,3 인 로우의 `name` 과 `cont` 값이 변경된 것을 확인할 수 있다.

---
### 참조
* [UPDATE 사용법, 쿼리로 데이터 변경 및 수정팁](https://jhnyang.tistory.com/entry/SQL-%EA%B8%B0%EC%B4%88-UPDATE-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%BF%BC%EB%A6%AC%EB%A1%9C-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%80%EA%B2%BD-%EB%B0%8F-%EC%88%98%EC%A0%95)
* [mysql update sql 독학 강의#18편 -sTricky](https://stricky.tistory.com/277)