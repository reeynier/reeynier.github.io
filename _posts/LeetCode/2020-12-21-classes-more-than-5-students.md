---
layout: post
title:  "Classes More Than 5 Students Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ Database ]
featured: false
hidden: false
excerpt: LeetCode 596. Please list out all classes which have more than or equal to 5 students.

---

<br />

## Description

LeetCode Problem 596. 

There is a table courses with columns: student and class.

Please list out all classes which have more than or equal to 5 students.

For example, the table:

```
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+
```

Should output:

```
+---------+
| class   |
+---------+
| Math    |
+---------+
```

<br />

## MySQL Solution


```sql
select class
from courses
group by class
having count(distinct student) >= 5
```
