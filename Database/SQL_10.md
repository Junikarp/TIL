# SQL_10

## group by 절
> group by 절은 집계 함수의 하나로 여러행들이 모여서 그룹당 단 하나의 결과를 돌려주는 함수이다.
> <br>집계함수와 함께 사용되는 상수는 group by 절에 추가하지 않아도 된다.

## group by 절 사용해보기

실습에 앞서 새로운 테이블을 생성하고 데이터를 집어넣어준다.
```sql
create table test4
(
    do varchar(100) null,
    city varchar(100) null,
    budget_value int null,
    population int null
);

INSERT INTO test4 (do, city, budget_value, population) VALUES ('서울특별시', '서울특별시', 23324, 345);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('부산광역시', '부산광역시', 34323, 5345);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경상남도', '창원시', 4331, 435);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경상남도', '양산시', 25436, 2134);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경상남도', '밀양시', 62341, 6523);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경기도', '부천시', 3242, 345);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경기도', '시흥시', 32454, 546);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('경기도', '수원시', 3234, 345);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('충청남도', '공주시', 2425, 436);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('충청남도', '논산시', 5534, 4567);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('강원도', '속초시', 6542, 3542);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('강원도', '강릉시', 23423, 4355);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('강원도', '태백시', 5465, 45);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('전라북도', '전주시', 456, 645);
INSERT INTO test4 (do, city, budget_value, population) VALUES ('전라북도', '군산시', 3243, 234);
```
입력한 데이터를 가지고 도/특별시/광역시별 예산의 평균과 합계를 구해본다.

```sql
select do as `도/특별시/광역시`, avg(budget_value) as 예산평균, sum(budget_value) as 예산합계
from test4
group by do;
```

![SQL_10_1.png](image%2FSQL_10%2FSQL_10_1.png)

위의 사진과 같이 도에 속해있는 시들은 도라는 한 그룹으로 묶여서 결과가 출력된 것을 확인 가능하다.

## group by 절에 함수 이용
> group by 절에 함수를 사용하려면 select 절과 group by 절 모두에 함수를 그대로 적어줘야한다.

* 실습 

```sql
select do ,
       avg(budget_value) as 예산평균,
       sum(budget_value) as 예산합계
from test4
group by if(do in ('서울특별시','경기도'), '수도권','지방');
```
위와 같이 사용하니 오류가 생겨 결과를 출력하지 않았다.

```sql
select if(do in ('서울특별시','경기도'), '수도권','지방') as 지역구분 ,
       avg(budget_value) as 예산평균,
       sum(budget_value) as 예산합계
from test4
group by if(do in ('서울특별시','경기도'), '수도권','지방');
```

![SQL_10_2.png](image%2FSQL_10%2FSQL_10_2.png)

group by 절과 select 절에 그룹화할 대상의 형태를 똑같이 작성하여 정확한 결과를 얻어낼 수 있었다.


---
### 참조
* [복수 행(window) 함수 잘 사용 하기(group by) 10편 -sTricky](https://stricky.tistory.com/241)
* [GROUP BY와 HAVING절](http://www.gurubee.net/lecture/1032)