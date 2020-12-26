---
layout: post
title:  "Nth Highest Salary Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ Database ]
featured: false
hidden: false
excerpt: LeetCode 177. Write a SQL query to get the nth highest salary from the Employee table.
---

<br />

## Description

LeetCode Problem 177. 

Write a SQL query to get the nth highest salary from the Employee table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```

For example, given the above Employee table, the nth highest salary where n = 2 is 200. If there is no nth highest salary, then the query should return null.

```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```

<br />

## MySQL Solution


```sql
create function getNthHighestSalary(N int) returns int
begin
  return (
      select distinct salary as 'getNthHighestSalary(2)'
       from  (
          select salary,
                dense_rank() over(order by salary desc) as rnk
          from employee
      )  sal_rnk
      where rnk = n      
  );
end
```
