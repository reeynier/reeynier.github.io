---
layout: post
title:  "MySQL OR Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
excerpt: The `OR` operator combines two Boolean expressions and returns true when either condition is true.
---

<br />

## Introduction

The MySQL `OR` operator combines two Boolean expressions and returns true when either condition is true.

The following illustrates the syntax of the `OR` operator.

```sql
boolean_expression_1 OR boolean_expression_2
```


Both boolean_expression_1 and boolean_expression_2 are Boolean expressions that return true, false, or NULL.

When we use more than one logical operator in an expression, MySQL always evaluates the `OR` operators after the `AND` operators. 


## Examples



Suppose we want a list of all
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


