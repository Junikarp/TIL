# SQL_21

## DDL (Data Definition Language)
> DB 내의 오브젝트들을 생성하고 변경하고 관리하기 위한 명령문

| DDL 명령어  |                  정의                  |
|:--------:|:------------------------------------:|
|  CREATE  |         새로운 오브젝트나 스키마 등을 생성          |
|  ALTER   |       이미 만들어져 있는 오브젝트의 내용을 변경        |
| TRUNCATE |       테이블의 데이터를 모두 삭제하고 공간을 반납       |
|   DROP   | 테이블 자체를 삭제 <br/>(테이블 뿐만 아니라 인덱스도 삭제) |

## CREATE
> create 문을 이용하면 대부분의 SQL 오브젝트를 생성할 수 있다.

### create table
```sql
create table test (
    name     varchar(10) not null comment '이름',
    age      int         not null comment '나이',
    birthday datetime    not null comment '생일',
    id       varchar(20) not null comment '아이디'
                  primary key (id)
)
    comment '인물' engine = InnoDB;
```
차근차근 살펴보도록 하겠다.
* create table 테이블명으로 테이블을 생성하며 소괄호 안에는 테이블 내의 칼럼을 명시한다.
* 앞에서부터 순서대로 칼럼명, 데이터타입, null 허용 여부, 논리 칼럼명 순으로 명시한다.
* `primary key`는 해당 테이블의 PK 칼럼으로 설정한다는 뜻이며, 이 때 PK 칼럼은 `not null`로 정의해야한다.
* 괄호밖의 comment 는 테이블의 논리명, 혹은 코멘트를 이야기하는 것이다.
* `engine =`은 MySQL 의 두가지 테이블 스토리지 엔진인 `InnoDB`와 `MyISAM` 중 어떤 스토리지 엔진으로 테이블데이터를 저장할 것인지 선택하는 부분이다.

### create user
> DB 의 계정을 생성하기 위한 명령어이다.

아래와 같이 계정을 생성할 수 있다.
```sql
# localhost 에서만 접속 허용
create user 'user'@'127.0.0.1' identified by 'Password'

# 어디에서나 접속 허용
create user 'user'@'%' identified by 'Password'
```

## ALTER
> alter 문은 DB 내의 다양한 오브젝트들을 수정하거나 변경하기 위한 명령어이다.

다양한 예시를 통해 ALTER 문이 어떠한 방식으로 사용되는지 알아보자.
```sql
# not null 옵션의 컬럼을 null로 변경
alter table send_log modify createdAt datetime default current_timestamp() null;

# sendType 컬럼명을 sendType2으로 변경
alter table send_log change sendType sendType2 varchar(4) not null;

# 컬럼 코멘트를 변경
alter table send_log modify fee decimal(20,8) null comment '컬럼코멘트';

# 신규 컬럼을 추가 하는데, fee 컬럼 뒤로 위치
alter table send_log add column_8 int null after fee;

# receive 컬럼의 데이터 타입을 변경
alter table send_log modify receive int not null;
```

## TRUNCATE
> truncate 문은 테이블의 데이터 삭제와 함께 테이블이 사용하던 공간을 반납하게 한다.
> <br>drop 하고 create 하는 방식으로 동작한다.

truncate 문은 delete 보다 데이터 삭제가 빠르지만 이후에 데이터를 복구할 수 없기 때문에 사용할 때 염두해야 한다.
```sql
truncate table 테이블명;
```

## drop
> drop 문은 테이블 및 오브젝트들을 삭제하기 위한 명령어이다.
> <br>테이블 삭제시 해당 테이블의 row 및 인덱스와 저장공간도 모두 반납한다.

아래와 같이 간단하게 테이블을 삭제하는 것이 가능하다.
```sql
drop table 테이블명;
```

---

### 참조
* [DDL문 완전정복 SQL 독학 강의#21편 -sTricky](https://stricky.tistory.com/294)
* [표준 SQL의 데이터 정의 언어(DDL) 문](https://cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language?hl=ko)