# SQL (Structured Query Language): сучасний конспект 2024+

---

## Зміст

-   [Вступ](#вступ)
-   [Що таке SQL](#що-таке-sql)
-   [Історія та роль SQL](#історія-та-роль-sql)
-   [Типи СУБД: реляційні, NewSQL, cloud-native, embedded, distributed](#типи-субд-реляційні-newsql-cloud-native-embedded-distributed)
-   [Встановлення, середовище, робочі інструменти](#встановлення-середовище-робочі-інструменти)
-   [Базові команди SQL: SELECT, INSERT, UPDATE, DELETE](#базові-команди-sql-select-insert-update-delete)
-   [Фільтрація, сортування, агрегація, групування](#фільтрація-сортування-агрегація-групування)
-   [JOIN: INNER, LEFT, RIGHT, FULL, CROSS, SELF](#join-inner-left-right-full-cross-self)
-   [Підзапити, CTE, рекурсія, window-функції](#підзапити-cte-рекурсія-window-функції)
-   [Індекси, оптимізація запитів, EXPLAIN, performance traps](#індекси-оптимізація-запитів-explain-performance-traps)
-   [Таблиці: створення, типи даних, constraints, нормалізація, ERD](#таблиці-створення-типи-даних-constraints-нормалізація-erd)
-   [Транзакції, ACID, ізоляція, deadlocks, MVCC](#транзакції-acid-ізоляція-deadlocks-mvcc)
-   [Функції, процедури, тригери, events](#функції-процедури-тригери-events)
-   [JSON, XML, сучасні типи даних, search, fulltext, spatial](#json-xml-сучасні-типи-даних-search-fulltext-spatial)
-   [Внутрішні механізми: план виконання, storage, locking, concurrency, replication, sharding](#внутрішні-механізми-план-виконання-storage-locking-concurrency-replication-sharding)
-   [Типові підводні камені, security traps, injection, access control](#типові-підводні-камені-security-traps-injection-access-control)
-   [Best practices](#best-practices)
-   [Візуалізації, схеми, ERD, діаграми](#візуалізації-схеми-erd-діаграми)
-   [Корисні ресурси та документація](#корисні-ресурси-та-документація)
-   [Короткий підсумок](#короткий-підсумок)

---

## Вступ

**SQL (Structured Query Language)** — мова для роботи з реляційними і сучасними базами даних: опис структури, запит, зміна, аналітика, контроль доступу.  
У 2024+ році SQL — стандарт для OLTP/OLAP, Data Engineering, BI, ETL, Cloud DB, real-time data, Data Warehouses, AI solutions.

---

## Що таке SQL

-   **SQL** — декларативна мова для роботи з даними: запит, зміна, структура, аналітика.
-   Основні ролі: CRUD (Create, Read, Update, Delete), агрегування, трансформація, безпека.
-   Підтримується всіма сучасними СУБД: PostgreSQL, MySQL, MariaDB, SQLite, MS SQL Server, Oracle, Google Cloud Spanner, CockroachDB, TiDB.

---

## Історія та роль SQL

-   **1970:** Концепція реляційної моделі даних (Edgar F. Codd).
-   **1979–1990:** Поява перших реалізацій (Oracle, DB2, Ingres).
-   **2000+:** SQL — основа для OLTP/OLAP, data engineering, BI.
-   **2024+:** SQL — стандарт для cloud-native, distributed, serverless databases, Data Lakes, Big Data.

---

## Типи СУБД: реляційні, NewSQL, cloud-native, embedded, distributed

-   **Реляційні (RDBMS):** PostgreSQL, MySQL, Oracle, MSSQL, SQLite.
-   **NewSQL:** CockroachDB, Google Cloud Spanner, TiDB, YugabyteDB (масштабованість, strong consistency, distributed ACID).
-   **Cloud-native:** AWS Aurora, Google Cloud SQL, Azure SQL, serverless, autoscale.
-   **Embedded DB:** SQLite, DuckDB (інтеграція в додатки, BI).
-   **Distributed DB:** Amazon Redshift, Snowflake, BigQuery, Data Lakehouse.

---

## Встановлення, середовище, робочі інструменти

-   Встановлення через docker, cloud, локальні інсталятори.
-   GUI: DBeaver, DataGrip, pgAdmin, Azure Data Studio, TablePlus.
-   CLI: psql, mysql, sqlite3, mssql-cli.
-   Для production: використовуйте managed cloud СУБД.
-   ERD (entity-relationship diagrams): dbdiagram.io, draw.io.

---

## Базові команди SQL: SELECT, INSERT, UPDATE, DELETE

### SELECT

```sql
SELECT id, name FROM users WHERE active = TRUE ORDER BY created_at DESC;
```

### INSERT

```sql
INSERT INTO users (name, email) VALUES ('Oleg', 'oleg@email.com');
```

### UPDATE

```sql
UPDATE users SET active = FALSE WHERE last_login < '2024-01-01';
```

### DELETE

```sql
DELETE FROM users WHERE active = FALSE;
```

---

## Фільтрація, сортування, агрегація, групування

### WHERE, AND, OR

```sql
SELECT * FROM orders WHERE amount > 500 AND status = 'completed';
```

### ORDER BY, LIMIT, OFFSET

```sql
SELECT name, score FROM leaderboard ORDER BY score DESC LIMIT 10 OFFSET 20;
```

### GROUP BY, HAVING

```sql
SELECT status, COUNT(*) as total FROM orders GROUP BY status HAVING total > 100;
```

### Агрегатні функції

```sql
SELECT AVG(amount), SUM(amount), MAX(amount), MIN(amount) FROM payments;
```

---

## JOIN: INNER, LEFT, RIGHT, FULL, CROSS, SELF

### INNER JOIN

```sql
SELECT u.name, o.amount
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
```

### LEFT JOIN

```sql
SELECT u.name, o.amount
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

### RIGHT JOIN

```sql
SELECT u.name, o.amount
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

### FULL OUTER JOIN

```sql
SELECT u.name, o.amount
FROM users u
FULL OUTER JOIN orders o ON u.id = o.user_id;
```

### CROSS JOIN

```sql
SELECT *
FROM products p
CROSS JOIN categories c;
```

### SELF JOIN

```sql
SELECT e.name, m.name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.id;
```

---

## Підзапити, CTE, рекурсія, window-функції

### Підзапит (subquery)

```sql
SELECT name FROM users
WHERE id IN (SELECT user_id FROM orders WHERE amount > 1000);
```

### CTE (Common Table Expression, WITH)

```sql
WITH recent_orders AS (
  SELECT * FROM orders WHERE created_at > NOW() - INTERVAL '7 days'
)
SELECT * FROM recent_orders WHERE status = 'completed';
```

### Рекурсивний CTE

```sql
WITH RECURSIVE user_tree AS (
  SELECT id, parent_id FROM users WHERE parent_id IS NULL
  UNION ALL
  SELECT u.id, u.parent_id FROM users u
  INNER JOIN user_tree ut ON u.parent_id = ut.id
)
SELECT * FROM user_tree;
```

### Window-функції

```sql
SELECT
  id,
  amount,
  AVG(amount) OVER (PARTITION BY user_id) as avg_user_amount,
  ROW_NUMBER() OVER (ORDER BY amount DESC) as rank
FROM orders;
```

---

## Індекси, оптимізація запитів, EXPLAIN, performance traps

### Індекси

-   Типи: B-tree, Hash, GiST, GIN, BRIN, Fulltext, Spatial.
-   Створення:

```sql
CREATE INDEX idx_user_email ON users(email);
```

-   Уникай надмірної кількості індексів — це уповільнює INSERT/UPDATE.

### EXPLAIN

```sql
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 5;
```

-   Оцінюй план виконання, шукай Seq Scan (повний скан — погано для великих таблиць).

### Performance traps

-   Full Table Scan.
-   N+1 проблема (надмірні запити).
-   Неоптимізований GROUP BY.
-   Зайві підзапити.

#### Схема плану виконання

```
[Seq Scan] → [Filter] → [Join] → [Aggregate] → [Sort] → [Result]
```

---

## Таблиці: створення, типи даних, constraints, нормалізація, ERD

### Створення таблиці

```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE,
  birthdate DATE,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### Типи даних

-   INT, BIGINT, FLOAT, NUMERIC, VARCHAR, TEXT, DATE, TIMESTAMP, BOOLEAN, JSON, XML, ARRAY, UUID, ENUM, MONEY, POINT, GEOMETRY.

### Constraints

-   PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK, DEFAULT, NOT NULL.

### Нормалізація

-   1NF, 2NF, 3NF, BCNF.
-   ERD — схема зв’язків таблиць.

### Схема ERD (приклад)

```
[Users] --< [Orders] >-- [Products]
```

---

## Транзакції, ACID, ізоляція, deadlocks, MVCC

### Транзакція

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

### ACID

-   Atomicity, Consistency, Isolation, Durability.

### Isolation levels

-   READ UNCOMMITTED, READ COMMITTED, REPEATABLE READ, SERIALIZABLE.

### Deadlocks

-   Перехресне блокування — уникай циклічних UPDATE, LOCK TABLE.

### MVCC (Multi-Version Concurrency Control)

-   Паралельна робота багатьох транзакцій: кожна бачить свою версію даних.

---

## Функції, процедури, тригери, events

### Функція

```sql
CREATE FUNCTION get_bonus(amount NUMERIC) RETURNS NUMERIC AS $$
BEGIN
  RETURN amount * 0.1;
END;
$$ LANGUAGE plpgsql;
```

### Процедура

```sql
CREATE PROCEDURE transfer_funds(sender INT, receiver INT, amount NUMERIC)
LANGUAGE plpgsql
AS $$
BEGIN
  UPDATE accounts SET balance = balance - amount WHERE id = sender;
  UPDATE accounts SET balance = balance + amount WHERE id = receiver;
END;
$$;
```

### Тригери

```sql
CREATE TRIGGER update_timestamp
BEFORE UPDATE ON users
FOR EACH ROW
EXECUTE FUNCTION update_modified_column();
```

### Events

-   В MySQL: EVENT SCHEDULER для періодичних задач.

```sql
CREATE EVENT clean_old_logs
ON SCHEDULE EVERY 1 DAY
DO
  DELETE FROM logs WHERE created_at < NOW() - INTERVAL '30 days';
```

---

## JSON, XML, сучасні типи даних, search, fulltext, spatial

### JSON (PostgreSQL, MySQL 5.7+)

```sql
CREATE TABLE logs (
  id SERIAL PRIMARY KEY,
  data JSONB
);

INSERT INTO logs (data) VALUES ('{"event": "login", "user": "Oleg"}');

SELECT data->>'event' FROM logs;
```

### XML

```sql
CREATE TABLE xml_store (
  id SERIAL PRIMARY KEY,
  info XML
);
```

### ARRAY (PostgreSQL)

```sql
CREATE TABLE tags (
  id SERIAL PRIMARY KEY,
  tag_list TEXT[]
);

INSERT INTO tags (tag_list) VALUES (ARRAY['sql', 'performance', '2024']);
```

### Fulltext search

```sql
CREATE INDEX idx_post_text ON posts USING gin(to_tsvector('english', text));
SELECT * FROM posts WHERE to_tsvector('english', text) @@ to_tsquery('sql');
```

### Spatial дані (PostGIS)

```sql
CREATE TABLE locations (
  id SERIAL PRIMARY KEY,
  point GEOGRAPHY(Point, 4326)
);

SELECT * FROM locations WHERE ST_DWithin(point, ST_MakePoint(30.5, 50.5)::geography, 1000);
```

---

## Внутрішні механізми: план виконання, storage, locking, concurrency, replication, sharding

### План виконання

-   СУБД компілює запит у plan: Seq Scan, Index Scan, Hash Join, Merge Join, Aggregate, Sort.
-   EXPLAIN — аналізуй план для оптимізації.

### Storage

-   Row-based, columnar, partitioning, sharding.
-   Partitioning — розподіл таблиці на частини (range/list/hash).

### Locking

-   Row-level, table-level, optimistic/pessimistic concurrency control.

### Concurrency

-   MVCC (PostgreSQL): транзакції бачать свою версію даних.
-   Locks: read/write, advisory, shared/exclusive.

### Replication

-   Master-slave, multi-master, synchronous/asynchronous.

### Sharding

-   Розподіл даних по різних вузлах/серверних групах для масштабування.

### Схема архітектури (deep dive)

```
[Client] → [SQL Parser] → [Planner] → [Executor] → [Storage Engine] → [Disk/Mem]
```

---

## Типові підводні камені, security traps, injection, access control

-   **SQL Injection:** завжди використовуй параметризовані запити, prepared statements.
-   **Full Table Scan:** додавай індекси для WHERE/JOIN.
-   **Deadlocks:** контролюй порядок транзакцій, уникай циклічних UPDATE.
-   **Великі JOIN:** оптимізуй схему, розбивай запити, використовуйте CTE.
-   **Outdated privileges:** обмежуй права, закривай доступ до схеми.
-   **Відсутність backup:** автоматизуй резервне копіювання.
-   **Недостатня нормалізація:** уникай дублювання даних, перевіряй ERD.
-   **Відкриті порти:** закривай доступ, використовуй VPN/SSL/TLS.
-   **Відсутність logging/auditing:** логуй всі критичні операції.

---

## Best practices

-   Використовуй prepared statements, ORM для запитів.
-   Структуруй базу через нормалізацію (1NF, 2NF, 3NF, BCNF).
-   Додавай індекси для пошуку, JOIN, ORDER BY.
-   Профілюй запити через EXPLAIN, ANALYZE.
-   Використовуй транзакції для критичних операцій.
-   Кешуй результати складних запитів (Redis, Memcached).
-   Перевіряй права доступу: мінімальні GRANT.
-   Документуй схему бази (ERD, dbdocs.io).
-   Використовуй сучасні типи даних (JSON, ARRAY, GEOMETRY).
-   Автоматизуй backup та disaster recovery.
-   Використовуй cloud-native рішення для масштабування.
-   Оновлюй СУБД, драйвери, перевіряй security checklist.
-   Використовуй audit logging.
-   Використовуй migration tools (Flyway, Liquibase, Alembic).

---

## Візуалізації, схеми, ERD, діаграми

-   Використовуй dbdiagram.io для ERD.
-   Відображай зв’язки: ONE-TO-MANY, MANY-TO-MANY, SELF.
-   Відслідковуй план виконання через explain.depesz.com (PostgreSQL).
-   Візуалізуй sharding/replication схеми через draw.io.

---

## Корисні ресурси та документація

-   [PostgreSQL Docs](https://www.postgresql.org/docs/)
-   [MySQL Docs](https://dev.mysql.com/doc/)
-   [SQL Server Docs](https://learn.microsoft.com/en-us/sql/?view=sql-server-ver16)
-   [CockroachDB Docs](https://www.cockroachlabs.com/docs/)
-   [TiDB Docs](https://docs.pingcap.com/tidb/stable/)
-   [DBeaver](https://dbeaver.io/)
-   [DataGrip](https://www.jetbrains.com/datagrip/)
-   [SQL Style Guide](https://www.sqlstyle.guide/)
-   [SQL Injection Guide](https://owasp.org/www-community/attacks/SQL_Injection)
-   [ERD Tools](https://dbdiagram.io/home)
-   [Modern SQL](https://modern-sql.com/)
-   [Cloud SQL Docs](https://cloud.google.com/sql/docs)
-   [Performance Deep Dive](https://use-the-index-luke.com/)
-   [Migration Tools (Flyway, Liquibase)](https://flywaydb.org/)

---

## Короткий підсумок

**SQL — це сучасна, структурована, масштабована мова для роботи з даними, аналітики, трансформації, безпеки, оптимізації.**  
Використовуй індекси, оптимізуй запити, профілюй план виконання, впроваджуй транзакції та security best practices.  
Документуй схему, автоматизуй backup, розбирайся у підкапотних механізмах — і твоя база буде надійною, швидкою та сучасною у 2024+!

---
