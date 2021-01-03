---
layout: post
title:  "MySQL ORDER BY Clause"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL ]
featured: false
hidden: false
excerpt: The `ORDER BY` clause is used to sort the result-set in ascending or descending order.
---

<br />

## Introduction

In a relational database, the rows in a table form a set; there is no intrinsic order between the rows,
and so we have to ask MySQL to sort the results if we want them in a particular order.

The `ORDER BY` clause is used to sort the result-set in ascending or descending order. The `ORDER BY` clause sorts the records in ascending order by default. To sort the records in descending order, use the `DES` keyword. Sorting has no
effect on what is returned, and only affects what order the results are returned.


To use the `ORDER BY` clause in MySQL, we follow this syntax:

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC], column2 [ASC|DESC], ...;
```

Note that the ORDER BY clause is always evaluated after the FROM and SELECT clause.


## Examples

#### Sort By One Column

Suppose we want to return a list of the artists in the artist table, sorted in alphabetical order by the artist_name. Here’s what we’d type:

```
mysql> SELECT * FROM artist ORDER BY artist_name;
+-----------+---------------------------+
| artist_id | artist_name               |
+-----------+---------------------------+
| 6         | Kylie Minogue             |
| 3         | Miles Davis               |
| 1         | New Order                 |
| 2         | Nick Cave & The Bad Seeds |
| 4         | The Rolling Stones        |
| 5         | The Stone Roses           |
+-----------+---------------------------+
```

We can also sort in descending order, and we can control this behavior for each sort
key. Suppose we want to sort the artists by descending alphabetical order. We type
this:

```
mysql> SELECT artist_name FROM artist ORDER BY artist_name DESC;
+---------------------------+
| artist_name               |
+---------------------------+
| The Stone Roses           |
| The Rolling Stones        |
| Nick Cave & The Bad Seeds |
| New Order                 |
| Miles Davis               |
| Kylie Minogue             |
+---------------------------+
```


#### Sort By Multiple Columns

Let’s sort the output from the track table by
ascending track length—that is, by the time column. Since it’s likely that two or more
tracks have the same length, we’ll add a second sort key to resolve collisions and determine how such ties should be broken. In this case, when the track times are the same,
we’ll sort the answers alphabetically by track_name. Here’s what we type:

```
mysql> SELECT time, track_name FROM track ORDER BY time, track_name;
+------+-----------------------------+
| time | track_name                  |
+------+-----------------------------+
| 2.90 | I Just Want To See His Face |
| 2.97 | Sweet Black Angel           |
| 2.99 | Your Star Will Shine        |
| 3.00 | Shake Your Hips             |
| 3.08 | Happy                       |
| 3.20 | Dreams Never End            |
| 3.26 | Straight To The Man         |
| 3.40 | Under The Influence Of Love |
| 3.40 | Ventilator Blues            |
| 3.42 | Cries And Whispers          |
+------+-----------------------------+
```

Notice that there’s a collision of track
times where the length is 3.40. In this case, the second sort key, track_name, is used to
resolve the collision so that “Under the Influence of Love” appears before “Ventilator
Blues.” 













