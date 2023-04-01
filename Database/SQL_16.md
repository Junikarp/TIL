# SQL_16

## 서브 쿼리 (sub query)
> 서브 쿼리란 SQL 내에서 또 다른 select 문을 사용하는 문법을 의미한다.
> <br> 서브 쿼리를 사용하면 SQL 에서 데이터를 폭넓게 사용할 수 있는 이점이 존재하며, 복잡한 쿼리를 단순화 할 수 있다.
> <br> 하지만 join 을 이용하여 풀 수 있는 문제를 서브쿼리로 풀면 성능에 악영향을 줄 수 있다.

![SQL_16_1.png](image%2FSQL_16%2FSQL_16_1.png)

## 서브 쿼리 사용시 주의사항
* 서브쿼리를 괄호로 감싸서 사용한다.
* 서브쿼리는 단일 행 혹은 복수 행 비교 연산자와 함께 사용 가능하다.
* 서브쿼리에서는 order by 를 사용하지 못한다.

## 서브 쿼리 종류
|  사용 위치   |               명칭               |
|:--------:|:------------------------------:|
| select 절 | 스칼라 서브쿼리<br/>(Scalar Subquery) |
|  from 절  |    인라인 뷰<br/>(Inline view)     |
| where 절  |        중첩 서브쿼리 or 서브쿼리         |

## 스칼라 서브쿼리
> 스칼라 서브쿼리는 select 절에서 사용하는 서브쿼리이다.
```sql
select
    (select B.name
     from dept B
     where b.dept_no = a.emp_no)
from emp_no A
```
스칼라 서브 쿼리는 select 로 시작하고 다시 `(`괄호를 열어서 select 절(스칼라 서브쿼리)이 들어간다.
<br> 이 때 스칼라 서브쿼리의 where 절에 메인쿼리의 칼럼 값이 들어가게 되며 그 값으로 스칼라 서브쿼리에서 검색된 값이 출력값으로 나온다.

* 실습
학생 테이블과 학과 테이블에서 스칼라 서브쿼리를 통해 학생별 학과명을 출력해본다.
```sql
select name                            as 학생이름,
       (select major_title
        from major b
        where b.major_id = a.major_id) as 학과명
from student a;
```

![SQL_16_2.png](image%2FSQL_16%2FSQL_16_2.png)

이 때 서브쿼리에서 하나 이상의 행이 리턴되면 오류가 생긴다.

## 인라인 뷰 (Inline view)
> 인라인 뷰는 from 절에서 사용되는 서브쿼리이다.
> <br>select 절에서 사용하는 것과 마찬가지로 from 절에 `(`괄호를 열고 그안에 select 절을 넣으면 된다.
> <br> 하나의 테이블로 생각하고 사용하면 된다.

* 실습

```sql
select a.name        as 학생이름,
       b.major_title as 학과명
from student a, (select major_title, major_id
                 from major) b
where a.major_id = b.major_id;
```

![SQL_16_3.png](image%2FSQL_16%2FSQL_16_3.png)

위와 같이 테이블처럼 사용 가능하다.

## 서브 쿼리
> where 절에서 사용할 때는 단일행 서브쿼리와 복수행 서브쿼리로 나눌 수 있다.

* 단일행 서브쿼리 연산자

|  연산자  |   의미   |
|:-----:|:------:|
|  `=`  |   같다   |
| `<>`  | 같지 않다  |
|  `>`  |   크다   |
| `>=`  | 크거나 같다 |
|  `<`  |   작다   |
| `<=`  | 작거나 같다 |

* 복수행 서브쿼리 연산자

|    연산자     |   의미   |
|:----------:|:------:|
| in(not in) | 모두 포함함 |
|   exist    | 서브쿼리의 값이 있을 경우 반환 |
| not exist  | 서브쿼리의 값이 없는 경우 반환 |

* 실습

<br>소속학과가 컴퓨터 공학과인 학생들을 출력해본다.
```sql
select name as 학생이름
from student
where major_id = (select major.major_id from major where major_title = '컴퓨터공학과');
```

![SQL_16_4.png](image%2FSQL_16%2FSQL_16_4.png)

위는 단일행 서브쿼리의 결과이고, 아래는 복수행 서브쿼리의 결과이다.

```sql
select name as 학생이름
from student
where major_id in (select major.major_id from major where major_title in ('컴퓨터공학과','국문학과'));
```

![SQL_16_5.png](image%2FSQL_16%2FSQL_16_5.png)


---
### 참조
* [서브쿼리란? 서브쿼리 사용해보기](https://mozi.tistory.com/233)
* [sub query 서브쿼리 16편 -sTricky](https://stricky.tistory.com/265)