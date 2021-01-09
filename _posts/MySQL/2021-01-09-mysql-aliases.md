---
layout: post
title:  "MySQL Aliases"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
sidenav: MySQL
excerpt: Aliases are nicknames. They give us a shorthand way of expressing a column, table, or function name, allowing us to write short and clear queries.
---

<br />

## Introduction


Aliases are nicknames. They give us a shorthand way of expressing a column, table,
or function name, allowing us to write short and clear queries. An alias only exists for the duration of the query.

MySQL supports two kinds of aliases which are known as `column alias` and `table alias`. 


#### Column Aliases

The following statement illustrates how to use the column alias:

```sql
SELECT column_name AS alias_name, expression As `descriptive name`
FROM table_name;
```

To assign an alias to a column, we can use the `AS` keyword followed by the alias, but the `AS` keyword is optional. If the alias contains spaces, we must quote it.

#### Table Aliases

The following statement illustrates how to use the table alias:

```sql
SELECT column_name(s)
FROM table_name AS alias_name;
```


## Examples

#### Column Aliases

Here’s an example that uses a
`CONCAT` function and an `ORDER BY` clause:

```
mysql> SELECT CONCAT(artist_name, " recorded ", album_name) AS recording
 -> FROM artist INNER JOIN album USING (artist_id)
 -> ORDER BY recording;
+-------------------------------------------------------------+
| recording                                                   |
+-------------------------------------------------------------+
| Kylie Minogue recorded Light Years                          |
| Miles Davis recorded In A Silent Way                        |
| Miles Davis recorded Live Around The World                  |
| New Order recorded Brotherhood                              |
| New Order recorded Power, Corruption & Lies                 |
| New Order recorded Retro - John McCready FAN                |
| New Order recorded Retro - Miranda Sawyer POP               |
| New Order recorded Retro - New Order / Bobby Gillespie LIVE |
| New Order recorded Substance (Disc 2)                       |
| New Order recorded Substance 1987 (Disc 1)                  |
| Nick Cave & The Bad Seeds recorded Let Love In              |
| The Rolling Stones recorded Exile On Main Street            |
| The Stone Roses recorded Second Coming                      |
+-------------------------------------------------------------+
```

There are restrictions on where we can use column aliases. We can’t use them in a
`WHERE` clause, or in the `USING` and `ON` clauses. This
means we can’t write a query such as:

```
mysql> SELECT artist_name AS a FROM artist WHERE a = "New Order";
ERROR 1054 (42S22): Unknown column 'a' in 'where clause'
```

We can’t do this because MySQL doesn’t always know the column values before it
executes the `WHERE` clause. However, we can use column aliases in the `ORDER BY` clause,
and in the `GROUP BY` and `HAVING` clauses.

#### Table Aliases

Here’s a basic table-alias example:

```
mysql> SELECT ar.artist_id, al.album_name, ar.artist_name FROM
 -> album AS al INNER JOIN artist AS ar
 -> USING (artist_id) WHERE al.album_name = "Brotherhood";
+-----------+-------------+-------------+
| artist_id | album_name  | artist_name |
+-----------+-------------+-------------+
| 1         | Brotherhood | New Order   |
+-----------+-------------+-------------+
```

Consider another example: suppose we want to
know whether two or more artists have released an album of the same name and, if so,
what the identifiers for those artists are. Here is the query:

```
mysql> SELECT a1.artist_id, a2.album_id
 -> FROM album AS a1, album AS a2
 -> WHERE a1.album_name = a2.album_name
 -> AND a1.artist_id != a2.artist_id;
```
