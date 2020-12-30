---
layout: post
title:  "Duplicate Emails Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup2 ]
featured: false
hidden: false
excerpt: LeetCode 182. Write a SQL query to find all duplicate emails in a table named Person.
---

<br />

## Description

LeetCode Problem 182. 

Write a SQL query to find all duplicate emails in a table named Person.

```
+----+---------+
| Id | Email   |
+----+---------+
| 1  | a@b.com |
| 2  | c@d.com |
| 3  | a@b.com |
+----+---------+
```

For example, your query should return the following for the above table:

```
+---------+
| Email   |
+---------+
| a@b.com |
+---------+
```

<br />

## MySQL Solution


```sql
select p.Email
from (select Email, count(Email) as count
     from Person
     group by Email) p
where p.count > 1
```
