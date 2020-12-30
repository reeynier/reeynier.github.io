---
layout: post
title:  "Second Highest Salary Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup1 ]
featured: false
hidden: false
excerpt: LeetCode 176. Given the Employee table, write a SQL query that finds out employees who earn more than their managers.
---

<br />

## Description

LeetCode Problem 176. 

Write a SQL query to get the second highest salary from the Employee table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the query should return 200 as the second highest salary. If there is no second highest salary, then the query should return null.

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

<br />

## MySQL Solution

We can sort the distinct salary in descending order. Then we can utilize the **limit** clause to get the second highest salary. This is the inner select clause.

However, we need to consider the case when there is only one record in the table. The outer select clause is to take the select result as a table to avoid this issue.

```sql
select
    (select distinct Salary
        from Employee
        order by Salary desc
        limit 1 offset 1) 
as SecondHighestSalary;
```
