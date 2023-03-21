# SQL_04

## SQL 함수
> * SQL 에는 출력값을 변환하는 여러가지 함수들이 존재한다.
> * DBMS 에서 함수를 분류하는 기준이 존재한다.
> * SQL 에서 내장여부에 따라 내장함수와 사용자 정의 함수로 분류 가능하다.
> * 내장함수는 단일행 함수와 복수행 함수로 구분 가능하다.
> * 또한 단일행 함수는 문자 함수, 숫자 함수, 날짜 함수, 형변환 함수, 일반 함수 등으로 분류할 수 있다.

## SQL 내장 함수
> SQL 내장함수는 상수나 속성 이름을 입력 값으로 받아, 단일 값을 결과로 반환한다.
> <br>SELECT, WHERE, UPDATE 등에서 모두 사용이 가능하다.

* MySQL 에서 제공하는 주요 내장함수

![SQL_04_1.png](image%2FSQL_04_1.png)

## 문자 함수
> 문자형 함수는 문자 데이터를 매개 변수로 문자나 숫자 값의 결과를 돌려주는 함수를 말한다.

여러가지 문자 함수를 다뤄보기 전 실습을 위해 데이터를 추가한다.
```sql
create table country
(
    country_name varchar(100),
    capital_city varchar(100),
    continent varchar(100)

) character set utf8;

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('USA', 'Washington', 'America');

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('England', 'London', 'Europe');

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('S.Korea', ' Seoul', 'Asia');

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('Australia', ' Canberra', 'Oceania');

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('Ghana', 'Accra', 'Africa');

INSERT INTO country (country_name, capital_city, continent) 
VALUES ('Argentina', 'Buenos aires', 'America');
```

## lower / upper 함수
> lower 함수는 입력된 문자를 소문자로 변경시키는 함수이다.
> <br> upper 함수는 입력된 문자를 대문자로 바꾸어주는 함수이다.

* 사용법
```sql
lower(칼럼명)
upper(칼럼명)
```

* 실습
```sql
select country_name as 나라이름,
       lower(country_name) as 소문자,
       upper(country_name) as 대문자 from country;
```

![SQL_04_2.png](image%2FSQL_04_2.png)

사진과 같이 모든 문자가 소문자 또는 대문자로 변환된 것을 확인할 수 있다.

## length 함수
> length 함수는 데이터의 길이를 숫자 형태로 반환해주는 함수이다.

* 사용법
```sql
length(칼럼명)
```

* 실습
```sql
select country_name as 나라이름, length(country_name) as 길이 from country;
```
![SQL_04_3.png](image%2FSQL_04_3.png)

위의 사진과 같이 데이터의 길이가 반환된 모습을 확인 가능하다.

## concat 함수
> concat 함수를 사용하면 문자나, 컬럼값을 붙여서 출력하는 것이 가능하다.

* 사용법
```sql
concat(컬럼값,'내용',컬럼값,'내용')
```

* 실습
```sql
select concat(country_name,'이 있는 대륙은 ',continent,'입니다!') as 어느대륙 from country;
```

![SQL_04_4.png](image%2FSQL_04_4.png)

위와 같이 컬럼값과 문자열이 결합된 새로운 데이터의 출력형태를 확인하는 것이 가능하다.

## substr/mid/substring 함수
> substr/mid/substring 은 셋 다 같은 기능을 하지만 이름만 다른 함수이다.
> <br>시작할 문자열의 위치값과 리턴값의 길이를 입력하면 문자열을 잘라내서 반환해준다.

* 사용법
```sql
substr/mid/substring(칼럼명, 시작할 문자열의 위치값, 리턴시킬 값의 길이)
```

* 실습
```sql
select country_name as 원본,
       substr(country_name, 1, 3) as substr,
       mid(country_name, 1, 3) as mid,
       substring(country_name, 1, 3) as substring from country;
```
![SQL_04_5.png](image%2FSQL_04_5.png)

세가지 함수 모두 이름만 다를 뿐 첫번째 글자로부터 3개의 글자를 반환했으므로, 같은 결과를 반환하는 것을 확인 가능하다.

## instr 함수
> instr 함수는 특정 문자열의 위치를 숫자로 리턴해주는 함수이다.
> <br>instr 함수는 대소문자를 구분하지 않고 문자열 위치를 리턴한다.

* 사용법
```sql
instr(칼럼 값,'찾는 문자')
```
* 실습
```sql
select country_name as 나라이름,
       instr(country_name, 'A') as A위치 from country;
```
![SQL_04_6.png](image%2FSQL_04_6.png)

위의 사진과 같이 A 문자열의 위치를 리턴해주는 것을 확인 가능하다.
또한 같은 문자열이 여러개인 경우 가장 앞에 있는 문자열의 위치를 리턴해주는 것을 확인할 수 있었다.

### lpad/rpad 함수
> lpad 와 rapd 는 어떤 데이터가 기준보다 짧을 경우 왼쪽/오른쪽에 원하는 문자를 채워 자릿수를 맞춰주는 함수이다.
> <br>lpad 는 왼쪽, rpad 는 오른쪽에 문자 혹은 숫자를 채운다.

* 사용법
```sql
lpad/rpad(칼럼명, 기준 자릿수, 채워 넣은 숫자/문자)
```

* 실습
```sql
select continent as 원본,
       rpad(continent, 10, 'X') as rpad, 
       lpad(continent, 10, 'X') as lpad from country;
```

![SQL_04_7.png](image%2FSQL_04_7.png)

위의 사진과 같이 기준 자릿수에 미달한만큼 왼쪽/오른쪽에 지정한 문자가 채워넣어진 것을 확인 가능하다.

## trim / ltrim / rtrim 함수
> trim 은 어떤 문자열의 공백을 지워주는 함수이다.
> <br>rtrim 은 오른쪽의 공백만을 제거하고, ltrim 은 왼쪽의 공백만을 제거한다.

* 사용법
```sql
trim/ltrim/rtrim(칼럼명)
```

* 실습
```sql
select capital_city as 원본,
       trim(capital_city) as trim,
       ltrim(capital_city) as ltrim,
       rtrim(capital_city) as rtrim from country;
```

위와 같이 각각 양쪽/왼쪽/오른쪽의 공백이 제거된 모습을 확인 가능하다.

## replace 함수
> replace 함수는 특정 문자열을 찾아 지정한 다른 문자열로 치환해주는 함수이다.
> <br>instr 함수와는 다르게 대소문자의 구별이 필요하다.
* 사용법
```sql
replace(컬럼명, '찾을 문자', '치환할 문자')
```

* 실습
```sql
select country_name as 원본,  
       replace(country_name,'A','#') as 치환 from country;
```

![SQL_04_9.png](image%2FSQL_04_9.png)

사진과 같이 기존의 문자열이 지정한대로 치환되어 리턴된 것을 확인 가능하다.

### 참조
* [SQL 내장함수](https://velog.io/@songyw0517/SQL-%EB%82%B4%EC%9E%A5%ED%95%A8%EC%88%98)
* [단일행 함수 잘 사용 하기(문자 함수) 4편 -sTricky](https://stricky.tistory.com/210)
