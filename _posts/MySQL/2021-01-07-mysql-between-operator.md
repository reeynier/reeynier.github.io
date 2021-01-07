---
layout: post
title:  "MySQL BETWEEN Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `OR` operator combines two Boolean expressions and returns true when either condition is true.
---

<br />

## Introduction

The `BETWEEN` operator selects values within a given range. The values can be numbers, text, or dates. The `BETWEEN` operator is inclusive: begin and end values are included. 

The following illustrates the syntax of the `BETWEEN` operator:

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```


## Examples



Suppose we want a list of all
albums that have an album_id between 2 and 7. We’d write the query:

```
mysql> SELECT * FROM album WHERE album_id BETWEEN 2 AND 7;
+-----------+----------+------------------------------------------+
| artist_id | album_id | album_name                               |
+-----------+----------+------------------------------------------+
| 1         | 2        | Substance (Disc 2)                       |
| 1         | 4        | Retro - New Order / Bobby Gillespie LIVE |
| 3         | 2        | In A Silent Way                          |
| 1         | 5        | Power, Corruption & Lies                 |
| 1         | 6        | Substance 1987 (Disc 1)                  |
| 1         | 7        | Brotherhood                              |
+-----------+----------+------------------------------------------+
```

We can also use the `BETWEEN` operator to select dates within a range. The following query selects all orders with an OrderDate between 1996-07-01 and 1996-07-31.

```
mysql> SELECT * FROM Orders
 -> WHERE OrderDate BETWEEN '1996-07-04' AND '1996-07-10';
+-----------+-----------+-----------+
|OrderID    |CustomerID |OrderDate  |
+-----------+-----------+-----------+
|10248      |90         |7/4/1996   |
|10249 	    |81         |7/5/1996   |
|10250 	    |34         |7/8/1996   |
|10251 	    |84         |7/8/1996   |
|10252 	    |76         |7/9/1996   |
|10253 	    |34         |7/10/1996  |
+-----------+-----------+-----------+
```
