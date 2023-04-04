# SQL_20

## insert into on duplicate key
> 어떤 데이터를 입력할 때, 대상 테이블에 해당 키에 해당하는 데이터가 있으면 insert 문을 실행하여 입력한다.
> <br> 해당 키가 이미 대상 테이블에 있다면 해당 키의 칼럼값을 update 하여 값을 갱신한다.
> <br> oracle 에서의 merge 문과 같은 기능이다.

![SQL_20_3.png](image%2FSQL_20%2FSQL_20_3.png)

위의 사진과 같이 원본 테이블에 존재하지 않는 key 값을 가진 데이터는 insert 되고, 그렇지 않은 데이터는 update 하는 것을 확인 가능하다.

## insert into on duplicate key 작성방법
실습에는 insert 문을 실습할 때 사용했었던 `insert_test`, `insert_test2` 테이블을 사용한다.

* insert_test

![SQL_20_1.png](image%2FSQL_20%2FSQL_20_1.png)

* insert_test2

![SQL_20_2.png](image%2FSQL_20%2FSQL_20_2.png)

### 실습
```sql
insert into insert_test
select * from insert_test2 b
on duplicate key update name = b.name,
                        cont = b.cont,
                        tel_num = b.tel_num,
                        input_date = b.input_date;
```

![SQL_20_4.png](image%2FSQL_20%2FSQL_20_4.png)

위의 사진과 같이 key 값인 `seq` 가 3으로 중복인 데이터는 update 되고 1,2 인 부분은 새롭게 insert 된 모습을 확인 가능하다.

```sql
insert into insert_test
values (2, '감사합니다', '채치수', 12345678, now())
on duplicate key update cont = '감사합니다',
                        name = '채치수',
                        tel_num = 12345678,
                        input_date = now();
```
```sql
insert into insert_test
values (6, '감사합니다', '채치수', 12345678, now())
on duplicate key update cont = '감사합니다',
                        name = '채치수',
                        tel_num = 12345678,
                        input_date = now();
```

위와 같이 데이터를 삽입할 때에도 키값에 따라 update 되거나 insert 되는 모습을 확인 가능하다.

---
### 참조
* [insert into on duplicate key MySQL merge SQL 독학 강의#20편 -sTricky](https://stricky.tistory.com/286)
