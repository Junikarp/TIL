# SQL_12

## Ansi SQL
> RDBMS 마다 서로 조금씩 다른 SQL 문법을 가지는데, 모든 RDBMS 에서 통용되는 문법

## 카티션 곱(Cartesian Product)
> where 절이나 on 절에 조건을 주지않고 join 을 수행하게 되면 카티션 곱이 수행된다.
> <br>Ansi SQL 에서는 cross join 이라고도 부른다.
> <br> 카티션 곱 join 의 결과는 from 절에서 참조한 테이블들의 행 개수를 각각 모두 곱한 값만큼의 결과가 출력된다.

## 카티션 곱의 활용
> 카티션곱이 사용되는 경우는 크게 아래와 같다.
* 데이터의 대량 복제가 필요할 때
* 특정 데이터의 튜플만 복제되어야 할 때
* 연결고리가 없는 두 테이블의 데이터를 무작위로 합쳐야할 때

## 카티션 곱 SQL 작성
```sql
select * from major;
```

![SQL_12_1.png](image%2FSQL_12%2FSQL_12_1.png)

```sql
select * from professor;
```

![SQL_12_2.png](image%2FSQL_12%2FSQL_12_2.png)

위의 `major` 테이블과 `professor` 테이블은 각각 5건과 10건의 데이터를 가지고 있다.

```sql
# MySQL
select m.major_id,
       m.major_title,
       p.prfs_id,
       p.name
from major m,  professor p;

# Ansi SQL
select m.major_id,
       m.major_title,
       p.prfs_id,
       p.name
from major m cross join professor p;    
```

![SQL_12_3.png](image%2FSQL_12%2FSQL_12_3.png)

위의 결과값에서 볼 수 있듯이 두 테이블의 카티션 곱 결과값이 5*10 = 50 건이 출력된 것을 확인 가능하다.
<br> 이 때, m 과 p 는 각각 major 테이블과 professor 테이블의 alias 명이다.
<br> 또한 모든 교수이름 하나당 5개의 과가 연결되어 있는 모습을 통해 카티션 곱이 어떤 방식으로 결과를 출력하는지 확인 가능하다.


---
### 참조
* [Cartesian Product 카티션 곱 ansi SQL 문법 12편 -sTricky](https://stricky.tistory.com/245)