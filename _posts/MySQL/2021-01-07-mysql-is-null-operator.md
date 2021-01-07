---
layout: post
title:  "MySQL IS NULL Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: To test whether a value is NULL or not, we use the  `IS NULL` operator.
---

<br />

## Introduction

To test whether a value is NULL or not, we use the  `IS NULL` operator.

Here is the basic syntax of the `IS NULL` operator:


```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```

If the value is NULL, the expression returns true. Otherwise, it returns false.

To check if a value is not NULL, we use `IS NOT NULL` operator:

```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```


## Examples

The following query lists all customers with a NULL value in the "Address" field:

```
mysql> SELECT CustomerName, ContactName, Address FROM Customers
 -> WHERE Address IS NULL;
+---------------------+--------------+---------+
| CustomerName        | ContactName  | Address |
+---------------------+--------------+---------+
| Alfreds Futterkiste | Maria Anders | NULL    |	
+---------------------+--------------+---------+
```
