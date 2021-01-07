---
layout: post
title:  "MySQL LIKE Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.
---

<br />

## Introduction

The `LIKE` operator is used in a `WHERE` clause to search for a specified pattern in a column.

There are two wildcards often used in conjunction with the `LIKE` operator:

* % - The percent sign represents zero, one, or multiple characters
* _ - The underscore represents a single character

For example, *s%* matches any string starts with the character *s*, such as sun and six. The *se_* matches any string starts with *se* and is followed by any character, such as see and sea.

Here is the syntax of the `LIKE` operator.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```


## Examples


For example, we might want
to find all album names beginning with the word “Retro.” We can do this with the
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

We can combine the `NOT` operator with `LIKE`. Suppose we want all albums that don’t
begin with an L:

```
mysql> SELECT album_name FROM album WHERE album_name NOT LIKE "L%";
+------------------------------------------+
| album_name                               |
+------------------------------------------+
| Retro - John McCready FAN                |
| Substance (Disc 2)                       |
| Retro - Miranda Sawyer POP               |
| Retro - New Order / Bobby Gillespie LIVE |
| In A Silent Way                          |
| Power, Corruption & Lies                 |
| Exile On Main Street                     |
| Substance 1987 (Disc 1)                  |
| Second Coming                            |
| Brotherhood                              |
+------------------------------------------+
```



















