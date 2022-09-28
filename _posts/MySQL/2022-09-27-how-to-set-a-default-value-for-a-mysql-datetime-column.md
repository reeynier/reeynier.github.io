---
layout: post
title:  "How To Set A Default Value For A MySQL Datetime Column"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: How to set a default value for a MySQL Datetime column.
---

<br />

## Short Answer

```sql
CREATE TABLE test (
    creation_time DATETIME DEFAULT CURRENT_TIMESTAMP,
    modification_time DATETIME ON UPDATE CURRENT_TIMESTAMP
)
```

## Example

```sql
-- create
CREATE TABLE EMPLOYEE (
  empId INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  dept TEXT NOT NULL,
  creation_time DATETIME DEFAULT CURRENT_TIMESTAMP,
  modification_time DATETIME ON UPDATE CURRENT_TIMESTAMP
);

-- insert
INSERT INTO EMPLOYEE (empId, name, dept) VALUES (0001, 'Clark', 'Sales');
INSERT INTO EMPLOYEE (empId, name, dept) VALUES (0002, 'Dave', 'Accounting');
INSERT INTO EMPLOYEE (empId, name, dept) VALUES (0003, 'Ava', 'Sales');

-- fetch 
SELECT * FROM EMPLOYEE;
```

Query output:
```
+-------+-------+------------+---------------------+-------------------+
| empId	| name  | dept       | creation_time       | modification_time |
+-------+-------+------------+---------------------+-------------------+
|     1 | Clark	| Sales      | 2022-09-28 06:39:17 | NULL              |
|     2	| Dave	| Accounting | 2022-09-28 06:39:17 | NULL              |
|     3	| Ava	| Sales      | 2022-09-28 06:39:17 | NULL              |
+-------+-------+------------+---------------------+-------------------+
```



















