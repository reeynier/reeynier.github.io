---
layout: post
title:  "How To Specify Unique Constraint For Multiple Columns In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: How to make multiple columns unique (together) in an existing table in MySQL.
---

<br />

How to make multiple columns unique (together) in MySQL.

## Short Answer

* For an existing table:

```sql
ALTER TABLE `tablename` ADD UNIQUE `unique_id` (`column1`, `column2`);
```

ALTER TABLE is to change the table schema. ADD UNIQUE is to add the unique constraint. Then we can define the new unique key with multiple columns.

* To create a new table:

```sql
CREATE TABLE `tablename` (
  id INTEGER PRIMARY KEY,
  column1 TEXT NOT NULL,
  column2 TEXT NOT NULL,
  UNIQUE KEY `unique_id` (`column1`, `column2`)
);
```


## Example

Suppose we have the following EMPLOYEE table, we would like to make the combination of name and dept unique.

Table EMPLOYEE:
```
+-------+-------+------------+
| empId | name  | dept       |
+-------+-------+------------+
|     1 | Clark | Sales      |
|     2 | Dave  | Accounting |
|     3 | Ava   | Sales      |
+-------+-------+------------+
```

* For an existing table, we can do the following:

```sql
-- create
CREATE TABLE EMPLOYEE (
  empId INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  dept TEXT NOT NULL
);

-- insert
INSERT INTO EMPLOYEE VALUES (0001, 'Clark', 'Sales');
INSERT INTO EMPLOYEE VALUES (0002, 'Dave', 'Accounting');
INSERT INTO EMPLOYEE VALUES (0003, 'Ava', 'Sales');

ALTER TABLE EMPLOYEE ADD UNIQUE uniq_id (name(255), dept(255));
```

* To create a new table with unique key:

```sql
-- create
CREATE TABLE EMPLOYEE (
  empId INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  dept TEXT NOT NULL, 
  UNIQUE KEY uniq_id (name(255), dept(255))
);

-- insert
INSERT INTO EMPLOYEE VALUES (0001, 'Clark', 'Sales');
INSERT INTO EMPLOYEE VALUES (0002, 'Dave', 'Accounting');
INSERT INTO EMPLOYEE VALUES (0003, 'Ava', 'Sales');
```













