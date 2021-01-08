---
layout: post
title:  "MySQL SELECT Statement"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation ]
featured: false
hidden: false
sidenav: MySQL
excerpt: The `SELECT` statement allows us to read data from one or more tables.
---

<br />

## Introduction

The `SELECT` statement allows us to read data from one or more tables. To write a SELECT statement in MySQL, we follow this syntax:

```sql
SELECT select_list
FROM table_name;
```

A simple SELECT statement has four components:
1. The keyword SELECT.
2. The columns to be displayed. 
3. The keyword FROM.
4. The table name.

The semicolon ; is the statement delimiter. It specifies the end of a statement. If we have two or more statements, we use the semicolon ; to separate them so that MySQL will execute each statement individually.

In the `SELECT` statement, the **SELECT** and **FROM** are keywords and written in capital letters. Basically, it is just about formatting. The uppercase letters make the keywords stand out. Since SQL is **not** a case-sensitive language, we can write the keywords in lowercase e.g., select and from, the code will still run.


When evaluating the SELECT statement, MySQL evaluates the FROM clause first and then the SELECT clause.


## Examples

#### Single Table SELECTs

The most basic form of SELECT reads the data in all rows and columns from a table. Below is an example to retrieve all of the data in the artist table. The \* wildcard character is used to retrieve all columns in a table.

```
mysql> SELECT * FROM artist;
+-----------+---------------------------+
| artist_id | artist_name               |
+-----------+---------------------------+
|         1 | New Order                 |
|         2 | Nick Cave & The Bad Seeds |
|         3 | Miles Davis               |
|         4 | The Rolling Stones        |
|         5 | The Stone Roses           |
|         6 | Kylie Minogue             |
+-----------+---------------------------+
```

#### Choosing Columns

If we don’t want to display all the columns, it’s easy to be more specific by listing the columns
we want, in the order we want them, separated by commas. For example, if we want
only the artist_name column from the artist table, we would type:


```
mysql> SELECT artist_name FROM artist;
+---------------------------+
| artist_name               |
+---------------------------+
| New Order                 |
| Nick Cave & The Bad Seeds |
| Miles Davis               |
| The Rolling Stones        |
| The Stone Roses           |
| Kylie Minogue             |
+---------------------------+
```


















