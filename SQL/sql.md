# 🗄️ SQL (Structured Query Language)

## 📌 개요

SQL(Structured Query Language)은 관계형 데이터베이스(RDBMS)에서 데이터를 정의, 조작, 제어하기 위한 표준 프로그래밍 언어입니다. MySQL, PostgreSQL, Oracle, SQL Server 등 다양한 시스템에서 사용되며, 데이터베이스를 다루는 개발자나 분석가에게 필수적인 기술입니다.

이 문서는 SQL의 전반적인 개념, 구문, 고급 기능 및 실무 활용 팁까지 폭넓고 깊이 있게 다룹니다.

---

## 🧱 1. SQL의 주요 종류

### 1.1 DDL (Data Definition Language)

- 데이터베이스 구조 정의

```sql
CREATE, ALTER, DROP, TRUNCATE
```

### 1.2 DML (Data Manipulation Language)

- 데이터를 삽입, 수정, 삭제, 조회

```sql
SELECT, INSERT, UPDATE, DELETE
```

### 1.3 DCL (Data Control Language)

- 사용자 권한 제어

```sql
GRANT, REVOKE
```

### 1.4 TCL (Transaction Control Language)

- 트랜잭션 관리

```sql
COMMIT, ROLLBACK, SAVEPOINT
```

---

## 🔍 2. SELECT 문 기본 구문

```sql
SELECT column1, column2
FROM table_name
WHERE 조건
GROUP BY column
HAVING 조건
ORDER BY column ASC|DESC
LIMIT 숫자;
```

### ✅ 예시

```sql
SELECT name, salary
FROM employees
WHERE department = 'Sales'
ORDER BY salary DESC
LIMIT 10;
```

---

## 📊 3. JOIN의 종류와 활용

관계형 데이터베이스의 핵심: 여러 테이블을 논리적으로 연결

### INNER JOIN

- 공통된 키를 기준으로 양쪽 모두에 존재하는 값만 반환

```sql
SELECT *
FROM orders o
INNER JOIN customers c ON o.customer_id = c.id;
```

### LEFT JOIN / RIGHT JOIN

- 기준 테이블(왼쪽 또는 오른쪽)을 모두 포함

### FULL OUTER JOIN (일부 RDBMS에서 지원)

- 양쪽 테이블 모두의 모든 행 반환

### SELF JOIN

- 같은 테이블을 자기 자신과 JOIN

---

## 🧮 4. GROUP BY & 집계 함수

### 🔢 집계 함수

- `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`

### ✅ 예시

```sql
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department
HAVING avg_salary > 5000;
```

---

## 🧩 5. 서브쿼리와 CTE

### 서브쿼리 (Subquery)

- SELECT 내에서 또 다른 SELECT 실행

### CTE (Common Table Expression)

```sql
WITH high_salary AS (
  SELECT * FROM employees WHERE salary > 7000
)
SELECT name FROM high_salary;
```

---

## ⚙️ 6. 인덱스 & 성능 최적화

### ✅ 인덱스(Index)

- 검색 속도 향상 vs. 쓰기 성능 저하
- B-Tree, Hash 인덱스

### 🔍 최적화 팁

- WHERE 절에 자주 등장하는 컬럼에 인덱스 생성
- EXPLAIN 키워드로 실행 계획 확인
- 정규화와 반정규화의 균형 유지

---

## 🔐 7. 트랜잭션과 ACID

### 트랜잭션(Transaction)

- 여러 쿼리를 하나의 작업 단위로 묶음

### ACID 원칙

- **Atomicity**: 모두 실행되거나 모두 실패
- **Consistency**: 일관된 상태 유지
- **Isolation**: 트랜잭션 간 간섭 없음
- **Durability**: 영구적으로 저장

### ✅ 예시

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

---

## 💾 8. 정규화와 테이블 설계

### 정규화(Normalization)

- 중복 제거와 무결성 보장을 위한 테이블 분해 과정
- 1NF → 2NF → 3NF → BCNF

### 반정규화(Denormalization)

- 성능 향상을 위해 중복을 허용하고 구조 단순화

### 설계 팁

- 명확한 기본 키 설정
- 제약 조건 (PRIMARY KEY, FOREIGN KEY, UNIQUE 등)
- 다대다 관계는 중간 테이블로 처리

---

## 🧰 9. 실무에서 자주 쓰는 고급 기능

### CASE 문

```sql
SELECT name,
  CASE
    WHEN score >= 90 THEN 'A'
    WHEN score >= 80 THEN 'B'
    ELSE 'F'
  END AS grade
FROM students;
```

### 윈도우 함수

```sql
SELECT name, salary,
  RANK() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank
FROM employees;
```

### JSON 데이터 다루기 (PostgreSQL, MySQL 5.7+)

```sql
SELECT json_data->>'name' AS name
FROM users
WHERE json_data->>'age'::int > 25;
```

---

## 🛠️ 유용한 SQL 툴 및 클라우드 플랫폼

- SQL Developer (Oracle)
- DBeaver, TablePlus, DataGrip
- AWS RDS / Aurora
- Google Cloud SQL

---

## 📚 참고 자료

- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [Mode Analytics SQL SQL School](https://mode.com/sql-tutorial/)
- [PostgreSQL 공식 문서](https://www.postgresql.org/docs/)
- [MySQL 공식 문서](https://dev.mysql.com/doc/)

---
