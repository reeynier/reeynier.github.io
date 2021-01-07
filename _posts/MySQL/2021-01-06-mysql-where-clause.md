---
layout: post
title:  "MySQL WHERE Clause"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `WHERE` clause allows us to choose which rows are returned from a `SELECT` statement.
---

<br />

## Introduction

The `WHERE` clause allows us to choose which rows are returned from a `SELECT` statement. To use the `WHERE` clause in MySQL, we follow this syntax:

```sql
SELECT select_list
FROM table_name
WHERE search_condition;
```

In the `SELECT` statement, the `WHERE` clause is evaluated after the `FROM` clause and before the `SELECT` clause.

## Examples


The simplest `WHERE` clause is one that exactly matches a value. Consider an example
where we want to find out the details of the artist with the name “New Order.” Here’s
what we type:

```
mysql> SELECT * FROM artist WHERE artist_name = "New Order";
+-----------+-------------+
| artist_id | artist_name |
+-----------+-------------+
| 1         | New Order   |
+-----------+-------------+
```


We can also retriev values in a range. We want to find the names of all artists with an artist_id less than 5. To do this, type:

```
mysql> SELECT artist_name FROM artist WHERE artist_id < 5;
+---------------------------+
| artist_name               |
+---------------------------+
| New Order                 |
| Nick Cave & The Bad Seeds |
| Miles Davis               |
| The Rolling Stones        |
+---------------------------+
```


