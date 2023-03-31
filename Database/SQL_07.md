# SQL_07

## 데이터 타입
> 데이터 타입이란 시스템과 프로그래밍 언어에서 실수, 소수, 자료형 등 여러 데이터를 식별하는 타입이다.

## 문자형 데이터 타입
|          데이터 유형          |                                 정의                                  |
|:------------------------:|:-------------------------------------------------------------------:|
|         CHAR(M)          |                  고정 길이를 갖는 문자열 저장<br/>최대 255 byte                   |
|        VARCHAR(M)        |                 가변 길이를 갖는 문자열 저장<br/>최대 65535 byte                  |
|       TINYTEXT(M)        |                             최대 255 byte                             |
|           TEXT           |                            최대 65535 byte                            |
|        MEDIUMTEXT        |                          최대 16777215 byte                           |
|         LONGTEXT         |                         최대 4294967295 byte                          |
| ENUM('VALUE1', 'VALUE2') | 열거형, 정해진 몇가지 값들중 하나만 저장<br/>최대 65535개의 개별값을 가질 수 있고, 내부적으로 정수값으로 표현 |
| SET('VALUE1', 'VALUE2')  |  집합형, 정해진 몇가지 값들중 여러개 저장<br/>최대 64개의 요소로 구성될 수 있고, 내부적으로 정수값으로 표현   |
|           JSON           |               JSON 문자열 데이터 타입<br/>JSON형태의 포맷을 꼭 준수해야함               |

## 숫자형 데이터 타입
|     데이터 유형      |                                                                               정의                                                                               |
|:---------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|     BIT(M)      |                                                                      비트 데이터 타입(최대 64 bit)                                                                      |
|  BOOL, BOOLEAN  |                                                                   0은 false, 0이 아닌값은 true로 간주                                                                   |
|   TINYINT(M)    |                                                                       정수형 데이터 타입(1 byte)                                                                       |
|   SMALLINT(M)   |                                                                       정수형 데이터 타입(2 byte)                                                                       |
|  MEDIUMINT(M)   |                                                                       정수형 데이터 타입(3 byte)                                                                       |
|     INT(M)      |                                                                       정수형 데이터 타입(4 byte)                                                                       |
|    BIGINT(M)    |                                                               정수형 데이터 타입(8 byte)<br/>무제한 수 표현 가능                                                               |
|  FLOAT(길이, 소수)  |                                                             부동 소수형 데이터 타입(4 byte)<br/>고정 소수점 사용 형태                                                             |
| DECIMAL(길이, 소수) | 소수형 데이터 타입(길이 + 1 byte)<br/>소수점 사용 형태<br/> DECIMAL(5)의 경우 : -99999 ~ 99999 <br/>DECIMAL(5, 1)의 경우 : -9999.9 ~ 9999.9 <br/>DECIMAL(5, 2)의 경우 : -999.99 ~ 999.99 |
| DOUBLE(길이, 소수)] |                                                             부동 소수형 데이터 타입(8 byte)<br/>고정 소수점 사용 형태                                                             |

## 날짜형 데이터 타입
|  데이터 타입   |                               정의                               |
|:---------:|:--------------------------------------------------------------:|
|   DATE    |              날짜(년, 월, 일) 형태의 기간 표현 데이터 타입(3 byte)              |
|   TIME    |              시간(시, 분, 초) 형태의 기간 표현 데이터 타입(3 byte)              |
| DATETIME  |                날짜와 시간 형태의 기간 표현 데이터 타입(3 byte)                 |
| TIMESTAMP | 날짜와 시간 형태의 기간 표현 데이터 타입(4 byte)<br/>시스템 변경시 자동으로 그 날짜와 시간이 저장됨 |
|   YEAR    |                      년도 표현 데이터 타입(1 byte)                      |

## 이진 데이터 타입
|        데이터 타입         |                  정의                  |
|:---------------------:|:------------------------------------:|
| BINARY(N)<br/>BYTE(N) |   CHAR 형태의 이진 데이터 타입(최대 255 byte)    |
|     VARBINARY(N)      | VARCHAR 형태의 이진 데이터 타입(최대 65535 byte) |
|      TINYBLOB(N)      |       이진 데이터 타입 (최대 255 byte)        |
|        BLOB(N)        |      이진 데이터 타입 (최대 65535 byte)       |
|     MIDIUMBLOB(N)     |     이진 데이터 타입 (최대 16777215 byte)     |
|      LONGBLOB(N)      |    이진 데이터 타입 (최대 4294967259 byte)    |

## 묵시적 형 변환
> 묵시적 형 변환이란, 데이터의 형태를 사용자의 의도에 맞춰서 데이터베이스가 알아서 형변환 하여 결과를 출력하는 행위를 말한다.

* 예시
```sql
select 100 + '200', concat(2023,'은 이번 년도 입니다.') from dual;
```

![SQL_07_1.png](image%2FSQL_07%2FSQL_07_1.png)

위와 같이 숫자와 문자가 섞여있는 상황에서 묵시적 형 변환에 의해 정상적으론 출력이 되는 모습을 확인 가능하다.

## cast, convert 함수
> cast 함수와 convert 함수는 mysql 에서 데이터 타입을 서로 변환시켜주는 형 변환 함수이다.

* 사용법

```sql
cast(표현할 값 as 데이터 형식(길이))
convert(표현할 값, 데이터 형식(길이))
```

![SQL_07_2.png](image%2FSQL_07%2FSQL_07_2.png)

위와 같이 cast 함수와 convert 함수를 사용하면 형 변환을 하는 것이 가능하다.

---
### 참조
* [DB - 데이터 타입 MYSQL](http://www.incodom.kr/DB_-_%EB%8D%B0%EC%9D%B4%ED%84%B0_%ED%83%80%EC%9E%85/MYSQL)
* [단일행 함수 잘 사용 하기(형 변환 함수) 7편 -sTricky](https://stricky.tistory.com/232)
* [MySQL Chapter-11 data Types](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)