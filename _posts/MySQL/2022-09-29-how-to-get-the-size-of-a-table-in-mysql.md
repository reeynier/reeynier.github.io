---
layout: post
title:  "How To Get The Size Of A Table In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: How to get the size of a table in MySQL
---

<br />

## Short Answer

```sql
SELECT 
    table_name AS `Table`, 
    round(((data_length + index_length) / 1024 / 1024), 2) AS `Size in MB` 
FROM information_schema.TABLES 
WHERE table_name = "TABLE_NAME";
```

Substitute the string TABLE_NAME with the name of the table we would like to check the size.


## Example

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

-- fetch 
SELECT 
    table_name AS `Table`, 
    round(((data_length + index_length) / 1024 / 1024), 2) AS `Size in MB` 
FROM information_schema.TABLES 
WHERE table_name = "EMPLOYEE";
```

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

Query output:
```
+----------+------------+
| Table    | Size in MB |
+----------+------------+
| EMPLOYEE | 0.02       |
+----------+------------+
```








