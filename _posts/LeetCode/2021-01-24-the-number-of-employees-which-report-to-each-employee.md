---
layout: post
title:  "The Number Of Employees Which Report To Each Employee"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ DatabaseGroup25 ]
featured: false
hidden: false
sidenav: LeetcodeDatabaseMedium3
excerpt: LeetCode 1731. Write an SQL query to report the ids and the names of the people that other employees reported to (excluding null values), the number of employees who report to them, and the average age of those members rounded to the nearest integer.
---

<br />

## Description

LeetCode Problem 1731. 

Table: Employees

```
+-------------+----------+
| Column Name | Type     |
+-------------+----------+
| employee_id | int      |
| name        | varchar  |
| reports_to  | int      |
| age         | int      |
+-------------+----------+
employee_id is the primary key for this table.
This table contains information about the employees and the id of the manager they report to. Some employees do not report to anyone (reports_to is null). 
```

Write an SQL query to report the ids and the names of the people that other employees reported to (excluding null values), the number of employees who report to them, and the average age of those members rounded to the nearest integer.

Return the result table ordered by employee_id.

The query result format is in the following example:

 
```
Employees table:
+-------------+---------+------------+-----+
| employee_id | name    | reports_to | age |
+-------------+---------+------------+-----+
| 9           | Hercy   | null       | 43  |
| 6           | Alice   | 9          | 41  |
| 4           | Bob     | 9          | 36  |
| 2           | Winston | null       | 37  |
+-------------+---------+------------+-----+

Result table:
+-------------+-------+---------------+-------------+
| employee_id | name  | reports_count | average_age |
+-------------+-------+---------------+-------------+
| 9           | Hercy | 2             | 39          |
+-------------+-------+---------------+-------------+
Alice and Bob report to Hercy, hence Hercy has 2 people report to him, and the average of their age is (41+36)/2 = 38.5 which is 39 after rounding it to the nearest integer.
```

<br />

## MySQL Solution


```sql
select e1.reports_to as employee_id,
       e2.name,
       count(e1.reports_to) as reports_count,
       round(avg(e1.age),0) as average_age
from employees e1
join employees e2
on e1.reports_to=e2.employee_id
group by e1.reports_to
order by e1.reports_to
```
