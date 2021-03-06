---
layout: post
title:  "Delete Duplicate Emails Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup2 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseEasy1
excerpt: LeetCode 196. Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.
---

<br />

## Description

LeetCode Problem 196. 

Write a SQL query to delete all duplicate email entries in a table named Person, keeping only unique emails based on its smallest Id.

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |
+----+------------------+
Id is the primary key column for this table.
```

For example, after running your query, the above Person table should have the following rows:

```
+----+------------------+
| Id | Email            |
+----+------------------+
| 1  | john@example.com |
| 2  | bob@example.com  |
+----+------------------+
```

<br />

## MySQL Solution


```sql
delete p1 
from Person p1, Person p2
where p1.Email = p2.Email and p1.Id > p2.Id
```
