---
layout: post
title:  "How To Change The Data Type Of A Column In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: Given a table EMPLOYEE, change the data type of the yoe (year of experience) column from INTEGER to FLOAT.
---

<br />

## Short Answer


```sql
ALTER TABLE table_name MODIFY column_name NEW_DATA_TYPE;
```


## Example

Given a table EMPLOYEE, change the data type of the yoe (year of experience) column from INTEGER to INTEGER UNSIGNED.

```sql
-- create
CREATE TABLE EMPLOYEE (
  empId INTEGER PRIMARY KEY,
  name TEXT NOT NULL,
  dept TEXT NOT NULL, 
  yoe INTEGER NOT NULL
);

-- insert
INSERT INTO EMPLOYEE VALUES (0001, 'Clark', 'Sales', 5);
INSERT INTO EMPLOYEE VALUES (0002, 'Dave', 'Accounting', 3);
INSERT INTO EMPLOYEE VALUES (0003, 'Ava', 'Sales', 8);

ALTER TABLE EMPLOYEE MODIFY yoe INTEGER UNSIGNED NOT NULL;

DESCRIBE EMPLOYEE;
```

Table EMPLOYEE:
```
+-------+-------+------------+-----+
| empId	| name  | dept       | yoe |
+-------+-------+------------+-----+
|     1 | Clark	| Sales      | 5   |
|     2	| Dave	| Accounting | 3   |
|     3	| Ava	| Sales      | 8   |
+-------+-------+------------+-----+
```

Query output:
```
+-------+--------------+------+-----+---------------+
| Field | Type         | Null | Key | Default Extra |
+-------+--------------+------+-----+---------------+
| empId | int          | NO   | PRI | NULL          |
| name  | text         | NO   |     | NULL          |
| dept  | text         | NO   |     | NULL          |
| yoe   | int unsigned | NO   |     | NULL          |
+-------+--------------+------+-----+---------------+
```








