## 📘 PostgreSQL Database & SQL Practice Guide
---
## 🔍 Overview
<p>This repository contains hands-on PostgreSQL database practice, covering everything from database creation to advanced SQL concepts like joins, functions, views, triggers, and foreign keys.</p>

 ### It is designed for:
- Beginners learning SQL & PostgreSQL
- Backend developers practicing real-world queries
- Understanding relational database concepts clearly
- The project demonstrates clean SQL syntax, practical examples, and real-use cases commonly used in backend development.
  
## 📌 Database Creation
CREATE DATABASE dbnm;
-- Example
```sql
CREATE DATABASE kurrecomputers77;
```
## 📌 Table Creation – Contact
```sql
CREATE TABLE contact (
  id SERIAL,
  name VARCHAR(50),
  email VARCHAR(50),
  mob VARCHAR(10),
  age INT,
  city VARCHAR(50)
);
```
### Insert Data
```sql
INSERT INTO contact(name,email,mob,age,city)
VALUES ('kumlesh','kumleshkurre77@gmail.com','1234567890',20,'samoda');
Select Queries
SELECT * FROM contact;
SELECT name, mob FROM contact;
SELECT name, mob, city FROM contact;
```
## 📌 WHERE Clause Examples
```sql
SELECT * FROM contact WHERE city='samoda';
SELECT * FROM contact WHERE age < 19;
SELECT * FROM contact WHERE age > 19;
```
### AND / OR
```sql
SELECT * FROM contact WHERE age <= 19 AND city='kusmund';
SELECT * FROM contact WHERE age <= 19 OR city='kusmund';
```
### IN / NOT IN
```sql
SELECT * FROM contact WHERE city IN ('kusmund','samoda');
SELECT * FROM contact WHERE city NOT IN ('kusmund','samoda');
```
## 📌 ORDER BY
```sql
SELECT * FROM contact ORDER BY name ASC;
SELECT * FROM contact ORDER BY name DESC;
```
## 📌 LIKE Pattern Matching
```sql
SELECT * FROM contact WHERE name LIKE 'k%';
SELECT * FROM contact WHERE name LIKE '%sh';
SELECT * FROM contact WHERE name LIKE '_a%';
```
## 📌 Employee Table
```sql
CREATE TABLE employe (
  id SERIAL,
  eid VARCHAR(50),
  ename VARCHAR(50),
  subject VARCHAR(10),
  dep VARCHAR(50),
  sal VARCHAR(50)
);
```
### Salary Queries
```sql
SELECT MAX(sal) FROM employe;
SELECT MIN(sal) FROM employe;
SELECT AVG(sal::numeric) FROM employe;
SELECT SUM(sal::numeric) FROM employe;
SELECT COUNT(*) FROM employe;
Highest / Lowest Salary Employee
SELECT ename, sal FROM employe WHERE sal=(SELECT MAX(sal) FROM employe);
SELECT ename, sal FROM employe WHERE sal=(SELECT MIN(sal) FROM employe);
```
## 📌 LIMIT & OFFSET
```sql
SELECT ename, sal FROM employe ORDER BY sal DESC LIMIT 3;
SELECT ename, sal FROM employe ORDER BY sal DESC LIMIT 1 OFFSET 1;
```
## 📌 Food Ordering Tables
### food_group
```sql
CREATE TABLE food_group (
  gid SERIAL,
  group_name VARCHAR(50)
);
```
### menu
```sql
CREATE TABLE menu (
  mid SERIAL,
  menu_name VARCHAR(50),
  menu_price INT,
  gid INT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```
### qtymast
```sql
CREATE TABLE qtymast (
  qid SERIAL,
  qty_type VARCHAR(50),
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```
## 📌 Joins
```sql
SELECT menu_name, menu_price, group_name
FROM menu, food_group
WHERE food_group.gid = menu.gid;
INNER / LEFT / RIGHT / CROSS JOIN
SELECT name, sname FROM staff INNER JOIN sub ON staff.id=sub.id;
SELECT name, sname FROM staff LEFT JOIN sub ON staff.id=sub.id;
SELECT name, sname FROM staff RIGHT JOIN sub ON staff.id=sub.id;
SELECT name, sname FROM staff CROSS JOIN sub;
```
## 📌 UNION
```sql
SELECT group_name FROM food_group
UNION
SELECT qty_type FROM qtymast;
```
## 📌 Calculations
```sql
SELECT menu_name, menu_price, 2 AS qty,
(2 * menu_price) AS total
FROM menu WHERE mid=2;
```
## 📌 String Functions
```sql
SELECT UPPER(menu_name) FROM menu;
SELECT REVERSE(UPPER(menu_name)) FROM menu;
SELECT LENGTH(menu_name) FROM menu;
SELECT REPLACE(menu_name,'ROL','ROLL') FROM menu;
```
## 📌 Math Functions
```sql
SELECT ABS(-10);
SELECT FLOOR(10.9);
SELECT CEIL(10.1);
SELECT ROUND(10.4);
```
## 📌 User Defined Function
```sql
CREATE OR REPLACE FUNCTION carea(r NUMERIC)
RETURNS NUMERIC AS $$
BEGIN
  RETURN 3.14 * r * r;
END;
$$ LANGUAGE plpgsql;
SELECT carea(8);
```
## 📌 Views
```sql
CREATE VIEW edata AS
SELECT ename, subject, sal FROM employe;
SELECT * FROM edata;
```
## 📌 Triggers (Backup & Audit)
### Backup Before Delete
```sql
CREATE OR REPLACE FUNCTION backup()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO back_contact(name,email,mob,age,city)
  VALUES (OLD.name,OLD.email,OLD.mob,OLD.age,OLD.city);
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
### Audit After Insert
```sql
CREATE OR REPLACE FUNCTION auditlog()
RETURNS TRIGGER AS $$
BEGIN
INSERT INTO audit(emp_id, entry_date)
VALUES (NEW.id, CURRENT_TIMESTAMP);
RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
## 🔐 Auto Increment ID (Identity Column)
```sql
ALTER TABLE employe
ALTER COLUMN id ADD GENERATED ALWAYS AS IDENTITY;
```

## Foreign Key Constraint (Table Relationship)
```sql
ALTER TABLE staff
ADD CONSTRAINT fk_staff_employe
FOREIGN KEY (id)
REFERENCES employe(id);
```
## 👨‍💻 Author

- Kumlesh Kurre
- Backend Developer
- Skills:  PostgreSQL
 
## ⭐ Support
If you like this project, please ⭐ star the repository to support my work!
  

