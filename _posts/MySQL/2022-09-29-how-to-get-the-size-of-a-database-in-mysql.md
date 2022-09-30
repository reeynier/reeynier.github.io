---
layout: post
title:  "How To Get The Size Of A Database In MySQL"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: How to get the size of a database in MySQL
---

<br />

## Short Answer


```sql
SELECT table_schema "Database Name",
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) "Database Size in MB" 
FROM information_schema.tables 
GROUP BY table_schema; 
```


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

SELECT table_schema "Database Name",
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) "Database Size in MB" 
FROM information_schema.tables 
GROUP BY table_schema; 
```

Query output:
```
+------------------+---------------------+
| Database Name    | Database Size in MB |
+------------------+---------------------+
| test_db          | 0.02                |
+------------------+---------------------+
```








