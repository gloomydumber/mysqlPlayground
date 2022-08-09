# Lesson 2 - 각종 연산자들

## 1. 사칙연산

|   연산자    |               의미                |
| :---------: | :-------------------------------: |
| +, -, \*, / | 각각 더하기, 빼기, 곱하기, 나누기 |
|   %, MOD    |              나머지               |

```sql
SELECT 1 + 2;
```

```sql
SELECT 5 - 2.5 AS DIFFERENCE;
```

```sql
SELECT 3 * (2 + 4) / 2, 'Hello';
```

```sql
SELECT 10 % 3;
```

❗ 문자열에 사칙연산을 가하면 0으로 인식

```sql
SELECT 'ABC' + 3;
```

```sql
SELECT 'ABC' * 3;
```

```sql
SELECT '1' + '002' * 3;

-- 숫자로 구성된 문자열은 숫자로 자동인식
```

```sql
SELECT
  OrderID + ProductID
FROM OrderDetails;
```

```sql
SELECT
  ProductName,
  Price / 2 AS HalfPrice
FROM Products;
```

## 2. 참/거짓 관련 연산자

```sql
SELECT TRUE, FALSE;
```

```sql
SELECT !TRUE, NOT 1, !FALSE, NOT FALSE;
```

💡 MySQL에서는 TRUE는 1, FALSE는 0으로 저장됩니다.

```sql
SELECT 0 = TRUE, 1 = TRUE, 0 = FALSE, 1 = FALSE;
```

```sql
SELECT * FROM Customers WHERE TRUE;
```

```sql
SELECT * FROM Customers WHERE FALSE;
```

| 연산자 |            의미             |
| :----: | :-------------------------: |
|   IS   | 양쪽이 모두 TRUE 또는 FALSE |
| IS NOT |  한쪽은 TRUE, 한쪽은 FALSE  |

```sql
SELECT TRUE IS TRUE;
```

```sql
SELECT TRUE IS NOT FALSE;
```

```sql
SELECT (TRUE IS FALSE) IS NOT TRUE;
```

|  연산자  |             의미             |
| :------: | :--------------------------: |
| AND, &&  | 양쪽이 모두 TRUE일 때만 TRUE |
| OR, \|\| | 양쪽이 모두 TRUE일 때만 TRUE |

```sql
SELECT TRUE AND FALSE, TRUE OR FALSE;
```

```sql
SELECT 2 + 3 = 6 OR 2 * 3 = 6;
```

```sql
SELECT * FROM Orders
WHERE
  CustomerId = 15 AND EmployeeId = 4;
```

```sql
SELECT * FROM Products
WHERE
  ProductName = 'Tofu' OR CategoryId = 8;
```

```sql
SELECT * FROM OrderDetails
WHERE
  ProductId = 20
  AND (OrderId = 10514 OR Quantity = 50);
```

| 연산자 |               의미               |
| :----: | :------------------------------: |
|   =    |          양쪽 값이 같음          |
| !=, <> |          양쪽 값이 다름          |
|  >, <  |    (왼쪽, 오른쪽) 값이 더 큼     |
| >=, <= | (왼쪽, 오른쪽) 값이 같거나 더 큼 |

```sql
SELECT 1 = 1, !(1 <> 1), NOT (1 < 2), 1 > 0 IS NOT FALSE;
```

```sql
SELECT 'A' = 'A', 'A' != 'B', 'A' < 'B', 'A' > 'B';
```

```sql
SELECT 'Apple' > 'Banana' OR 1 < 2 IS TRUE;
```

❗ MySQL의 기본 사칙연산자는 대소문자 구분을 하지 않습니다.

```sql
SELECT 'A' = 'a';
```

```sql
SELECT
  ProductName, Price,
  Price > 20 AS EXPENSIVE
FROM Products;
```

💡 테이블의 컬럼이 아닌 값으로 선택하기.

```sql
SELECT
  ProductName, Price,
  NOT Price > 20 AS CHEAP
FROM Products;
```

|           연산자            |            의미             |
| :-------------------------: | :-------------------------: |
|   BETWEEN {MIN} AND {MAX}   |      두 값 사이에 있음      |
| NOT BETWEEN {MIN} AND {MAX} | 두 값 사이가 아닌 곳에 있음 |

```sql
SELECT 5 BETWEEN 1 AND 10;
```

```sql
SELECT 'banana' NOT BETWEEN 'Apple' AND 'camera';
```

```sql
SELECT * FROM OrderDetails
WHERE ProductID BETWEEN 1 AND 4;
```

```sql
SELECT * FROM Customers
WHERE CustomerName BETWEEN 'b' AND 'c';
```

|    연산자    |            의미            |
| :----------: | :------------------------: |
|   IN (...)   | 괄호 안의 값들 가운데 있음 |
| NOT IN (...) | 괄호 안의 값들 가운데 없음 |

```sql
SELECT 1 + 2 IN (2, 3, 4)
```

```sql
SELECT 'Hello' IN (1, TRUE, 'hello')
```

```sql
SELECT * FROM Customers
WHERE City IN ('Torino', 'Paris', 'Portland', 'Madrid')
```

|      연산자       |              의미               |
| :---------------: | :-----------------------------: |
| LIKE '... % ...'  |   0 ~ N 개의 문자를 가진 패턴   |
| LIKE '... \_ ...' | \_ 개수 만큼의 문자를 가진 패턴 |

```sql
SELECT
  'HELLO' LIKE 'hel%',
  'HELLO' LIKE 'H%',
  'HELLO' LIKE 'H%O',
  'HELLO' LIKE '%O',
  'HELLO' LIKE '%HELLO%',
  'HELLO' LIKE '%H',
  'HELLO' LIKE 'L%'
```

```sql
SELECT
  'HELLO' LIKE 'HEL__',
  'HELLO' LIKE 'h___O',
  'HELLO' LIKE 'HE_LO',
  'HELLO' LIKE '_____',
  'HELLO' LIKE '_HELLO',
  'HELLO' LIKE 'HEL_',
  'HELLO' LIKE 'H_O'
```

```sql
SELECT * FROM Employees
WHERE Notes LIKE '%economics%'
```

```sql
SELECT * FROM OrderDetails
WHERE OrderID LIKE '1025_'
```

## 총 정리

|           연산자            |               의미                |
| :-------------------------: | :-------------------------------: |
|         +, -, \*, /         | 각각 더하기, 빼기, 곱하기, 나누기 |
|           %, MOD            |              나머지               |
|             IS              |    양쪽이 모두 TRUE 또는 FALSE    |
|           IS NOT            |     한쪽은 TRUE, 한쪽은 FALSE     |
|           AND, &&           |   양쪽이 모두 TRUE일 때만 TRUE    |
|          OR, \|\|           |   양쪽이 모두 TRUE일 때만 TRUE    |
|              =              |          양쪽 값이 같음           |
|           !=, <>            |          양쪽 값이 다름           |
|            >, <             |     (왼쪽, 오른쪽) 값이 더 큼     |
|           >=, <=            | (왼쪽, 오른쪽) 값이 같거나 더 큼  |
|   BETWEEN {MIN} AND {MAX}   |         두 값 사이에 있음         |
| NOT BETWEEN {MIN} AND {MAX} |    두 값 사이가 아닌 곳에 있음    |
|          IN (...)           |    괄호 안의 값들 가운데 있음     |
|        NOT IN (...)         |    괄호 안의 값들 가운데 없음     |
|      LIKE '... % ...'       |    0 ~ N 개의 문자를 가진 패턴    |
|      LIKE '... \_ ...'      |  \_ 개수 만큼의 문자를 가진 패턴  |
