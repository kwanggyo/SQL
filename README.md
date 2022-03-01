# SQL

Structured Query Language(구조적 질의 언어)의 줄임말로, 관계형 데이터베이스 시스템(RDBMS)에서 자료를 관리 및 처리하기 위해 설계된 언어이다.

## SQL 문법의 종류

**DDL(Data Definition Language, 데이터 정의 언어)**

- 각 릴레이션을 정의하기 위해 사용되는 언어이다.
- DB 설계 단계에서 주로 사용된다.
- CREATE, ALTER, DROP...

**DML(Data manipulation Language, 데이터 조작 언어)**

- 데이터를 추가, 수정, 삭제하기 위한 즉, 데이터 관리를 위한 언어이다.
- SELECT, INSERT, UPDATE, DELETE...

**DCL(Data Control Language, 데이터 제어 언어)**

- 사용자 관리 및 사용자별로 릴레이션 또는 데이터를 관리하고 접근하는 권한을 다루기 위한 언어이다.
- GRANT, REVOKE...

## SQL의 언어적 특성

1. 대소문자를 가리지 않는다.

   단, 서버 환경이나 DBMS 종류에 따라 데이터베이스 또는 필드명에 대해 대소문자를 구분하기도 한다.

2. SQL 명령은 반드시 세미콜론(;)으로 끝나야 한다.

   세미콜론(;)을 만나기 전까지 절대 실행되지 않는다. → 비교적 자유롭게 들여쓰기 가능

3. 고유의 값은 따옴표(’’)로 감싸준다.

   ```sql
   SELECT * FROM INFO NAME = ‘GilDong’;
   ```

4. SQL에서 객체를 나타낼 때는 백틱(``)으로 감싸준다.

   ```sql
   SELECT `COST`, `TYPE`, FROM `INVOICE`;
   ```

5. 한 줄 주석은 문장 앞에 --를 붙여서 사용한다.

   ```sql
   -- SELECT * FROM INFO; → 실행되지 않는다.
   ```

6. 여러 줄 주석은 /* */로 감싸준다.

   ```sql
   /*
   SELECT * FROM INFO WHERE ID=(SELECT * FROM WHERE NAME=’홍길동’)
   */
   ```

## 용어의 개념

**스키마**

관계형 데이터베이스에서 구조와 제약조건에 관련한 전반적인 명세를 기술 한 것

**테이블**

열과 행의 모델을 사용해 조직된 데이터 요소들의 집합

**컬럼**

고유한 데이터 형식이 지정되는 열

**레코드**

단일 구조 데이터 항목을 가리키는 행

**기본키**

각 행의 고유 값

## 데이터 추가, 읽기, 수정, 삭제(CRUD)

### C : INSERT

INSERT INTO classmates(name, age, address) VALUES(’홍길동’, ‘30’, ‘서울’);

```sql
INSERT INTO table (column1, column2, ...)
VALUES(value1, value2);
```

### R : SELECT

SELECT * FROM classmates WHERE id=1;

```sql
-- 모든 컬럼 가져오기 --
SELECT * FROM table;

-- 특정 컬럼 가져오기 --
SELECT column1, column2 FROM table;

-- LIMIT: 원하는 개수(num)만큼 가져오기 -- 
SELECT column1, column2
FROM table
LIMIT num;

-- OFFSET: 특정 위치에서부터 가져올 때 --
-- (맨 위부터 num만큼 떨어진 값부터 가져온다는 의미)
SELECT column1, column2
FROM table
LIMIT num OFFSET num;

-- WHERE: 조건을 통해 값 가져오기 --
SELECT column1, column2
FROM table
WHERE column=value;

-- DISTINCT: 중복없이 가져오기 -- 
SELECT DISTINCT column FROM table;
```

### U : UPDATE

UPDATE classmates SET name=’철수’ WHERE id=1;

```sql
UPDATE table
SET column1=value1, column2=value2, ...
WHERE condition;

ex)
-- 이팡교님의 이름을 이광교로 바꾼다고 하면... --
UPDATE classmates
SET name='이광교', address='대한민국'
WHERE name='이팡교';
```

### D : DELETE

DELETE FROM classmates WHERE id=1;

```sql
DELETE FROM table
WHERE condition;

ex)
DELETE FROM classmates
WHERE name='팡교';
```

## 심화 SQL문

### Expressions

- COUNT (레코드 값들의 개수 반환)

  ```
  SELECT COUNT(*) FROM users;
  ```

- AVG (레코드 값들의 평균값 반환)

  ```
  SELECT AVG(age)
  FROM users
  WHERE age >= 30;
  ```

- MAX (레코드 값들의 최대값 반환)

- MIN (레코드 값들의 최소값 반환)

- SUM (레코드 값들의 합 반환)

### LIKE

LIKE는 두 가지 와일드 카드(언더스코어 그리고 퍼센트 기호)와 함께 동작한다.

- `_` (반드시 이 자리에 한 개의 문자가 존재해야 한다는 뜻)

  ```
  -- 20대인 사람들만 가져올 때 --
  SELECT *
  FROM users
  WHERE age LIKE '2_';
  ```

- `%` (이 자리에 문자열이 있을 수도, 없을 수도 있다. 0개 이상이라는 뜻)

  ```
  -- 지역번호가 02인 사람만 가져올 때 --
  SELECT *
  FROM users
  WHERE phone LIKE '02-%';
  ```

- 두 개를 조합해서 사용할 수도 있다.

  ```
  -- 핸드폰 중간 번호가 반드시 4자리면서 511로 시작되는 사람들 --
  
  SELECT * FROM users
  WHERE phone LIKE '%-511_-%';
  ```

### ORDER BY(정렬)

- ASC : 오름차순, DESC : 내림차순

  ```sql
  SELECT columns FROM table
  ORDER BY column1, column2 ASC | DESC;
  
  -- ASC: 오름차순 / DESC: 내림차순 --
  ```

- 예시

  ```sql
  -- 나이, 성 순서로 오름차순 정렬하여 상위 10개만 뽑아보면? --
  SELECT * 
  FROM users
  ORDER BY age, last_name ASC
  LIMIT 10;
  ```

### GROUP BY

- 지정된 기준에 따라 행 세트를 그룹으로 결합한다.

- 데이터를 요약하는 상황에서 주로 사용한다.

  ```sql
  SELECT column1, aggregate_function(column_2)
  FROM table
  GROUP BY column1, column2;
  ```

- 예시

  ```sql
  -- 성(last_name)씨가 몇 명인지 조회할 때 --
  SELECT last_name, COUNT(*)
  FROM users
  GROUP BY last_name;
  ```

