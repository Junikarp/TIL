# SQL_11

## join
> * join 은 두개의 테이블을 서로 묶어서 하나의 결과를 만들어 내는 것이다.
> * 다시말해 여러 테이블이나 스키마에 분산된 데이터를 하나의 view 로 출력하게 하는 것이다.
> * inner join, outer join, cross join, self join 등의 join 이 있다.

## join 실습용 데이터 생성
```sql
create table student (
                         student_id int(10) comment '학생번호',
                         major_id int(10) comment '학과ID',
                         bl_prfs_id int(10) comment '담당교수ID',
                         name varchar(20) comment '학생이름',
                         tel varchar(15) comment '학생연락처'
);


create table professor (
                           prfs_id int(10) comment '교수ID',
                           bl_major_id int(10) comment '소속학과ID',
                           name varchar(20) comment '교수이름',
                           tel varchar(15) comment '교수연락처'
);

create table major (
                       major_id int(10) comment '학과ID',
                       major_title varchar(30) comment '학과명',
                       major_prfs_cnt int(5) comment '학과소속교수수',
                       major_student_cnt int(5) comment '학과소속학생수',
                       tel varchar(15) comment '학과사무실연락처'
);
```
위와 같이 테이블을 생성해준다.

```sql
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1001, 9901, 7029901, '한지호', '01098447362');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1002, 9902, 7029902, '김은숙', '01023456787');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1003, 9903, 7039903, '강경호', '01092938476');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1004, 9904, 7049904, '민현민', '01088786623');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1005, 9905, 7059905, '조승우', '01092877795');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1006, 9901, 7069901, '이남철', '01045671234');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1007, 9902, 7079902, '이강철', '01021213434');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1008, 9903, 7089903, '조민수', '01098937262');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1009, 9904, 7099904, '박찬경', '01029884432');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1010, 9905, 7109905, '이도경', '01029385647');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1011, 9901, 7019901, '이만호', '01099996453');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1012, 9902, 7029902, '김효민', '01092887666');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1013, 9903, 7039903, '최효성', '01098999933');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1014, 9904, 7049904, '우민국', '01087651112');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1015, 9905, 7059905, '지대한', '01093934848');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1016, 9901, 7069901, '한나름', '01023329882');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1017, 9902, 7079902, '유육경', '01099881111');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1018, 9903, 7089903, '조민경', '01023311120');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1019, 9904, 7099904, '경지수', '01029100293');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1020, 9905, 7109905, '오종환', '01098882226');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1021, 9901, 7019901, '조형민', '01098909876');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1022, 9902, 7029902, '이수강', '01099992222');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1023, 9903, 7039903, '서민호', '01092997654');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1024, 9904, 7049904, '박효숙', '01022293332');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1025, 9905, 7059905, '남궁옥경', '01099938475');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1026, 9901, 7069901, '피경남', '01029222233');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1027, 9902, 7079902, '고주경', '01099226655');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1028, 9903, 7089903, '하지만', '01022228965');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1029, 9904, 7099904, '기지효', '01012090912');
INSERT INTO student (student_id, major_id, bl_prfs_id, name, tel) VALUES (1030, 9905, 7109905, '박민호', '01074746363');

INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7019901, 9901, '김보경', '023445678');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7029902, 9902, '조숙', '023446789');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7039903, 9903, '이호', '023449584');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7049904, 9904, '박철남', '023449588');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7059905, 9905, '이만기', '023443443');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7069901, 9901, '강조교', '023449994');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7079902, 9902, '이희숙', '023443321');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7089903, 9903, '소머리', '023440123');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7099904, 9904, '두수위', '023443327');
INSERT INTO professor (prfs_id, bl_major_id, name, tel) VALUES (7109905, 9905, '지만래', '023449995');

INSERT INTO major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9901, '컴퓨터공학과', 7, 123, '023454321');
INSERT INTO major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9902, '아동보육학과', 8, 345, '023456676');
INSERT INTO major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9903, '국문학과', 6, 213, '023456567');
INSERT INTO major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9904, '경제학과', 5, 432, '023456987');
INSERT INTO major (major_id, major_title, major_prfs_cnt, major_student_cnt, tel) VALUES (9905, '사회복지학과', 9, 312, '023454534');
```
필요한 데이터를 입력해준다.

## join 의 종류

### 카티션곱 join
   * 테이블들을 join 할 때 join 조건을 기술하지 않고 하는 join 을 말한다.
   * 카티션곱 join 의 결과는 두 테이블을 row 건수를 서로 곱한 것 만큼의 결과를 출력한다. 

### Equi join
   * 양쪽 테이블의 어떤 칼럼에 같은 값이 존재할 때 이걸을 Equal 연산자(=)를 이용하여 양쪽에 다 존재하는 값만 결과로 출력하는 join 이다.
   * inner join 이라고도 불리운다.

### Non Equi join
   * Equi join 의 반대개념으로, 두 테이블의 칼럼에서 서로 다른값을 가지거나, 한쪽 데이터가 다른쪽 테이블의 데이터 범위 내에만 있는 것만 출력한다.
   * inner join 에 속한다.

### Outer join
* Outer join 은 left outer join, right outer join, full outer join 으로 구분된다.
* left outer join, right outer join 은 어느 한쪽의 데이터를 모두 출력하고 조건에 맞는 데이터만 다른 쪽에 출력하는 것을 말한다.
* 조건에 맞지 않는 데이터는 null 이 표시된다.

---
### 참조
* [mysql join (정의 및 종류) 11편 -sTricky](https://stricky.tistory.com/243)