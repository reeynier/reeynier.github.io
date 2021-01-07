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

#### Basic 

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

#### With `AND`, `OR`, `NOT` Operators

Suppose we want to find all albums with a title that begins
with a character greater than C but less than M. This is straightforward with the `AND`
operator:

```
mysql> SELECT album_name FROM album WHERE
 -> album_name > "C" AND album_name < "M";
+-----------------------+
| album_name            |
+-----------------------+
| Let Love In           |
| Live Around The World |
| In A Silent Way       |
| Exile On Main Street  |
| Light Years           |
+-----------------------+
```

Here is another example. Suppose we want a list of all
albums except the ones having an album_id of 1 or 3. We’d write the query:

```
mysql> SELECT * FROM album WHERE NOT (album_id = 1 OR album_id = 3);
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

#### With `LIKE` Operator

A common task to perform with strings is to find matches that
begin with a prefix, contain a string, or end in a suffix. For example, we might want
to find all album names beginning with the word “Retro.” You can do this with the
`LIKE` operator in a WHERE clause:

```
mysql> SELECT album_name FROM album WHERE album_name LIKE "Retro%";
+------------------------------------------+
| album_name                               |
+------------------------------------------+
| Retro - John McCready FAN                |
| Retro - Miranda Sawyer POP               |
| Retro - New Order / Bobby Gillespie LIVE |
+------------------------------------------+
```


