---
layout: post
title:  "Highest Grade For Each Student Problem"
categories: [ Database ]
tags: [ MySQL, Leetcode ]
similar: [ Database ]
featured: false
hidden: false
excerpt: LeetCode 1112. Write a SQL query to find the highest grade with its corresponding course for each student. 

---

<br />

## Description

LeetCode Problem 1112. 

Table: Enrollments

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| student_id    | int     |
| course_id     | int     |
| grade         | int     |
+---------------+---------+
(student_id, course_id) is the primary key of this table.
```

Write a SQL query to find the highest grade with its corresponding course for each student. In case of a tie, you should find the course with the smallest course_id. The output must be sorted by increasing student_id.

The query result format is in the following example:

```
Enrollments table:
+------------+-------------------+
| student_id | course_id | grade |
+------------+-----------+-------+
| 2          | 2         | 95    |
| 2          | 3         | 95    |
| 1          | 1         | 90    |
| 1          | 2         | 99    |
| 3          | 1         | 80    |
| 3          | 2         | 75    |
| 3          | 3         | 82    |
+------------+-----------+-------+

Result table:
+------------+-------------------+
| student_id | course_id | grade |
+------------+-----------+-------+
| 1          | 2         | 99    |
| 2          | 2         | 95    |
| 3          | 3         | 82    |
+------------+-----------+-------+
```

<br />

## MySQL Solution


```sql
select e1.student_id, min(e1.course_id) as course_id, e1.grade
from Enrollments e1
where e1.grade = 
    (select max(grade) as max_grade
    from Enrollments e2
    where e1.student_id = e2.student_id) 
group by e1.student_id
order by e1.student_id
```
