---
layout: post
title:  "How To Concatenate Multiple Rows Into One Field In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: How to concatenate multiple rows into one field in MySQL
---

<br />

## Short Answer

Use GROUP_CONCAT:

```sql
SELECT col1,
   GROUP_CONCAT(col2 ORDER BY col2 SEPARATOR ', ')
FROM TABLE
GROUP BY col1;
```


## Example

Given an EMPLOYEE table, for each department, return all the names of employees belong to this department. All the names should be in one field.

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

SELECT dept, GROUP_CONCAT(name ORDER BY name SEPARATOR ', ') AS names
FROM EMPLOYEE
GROUP BY dept;
```

Table EMPLOYEE:
```
+-------+-------+------------+
| empId	| name  | dept       |
+-------+-------+------------+
|     1 | Clark	| Sales      |
|     2	| Dave	| Accounting |
|     3	| Ava	| Sales      |
+-------+-------+------------+
```

Query output:
```
+------------+------------+
| dept       | names      |
+------------+------------+
| Accounting | Dave       |
| Sales      | Ava, Clark |
+------------+------------+
```








