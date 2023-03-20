# SQL_01

## 데이터베이스 (Database)
 * 데이터베이스는 한 마디로 데이터의 집합이라고 할 수 있다.
 * 우리가 일상을 살아가면서 사용하는 교통카드, 물건 구매시의 기록, 메시지 등 모든 정보는 데이터베이스에 기록된다.

## DBMS (DataBase Management System)
 * 데이터베이스를 관리하고 운영하는 소프트웨어
 * 데이터베이스에 적재된 데이터 작업 수행 및 데이터베이스를 보호하고 보안을 제공한다.
 * DBMS 의 기능은 크게 구성(정의), 조작, 제어 기능으로 구분 가능하다.

## DBMS 의 종류
* DBMS 는 특정목적을 처리하기 위한 프로그램이므로, 데이터 베이스를 사용하기 위해서는 DBMS 를 설치해서 사용해야한다.
![MySQL_01_1.png](image%2FMySQL_01_1.png)
위와 같은 종류의 DBMS 들이 존재한다.

## RDBMS (Relational DBMS)
* RDBMS 는 테이블이라는 최소단위로 구성된 DBMS 로 테이블은 하나 이상의 열(column)과 행(row)으로 이루어져있다.
![MySQL_01_2.png](image%2FMySQL_01_2.png)

## SQL (Structured Query Language)
* SQL 은 관계형 데이터베이스에서 데이터를 조작하고 쿼리하는 표준 언어이다.
* 사용자가 원하는 데이터를 얻기 위해서는 정확하게 데이터베이스에 질의(쿼리)하는 방법을 아는 것이 중요하다.

## SQL 의 기본 명령어
> SQL 의 명령어는 DDL, DML, DCL 의 3가지로 구분된다.

### DDL(Data Definition Language) - 데이터 정의 언어
> DDL 은 데이터베이스의 구조와 테이블, 뷰, 인덱스와 같은 개체를 정의하는데 사용된다.
> DDL 문은 즉시 시행되고 영구적인 명령어이므로 변경사항을 취소하는 것이 불가능하다.
> 따라서 실행 전에 백업이 있는지 확인하는 것이 중요하다.
* CREATE
   * 데이터베이스 내의 개체를 생성
* DROP
   * 데이터베이스 내의 개체를 삭제
* ALTER
   * 데이터베이스 내의 개체의 속성 및 정의를 변경 
* RENAME
   * 데이터베이스 내 개체의 이름 변경
   * 한 번에 다수의 테이블의 이름을 변경 가능
   * 테이블을 다른 데이터 베이스로 이동시키는 것도 가능
* TRUNCATE
   * 테이블 내 모든 데이터를 빠르게 삭제 
   * DROP 문과 달리 테이블의 구조와 인덱스는 그대로 유지
```sql
CREATE TABLE board(
    field1 INT,
    field2 VARCHAR(30),
    field3 DATE NOT NULL,
    PRIMARY KEY (field1, field2)
);

ALTER TABLE board Add field4 NUMBER(3) NOT NULL;

DROP TABLE board;

RENAME TABLE old_1 TO new_1
             old_2 TO new_2
             old_3 TO new_3
    
TRUNCATE TABLE board;
```

## DML (Data Manipulation Language) - 데이터 조작 언어
> DML 은 데이터베이스 내의 데이터를 조작하는데 사용되는 명령어이다.
> DDL 문은 데이터 베이스 개체를 생성, 변경, 삭제하는 데 사용되지만 DML 문은 해당 개체 내의 데이터를 삽입, 업데이트 및 삭제하는 데 사용된다.
> DML 문은 즉시 실행되며 롤백 문으로 취소가 가능하다.
* INSERT
   * 특정 테이블에 데이터를 신규로 삽입
* UPDATE
   * 특정 테이블 내 데이터의 전체, 혹은 일부를 새로운 값으로 수정
* DELETE
   * 특정 테이블 내 데이터의 전체, 혹은 일부를 삭제
* SELECT
   * 특정 테이블 내 데이터의 전체, 혹은 일부를 획득 
   * 주로 하나 이상의 테이블에서 데이터를 검색하는데 사용
```sql
INSERT INTO 테이블명(COLUMN_LIST) VALUES (COLUMN_LIST에 넣을 VALUE_LIST); // 특정 컬럼을 선택하여 입력

INSERT INTO 테이블명 VALUES (COLUMN에 넣을 VALUE_LIST); // 테이블 내 모든 컬럼에 값을 입력

UPDATE 테이블명 SET 컬럼명 = '갱신할 값' WHERE 조건절;

DELETE FROM 테이블명 WHERE 조건절;

SELECT 컬럼리스트 FROM 테이블명 WHERE 조건절;
```
## DCL (Data Control Language) - 데이터 제어어
> 데이터베이스에 접근하거나 객체들을 용하도록 권한을 주고 회수하는 명령어
> GRANT, REVOKE 를 제외한 명령어들은 단독으로 사용되는 경우가 많음
* GRANT
   * 데이터베이스 사용자에게 특정 작업의 수행 권한을 부여
* REVOKE
   * 데이터베이스 사용자에게 부여된 수행 권한을 박탈
* SET TRANSACTION
   * 트랜잭션 모드로 설정
* BEGIN
   * 트랜잭션의 시작을 의미
* COMMIT 
   * 트랜잭션을 실행
* ROLLBACK
   * 트랜잭션을 취소
* SAVEPOINT
   * 롤백 지점을 설정
* LOCK
   * 테이블 자원을 점유
```sql
GRANT SELECT ON SCOTT.EMP TO EXPERT

REVOKE 뺏을 권한 ON 객체이름 FROM 누구;
```
---
### 참조
* [테이블 (데이터베이스)](http://wiki.hash.kr/index.php/%ED%85%8C%EC%9D%B4%EB%B8%94_%28%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4%29)
* [Database(DB), DBMS, SQL의 개념](https://hongong.hanbit.co.kr/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-databasedb-dbms-sql%EC%9D%98-%EA%B0%9C%EB%85%90/)
* [sql 독학 강의# 개념 파악 및 공부법 안내 1편 -sTricky](https://stricky.tistory.com/202)
* [DDL과 DML의 차이점](https://appmaster.io/ko/blog/ddlgwa-dmlyi-caijeom)