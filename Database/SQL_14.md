# SQL_14

## 비등가 join
> 비등가 join 은 A,B 두 테이블을 join 할 때 값이 서로 같지는 않지만 join 조건에서 지정한 범위에 일치할 때 서로 데이터를 join 해 주는 것을 이야기한다.

## 비등가 join 예시
실습을 진행하기에 앞서 필요한 테이블을 생성하고 데이터를 넣어준다.
```sql
create table customer
( name varchar(10),
point int);

create table gift
(
	name varchar(20) null,
	point_s int null,
	point_e int null
);


INSERT INTO customer (name, point) VALUES ('조성모', 5);
INSERT INTO customer (name, point) VALUES ('이기찬', 12);
INSERT INTO customer (name, point) VALUES ('이소라', 14);
INSERT INTO customer (name, point) VALUES ('서태지', 18);
INSERT INTO customer (name, point) VALUES ('박효신', 21);
INSERT INTO customer (name, point) VALUES ('김정민', 16);
INSERT INTO customer (name, point) VALUES ('양파', 9);
INSERT INTO customer (name, point) VALUES ('강수지', 22);
INSERT INTO customer (name, point) VALUES ('강타', 24);


INSERT INTO gift (name, point_s, point_e) VALUES ('공기청정기', 11, 15);
INSERT INTO gift (name, point_s, point_e) VALUES ('아이폰11', 21, 25);
INSERT INTO gift (name, point_s, point_e) VALUES ('로봇청소기', 6, 10);
INSERT INTO gift (name, point_s, point_e) VALUES ('상품권', 1, 5);
INSERT INTO gift (name, point_s, point_e) VALUES ('스마트패드', 16, 20);
```
아래와 같이 고객테이블과 선물테이블을 확인 가능하다.

* 고객테이블

![SQL_14_1.png](image%2FSQL_14%2FSQL_14_1.png)

* 선물테이블

![SQL_14_2.png](image%2FSQL_14%2FSQL_14_2.png)

---

위와 같은 상황에서 어떤 선물에 필요한 최소 포인트와 최대 포인트 사이의 포인트를 가지고 있다면 선물을 지급하는 선물 매칭 테이블을 비동기 join 을 통해 만들 수 있다.
```sql
# MySQL
select c.name as 고객명,
       c.point as 보유포인트,
       g.name as 상품명
from customer c,
     gift g
where c.point between g.point_s and g.point_e;

# Ansi SQL
select c.name as 고객명,
       c.point as 보유포인트,
       g.name as 상품명
from customer c join 
     gift g
on c.point between g.point_s and g.point_e;
```

![SQL_14_3.png](image%2FSQL_14%2FSQL_14_3.png)

위와 같이 A 이상 B 이하를 뜻하는 `between A and B`를 이용하여 비동기 join 을 작성하는 것이 가능하다.

---

### 참조
* [비등가 join with ansi SQL 14편 -sTricky](https://stricky.tistory.com/255)