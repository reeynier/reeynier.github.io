---
layout: post
title:  "How To Find Duplicate Values In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: Do a SELECT with a GROUP BY clause. 
---

<br />

## Short Answer

Do a SELECT with a GROUP BY clause. 

```sql
SELECT col, COUNT(*) count 
FROM TABLE 
GROUP BY col 
HAVING count > 1;
```

Suppose `col` is the column we want to find duplicate values in. This will return a result with the `col` value in the first column, and a `count` of how many times that value appears in the second column.  

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
SELECT GROUP_CONCAT(empId) ids, dept, COUNT(*) count 
FROM EMPLOYEE 
GROUP BY dept 
HAVING count > 1;
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
+-----+-------+-------+
| ids | dept  | count |
+-----+-------+-------+
| 1,3 | Sales | 2     |
+-----+-------+-------+
```



















