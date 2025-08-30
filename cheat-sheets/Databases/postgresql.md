# POSTGRESQL

PostgreSQL — потужна реляційна СУБД з підтримкою транзакцій, розширень, JSON, CTE, window-функцій, індексів, реплікації та багатьох сучасних можливостей.

## Категорія: Основні команди CLI

| Команда/метод             | Опис                 | Приклад/Аутпут                 |
| ------------------------- | -------------------- | ------------------------------ |
| psql -U user -d db        | підключення до БД    | psql -U postgres -d mydb       |
| createdb mydb             | створити БД          | createdb mydb                  |
| dropdb mydb               | видалити БД          | dropdb mydb                    |
| createuser user           | створити користувача | createuser myuser              |
| dropuser user             | видалити користувача | dropuser myuser                |
| \\l, \\c, \\dt, \\d table | список БД, таблиць   | \\l, \\c mydb, \\dt, \\d users |
| \\q                       | вийти                | \\q                            |
| \i file.sql               | виконати SQL-скрипт  | \i init.sql                    |

## Категорія: Основні типи даних

| Тип даних             | Опис                     | Приклад/Аутпут                    |
| --------------------- | ------------------------ | --------------------------------- |
| INTEGER, SERIAL       | цілі числа               | id SERIAL PRIMARY KEY             |
| VARCHAR(n), TEXT      | рядки                    | name VARCHAR(100)                 |
| BOOLEAN               | булевий                  | is_active BOOLEAN                 |
| DATE, TIMESTAMP       | дати/час                 | created TIMESTAMP                 |
| NUMERIC, REAL, DOUBLE | числа з плаваючою        | price NUMERIC(10,2)               |
| JSON, JSONB           | JSON-дані                | data JSONB                        |
| UUID                  | унікальний ідентифікатор | id UUID DEFAULT gen_random_uuid() |
| ARRAY                 | масив                    | tags TEXT[]                       |

## Категорія: Основні SQL-запити

| Команда/метод                | Опис                 | Приклад/Аутпут                       |
| ---------------------------- | -------------------- | ------------------------------------ |
| SELECT ... FROM ...          | вибірка              | SELECT \* FROM users;                |
| WHERE, AND, OR, NOT          | фільтрація           | WHERE age > 18 AND active            |
| INSERT INTO ... VALUES ...   | вставка              | INSERT INTO users(name) VALUES('A')  |
| UPDATE ... SET ... WHERE ... | оновлення            | UPDATE users SET name='B' WHERE id=1 |
| DELETE FROM ... WHERE ...    | видалення            | DELETE FROM users WHERE id=1         |
| ORDER BY, LIMIT, OFFSET      | сортування/пагінація | ORDER BY age DESC LIMIT 10 OFFSET 5  |
| GROUP BY, HAVING             | агрегація            | GROUP BY role HAVING count(\*)>1     |
| DISTINCT                     | унікальні            | SELECT DISTINCT name FROM users      |
| JOIN, LEFT JOIN, ...         | з'єднання            | SELECT \* FROM a JOIN b ON ...       |
| UNION, INTERSECT, EXCEPT     | множини              | SELECT ... UNION SELECT ...          |

## Категорія: Агрегації, window-функції

| Команда/метод                       | Опис            | Приклад/Аутпут                      |
| ----------------------------------- | --------------- | ----------------------------------- |
| COUNT(), SUM(), AVG(), MIN(), MAX() | агрегації       | SELECT COUNT(\*) FROM users         |
| window-функції                      | аналітика       | row_number() OVER (ORDER BY age)    |
| PARTITION BY                        | розбивка        | SUM(s) OVER (PARTITION BY city)     |
| CTE (WITH ...)                      | загальні вирази | WITH t AS (SELECT ...) SELECT ...   |
| CASE WHEN ... THEN ... END          | умовний вираз   | SELECT CASE WHEN x>0 THEN 'yes' END |

## Категорія: Робота зі схемами, індекси, транзакції

| Команда/метод           | Опис              | Приклад/Аутпут                      |
| ----------------------- | ----------------- | ----------------------------------- |
| CREATE SCHEMA s         | створити схему    | CREATE SCHEMA analytics;            |
| CREATE INDEX ...        | індекс            | CREATE INDEX idx ON t(col);         |
| CREATE UNIQUE INDEX ... | унікальний індекс | CREATE UNIQUE INDEX uidx ON t(col); |
| BEGIN, COMMIT, ROLLBACK | транзакції        | BEGIN; ... COMMIT;                  |
| SAVEPOINT, RELEASE      | savepoint         | SAVEPOINT s1; ROLLBACK TO s1;       |
| EXPLAIN                 | план запиту       | EXPLAIN SELECT \* FROM t;           |

## Категорія: JSON, масиви, advanced

| Команда/метод                       | Опис                     | Приклад/Аутпут               |
| ----------------------------------- | ------------------------ | ---------------------------- |
| ->, ->>, #>, #>>                    | доступ до JSON           | data->'a', data->>'a'        |
| jsonb_set(), jsonb_array_elements() | робота з JSONB           | jsonb_set(data,'{a}', '1')   |
| ANY, ALL                            | перевірка в масиві       | 2 = ANY(arr)                 |
| array_agg(), unnest()               | агрегація/розгортання    | array_agg(name), unnest(arr) |
| generate_series()                   | генерація послідовностей | SELECT generate_series(1,10) |

## Категорія: Користувачі, права, безпека

| Команда/метод                 | Опис                     | Приклад/Аутпут                   |
| ----------------------------- | ------------------------ | -------------------------------- |
| CREATE USER ... WITH PASSWORD | створити користувача     | CREATE USER u WITH PASSWORD 'p'; |
| GRANT, REVOKE                 | права доступу            | GRANT SELECT ON t TO u;          |
| ALTER USER ...                | змінити користувача      | ALTER USER u WITH PASSWORD 'x';  |
| \\du, \\dg                    | список користувачів/груп | \\du, \\dg                       |
| pg_hba.conf                   | налаштування доступу     | host all all 0.0.0.0/0 md5       |

## Категорія: Бекапи, best practices

| Команда/метод          | Опис                | Приклад/Аутпут                 |
| ---------------------- | ------------------- | ------------------------------ |
| pg_dump db > f.sql     | бекап БД            | pg_dump mydb > dump.sql        |
| pg_restore -d db f.sql | відновлення         | pg_restore -d mydb dump.sql    |
| psql -f f.sql          | виконати скрипт     | psql -U user -d db -f dump.sql |
| VACUUM, ANALYZE        | оптимізація         | VACUUM FULL; ANALYZE;          |
| REINDEX                | перебудова індексів | REINDEX TABLE t;               |
| Документація           | офіційна            | postgresql.org/docs            |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
