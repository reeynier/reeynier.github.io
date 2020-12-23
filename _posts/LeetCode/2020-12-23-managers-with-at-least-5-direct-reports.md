---
layout: post
title:  "Managers With At Least 5 Direct Reports Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ Database ]
featured: false
hidden: false
excerpt: LeetCode 570. Given the Employee table, write a SQL query that finds out managers with at least 5 direct report.

---

<br />

## Description

LeetCode Problem 570. 

The Employee table holds all employees including their managers. Every employee has an Id, and there is also a column for the manager Id.

```
+------+----------+-----------+----------+
|Id    |Name      |Department |ManagerId |
+------+----------+-----------+----------+
|101   |John      |A          |null      |
|102   |Dan       |A          |101       |
|103   |James     |A          |101       |
|104   |Amy       |A          |101       |
|105   |Anne      |A          |101       |
|106   |Ron       |B          |101       |
+------+----------+-----------+----------+
```

Given the Employee table, write a SQL query that finds out managers with at least 5 direct report. For the above table, your SQL query should return:

```
+-------+
| Name  |
+-------+
| John  |
+-------+
```

<br />

## MySQL Solution


```sql
select Name
from Employee as t1 
join (select ManagerId
    from Employee
    group by ManagerId
    having count(ManagerId) >= 5) as t2
on t1.Id = t2.ManagerId
```
