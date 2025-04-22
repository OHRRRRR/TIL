# 인덱싱과 쿼리 최적화 전략

## 1. 인덱스(Index)란?

인덱스는 데이터베이스에서 **데이터 검색 속도를 향상**시키기 위한 자료구조이다. 인덱스를 활용하면 테이블을 풀스캔하지 않고도 원하는 데이터를 빠르게 찾을 수 있다.

### 🔹 인덱스의 종류

- **B-Tree 인덱스**: 대부분의 RDBMS에서 기본으로 사용.
- **Hash 인덱스**: 해시 기반으로 정확한 값 조회에 빠르나 범위 검색 불가능.
- **Bitmap 인덱스**: 값의 종류가 적은 컬럼에 적합 (예: 성별).
- **Composite 인덱스**: 여러 컬럼을 조합한 인덱스.

```sql
-- 단일 인덱스 생성
CREATE INDEX idx_user_name ON users(name);

-- 복합 인덱스 생성
CREATE INDEX idx_user_name_age ON users(name, age);
```

### 🔸 인덱스 사용 시 주의사항

- 자주 조회되는 컬럼에 적용
- WHERE 절, JOIN, ORDER BY, GROUP BY 등에 사용되는 컬럼에 적용
- INSERT/UPDATE/DELETE 성능 저하 유의 (인덱스도 갱신 필요하기 때문)

---

## 2. 인덱스가 사용되지 않는 경우

- 함수로 감싸진 컬럼 (예: `WHERE UPPER(name) = 'JOHN'`)
- `LIKE '%값%'` 와 같이 와일드카드 앞에 오는 검색
- 인덱스의 순서를 지키지 않은 복합 인덱스 접근

```sql
-- 복합 인덱스 순서 유의
CREATE INDEX idx_name_age ON users(name, age);

-- name으로 먼저 검색하지 않으면 인덱스 미사용
SELECT * FROM users WHERE age = 25; -- 인덱스 비사용 가능성
```

---

## 3. 실행 계획(EXPLAIN)으로 성능 분석

SQL 쿼리의 실행 계획을 분석하여 어떤 방식으로 데이터에 접근하고 있는지 확인할 수 있다.

```sql
EXPLAIN SELECT * FROM users WHERE name = 'Alice';
```

### 주요 컬럼 의미

- **type**: 접근 방식 (ALL, index, range, ref, const 등)
- **key**: 사용된 인덱스
- **rows**: 예측 검색 행 수
- **Extra**: 인덱스 사용 여부 및 조건 적용 방식

---

## 4. 실무에서 자주 쓰는 쿼리 최적화 팁

### ✅ SELECT 문 최적화

- 필요한 컬럼만 SELECT
- 서브쿼리 대신 JOIN 활용
- WHERE 조건 최대한 빠르게 적용

```sql
-- 나쁜 예: 전체 데이터 가져옴
SELECT * FROM orders;

-- 좋은 예: 필요한 컬럼만 선택
SELECT id, total_price FROM orders WHERE created_at >= '2024-01-01';
```

### ✅ JOIN 최적화

- 조인 순서, 인덱스 여부 확인
- 드라이빙 테이블의 행 수 최소화
- ON 절 조건 명확하게 작성

```sql
-- 잘못된 JOIN 순서로 인해 성능 저하
SELECT * FROM big_table A JOIN small_table B ON A.id = B.a_id;

-- 최적화된 JOIN 순서 (small_table 먼저 필터링)
SELECT * FROM small_table B JOIN big_table A ON A.id = B.a_id;
```

### ✅ 서브쿼리 최적화

- 중복 호출 방지 → WITH 문 (CTE) 사용 고려
- EXISTS / IN 의 차이 이해

```sql
-- EXISTS vs. IN
SELECT name FROM users u WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.user_id = u.id
);
```

---

## 5. 파티셔닝과 샤딩

### 🔹 파티셔닝(Partitioning)

하나의 테이블을 논리적으로 분할하여 관리. 대량의 데이터 처리에 유리.

- Range Partition
- List Partition
- Hash Partition

```sql
CREATE TABLE sales (
  id INT,
  sale_date DATE,
  amount INT
)
PARTITION BY RANGE (YEAR(sale_date)) (
  PARTITION p2022 VALUES LESS THAN (2023),
  PARTITION p2023 VALUES LESS THAN (2024)
);
```

### 🔹 샤딩(Sharding)

물리적으로 데이터를 나누어 여러 DB 서버에 분산 저장. 확장성 확보.

---

## 6. SQL 성능 분석 도구

- **MySQL**: `EXPLAIN`, `SHOW PROFILE`, `SLOW QUERY LOG`
- **PostgreSQL**: `EXPLAIN ANALYZE`
- **Oracle**: `AUTOTRACE`, `SQL TRACE`

---

## 🔚 마무리

인덱스는 성능 개선의 핵심이지만, 잘못 사용할 경우 오히려 오버헤드가 될 수 있다. 항상 실행 계획과 실제 데이터 분포를 기반으로 최적화하는 습관이 필요하다.

---

## 📌 참고 자료

- [MySQL 공식문서: 인덱스](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)
- [PostgreSQL 성능 튜닝 가이드](https://wiki.postgresql.org/wiki/Performance_Optimization)
