---
layout: post
title:  "MySQL Inner Join Clause"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
sidenav: MySQL
excerpt: The `INNER JOIN` keyword selects records that have matching values in both tables.
---

<br />

## Introduction


The `INNER JOIN` keyword selects records that have matching values in both tables.

Here is the syntax of the `INNER JOIN` clause:

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

The `INNER JOIN` clause compares each row in table1 with every row in table2 based on the join condition.

If rows from both tables cause the join condition to evaluate to TRUE, the `INNER JOIN` creates a new row whose columns contain all columns of rows from the tables and includes this new row in the result set. Otherwise, the `INNER JOIN` just ignores the rows.

In case no row between tables causes the join condition to evaluate to TRUE, the `INNER JOIN` returns an empty result set. This logic is also applied when we join more than 2 tables.



## Examples

For example, if we’re selecting from the artist and
album tables the rows where the identifiers match between the tables, we use the 
following query.

```
mysql> SELECT artist_name, album_name FROM
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


This is equivalent of the following two queries.

```
mysql> SELECT artist_name, album_name FROM
 -> artist INNER JOIN album USING (artist_id);
```

```
mysql> SELECT artist_name, album_name FROM artist, album
 -> WHERE artist.artist_id = album.artist_id;
```







