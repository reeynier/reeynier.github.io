---
layout: post
title:  "Triangle Judgement Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup7 ]
featured: false
hidden: false
excerpt: LeetCode 610. A pupil Tim gets homework to identify whether three line segments could possibly form a triangle.

---

<br />

## Description

LeetCode Problem 610. 

A pupil Tim gets homework to identify whether three line segments could possibly form a triangle.
 

However, this assignment is very heavy because there are hundreds of records to calculate.
 

Could you help Tim by writing a query to judge whether these three sides can form a triangle, assuming table triangle holds the length of the three sides x, y and z.
 
```
| x  | y  | z  |
|----|----|----|
| 13 | 15 | 30 |
| 10 | 20 | 15 |
```

For the sample data above, your query should return the follow result:

```
| x  | y  | z  | triangle |
|----|----|----|----------|
| 13 | 15 | 30 | No       |
| 10 | 20 | 15 | Yes      |
```

<br />

## MySQL Solution


```sql
select *, 
    if(x+y>z and x+z>y and y+z>x, 'Yes', 'No') as triangle
from triangle
```
