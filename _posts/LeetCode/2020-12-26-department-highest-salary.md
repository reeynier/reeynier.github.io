---
layout: post
title:  "Department Highest Salary Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup2 ]
featured: false
hidden: false
excerpt: LeetCode 184. Write a SQL query to find employees who have the highest salary in each of the departments.
---

<br />

## Description

LeetCode Problem 184. 

The Employee table holds all employees. Every employee has an Id, a salary, and there is also a column for the department Id.

```
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
```

The Department table holds all departments of the company.

```
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```

Write a SQL query to find employees who have the highest salary in each of the departments. For the above tables, your SQL query should return the following rows (order of rows does not matter).

```
+------------+----------+--------+
| Department | Employee | Salary |
+------------+----------+--------+
| IT         | Max      | 90000  |
| IT         | Jim      | 90000  |
| Sales      | Henry    | 80000  |
+------------+----------+--------+
```

Explanation: Max and Jim both have the highest salary in the IT department and Henry has the highest salary in the Sales department.

<br />

## MySQL Solution


```sql
select
    Department.name as 'Department',
    Employee.name as 'Employee',
    Salary
from
    Employee
join
    Department on Employee.DepartmentId = Department.Id
where
    (Employee.DepartmentId , Salary) in
    (select
        DepartmentId, max(Salary)
    from
        Employee
    group by DepartmentId)
```
