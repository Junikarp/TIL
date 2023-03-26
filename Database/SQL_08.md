# SQL_08

## 일반 함수
> 일반 함수는 함수의 입력되는 값이 숫자, 문자, 날짜 구분없이 사용 가능한 함수이다.

## ifnull 함수
> oracle 에서는 NVL, MySQL 에서는 ifnull 로 사용한다.
> <br>null 인 데이터 값이 있을 때 null 이라고 출력하는 것 대신 지정된 값으로 출력하게 해주는 함수이다.
> null 은 0과 달리 데이터 자체가 없다는 뜻, 당연히 연산도 불가하다.

* 사용법
```sql
ifnull(data, 'null 대신 들어갈 문자나 숫자, 또는 컬럼명')
```

* 실습
실습을 위해 테이블을 생성하고 적당한 값들을 집어넣어 줍니다.

```sql
create table test3
(
    name    varchar(50),
    dept    varchar(10),
    salary  varchar(10),
    bonus   varchar(10)
) character set utf8;
```
```sql
insert into test3 (name, dept, salary, bonus)
    value ('강백호', 'A', '100', '200');
insert into test3 (name, dept, salary, bonus)
    value ('서태웅', 'A', '200', '400');
insert into test3 (name, dept, salary)
    value ('송태섭', 'B', '300' );
insert into test3 (name, dept, salary)
    value ('채치수', 'B', '150' );
insert into test3 (name, dept, salary, bonus)
    value ('정대만', 'C', '1000', '200');
```

![SQL_08_1.png](SQL_08%2FSQL_08_1.png)

데이터를 넣어주고 ifnull 을 이용해 null 대신 '빈칸입니다' 라는 문자열을 출력합니다.
```sql
select name, dept, salary, ifnull(bonus, '빈칸입니다') from test3;
```

![SQL_08_2.png](SQL_08%2FSQL_08_2.png)

또한 출력할 데이터로 칼럼을 지정하는 방법으로도 사용 가능하다.
```sql
select name, dept, salary, ifnull(bonus, name) from test3;
```

![SQL_08_3.png](SQL_08%2FSQL_08_3.png)

## if 함수
> if 함수는 조건을 지정하여 조건이 성립하였을 경우와 조건이 성립하지 않았을 경우의 출력값을 각각 지정하여 출력하는 함수이다.
> <br> ifnull 함수를 if 함수로 구현하는 것이 가능하다.
* 사용법
```sql
if(조건, 조건이 성립하였을 때 출력값, 조건이 미성립 했을 때 출력값)
```

* 실습

salary 칼럼의 값이 300 이상이면 고액연봉자, 300 미만이면 일반 연봉자로 출력하도록 조건을 건다.
```sql
select name, dept, salary, if(salary >= 300, '고액연봉자', '일반연봉자') from test3;
```

![SQL_08_4.png](SQL_08%2FSQL_08_4.png)

위와 같이 조건 성립 여부에 따라 출력값이 달라지는 것을 확인가능하다.

## case 함수
> case 함수는 조건에 따른 출력값을 지정해주는 함수이다.

* 사용법
```sql
CASE 컬럼  
WHEN 조건1 THEN 값1 
WHEN 조건2 THEN 값2 
ELSE 값3
END
```

* 실습

dept 칼럼에 따라 A 는 경영지원부, B는 영업부, 그 외에는 회계팀으로 출력하는 함수를 작성해본다.
```sql
select name
     , case when dept = 'A' then '경영지원부'
            when dept = 'B' then '영업부'
            else '회계팀' end as dept
     , salary
     , bonus
from test3;
```

![SQL_08_5.png](SQL_08%2FSQL_08_5.png)

위와 같이 case 에 따라 출력된 모습을 확인 가능하다.

## 복합적 사용 실습
공부한 내용을 통해 테이블을 정리해본다
```sql
select name as 이름
     , case when dept = 'A' then '경영지원부'
            when dept = 'B' then '영업부'
            when dept = 'C' then '회계팀' end as 부서
     , salary as 봉급
     , if(salary >= 300 , '고액연봉', '일반연봉') as 고연봉자
     , ifnull(bonus, 0) as 보너스
     , case when ifnull(bonus, 0) = 0 then '해당없음'
            else '보너스 해당자' end as 보너스해당여부
from test3;
```

![SQL_08_6.png](SQL_08%2FSQL_08_6.png)

위와 같이 테이블을 표현하는 것이 가능하다.

---

### 참조
* [ 단일행 함수 잘 사용 하기(일반 함수) 8편 -sTricky](https://stricky.tistory.com/233)
* [CASE 문 . 조건에 따라 값 정하기 ! CASE WHEN THEN](https://121202.tistory.com/46)
