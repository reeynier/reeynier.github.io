---
layout: post
title:  "How To Select One Row Per ID With Max Value On A Column"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Common Query ]
featured: false
hidden: false
sidenav: MySQL
excerpt: Suppose we have the following REIMBURSEMENT table, find the max reimbursement value for each employee.
---

<br />



## Short Answer

Approach 1: 

```sql
SELECT a.*
FROM TABLE a 
INNER JOIN (
  SELECT id, MAX(col) AS col
  FROM TABLE
  GROUP BY id
) b ON a.id = b.id AND a.col = b.col;
```

First we find the group identifier and max value in group in a sub query, then we join the table to the sub query with equality on both group identifier and max value in group.

Approach 2: 

```sql
SELECT a.*
FROM TABLE a
LEFT OUTER JOIN TABLE b
	ON  a.id = b.id AND a.col < b.col
WHERE b.id is NULL;
```

First we left join the table with itself with equality of group identifier and left side value less than right side value. Then we filter the joined result, showing only the rows where the right side is NULL, because when we do the left join, the rows with max value will have NULL in the right side.

Approach 3: 

```sql
SELECT a.*
  FROM (SELECT *,
        ROW_NUMBER() OVER (PARTITION BY id ORDER BY col DESC) ranked_order
        FROM TABLE) a
 WHERE a.ranked_order = 1 
```

## Example

Suppose we have the following REIMBURSEMENT table, find the max reimbursement value for each employee.

Table REIMBURSEMENT:
```
+-------+-------+------------+-------+
| empId	| name  | dept       | reimb |
+-------+-------+------------+-------+
|     1 | Clark	| Sales      | 3000  |
|     2	| Dave	| Accounting | 500   |
|     2	| Dave	| Accounting | 1500  |
|     3	| Ava 	| Sales      | 700   |
|     1 | Clark	| Sales      | 300   |
|     1 | Clark	| Sales      | 60    |
|     3	| Ava  	| Sales      | 1700  |
+-------+-------+------------+-------+
```

Expected output:
```
+-------+-------+------------+-------+
| empId	| name  | dept       | reimb |
+-------+-------+------------+-------+
|     1 | Clark	| Sales      | 3000  |
|     2	| Dave	| Accounting | 1500  |
|     3	| Ava	| Sales      | 1700  |
+-------+-------+------------+-------+
```

Create the table:

```sql
-- create
CREATE TABLE REIMBURSEMENT (
  empId INTEGER NOT NULL,
  name TEXT NOT NULL,
  dept TEXT NOT NULL,
  reimb INTEGER NOT NULL
);

-- insert
INSERT INTO REIMBURSEMENT VALUES (1, 'Clark', 'Sales', 300);
INSERT INTO REIMBURSEMENT VALUES (2, 'Dave', 'Accounting', 500);
INSERT INTO REIMBURSEMENT VALUES (2, 'Dave', 'Accounting', 1500);
INSERT INTO REIMBURSEMENT VALUES (3, 'Ava', 'Sales', 700);
INSERT INTO REIMBURSEMENT VALUES (1, 'Clark', 'Sales', 3000);
INSERT INTO REIMBURSEMENT VALUES (1, 'Clark', 'Sales', 60);
INSERT INTO REIMBURSEMENT VALUES (3, 'Ava', 'Sales', 1700);
```

Approach 1: 

```sql
SELECT a.*
FROM REIMBURSEMENT a 
INNER JOIN (
  SELECT empId, MAX(reimb) AS reimb
  FROM REIMBURSEMENT
  GROUP BY empId
) b ON a.empId = b.empId AND a.reimb = b.reimb
ORDER BY a.empId;
```

Approach 2:

```sql
SELECT a.*
FROM REIMBURSEMENT a
LEFT OUTER JOIN REIMBURSEMENT b
	ON  a.empId = b.empId AND a.reimb < b.reimb
WHERE b.empId is NULL
ORDER BY a.empId;
```

Approach 3:

```sql
SELECT a.empId, a.name, a.dept, a.reimb
  FROM (SELECT *,
        ROW_NUMBER() OVER (PARTITION BY empId ORDER BY reimb DESC) ranked_order
        FROM REIMBURSEMENT) a
 WHERE a.ranked_order = 1 
```
















