# SQL_13

## inner join
> inner join 은 A,B 두 테이블이 있을 때 서로 연결되는 key 가 있다고 가정하고, 해당 키의 값이 같은 데이터를 가지고 와서 출력하는 것을 의미한다.

## inner join 사용
아래와 같이 학과 테이블과 교수 테이블이 있다.
```sql
select * from class.major;
```

![SQL_13_1.png](image%2FSQL_13%2FSQL_13_1.png)

```sql
select * from professor;
```

![SQL_13_2.png](image%2FSQL_13%2FSQL_13_2.png)

두 테이블을 살펴보면 교수 테이블과 학과 테이블에 각각 `bl_major_id`,`major_id`라는 이름의 소속 학과 데이터가 존재한다.
<br> 이 소속학과는 두 테이블을 연결해주는 key 가 될 수 있으며 이것을 Foreign Key, 줄여서 FK 라고 부른다.
<br> 우리는 inner join 시에 이 FK 를 조건으로서 넣어주게 된다.

---
위의 FK 를 사용하여 우리는 아래와 같이 inner join 할 수 있다.

```sql
select p.name as 교수이름, m.major_title as 학과명
from professor p , major m
where p.bl_major_id = m.major_id;
```
또한 아래와 같이 작성하여도 같은 결과를 얻을 수 있다.
```sql
select p.name as 교수이름, m.major_title as 학과명
from professor p
         join major m
              on p.bl_major_id = m.major_id;
              
select p.name as 교수이름, m.major_title as 학과명
from professor p
         cross join major m
              on p.bl_major_id = m.major_id;
              
select p.name as 교수이름, m.major_title as 학과명
from professor p
         inner join major m
              on p.bl_major_id = m.major_id;
```

![SQL_13_3.png](image%2FSQL_13%2FSQL_13_3.png)

위와 같이 교수이름과 학과명이 연결된 테이블을 얻을 수 있다.

## 3개의 테이블을 inner join
3개의 테이블을 inner join 하는 것은 먼저 2개의 테이블을 join 한 후 나머지 테이블과 join 해주는 방식이다.

![SQL_13_5.png](image%2FSQL_13%2FSQL_13_5.png)

이번에는 학생 테이블을 추가하여 3개의 테이블을 inner join 해본다.

```sql
select * from student;
```

![SQL_13_4.png](image%2FSQL_13%2FSQL_13_4.png)

아래와 같이 공통된 FK 를 찾아서 테이블 2개씩 inner join 해준다.
```sql
# MySQL
select m.major_title as 학과이름,
       p.name as 교수이름,
       s.name as 학생이름
from  major as m,
      professor as p,
      student as s
where m.major_id = p.bl_major_id and
      m.major_id = s.major_id;

# Ansi SQL
select m.major_title as 학과이름,
       p.name as 교수이름,
       s.name as 학생이름
from  major as m 
    inner join professor as p 
    inner join student as s
      on m.major_id = p.bl_major_id 
             and m.major_id = s.major_id;
```

![SQL_13_6.png](image%2FSQL_13%2FSQL_13_6.png)

위의 사진과 같이 3개의 테이블이 inner join 된 것을 확인 가능하다.

---
### 참조
* [inner join with ansi SQL 13편 -sTricky](https://stricky.tistory.com/248)