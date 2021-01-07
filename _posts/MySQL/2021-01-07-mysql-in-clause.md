---
layout: post
title:  "MySQL IN Clause"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `IN`  operator allows us to determine if a specified value matches any value in a set of values or returned by a subquery.
---

<br />

## Introduction

The `IN`  operator allows us to determine if a specified value matches any value in a set of values or returned by a subquery.

The following illustrates the syntax of the `IN`  operator:

```sql
SELECT column1,column2,...
FROM table_name
WHERE (expr|column_1) IN ('value1','value2',...);
```

The `IN` operator returns 1 if the value of the *column_1* or the result of the *expr*  expression is equal to any value in the list, otherwise, it returns 0.

## Examples



Suppose we want to know the producers who
are also engineers. We can do this with the following nested query:

```
mysql> SELECT producer_name FROM producer WHERE producer_name
 -> IN (SELECT engineer_name FROM engineer);
+---------------+
| producer_name |
+---------------+
| George Martin |
+---------------+
```

For this particular example, we could also have used a `JOIN` query:

```
mysql> SELECT producer_name FROM producer INNER JOIN engineer
 -> ON (producer_name = engineer_name);
+---------------+
| producer_name |
+---------------+
| George Martin |
+---------------+
```

We can use `NOT IN` to s find all the engineers who
aren't producers.

```
mysql> SELECT engineer_name FROM engineer WHERE
 -> engineer_name NOT IN
 -> (SELECT producer_name FROM producer);
+---------------+
| engineer_name |
+---------------+
| Eddie Kramer  |
| Jeff Jarratt  |
| Ed Stasium    |
+---------------+
```