# SQL_15

## outer join
> outer join 은 key 값을 기준으로 일치하는 값이 없더라도 모두 출력을 하는 join 이다.
> <br>left outer join, right outer join, full outer join 이 있으며 MySQL 에서는 full outer join 을 지원하지 않는다.
> <br>outer join 은 모든 데이터를 가지고 올때 full scan 을 하기 때문에 DB 에 무리를 가할 수 있으므로 적절할 때만 사용한다.

![SQL_15_1.png](image%2FSQL_15%2FSQL_15_1.png)

```sql
# MySQL 에서는 full outer join 을 union 으로 구현
select *
from A full outer join B
on A.a = B.b;

select *
from A left outer join B
on A.a = B.b
union
select *
from B left outer join A
on A.a = B.b;
```

## outer join 사용

실습에 앞서 inner join 에서 사용했던 학생테이블에 담당교수가 없는 학생들의 데이터를 추가한다.
```sql
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1031, 9901, null, '신채령', '01044755564');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1032, 9902, null, '이만도', '01022287777');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1033, 9903, null, '박만호', '01099972253');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1034, 9904, null, '최이강', '01029386577');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1035, 9905, null, '강이민', '01033334444');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1036, 9901, null, '민형도', '01099973331');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1037, 9902, null, '도지란', '01055567774');
```

학생 테이블과 교수 테이블을 교수 아이디를 기준으로 left outer join 해준다.

```sql
select s.name as 학생이름,
       s.bl_prfs_id as 교수아이디,
       p.name as 교수이름,
       p.prfs_id as 교수아이디
from student s left outer join professor p
on s.bl_prfs_id = p.prfs_id;
```

![SQL_15_2.png](image%2FSQL_15%2FSQL_15_2.png)

![SQL_15_3.png](image%2FSQL_15%2FSQL_15_3.png)

위의 사진과 같이 한쪽의 교수아이디가 null 값이거나 양쪽이 null 값이라 연결되지않은 데이터들도 누락되지않고 출력된 모습을 확인 가능하다.

```sql
select s.name as 학생이름,
       s.bl_prfs_id as 교수아이디,
       p.name as 교수이름,
       p.prfs_id as 교수아이디
from student s right outer join professor p
on s.bl_prfs_id = p.prfs_id;
```

![SQL_15_4.png](image%2FSQL_15%2FSQL_15_4.png)

같은 조건으로 right outer join 을 한 경우에는 왼쪽의 학생 테이블에서의 null 값은 포함하지 않는 모습을 확인 가능하다.

---
### 참조
* [outer join SQL 15편 -sTricky](https://stricky.tistory.com/260)