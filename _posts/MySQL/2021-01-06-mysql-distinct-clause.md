---
layout: post
title:  "MySQL DISTINCT Clause"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: In order to remove duplicate rows, we use the `DISTINCT` clause in the `SELECT` statement.
---

<br />

## Introduction

When querying data from a table, we may get duplicate rows. In order to remove these duplicate rows, we use the `DISTINCT` clause in the `SELECT` statement.

Here is the syntax of the `DISTINCT` clause:

```sql
SELECT DISTINCT select_list
FROM table_name;
```

## Examples

Consider the following example. 

```
mysql> SELECT DISTINCT artist_name FROM
 -> artist INNER JOIN album USING (artist_id);
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


The query finds artists who have made albums—by joining together artist and
album with an `INNER JOIN` clause—and reports one example of each artist. We can see
that we have six artists in our database for whom we own albums. 

If we remove the `DISTINCT` clause, we get one row of output for each album we own:

```
mysql> SELECT artist_name FROM
 -> artist INNER JOIN album USING (artist_id);
+---------------------------+
| artist_name               |
+---------------------------+
| New Order                 |
| New Order                 |
| New Order                 |
| New Order                 |
| New Order                 |
| New Order                 |
| New Order                 |
| Nick Cave & The Bad Seeds |
| Miles Davis               |
| Miles Davis               |
| The Rolling Stones        |
| The Stone Roses           |
| Kylie Minogue             |
+---------------------------+
```


The `DISTINCT` clause applies to the query output and removes rows that have identical
values in the columns selected for output in the query. If we rephrase the previous
query to output both artist_name and album_name (but otherwise don’t change the
`JOIN` clause and still use `DISTINCT`), we will get all 13 rows in the output:

```
mysql> SELECT DISTINCT artist_name, album_name FROM
 -> artist INNER JOIN album USING (artist_id);
+---------------------------+------------------------------------------+
| artist_name               | album_name                               |
+---------------------------+------------------------------------------+
| New Order                 | Retro - John McCready FAN                |
| New Order                 | Substance (Disc 2)                       |
| New Order                 | Retro - Miranda Sawyer POP               |
| New Order                 | Retro - New Order / Bobby Gillespie LIVE |
| New Order                 | Power, Corruption & Lies                 |
| New Order                 | Substance 1987 (Disc 1)                  |
| New Order                 | Brotherhood                              |
| Nick Cave & The Bad Seeds | Let Love In                              |
| Miles Davis               | Live Around The World                    |
| Miles Davis               | In A Silent Way                          |
| The Rolling Stones        | Exile On Main Street                     |
| The Stone Roses           | Second Coming                            |
| Kylie Minogue             | Light Years                              |
+---------------------------+------------------------------------------+
```

Because none of the rows are identical, no duplicates are removed using `DISTINCT`.


