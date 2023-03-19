# MySQL_02

## Projection, Selection
* Projection
   * 테이블의 열을 column 이라고 부른다. 
   * column 을 가져오는 것을 Selection 이라고 한다.
* Selection
   * 테이블의 행을 row 라고 한다.
   * row 을 가져오는 것을 Projection 이라고 한다.

   * ![MySQL_02_1.png](image%2FMySQL_02_1.png)


## DESC (Describe)
> DESC 명령은 특정 테이블에 어떤 칼럼이 있는지 조회하는 명령어이다.
```sql
DESCRIBE 테이블명;
DESC 테이블명;
```
위와 같이 사용하여 테이블의 컬럼을 확인하는 것이 가능하다.

## SELECT 로 원하는 데이터 선택
```sql
SELECT * FROM 테이블명;
```
위의 SQL 문에서 `*`은 아스타 리스크라고 부르기도 하며, 주로 테이블의 모든 컬럼을 조회하는데 사용한다.
```sql
SELECT 칼럼명 FROM 테이블명;
```
위와 같이 작성시 원하는 컬럼만 출력하는 Projection 을 하는 것이 가능하다.

* **실습**

먼저 임의의 데이터베이스를 만들어주고 테이블을 생성한다.
```sql
create database Test1;

use Test1;

create table test1
(
  name    varchar(50),
  dept_cd varchar(1),
  phone   varchar(15),
  address varchar(100)
) character set utf8;
```
다음으로 임의의 데이터를 집어넣어준다.
```sql
INSERT INTO test1 (name, dept_cd, phone, address) 
VALUES ('홍길동', 'A', '01023456789', '조선 한양읍');

INSERT INTO test1 (name, dept_cd, phone, address) 
VALUES ('손흥민', 'A', '0112345434', '영국 런던');

INSERT INTO test1 (name, dept_cd, phone, address) 
VALUES ('박찬호', 'C', '01023433456', '충남 공주');

INSERT INTO test1 (name, dept_cd, phone, address) 
VALUES ('김유신', 'D', '0187766645', '신라 경주');

INSERT INTO test1 (name, dept_cd, phone, address)
VALUES ('박나래', 'D', '0192929384', '서울특별시 영등포구');

INSERT INTO test1 (name, dept_cd, phone, address)
VALUES ('강감찬', 'E', '01023432123', '고려');
```
SELECT 문을 이용해 name 과 address 에 해당하는 칼럼의 데이터만 표시하면 아래와 같이 쓸 수 있다.
```sql
select name, address from test1;
```
![MySQL_02_2.png](image%2FMySQL_02_2.png)

위의 사진과 같은 결과를 얻을 수 있었다.

## WHERE
> WHERE 은 조건절로도 부르며, 어떤 테이블에 존재하는 수많은 row 중에서 특정한 조건을 입력하여, 해당 조건에 해당하는 데이터만 가지고 오라는 명령어이다.
```sql
select 출력할 컬럼명
from 테이블명
where 출력할 데이터 조건;
```
위와 같은 형태로 사용할 수 있다.

* **실습**

위의 테이블에서 where 절 뒤에 여러가지 조건을 붙혀 데이터를 가져올 수 있다.
```sql
select * from test1;
where dept_cd = 'D';
```
![MySQL_02_3.png](image%2FMySQL_02_3.png)

## 표현식 (Expression)
> 표현식은 칼럼의 데이터 외에 다른 문자열이나 내용을 출력할 때 사용한다.
```sql
select name, '이름입니당' from test1;
```
![MySQL_02_4.png](image%2FMySQL_02_4.png)

위와 같이 우측에 `이름입니당`이라는 표현식에 리터럴 상수가 출력되는 것을 확인 가능하다.

## 별칭(alias) 사용하기
> 별칭은 값에 별칭을 주어 접근을 별칭 형태로 할 수 있도록 한 것이다.
> 데이터, 칼럼, 테이블, 서브쿼리, where 절 등에 사용 가능하며, 예약어는 AS 이다.
```sql
select * from A as B; // 테이블에 별칭 짓기
select A as B from table; // 칼럼에 별칭 짓기
```
* 예시
위에서 사용했던 표현식에 별칭을 주어보자.
```sql
select name 이름, '이름입니당' 별칭 from test1; 
select name as 이름, '이름입니당' as 별칭 from test1; 
```
위 아래는 같은 결과값을 내보낸다.

![MySQL_02_5.png](image%2FMySQL_02_5.png)

## DISTINCT
> DISTINCT 는 중복된 값을 제외하고 출력할 때 사용한다.

```sql
select distinct dept_cd from test1;
```
![MySQL_02_6.png](image%2FMySQL_02_6.png)

위와 같이 사용 시 중복되는 부분이 제외되는 것을 확인 가능하다.

## 연결 연산자
> 여러 칼럼의 값이나, 문자열로 된 표현식은 값을 붙여 하나의 칼럼으로 표현 가능하다.
> concat 이라는 함수는 문자열 혹은 칼럼의 값을 연결해주는 함수이다.
```sql
select concat(name,'이 사는 곳은 ',address,'입니다.') as 주소 from test1;
```

![MySQL_02_7.png](image%2FMySQL_02_7.png)

위와 같이 사용하는 것이 가능하다.

---
### 참조
* [select를 잘 이용하는 방법(1), 2편 -sTricky](https://stricky.tistory.com/204)