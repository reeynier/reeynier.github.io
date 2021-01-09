---
layout: post
title:  "Shortest Distance In A Plane Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup7 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium1
excerpt: LeetCode 612. Write a query to find the shortest distance between these points rounded to 2 decimals.

---

<br />

## Description

LeetCode Problem 612. 

Table point_2d holds the coordinates (x,y) of some unique points (more than two) in a plane.
 

Write a query to find the shortest distance between these points rounded to 2 decimals.
 
```
| x  | y  |
|----|----|
| -1 | -1 |
| 0  | 0  |
| -1 | -2 |
```

The shortest distance is 1.00 from point (-1,-1) to (-1,2). So the output should be:
 
```
| shortest |
|----------|
| 1.00     |
```


<br />

## MySQL Solution


```sql
select round(sqrt(min((pow(p1.x - p2.x, 2) + pow(p1.y - p2.y, 2)))), 2) as shortest
from point_2d p1
join point_2d p2 
on p1.x != p2.x or p1.y != p2.y
```
