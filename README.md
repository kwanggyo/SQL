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

