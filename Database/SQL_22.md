# SQL_22

## Data Dictionary
> 데이터 사전(Data Dictionary)란 대부분 읽기 전용으로 제공되는 테이블 및 뷰들의 집합으로 데이터베이스 전반에 대한 정보를 제공하는 것이다.

## information_schema
> information_schema 는 서버 내에 존재하는 DB 의 메타정보(테이블, 칼럼, 인덱스 등의 스키마 정보)를 모아둔 DB 이다.
> <br>메타 데이터란 데이터의 데이터로서, 데이터베이스 혹은 테이블의 이름, 컬럼의 데이터타입 또는 접근권한과 같은 것을 의미한다.

아래와 같이 테이블을 조회 가능하다.
```sql
select TABLE_SCHEMA, TABLE_NAME from information_schema.TABLES
where TABLE_SCHEMA = 'information_schema';
```

![SQL_22_1.png](image%2FSQL_22%2FSQL_22_1.png)

위와 같이 다양한 SYSTEM VIEW 가 존재하며 아래에서 몇가지 알아보도록 하겠다.

### information_schema.SCHEMATA
MySQL 내부의 스키마(데이터베이스) 목록을 볼 수 있으며, 스키마별 캐릭터 셋을 확인 가능하다.
```sql
select * from information_schema.SCHEMATA;
```
![SQL_22_2.png](image%2FSQL_22%2FSQL_22_2.png)

### information_schema.TABLES
MySQL 내부에 생성되어있는 SYSTEM VIEW 및 테이블에 관련된 정보를 확인 가능하다. 생성일, 수정일, 로우의 갯수, 테이블 코멘트, 테이블 스토리지 엔진 등을 확인 가능하다.
```sql
select * from information_schema.TABLES;
```

![SQL_22_3.png](image%2FSQL_22%2FSQL_22_3.png)

### information_schema.COLUMNS
MySQL 내부에 생성되어있는 칼럼의 이름, 초기입력값, 칼럼순서, 데이터타입, 데이터길이, 코멘트 등 다양한 정보를 확인 가능하다.
```sql
select * from information_schema.COLUMNS;
```
![SQL_22_4.png](image%2FSQL_22%2FSQL_22_4.png)

### information_schema.ROUTINES
MySQL 내부에 생성되어있는 Function 과 Procedure 에 관한 내용들이 저장되어 있으며, 각 프로그램 별 입출력 데이터 정보와 프로그램 소스 등의 정보가 저장되어 있다.
```sql
select * from information_schema.ROUTINES;
```

![SQL_22_5.png](image%2FSQL_22%2FSQL_22_5.png)

### information_schema.KEY_COLUMN_USAGE
MySQL 내부에 생성된 테이블별 PK 칼럼 혹은 unique 제약조건들의 목록을 확인 가능하다.

```sql
select * from information_schema.KEY_COLUMN_USAGE;
```

![SQL_22_6.png](image%2FSQL_22%2FSQL_22_6.png)

### information_schema.PROCESSLIST
현재 MySQL 에 접속되어 있는 세션 정보들을 확인 가능하며, 각 세션별 상태, 어떤 user 로 어디서 접속중인지, 어떤 SQL 을 실행하고 있는지 등의 정보를 확인 가능하다.

```sql
select * from information_schema.PROCESSLIST;
```

![SQL_22_7.png](image%2FSQL_22%2FSQL_22_7.png)

### information_schema 주요 DB 테이블 정리
위에서 살펴본 테이블을 포함해 몇가지 정리해보면 아래와 같다.

|        테이블        |        내용         |
|:-----------------:|:-----------------:|
|      COLUMNS      |   모든 스키마의 컬럼 확인   |
|      ENGINES      |    사용되는 엔진 확인     |
|      EVENTS       | 생성된 EVENT(스케줄) 확인 |
| KEY_COLUMN_USAGE  |    사용된 키 컬럼 확인    |
|    PROCESSLIST    |  수행 중인 프로세스 리스트   |
|     SCHEMATA      |    생성된 스키마 확인     |
| SCHEMA_PRIVILEGES |     스키마 권한 확인     |
|      TABLES       |   생성된 모든 테이블 정보   |
| TABLE_PRIVILEGES  |     테이블 권한 확인     |
|     TRIGGERS      |    생성된 트리거 확인     |
|  USER_PRIVILEGES  |     사용자 권한 정보     |
|       VIEWS       |     생성된 뷰 정보      |

이외에도 MySQL 스키마에서도 다양한 정보들을 제공하니 나중에 확인해보면 좋겠다.

---
### 참조
* [MySQL data dictionary SQL 독학 강의#22편](https://stricky.tistory.com/296)
* [information_schema란 ? (정의 및 테이블 종류)](https://rk1993.tistory.com/230)
