# SQL_03

## 산술 연산자
> 산술 연산자는 우리가 흔히 알고있는 +, _, *, /를 의미한다.
> SQL 에서도 다른 프로그래밍 언어와 마찬가지로 산술 연산을 사용하여 결과를 얻어낼 수 있다.

* **실습**

직접 실습해 보기에 앞서 산술연산자의 실습을 위한 테이블을 하나 생성합니다.
```sql
create table exam1
(
    name      varchar(50),
    math      int(10),
    english   int(10),
    korean    int(10)
) character set utf8;
```
```sql
INSERT INTO exam1 (name, math, english, korean)
VALUES ('강백호', 98, 65, 56);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('서태웅', 87, 76, 87);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('채치수', 76, 87, 75);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('송태섭', 78, 88, 55);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('정대만', 56, 90, 89);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('권준호', 90, 95, 78);

INSERT INTO exam1 (name, math, english, korean)
VALUES ('이달재', 99, 82, 83);
```

![SQL_03_1.png](image%2FSQL_03_1.png)

위와 같은 테이블에서 별칭과 산술 연산을 이용하여 여러가지 값들을 구해볼 수 있다.

* 총합
```sql
select * from exam1, math + english + korean as total;
```

![SQL_03_2.png](image%2FSQL_03_2.png)

* 평균
```sql
select name, math, english, korean, (math + english + korean)/3 as average from exam1;
```

![SQL_03_3.png](image%2FSQL_03_3.png)

## WHERE 절에 비교연산자 사용
> where 절에는 비교연산자를 이용하여 조건에 맞는 데이터만 출력하는 것이 가능하다.

* 실습
```sql
select name, math, english, korean from exam1
where math >= 80;
```
위와 같이 사용하여 math 가 80 이상인 데이터만 찾아낼 수 있다.

![SQL_03_4.png](image%2FSQL_03_4.png)

위와 같은 비교 연산자 이외에도 where 절에서 사용할 수 있는 다양한 연산자가 존재한다.

|          비교 연산자          |              설명              |
|:------------------------:|:----------------------------:|
|            =             |          같은 조건을 검색           |
|          !=, <>          |         같지 않은 조건을 검색         |
|     BETWEEN a AND b      |      a 와 b 사이에 있는 값을 검색      |
|       IN(a, b, c)        |    a, b, c 중 어느 하나인 것을 검색    |
|           like           |     특정 패턴을 가지고 있는 조건을 검색     |
|  in Null /  is Not Null  |   Null 이거나 Null 이 아닌 값을 검색   |
|         a AND b          |   a, b 두 조건 모두를 만족하는 값을 검색   |
|          a OR b          |  a 나 b 중 하나의 조건을 만족하는 값을 검색  |
|          NOT a           |       a 가 아닌 모든 값을 검색        |

## order by 절
> SQL 에서는 데이터를 어떤 기준으로 정렬하여 보고 싶을 때 order by 절을 사용한다.
> order by 사용 시 기본적으로 오름차순으로 정렬이 되며, desc 옵션을 사용하면 내림차순으로 정렬이 가능하다.
> 문자는 가나다, abc 순으로 정렬되며, 날짜는 최근 날짜가 더 큰 값으로 인식된다.

* 실습
```sql
select * from exam1 order by math; // math 를 기준으로 오름차순 정렬
```

![SQL_03_5.png](image%2FSQL_03_5.png) 

```sql
select * from exam1 order by math desc; // math 를 기준으로 내림차순 정렬
```

![SQL_03_6.png](image%2FSQL_03_6.png)

이외에도 order by 뒤에 산술연산자를 사용하거나, 칼럼의 위치에 따라 숫자만 집어넣어서 사용하는 것도 가능하다.

## 집합 연산자
> 데이터베이스에서는 기본적으로 한 테이블을 하나의 집합이라고 하고, SQL 에서 select 문으로 나오는 데이터 셋을 집합이라고 표현한다.
> 이러한 데이터들은 집합 연산자를 이용해 집합처럼 연산하는 것이 가능하다.

|                 집합 연산자                 |                    내용                    |
|:--------------------------------------:|:----------------------------------------:|
|            UNION <br/>(합집합)            | 두 집합을 더해서 결과를 출력한다. 중복값을 제거하고, 정렬을 수행한다. |
| UNION ALL<br/>(합집합)<br/> (중복 제거, 정렬 X) | 두 집합을 더해서 결과를 출력한다. 중복값 제거와 정렬을 하지 않는다.  |
|          INTERSECT<br/>(교집합)           |         두 집합의 교집합 결과를 정렬하여 출력한다.         |
|            MINUS<br/>(차집합)             | 두 집합의 차집합 결과를 정렬하여 출력한다. SQL 의 순서가 중요하다. |

### UNION (합집합)
실습을 위해 새로운 테이블과 데이터를 추가한다.
```sql
create table exam2
(
    name    varchar(50),
    math    int(10),
    english int(10),
    korean  int(10)
) character set utf8;

INSERT INTO exam2 (name, math, english, korean) 
VALUES ('신형만', 78, 90, 78);

INSERT INTO exam2(name, math, english, korean) 
VALUES ('봉미선', 68, 99, 68);

INSERT INTO exam2 (name, math, english, korean) 
VALUES ('신짱구', 84, 96, 98);

INSERT INTO exam2 (name, math, english, korean) 
VALUES ('신짱아', 67, 68, 75);

INSERT INTO exam2 (name, math, english, korean) 
VALUES ('흰둥이', 88, 93, 68);
```
UNION 을 이용해 두 테이블의 합집합을 구한다.

```sql
select * from exam1
union
select * from exam2;
```

![SQL_03_7.png](image%2FSQL_03_7.png)

사진과 같이 합쳐진 모습을 확인 가능하다.

### UNION ALL (중복 제거 X, 정렬 X 인 합집합)
```sql
select * from exam1
union
select * from exam1;
```
![SQL_03_8.png](image%2FSQL_03_8.png)

union 에서는 중복이 제거된 모습을 확인가능하다.
```sql
select * from exam1
union all
select * from exam1;
```
![SQL_03_9.png](image%2FSQL_03_9.png)

반면 union all 에서는 중복이 제거되지 않고, 같은 내용이 2번 출력된 모습을 확인 가능하다.

### INTERSECT (교집합)
실습을 위해 새로운 테이블과 데이터를 추가한다.

```sql
create table math_student
(
    name varchar(50),
    student_no varchar(10)
) ;

create table korean_student
(
    name varchar(50),
    student_no varchar(10)
) ;

INSERT INTO math_student (name, student_no) VALUES ('강백호', '111');
INSERT INTO math_student (name, student_no) VALUES ('서태웅', '112');
INSERT INTO math_student (name, student_no) VALUES ('채치수', '113');
INSERT INTO math_student (name, student_no) VALUES ('송태섭', '114');

INSERT INTO korean_student (name, student_no) VALUES ('강백호', '111');
INSERT INTO korean_student (name, student_no) VALUES ('서태웅', '112');
INSERT INTO korean_student (name, student_no) VALUES ('정대만', '201');
INSERT INTO korean_student (name, student_no) VALUES ('권준호', '202');
```

아래와 같이 입력해주면 교집합을 구할 수 있다.
```sql
select * from math_student
intersect 
select * from korean_student;
```
MySQL 의 경우에는 intersect 대신 아래와 같은 쿼리문을 이용하면 결과값을 얻을 수 있다.
```sql
select math_student.name as name, math_student.student_no 
from korean_student inner join math_student on math_student.name = korean_student.name;
```
![SQL_03_10.png](image%2FSQL_03_10.png)

###  MINUS (차집합)

아래와 같이 입력하면 차집합을 구할 수 있다.
```sql
select * from math_student
minus
select * from korean_student;
```
MySQL 의 경우에는 아래와 같이 입력하면 동일한 결과를 얻을 수 있다.
```sql
select math_student.name as name, math_student.student_no
from math_student
left join korean_student on math_student.name = korean_student.name 
where korean_student.name is null;
```
![SQL_03_11.png](image%2FSQL_03_11.png)

---
### 참조
* [select를 잘 이용하는 방법(2), 3편 -sTricky](https://stricky.tistory.com/205)
* [MySQL 곱집합, 합집합, 교집합, 차집합, 대칭차](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=islove8587&logNo=220953972194)
