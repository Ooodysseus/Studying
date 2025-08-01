# SQL Cheatsheet

## Basics
SELECT * FROM users;  
SELECT name, age FROM users;  
SELECT DISTINCT role FROM users;  
SELECT COUNT(*) FROM users;  
SELECT COUNT(DISTINCT role) FROM users;  
SELECT name FROM users WHERE age > 18;  
SELECT * FROM users WHERE age BETWEEN 18 AND 30;  
SELECT * FROM users WHERE name LIKE 'A%';  
SELECT * FROM users WHERE city IN ('Kyiv','Lviv');  
SELECT * FROM users WHERE NOT active;  

## Sorting
SELECT * FROM users ORDER BY name ASC;  
SELECT * FROM users ORDER BY age DESC;  
SELECT * FROM users ORDER BY age DESC, name ASC;  

## Limiting
SELECT * FROM users LIMIT 10;  
SELECT * FROM users LIMIT 10 OFFSET 20;  

## Aggregation
SELECT AVG(age) FROM users;  
SELECT MIN(age) FROM users;  
SELECT MAX(age) FROM users;  
SELECT SUM(salary) FROM employees;  
SELECT COUNT(*) FROM users;  

## Group By
SELECT role, COUNT(*) FROM users GROUP BY role;  
SELECT city, AVG(age) FROM users GROUP BY city;  
SELECT city, COUNT(*) FROM users GROUP BY city HAVING COUNT(*) > 10;  

## Joins
SELECT * FROM users INNER JOIN orders ON users.id = orders.user_id;  
SELECT * FROM users LEFT JOIN orders ON users.id = orders.user_id;  
SELECT * FROM users RIGHT JOIN orders ON users.id = orders.user_id;  
SELECT * FROM users FULL OUTER JOIN orders ON users.id = orders.user_id;  
SELECT u.name, o.amount FROM users u JOIN orders o ON u.id = o.user_id;  

## Subqueries
SELECT name FROM users WHERE id IN (SELECT user_id FROM orders WHERE amount > 100);  
SELECT name, (SELECT COUNT(*) FROM orders WHERE user_id = users.id) AS order_count FROM users;  

## Aliases
SELECT u.name AS username, o.amount FROM users u JOIN orders o ON u.id = o.user_id;  
SELECT name AS "User Name" FROM users;  

## Insert
INSERT INTO users (name, age, email) VALUES ('Ooodysseus', 30, 'oo@mail.com');  
INSERT INTO users VALUES (1, 'Alice', 28, 'alice@mail.com');  
INSERT INTO orders (user_id, total) SELECT id, 100 FROM users WHERE active = 1;  

## Update
UPDATE users SET age = 31 WHERE name = 'Ooodysseus';  
UPDATE users SET active = 0 WHERE last_login < '2025-01-01';  

## Delete
DELETE FROM users WHERE age < 18;  
DELETE FROM users WHERE id = 10;  

## Create Table
CREATE TABLE users (  
  id INTEGER PRIMARY KEY AUTO_INCREMENT,  
  name VARCHAR(100) NOT NULL,  
  age INTEGER,  
  email VARCHAR(255) UNIQUE,  
  created_at DATETIME DEFAULT CURRENT_TIMESTAMP  
);  

## Alter Table
ALTER TABLE users ADD COLUMN gender VARCHAR(10);  
ALTER TABLE users DROP COLUMN gender;  
ALTER TABLE users RENAME COLUMN name TO username;  
ALTER TABLE users MODIFY COLUMN age INT NOT NULL;  

## Drop Table & Database
DROP TABLE users;  
DROP DATABASE testdb;  

## Indexes
CREATE INDEX idx_name ON users(name);  
DROP INDEX idx_name ON users;  

## Constraints
PRIMARY KEY  
FOREIGN KEY  
UNIQUE  
NOT NULL  
DEFAULT  
CHECK (age >= 0)  

## Foreign Key
CREATE TABLE orders (  
  id INT PRIMARY KEY,  
  user_id INT,  
  FOREIGN KEY (user_id) REFERENCES users(id)  
);  

## Views
CREATE VIEW active_users AS SELECT * FROM users WHERE active = 1;  
SELECT * FROM active_users;  
DROP VIEW active_users;  

## Transactions
START TRANSACTION;  
UPDATE users SET balance = balance - 100 WHERE id = 1;  
UPDATE users SET balance = balance + 100 WHERE id = 2;  
COMMIT;  
ROLLBACK;  

## Functions
SELECT NOW();  
SELECT LENGTH(name);  
SELECT UPPER(name);  
SELECT LOWER(name);  
SELECT ROUND(salary, 2);  
SELECT SUBSTRING(name, 1, 3);  
SELECT COALESCE(email, 'no-email');  
SELECT IF(age > 18, 'adult', 'minor');  

## Case
SELECT name,  
  CASE WHEN age >= 18 THEN 'Adult' ELSE 'Child' END AS group  
FROM users;  

## Union
SELECT name FROM users WHERE age < 18  
UNION  
SELECT name FROM users WHERE active = 0;  

## Exists
SELECT name FROM users WHERE EXISTS (SELECT 1 FROM orders WHERE user_id = users.id);  

## IN
SELECT name FROM users WHERE id IN (1,2,3);  

## Backup & Restore
-- MySQL  
mysqldump -u user -p dbname > backup.sql  
mysql -u user -p dbname < backup.sql  

-- PostgreSQL  
pg_dump dbname > backup.sql  
psql dbname < backup.sql  

## Useful Commands
SHOW TABLES;  
SHOW DATABASES;  
DESCRIBE users;  
EXPLAIN SELECT * FROM users;  
SHOW COLUMNS FROM users;  
SHOW INDEX FROM users;  
SHOW CREATE TABLE users;  
SELECT VERSION();  
SELECT DATABASE();  

## Privileges
GRANT SELECT ON db.* TO 'user'@'localhost';  
REVOKE INSERT ON db.* FROM 'user'@'localhost';  
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'pass';  
DROP USER 'newuser'@'localhost';  
SET PASSWORD FOR 'user'@'localhost' = PASSWORD('newpass');  

## Stored Procedures
DELIMITER //  
CREATE PROCEDURE AddUser(IN username VARCHAR(100))  
BEGIN  
  INSERT INTO users(name) VALUES(username);  
END;  
//  
CALL AddUser('Ooodysseus');  
DROP PROCEDURE AddUser;  

## Triggers
CREATE TRIGGER before_insert BEFORE INSERT ON users  
FOR EACH ROW SET NEW.created_at = NOW();  
DROP TRIGGER before_insert;  

## Pagination
SELECT * FROM users LIMIT 10 OFFSET 20;  

## Advanced: Window Functions
SELECT name, age, RANK() OVER (ORDER BY age DESC) AS age_rank FROM users;  
SELECT name, salary, AVG(salary) OVER (PARTITION BY department) FROM employees;  

## Comments
-- Single line comment  
/* Multi-line  
   comment */  

## Best Practices
Normalize data  
Use indexes for performance  
Avoid SELECT * in production  
Validate data types  
Use transactions for consistency  
Backup databases regularly  
Limit user privileges  
Document schema  
Test queries  
Monitor slow queries  
Avoid redundant data  
Use constraints for integrity  
Sanitize inputs  
Use parameterized queries  
Limit query results  
Handle errors gracefully  
Archive old data  
Optimize joins  
Document stored procedures  
Version schema changes  
Automate backups  
Monitor database size  
Review execution plans  
Avoid nested subqueries  
Use views for reusable logic  
Limit open connections  
Audit user access  
Test with real data  
Refactor old tables  
Comment complex queries  
Prefer explicit JOINs  
Keep schema readable  
Review dependencies  
Set default values  
Use UNIQUE for keys  
Prefer composite indexes for search  
Monitor performance  
Automate migrations  
Document triggers  
Test edge cases  
Prefer window functions for analytics  
Use time zones correctly  
Optimize for scale  
Keep changelog  
Review updates  
Document intent  
Automate restores  
Test after restore  
Use proper naming conventions  
Limit use of stored procedures  
Handle NULLs carefully  
Support multiple DB engines  
Comment schema changes  
Review privileges regularly  
Minimize locking  
Support backup retention  
Optimize pagination  
Document table relationships  
Use separate schema for test  
Prefer small transactions  
Test concurrency  
Monitor replication  
