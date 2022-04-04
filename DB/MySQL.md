# MySQL 복습



- 기본 골자

``` sql
SELECT 속성 as 나타낼 이름
FROM 테이블
WHERE 조건
```



- `*` : 모든 것을 고름

- `order by` : 정렬 

- `limit`: 보여주는 개수

  ```sql
  SELECT DATETIME as 시간 
  from ANIMAL_INS order by DATETIME desc //내림차순
  limit 1 // 한개만 보여줌
  ```

- `count` : 개수 세기

- `group by`: 특성 속성으로 같은 그룹나누기

  ```sql
  SELECT ANIMAL_TYPE,count(*) as count 
  from ANIMAL_INS 
  group by ANIMAL_TYPE 
  order by ANIMAL_TYPE
  ```

- `having` : 그룹의 조건 정하기

  ```sql
  SELECT NAME, count(name) as count 
  from ANIMAL_INS  
  group by NAME 
  having count > 1
  ORDER BY NAME
  ```

- `SUM`

- `MAX`, `MIN`

- `distinct` : 중복 거르기

- `IS NULL`

- `LEFT JOIN`, `RIGHT JOIN`

  ```sql
  SELECT A.ANIMAL_ID, A.ANIMAL_TYPE, A.NAME
  FROM ANIMAL_OUTS A LEFT JOIN ANIMAL_INS B
  ON A.ANIMAL_ID = B.ANIMAL_ID // 조인의 조건
  WHERE A.SEX_UPON_OUTCOME != B.SEX_UPON_INTAKE AND A.ANIMAL_ID IS NOT NULL 
  ORDER BY A.ANIMAL_ID 
  ```

  