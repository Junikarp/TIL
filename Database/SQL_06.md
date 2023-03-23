# SQL_06

## 날짜형 함수
> 날짜형 함수는 날짜 데이터를 관리하고 다루기 위한 함수이다.

## 현재 시간 출력하기

|           SQL 명령            |        출력 결과        |
|:---------------------------:|:-------------------:|
|        select now();        | 2023-03-23 12:34:56 |
|      select sysdate();      | 2023-03-23 12:34:56 |
| select current_timestamp(); | 2023-03-23 12:34:56 |
|      select curdate();      |     2023-03-23      |
|   select current_date();    |     2023-03-23      |
|   select current_time();    |      12:34:56       |
|       select now()+0;       |   20230323123456    |
|  select current_time()+0;   |       123456        |

위의 결과처럼 시간 출력 함수 뒤에 `+0` 을 붙히면 숫자를 나열한 것처럼 결과를 출력하는 것이 가능하다.

## now() 와 sysdate()
> 두 함수 모두 현재 시간을 입력하거나 조회할 때 사용하는 함수지만 차이가 존재한다.
* now() 는 쿼리가 실행되는 순간을 기점으로 시간을 출력한다.
* sysdate() 는 함수가 실행되는 순간을 기점으로 삼는다.

아래의 예시를 통해 확인해보자. 
```sql
select now() as 전, sleep(2) as sleep, sysdate() as 후;
```

![SQL_06_1.png](image%2FSQL_06%2FSQL_06_1.png)

```sql
SELECT sysdate() as 전, sleep(2) as sleep, sysdate() as 후;
```

![SQL_06_2.png](image%2FSQL_06%2FSQL_06_2.png)

위의 결과값에서 확인할 수 있듯이 now() 함수의 경우 sleep 가 반영되지 않았지만, sysdate() 에서는 sleep 이 반영된 것을 확인 가능하다.

## 날짜, 시간에 따른 특정 정보 출력

|                  SQL 명령                   |  출력 결과   |          출력 내용           |
|:-----------------------------------------:|:--------:|:------------------------:|
| select dayofweek('2023-03-23 12:34:56');  |    5     | 1:일요일, 2:월요일, ..., 7:토요일 |
| select dayofmonth('2023-03-23 12:34:56'); |    23    |       몇일인지 일자를 출력        |
| select dayofyear('2023-03-23 12:34:56');  |    82    |    한 해에서 몇번째 날인지를 출력     |
|   select month('2023-03-23 12:34:56');    |    3     |        몇월인지 월을 출력        |
|  select dayname('2023-03-23 12:34:56');   | Thursday |       요일을 영문으로 출력        |
| select monthname('2023-03-23 12:34:56');  |  March   |        월을 영문으로 출력        |
|  select quarter('2023-03-23 12:34:56');   |    1     |          분기를 출력          |
|    select week('2023-03-23 12:34:56');    |    12    |     한 해의 몇번째 주인지를 출력     |
|    select year('2023-03-23 12:34:56');    |   2023   |          년도를 출력          |
|    select hour('2023-03-23 12:34:56');    |    12    |       몇시인지 시간을 출력        |
|   select minute('2023-03-23 12:34:56');   |    34    |        몇분인지 분을 출력        |
|   select second('2023-03-23 12:34:56');   |    56    |        몇초인지 초를 출력        |

## 날짜, 시간을 연산하여 출력
> 날짜, 시간을 더하고 싶다면 date_add(date, interval `expr` `type`), adddate(date, interval `expr` `type`) 로 표현한다.
> <br>날짜, 시간을 빼고 싶다면 date_sub(date, interval `expr` `type`), subdate(date, interval `expr` `type`) 로 표현한다.

* type 사용 방법

|   type 변수값    |             의미             | type 에 따른 expr 입력형태 |
|:-------------:|:--------------------------:|:-------------------:|
|    second     |          seconds           |          초          |
|    minute     |          minutes           |          분          |
|     hour      |           hours            |          시          |
|      day      |            days            |          일          |
|     month     |           months           |          월          |
|     year      |           years            |          년          |
| minute_second |       minute:second        |         분:초         |
|  hour_minute  |        hour:minute         |         시:분         |
|   day_hour    |         days hours         |         일 시         |
|  year_month   |        years months        |         년 월         |
|  hour_second  |   hours:minutes:seconds    |        시:분:초        |
|  day_minute   |     days hours:minutes     |        일 시:분        |
|  day_second   | days hours:minutes:seconds |       일 시:분:초       |

## 시간과 초 데이터 변환하여 출력
> sec_to_time 함수는 초를 시:분:초 형태로 변환하여 출력한다.
> <br>time_to_sec 함수는 시:분:초 형태의 시간을 몇초인지 초로 변환하여 출력한다.

* 예시

```sql
select sec_to_time(30000) as `초를 시:분:초로`, time_to_sec('12:34:56') as `시:분:초를 초로`;
```

![SQL_06_3.png](image%2FSQL_06%2FSQL_06_3.png)

위의 사진과 같이 변환된 모습을 확인 가능하다.

## period_add, period_diff
> period_add 는 입력된 년월에 원하는 개월 수를 더하는 함수이다.
> period_diff 는 앞에 입력된 년월에서 뒤에 입력된 년월을 빼서 개월수로 반환해주는 함수이다.

* period_add 실습
```sql
#입력값이 YYMM 
select period_add(2303,17);
#입력값을 YYYYMM 
select period_add(202303,17);
```

![SQL_06_4.png](image%2FSQL_06%2FSQL_06_4.png)

위와 같이 개월수가 더해지며 출력값은 둘 다 YYYYMM 형태로 동일하다.

* period_diff
```sql
#입력값이 YYMM 
select period_diff(2408,2303);
#입력값을 YYYYMM 
select period_diff(202408,202303);
```

![SQL_06_5.png](image%2FSQL_06%2FSQL_06_5.png)

위와 같이 개월수를 결과값으로 받을 수 있으며 만일 앞의 년월수가 작을 경우 음수의 형태로 결과를 받게된다.

## date_format
> date_format 함수는 원하는 데이터를 원하는 형태로 변경하여 출력할 때 사용하는 함수이다.
> <br> 간단한 파라미터 조정으로 결과를 얻을 수 있다는 장점이 존재한다.

* 사용법
````sql
select date_format('date','format 형태');
````

* format 변수

| format 변수 |                       설명                       |
|:---------:|:----------------------------------------------:|
|    %W     |             요일(Monday,...,Sunday)              |
|    %D     |               일자 (1st, 2nd,...)                |
|    %Y     |                    년도(YYYY)                    |
|    %y     |                     년도(YY)                     |
|    %a     |            요일 영문 약어 (Sun, Mon,...)             |
|    %d     |                일자(01,02,...,31)                |
|    %e     |                일자 (1,2,...,31)                 |
|    %m     |                월(01,02,...,12)                 |
|    %c     |                 월(1,2,...,12)                  |
|    %b     |              월 영문약자(Jan,...,Dec)               |
|    %j     |                 해당 년에서 몇번째 날인지                 |
|    %H     |                시(00,01,...,23)                 |
|    %k     |                시(0,1,2,...,23)                 |
|    %h     |                시(01,02,...,12)                 |
|    %l     |                 시(1,2,...,12)                  |
|    %I     |                시(01,02,...,12)                 |
|    %i     |                분(01,02,...,59)                 |
|    %r     |             시각(12)(hh:mm:ss(A/P))              |
|    %T     |                시각(24)(hh:mm:ss)                |
|   %S,s    |                초(00,01,...,59)                 |
|    %p     |                   오전/오후(A/P)                   |
|    %w     |      해당 요일에서 몇번째 날인지<br>(0:일요일,...,6:토요일)      |
|   %U,u    | 해당 년에서 몇번째 주인지<br>(U:일요일이 주의 시작, u:월요일이 주의 시작) |


### 참조
* [now() 와 sysdate()의 차이](https://velog.io/@kimju0913/mysql-now-%EC%99%80-sysdate%EC%9D%98-%EC%B0%A8%EC%9D%B4)
* [단일행 함수 잘 사용 하기(날짜 함수) 6편 -sTricky](https://stricky.tistory.com/220)