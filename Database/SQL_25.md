# SQL_25

## view
> 뷰는 가상의 테이블로 데이터는 없지만, SQL 이 저장되어 있는 object 를 말하며, 하나 이상의 기본 테이블이나 다른 뷰를 이용하여 생성된다.
> <br> 뷰를 select 하게 되면 view 가 가지고 있는 SQL 문이 실행된다.

![SQL_25_1.png](image%2FSQL_25%2FSQL_25_1.png)

## view 의 필요성
* 사용자마다 특정 객체만 조회할 수 있도록 할 필요가 있다.
* 복잡한 질의문을 뷰를 통해 단순화 할 수 있다.
* 데이터의 중복성을 최소화 할 수 있다.

## view 의 장·단점
* 장점
   * 논리적 독립정을 제공한다.
   * 데이터의 접근을 제어한다. (보안에 용이)
   * 사용자의 데이터 관리를 단순화한다.
   * 여러 사용자의 다양한 데이터 요구를 지원한다.
* 단점
   * 뷰의 정의를 변경 불가하다. (뷰에서는 alter 명령어를 사용할 수 없으므로 내용 수정을 위해서는 drop and create 를 해야한다.)
   * 삽입, 삭제, 갱신 연산에 제한이 있다.

## view 사용 방법
* view 생성
```sql
create view 뷰이름 as select 구문;
```

* view 삭제
```sql
drop view 뷰이름;
```

---

### 참조
* [뷰(view) - 뷰의 개념 / 필요성 / 장단점 / 구문 / 종류](https://reeme.tistory.com/54)
* [view 뷰에 대한 이해 SQL 독학 강의#25편](https://stricky.tistory.com/323)