---
layout: post
title:  "Convert Date Format Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup27 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseEasy4
excerpt: LeetCode 1853. Write an SQL query to convert each date in Days into a string.
---

<br />

## Description

LeetCode Problem 1853. 

Table: Days
```
+-------------+------+
| Column Name | Type |
+-------------+------+
| day         | date |
+-------------+------+
day is the primary key for this table.
```

Write an SQL query to convert each date in Days into a string formatted as "day_name, month_name day, year".

Return the result table in any order.

The query result format is in the following example:

 
```
Days table:
+------------+
| day        |
+------------+
| 2022-04-12 |
| 2021-08-09 |
| 2020-06-26 |
+------------+

Result table:
+-------------------------+
| day                     |
+-------------------------+
| Tuesday, April 12, 2022 |
| Monday, August 9, 2021  |
| Friday, June 26, 2020   |
+-------------------------+
Please note that the output is case-sensitive.
```

<br />

## MySQL Solution


```sql
select concat(dayname(day), ", ", monthname(day), " ", day(day), ", ", year(day)) as day
from Days
```
