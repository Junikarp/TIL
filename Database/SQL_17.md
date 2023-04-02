# SQL_17

## insert
> insert 는 기존에 없는 새로운 튜블을 테이블에 넣기위한 명령문이다.
> <br>join 이 가능한 select 와 다르게 insert 는 한 번에 하나의 테이블에만 데이터를 넣을 수 있다.

## insert 방법

실습에 앞서 insert 문을 실행해보기 위한 테이블을 생성한다.

```sql
create table insert_test
(
    seq        int(10) primary key ,
    cont       text,
    name       varchar(15),
    tel_num    int(11),
    input_date datetime
);
```

### 단일행 입력 (칼럼 미지정)
데이터를 insert 할 때 테이블의 칼럼을 지정하지 않고 insert 하는 방법

* 실습
```sql
insert into insert_test values (1,'안녕하세요', '강백호', 01012345678, now());
```

![SQL_17_1.png](image%2FSQL_17%2FSQL_17_1.png)

사진과 같이 데이터가 입력된 모습을 확인 가능하다.

```sql
insert into [테이블명] values ([seq],[cont],[name],[tel_num],[input_date]);
```

위의 실습 예시와 같이 칼럼을 미지정 할 때에는 `insert into` 대상 테이블명을 적고, 테이블의 컬럼 생성 순서에 맞게 `,`로 분리하여 나열하면 된다.
<br> 이 때 숫자로 정의된 칼럼에 데이터를 넣을때는 `'`로 감싸지 않아도 되며, text,varchar 등 문자로 정의된 컬럼에 데이터를 넣을때에는 `'`로 데이터 양쪽을 감싸야한다.

### 단일행 입력 (칼럼 지정)
데이터를 insert 할 때 테이블 명 뒤에 칼럼을 지정해서 넣는 방법이다.

* 실습
```sql
insert into insert_test (seq, cont, name) values (2,'안녕하세요', '강백호');
```

![SQL_17_2.png](image%2FSQL_17%2FSQL_17_2.png)

위의 예시와 같이 테이블명 뒤에 `(` 괄호를 적고, 테이블의 칼럼명을 적은 후 데이터를 넣을 수 있다.
<br> 이 때 칼럼 미지정 때와 다르게, 들어가는 데이터의 순서는 `()` 소괄호 안의 컬럼의 순서가 된다.

### 복수행 입력하기
```sql
insert into insert_test
values (3, '복수행입력1', '강백호', 01012345678, now()),
       (4, '복수행입력2', '강백호', 01012345678, now()),
       (5, '복수행입력3', '강백호', 01012345678, now()),
       (6, '복수행입력4', '강백호', 01012345678, now()),
       (7, '복수행입력5', '강백호', 01012345678, now());
```

![SQL_17_3.png](image%2FSQL_17%2FSQL_17_3.png)

위의 사진과 같이 복수의 행으로 데이터를 입력하여 insert 하는 것도 가능하다.




---
### 참조
* [mysql insert 사용 방법 17편 -sTricky](https://stricky.tistory.com/268)
