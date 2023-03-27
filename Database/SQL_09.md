# SQL_09

## 복수행 함수(== 그룹함수, window 함수)
> 복수행 함수란 복수의 데이터가 함수로 입력되는 함수를 말한다.
> <br> 복수행 함수에 *을 사용하면 NULL 포함하고 컬럼명을 쓰면 NULL 값이 제외하고 작업하므로 유의한다.

## count 함수
> count 함수는 전체 칼럼을 대상으로 입력되는 데이터의 총 건수를 계산하여 반환한다.

* 사용법
```sql
count(컬럼명)
```

* 실습
아래와 같은 테이블을 가지고 실습을 진행한다.

![SQL_09_1.png](image%2FSQL_09%2FSQL_09_1.png)

```sql
select count(*) from test3;
```

![SQL_09_2.png](image%2FSQL_09%2FSQL_09_2.png)

위와 같이 `count(*)` 을 사용하면 전체 칼럼을 대상으로 총 건수를 얻을 수 있다.

```sql
select count(bonus) from test3;
```

![SQL_09_3.png](image%2FSQL_09%2FSQL_09_3.png)

NULL 값이 포함된 칼럼에서는 NULL 값을 제외한 데이터의 총 건수가 출력된다.

## sum 함수
> sum() 함수는 입력된 데이터들의 합계 값을 반환하는 함수이다.

* 사용법
```sql
sum(칼럼명)
```

* 실습
```sql
select sum(salary) from test3;
```

![SQL_09_4.png](image%2FSQL_09%2FSQL_09_4.png)

위와 같이 `salary` 칼럼의 총 합계가 출력된 모습을 확인 가능하다.

## avg 함수
> avg() 함수는 입력된 데이터 값의 평균값을 반환하는 함수이다.

* 사용법
```sql
avg(칼럼명)
```

* 실습
```sql
select avg(salary) from test3;
```

![SQL_09_5.png](image%2FSQL_09%2FSQL_09_5.png)

위의 사진과 같이 평균값이 출력되는 모습을 확인하는 것이 가능하다.

## max, min 함수
> max 함수는 입력된 데이터 값의 최댓값을 반환하는 함수이다.
> min 함수는 입력된 데이터 값의 최소값을 반환하는 함수이다.

* 사용법
```sql
max(칼럼명)
min(칼럼명)    
```

* 실습
```sql
select max(salary), min(salary) from test3;
```

![SQL_09_6.png](image%2FSQL_09%2FSQL_09_6.png)

사진과 같이 각각 최댓값과 최소값이 구해진 모습을 확인 가능하다.

## stddev 함수
> stddev 함수는 입력된 데이터들의 표준편차를 구하는 함수이다.

* 사용법
```sql
stddev(칼럼명)
```

* 실습
```sql
select round(stddev(salary),4) from test3;
```

![SQL_09_7.png](image%2FSQL_09%2FSQL_09_7.png)

위의 사진과 같이 표준편차 값이 구해진 모습을 확인 가능하다.

## variance 함수
> variance 함수는 입력된 데이터들의 분산값을 구할 때 사용하는 함수이다.

* 사용법
```sql
variance(salary)
```

* 실습
```sql
select variance(salary) from test3;
```

![SQL_09_8.png](image%2FSQL_09%2FSQL_09_8.png)

사진과 같이 분산을 구할 수 있다.

---
### 참조
* [오라클 SQL과 PL/SQL ( 복수행 함수(그룹 함수) )](https://ms-record.tistory.com/104)
* [복수 행(window) 함수 잘 사용 하기(기본 사용법) 9편 -sTricky](https://stricky.tistory.com/240)