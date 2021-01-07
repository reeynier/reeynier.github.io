---
layout: post
title:  "MySQL LIMIT Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `LIMIT` clause is used in the `SELECT` statement to constrain the number of rows to return.
---

<br />

## Introduction

The `LIMIT` clause is used in the `SELECT` statement to constrain the number of rows to return. The `LIMIT` clause accepts one or two arguments. The values of both arguments must be zero or positive integers.

The following illustrates the `LIMIT` clause syntax with two arguments:

```sql
SELECT select_list
FROM table_name
LIMIT [offset,] row_count;
```

In this syntax:

* The offset specifies the offset of the first row to return. The offset of the first row is 0, not 1.
* The row_count specifies the maximum number of rows to return.

When you use the `LIMIT` clause with one argument, MySQL will use this argument to determine the maximum number of rows to return from the first row of the result set. Therefore, the following two clauses are equivalent.

```sql
LIMIT row_count;
LIMIT 0 , row_count;
```


## Examples


For example, in a
web database application, where we want to find the rows that match a condition but
only want to show the user the first 10 rows in a web page. Here’s an example:

```
mysql> SELECT track_name FROM track LIMIT 10;
+----------------------------+
| track_name                 |
+----------------------------+
| Do You Love Me?            |
| Nobody's Baby Now          |
| Loverman                   |
| Jangling Jack              |
| Red Right Hand             |
| I Let Love In              |
| Thirsty Dog                |
| Ain't Gonna Rain Anymore   |
| Lay Me Low                 |
| Do You Love Me? (Part Two) |
+----------------------------+
```

The `LIMIT` clause in this example restricts the output to the first 10 rows, saving the
cost of buffering, communicating, and displaying the remaining 143 tracks.



Here is another example. Suppose we want five rows, but we want the first one displayed to be
the sixth row of the answer set. We do this by starting from after the fifth answer:

```
mysql> SELECT track_name FROM track LIMIT 5,5;
+----------------------------+
| track_name                 |
+----------------------------+
| I Let Love In              |
| Thirsty Dog                |
| Ain't Gonna Rain Anymore   |
| Lay Me Low                 |
| Do You Love Me? (Part Two) |
+----------------------------+
```

