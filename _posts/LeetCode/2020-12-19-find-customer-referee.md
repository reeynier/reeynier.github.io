---
layout: post
title:  "Find Customer Referee Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup5 ]
featured: false
hidden: false
excerpt: LeetCode 584. Given a table customer holding customers information and the referee.

---

<br />

## Description

LeetCode Problem 584. 

Given a table customer holding customers information and the referee.

```
+------+------+-----------+
| id   | name | referee_id|
+------+------+-----------+
|    1 | Will |      NULL |
|    2 | Jane |      NULL |
|    3 | Alex |         2 |
|    4 | Bill |      NULL |
|    5 | Zack |         1 |
|    6 | Mark |         2 |
+------+------+-----------+
```

Write a query to return the list of customers NOT referred by the person with id '2'.

For the sample data above, the result is:

```
+------+
| name |
+------+
| Will |
| Jane |
| Bill |
| Zack |
+------+
```

<br />

## MySQL Solution


```sql
select name
from customer
where referee_id != '2' or referee_id is null
```
