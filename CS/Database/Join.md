> Join이란 두개 이상의 테이블을 묶어 하나의 결과 집합으로 만들어 내는  과정을  말한다.
> Join에는 크게 INNER JOIN, OUTER JOIN, CROSS JOIN, SELF JOIN이 있다.


## INNER JOIN
두가지 테이블에 내용이 존재하는 경우 결과가 검색된다.

```sql
SELECT <column 목록>
FROM <기준 테이블>
	INNER JOIN <참조 테이블>
	ON <조인 조건>
[WHERE 검색 조건]
```

## OUTER JOIN
두가지 테이블 중 하나의 테이블에만 내용이 있는 경우에도 결과가 검색된다.

```sql
SELECT <column 목록>
FROM <첫번째 테이블(LEFT)>
	< LEFT | RIGHT | OUTER > [OUTER] JOIN <두번째 테이블(RIGHT)>
	ON <조인 조건>
[WHERE 검색 조건]
```

LEFT OUTER JOIN의 경우 


## 