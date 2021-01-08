---
layout: post
title:  "MySQL AND Operator"
categories: [ MySQL ]
tags: [ Database, Query, MySQL ]
similar: [ MySQL Data Manipulation  ]
featured: false
hidden: false
sidenav: MySQL
excerpt: The `AND` operator is a logical operator that combines two or more Boolean expressions and returns true only if both expressions evaluate to true. 
---

<br />

## Introduction

The `AND` operator is a logical operator that combines two or more Boolean expressions and returns true only if both expressions evaluate to true. The `AND` operator returns false if one of the two expressions evaluate to false.

Here is the syntax of the `AND` operator:

```sql
boolean_expression_1 AND boolean_expression_2
```


The `AND` operator is often used in the `WHERE` clause of the `SELECT`, `UPDATE`, `DELETE` statement to form a condition. The `AND` operator is also used in join conditions of the  `INNER JOIN` and  `LEFT JOIN` clauses.

When evaluating an expression that has the `AND` operator, MySQL stops evaluating the remaining parts of the expression whenever it can determine the result. 

## Examples



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


