# SQL_23

## 제약조건 (Constraint)
> 제약조건은 DB 내의 테이블에 정해둔 어떤 규칙에 따라 올바른 데이터만 입력받고, 규칙에 어긋나거나 잘못된 데이터는 입력 및 변경이 되지 않도록 한다.
> <br> 제약조건을 활용하면 DB 내 테이블이 가진 데이터의 정확도와 신뢰성을 높일 수 있다.

## 제약조건의 종류

MySQL 내의 제약조건은 크게 6가지가 존재하며 아래와 같다.

### 1. primary key
> primary key 는 칼럼의 중복을 막고, null 을 허용하지 않으며, 각 로우를 특정짓는 구분키로 활용된다. (not null + unique)
><br> 테이블 당 하나의 primary key 만 생성가능하며, 데이터간의 유일성을 보장하는 칼럼에 설정된다.

아래와 같이 사용 가능하다.

```sql
# primary key 설정
create table 테이블명
(
    필드이름 필드타입 primary key,
    ...
);


# 제약조건에 이름 설정
create table 테이블명
(
    필드이름 필드타입 ,
    ...,
    [constraint 제약조건이름] primary key(필드이름)
);


# 테이블에 새로운 필드 추가시 해당 필드를 기본키로 설정
alter table 테이블명
add 필드이름 필드타입 primary key;

alter table 테이블명
add [constraint 제약조건이름] primary key (필드이름);


# 기존에 존재하는 필드를 기본키로 설정
alter table 테이블명
modify column 필드이름 필드타입 unique;

alter table 테이블명
modify column [constraint 제약조건이름] unique (필드이름);

    
# 테이블에서 primary key 제약조건 삭제
alter table 테이블명
drop primary key;
```

### 2. Foreign key
> 어떤 테이블의 칼럼 값은 다른 테이블의 칼럼 값을 참조하여야 한다는 제약조건이다.

아래와 같이 사용 가능하다.

```sql
# foreign 제약조건 설정
create table 테이블명
(
    필드이름 필드타입,
    ...,
    [constraint 제약조건이름]
    foreign key (필드이름)
    references 테이블명 (필드이름)
);

# 테이블에 새로운 필드를 추가할 때 해당 필드를 foreign key 로 설정
alter table 테이블명
add [constraint 제약조건이름]
foreign key (필드이름)
references 테이블명 (필드이름);

# foreign key 제약조건 삭제
alter 테이블명
drop foreign key 제약조건이름;
```

만일 참조되는 테이블에서 데이터의 수정이나 삭제가 발생하면 참조하고 있는 테이블의 데이터도 영향을 받는다. 이 때 참조하고 있는 테이블의 동작을 아래의 키워드로 미리 설정 가능하다.

1. ON DELETE 
   * 참조되는 테이블이 삭제될 경우의 동작을 설정
2. ON UPDATE
   * 참조되는 테이블이 수정될 경우의 동작을 설정

이 때 설정 가능한 동작은 아래와 같다.

|       명령어        |                          동작                          |
|:----------------:|:----------------------------------------------------:|
|     CASCADE      |             참조하는 테이블에서도 삭제와 수정이 같이 이루어짐              |
|     SET NULL     |               참조하는 테이블의 데이터를 NULL 로 변경               |
|    NO ACTION     |                 참조하는 테이블의 데이터는 변경없음                  |
|   SET DEFAULT    |             참조하는 테이블의 데이터는 필드의 기본값으로 설정              |
|     RESTRICT     |    참조하는 테이블에 데이터가 남아 있으면, 참조되는 테이블의 데이터 삭제, 수정 불가    |

### 3. not null
> 해당 칼럼에 null 값이 들어올 수 없다는 제약조건을 명시하는 것이다.
> <br> 테이블 내에 반드시 존재해야하는 컬럼에 명시한다.

아래와 같이 사용 가능하다.

```sql
create table 테이블명
(
    필드이름 필드타입 not null,
    ...
);

alter table 테이블명
add 필드이름 필드타입 not null;
```

### 4. unique
> 설정된 칼럼에 중복된 값이 들어가지 못하게 설정하는 제약조건이다.
> <br> primary key 를 제외하고 테이블 내 다른 칼럼 중 중복된 값이 들어오면 안되는 경우에 설정 가능하다.
> <br> unique 제약 조건을 설정하면, 해당 필드는 자동으로 인덱스로 만들어진다.

아래와 같이 사용가능하다.

```sql
# 테이블 생성 시 unique 제약조건 추가
create table 테이블명
(
    필드이름 필드타입 unique,
    ...
);


# unique 제약조건 이름 설정
create table 테이블명
(
    필드이름 필드타입,
    ...,
    [constraint 제약조건이름] unique (필드이름)
);


# 테이블에 새 필드 추가할 때 unique 제약조건 설정
alter table 테이블명
add 필드이름 필드타입 unique;

alter table 테이블명
add [constraint 제약조건이름] unique (필드이름);

    
# 기존 필드에 unique 제약조건 설정
alter table 테이블명
modify column 필드이름 필드타입 unique;

alter table 테이블명
modify column [constraint 제약조건이름] unique (필드이름);
```

### 5. default
> default 제약 조건은 해당 필드의 기본값을 설정 할 수 있게 하는 제약조건이다.
> <br> 만일 레코드 입력 시 해당 필드 값이 전달되지 않으면, 자동으로 설정한 기본값을 저장한다.

아래와 같이 사용가능하다.

```sql
# 테이블 생성 시 default 값 설정
create table 테이블명
(
    필드이름 필드타입 default 기본값,
    ...
);


# 필드 추가 시 default 값 설정
alter table 테이블명
add 필드이름 필드타입 default 기본값;


# 기존 필드에 default 값 설정
alter table 테이블명
modify column 필드이름 필드타입 default 기본값;

alter table 테이블명
alter 필드이름 set default 기본값;

# default 값 삭제
alter table 테이블명
alter 필드이름 drop default;
```

### 6. check
> check 는 어떤 칼럼값이 check 제약조건으로 지정된 값 이외의 다른 값을 들어오지 못하게 하는 제약조건이다.
> <br> 칼럼에 들어오는 값에 범위가 필요하거나, 어떤 것의 유무나 여부를 따지는 칼럼에 주로 사용되며 무결성을 보장하게 한다.

아래와 같이 사용가능하다.

```sql
# check 제약조건 설정
alter table 테이블명
add constraint 제약조건이름 check 제약조건;
   
# check 제약조건 삭제
alter table 테이블명
drop constraint 제약조건이름;
```

---
### 참조
* [mysql 제약조건 알아보기 SQL 독학 강의#23편](https://stricky.tistory.com/308)
* [TCP SCHOOL - 제약조건](http://tcpschool.com/mysql/mysql_constraint_notNull)