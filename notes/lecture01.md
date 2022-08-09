# Lesson 1 - SELECT 전반 기능 훑어보기

## 1. 테이블의 모든 내용 보기

`*(asterisk)` 는 테이블의 모든 컬럼을 뜻한다.

```sql
SELECT * FROM Customers;
-- 주석은 -(dash) 2개를 연속으로 표기하여 작성
```

## 2. 원하는 column(열)만 골라서 보기

```sql
SELECT CustomerName FROM Customers;
```

```sql
SELECT CustomerName, ContactName, Country
FROM Customers;
```

💡 테이블의 컬럼이 아닌 값도 선택할 수 있다.

아래 구문의 1과 Hello, NULL을 확인

```sql
SELECT
  CustomerName, 1, 'Hello', NULL
FROM Customers;
```

## 3. 원하는 조건의 row(행)만 걸러서 보기

`WHERE` 구문 뒤에 조건을 붙여 원하는 데이터만 가져올 수 있다.

```sql
SELECT * FROM Orders
WHERE EmployeeID = 3;
```

```sql
SELECT * FROM OrderDetails
WHERE Quantity < 5;
```

## 4. 원하는 순서로 데이터 가져오기

`ORDER BY` 구문을 사용해서 특정 컬럼을 기준으로 데이터를 정렬 할 수 있다.

| 구문 |   기준   | 기본 |
| :--: | :------: | :--: |
| ASC  | 오름차순 |  ✔️  |
| DESC | 내림차순 |      |

```sql
SELECT * FROM Customers
ORDER BY ContactName;
```

```sql
SELECT * FROM OrderDetails
ORDER BY ProductID ASC, Quantity DESC;
-- ORDER BY ProductID asc, Quantity desc; 와 같이 소문자로 해도 동작함
```

## 5. 원하는 만큼만 데이터 가져오기

`LIMIT {가져올 개수}` 또는 `LIMIT {건너뛸 개수}, {가져올 개수}` 를 사용하여, 원하는 위치에서 원하는 만큼만 데이터를 가져올 수 있다.

항목을 몇개 부터 몇개까지 페이지를 나누어 표기하는 _PAGING_ 등에 활용될 수 있다

```sql
SELECT * FROM Customers
LIMIT 10;
```

```sql
SELECT * FROM Customers
LIMIT 0, 10;
```

```sql
SELECT * FROM Customers
LIMIT 30, 10;
```

## 6. 원하는 별명(alias)으로 데이터 가져오기

`AS`를 사용해서 컬럼명을 변경할 수 있다.

```sql
SELECT
  CustomerId AS ID,
  CustomerName AS NAME,
  Address AS ADDR
FROM Customers;
```

```sql
SELECT
  CustomerId AS '아이디',
  CustomerName AS '고객명',
  Address AS '주소'
FROM Customers;
-- 한글은 '' 안에 표기해야 함
```

## 모두 활용해보기

```sql
SELECT
  CustomerID AS '아이디',
  CustomerName AS '고객명',
  City AS '도시',
  Country AS '국가'
FROM Customers
WHERE
  City = 'London' OR Country = 'Mexico'
ORDER BY CustomerName
LIMIT 0, 5;
```

## 정리

```sql
SELECT ColumnName AS aliasName FROM TableName WHERE RowCondition ORDER BY ColumnName DESC LIMIT startNumber, endNumber;
```
