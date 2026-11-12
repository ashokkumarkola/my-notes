# SQL Cheat Sheet

## Command groups

| Group | Commands |
|---|---|
| DDL (structure) | `CREATE` `ALTER` `DROP` `TRUNCATE` |
| DML (data) | `SELECT` `INSERT` `UPDATE` `DELETE` |
| DCL (access) | `GRANT` `REVOKE` |
| TCL (transactions) | `BEGIN` `COMMIT` `ROLLBACK` |

## Tables

```sql
CREATE TABLE users (
  id         SERIAL PRIMARY KEY,
  email      VARCHAR(255) UNIQUE NOT NULL,
  age        INT CHECK (age >= 0),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
  id      SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id) ON DELETE CASCADE,
  total   NUMERIC(10, 2)
);

ALTER TABLE users ADD COLUMN name TEXT;
ALTER TABLE users DROP COLUMN name;
DROP TABLE IF EXISTS orders;
CREATE INDEX idx_orders_user ON orders(user_id);
```

## CRUD

```sql
INSERT INTO users (email, age) VALUES ('a@x.com', 20), ('b@x.com', 30);
SELECT * FROM users;
UPDATE users SET age = 21 WHERE id = 1;     -- always WHERE
DELETE FROM users WHERE id = 1;             -- always WHERE
```

## Filter + sort

```sql
SELECT email, age FROM users
WHERE age BETWEEN 18 AND 30
  AND email LIKE '%@x.com'
  AND id IN (1, 2, 3)
  AND name IS NOT NULL
ORDER BY age DESC, email
LIMIT 10 OFFSET 20;
SELECT DISTINCT age FROM users;
```

## Aggregates

```sql
SELECT age, COUNT(*) AS n, AVG(age), MIN(age), MAX(age), SUM(age)
FROM users
GROUP BY age
HAVING COUNT(*) > 1;          -- HAVING filters groups, WHERE filters rows
```

## Joins

```sql
SELECT u.email, o.total
FROM users u
JOIN orders o ON o.user_id = u.id;          -- INNER

SELECT u.email, COUNT(o.id)
FROM users u
LEFT JOIN orders o ON o.user_id = u.id      -- keep users with 0 orders
GROUP BY u.email;
```

| Join | Rows |
|---|---|
| `INNER JOIN` | Match in both |
| `LEFT JOIN` | All left + matches (NULL if none) |
| `RIGHT JOIN` | All right + matches |
| `FULL JOIN` | All from both |
| `CROSS JOIN` | Every combination |

## Subqueries + CTE

```sql
SELECT * FROM users WHERE id IN (SELECT user_id FROM orders WHERE total > 100);

WITH big AS (
  SELECT user_id, SUM(total) AS spent FROM orders GROUP BY user_id
)
SELECT u.email, b.spent FROM users u JOIN big b ON b.user_id = u.id;
```

## Window functions

```sql
SELECT email, age,
  ROW_NUMBER() OVER (ORDER BY age DESC)          AS rn,
  RANK()       OVER (PARTITION BY age ORDER BY id) AS rnk,
  SUM(age)     OVER ()                           AS total_age
FROM users;
```

## Transactions

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;        -- or ROLLBACK;
```

ACID: Atomic · Consistent · Isolated · Durable.

## Execution order

```text
FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT
```
