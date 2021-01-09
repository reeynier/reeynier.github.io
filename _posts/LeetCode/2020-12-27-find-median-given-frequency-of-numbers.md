---
layout: post
title:  "Find Median Given Frequency Of Numbers Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup4 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseHard1
excerpt: LeetCode 571. Write a query to find the median of all numbers and name the result as median.
---

<br />

## Description

LeetCode Problem 571. 

The Numbers table keeps the value of number and its frequency.

```
+----------+-------------+
|  Number  |  Frequency  |
+----------+-------------|
|  0       |  7          |
|  1       |  1          |
|  2       |  3          |
|  3       |  1          |
+----------+-------------+
```

In this table, the numbers are 0, 0, 0, 0, 0, 0, 0, 1, 2, 2, 2, 3, so the median is (0 + 0) / 2 = 0.

```
+--------+
| median |
+--------|
| 0.0000 |
+--------+
```

Write a query to find the median of all numbers and name the result as median.



<br />

## MySQL Solution


```sql
select round(sum(Number) / count(Number), 2) as median
from (select Number, Frequency,
      sum(Frequency) over (order by Number) as cumulative_num,
      sum(Frequency) over () as total_num
      from Numbers) sub
where total_num / 2.0 between cumulative_num - Frequency and cumulative_num
```
