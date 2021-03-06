---
layout: post
title:  "Evaluate Boolean Expression Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup19 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium3
excerpt: LeetCode 1440. Write an SQL query to evaluate the boolean expressions in Expressions table.

---

<br />

## Description

LeetCode Problem 1440. 

Table Variables:

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| name          | varchar |
| value         | int     |
+---------------+---------+
name is the primary key for this table.
This table contains the stored variables and their values.
```

Table Expressions:

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| left_operand  | varchar |
| operator      | enum    |
| right_operand | varchar |
+---------------+---------+
(left_operand, operator, right_operand) is the primary key for this table.
This table contains a boolean expression that should be evaluated.
operator is an enum that takes one of the values ('<', '>', '=')
The values of left_operand and right_operand are guaranteed to be in the Variables table.
```

Write an SQL query to evaluate the boolean expressions in Expressions table.

Return the result table in any order.

The query result format is in the following example.

```
Variables table:
+------+-------+
| name | value |
+------+-------+
| x    | 66    |
| y    | 77    |
+------+-------+

Expressions table:
+--------------+----------+---------------+
| left_operand | operator | right_operand |
+--------------+----------+---------------+
| x            | >        | y             |
| x            | <        | y             |
| x            | =        | y             |
| y            | >        | x             |
| y            | <        | x             |
| x            | =        | x             |
+--------------+----------+---------------+

Result table:
+--------------+----------+---------------+-------+
| left_operand | operator | right_operand | value |
+--------------+----------+---------------+-------+
| x            | >        | y             | false |
| x            | <        | y             | true  |
| x            | =        | y             | false |
| y            | >        | x             | true  |
| y            | <        | x             | false |
| x            | =        | x             | true  |
+--------------+----------+---------------+-------+
As shown, you need find the value of each boolean exprssion in the table using the variables table.
```

<br />

## MySQL Solution


```sql
select e.left_operand, e.operator, e.right_operand,
    case
        when e.operator = '<' then if(l.value < r.value,'true','false')
        when e.operator = '>' then if(l.value > r.value,'true','false')
        else if(l.value = r.value,'true','false')
    end as value
from expressions e 
left join variables l on e.left_operand = l.name 
left join variables r on e.right_operand = r.name
```
