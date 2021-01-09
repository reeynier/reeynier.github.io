---
layout: post
title:  "Second Degree Follower Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup7 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium1
excerpt: LeetCode 614. Please write a sql query to get the amount of each follower’s follower if he/she has one.
---

<br />

## Description

LeetCode Problem 614. 

In facebook, there is a follow table with two columns: followee, follower.

Please write a sql query to get the amount of each follower’s follower if he/she has one.

For example:

```
+-------------+------------+
| followee    | follower   |
+-------------+------------+
|     A       |     B      |
|     B       |     C      |
|     B       |     D      |
|     D       |     E      |
+-------------+------------+
```

should output:

```
+-------------+------------+
| follower    | num        |
+-------------+------------+
|     B       |  2         |
|     D       |  1         |
+-------------+------------+
```

Explaination: Both B and D exist in the follower list, when as a followee, B's follower is C and D, and D's follower is E. A does not exist in follower list.
 

Note: Followee would not follow himself/herself in all cases. Please display the result in follower's alphabet order.

<br />

## MySQL Solution


```sql
select f1.follower, count(distinct f2.follower) as num 
from follow f1 
join follow f2 
on f1.follower = f2.followee 
group by f1.follower
```
